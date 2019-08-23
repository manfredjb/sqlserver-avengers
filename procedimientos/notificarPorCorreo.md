```tsql

drop procedure notificarPorCorreo;

create proc notificarPorCorreo
as
	DECLARE @cavengers CURSOR;
	DECLARE @avenger CURSOR;
	DECLARE @email CURSOR;
	DECLARE @hero CURSOR;
	DECLARE @superpower CURSOR;


begin
	SET @cavengers = CURSOR FOR
    select b.name avengerName, b.email, c.name heroName, c.superpower
	from dbo.missions a
	join dbo.avengers b on a.avenger = b.idAvenger
	join dbo.heroes c on a.hero = c.idHero
	where b.welcome = 1;  

	OPEN @cavengers 
    FETCH NEXT FROM @cavengers 
    INTO @avenger, @email, @hero, @superpower

	WHILE @@FETCH_STATUS = 0
    BEGIN
      
	  EXEC sp_send_dbmail @profile_name='notificador',
		@recipients=@email,
		@subject='Bienvenido, Vengador!'
		,
		@body=concat('Shield requiere de tu ayuda como ', @hero, ' contando con el sus superpoderes de ', @superpower, 
		'. Te esperamos pronto, ', @avenger);

      FETCH NEXT FROM @cavengers 
      INTO @avenger, @email, @hero, @superpower
    END; 

	CLOSE @cavengers ;
    DEALLOCATE @cavengers;

end;
```
