```tsql

drop procedure notificarPorCorreo;

create proc notificarPorCorreo
as
	DECLARE @cavengers CURSOR;
	DECLARE @message varchar(400);
	DECLARE @email varchar(100);

begin
	SET @cavengers = CURSOR FOR
    select concat('Shield requiere de tu ayuda como ', c.name, ' contando con sus superpoderes de ', c.superpower, 
		'. Te esperamos pronto, ', b.name, '!') message, b.email
	from dbo.missions a
	join dbo.avengers b on a.avenger = b.idAvenger
	join dbo.heroes c on a.hero = c.idHero
	where b.welcome = 1; 

	OPEN @cavengers 
    FETCH NEXT FROM @cavengers 
    INTO @message, @email

	WHILE @@FETCH_STATUS = 0
    BEGIN
      
	  EXEC msdb.dbo.sp_send_dbmail @profile_name='notificador',
		@recipients=@email,
		@subject='Bienvenido, Vengador!',
		@body=@message

      FETCH NEXT FROM @cavengers 
      INTO @message, @email
    END; 

	CLOSE @cavengers ;
    DEALLOCATE @cavengers;
    
    update dbo.avengers set welcome = 0 where welcome = 1;

end;
```
