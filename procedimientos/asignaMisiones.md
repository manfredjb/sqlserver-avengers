```tsql
drop procedure asignaMisiones;

CREATE PROC asignaMisiones
AS
	DECLARE @idHero int;
	DECLARE @idAvenger int;
	DECLARE @cavengers CURSOR;
begin
	

	SET @cavengers = CURSOR FOR
    select idAvenger from dbo.avengers
        where welcome = 1;  

	 OPEN @cavengers 
    FETCH NEXT FROM @cavengers 
    INTO @idAvenger

	WHILE @@FETCH_STATUS = 0
    BEGIN
      
	  set @idHero = ABS(CHECKSUM(NEWID()) % 6) + 1;
	  insert into dbo.missions(avenger, hero) values(@idAvenger, @idHero);

      FETCH NEXT FROM @cavengers 
      INTO @idAvenger 
    END; 

	CLOSE @cavengers ;
    DEALLOCATE @cavengers;

end;
```
