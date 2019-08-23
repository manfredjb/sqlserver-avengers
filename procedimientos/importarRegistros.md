```tsql

drop procedure dbo.importarRegistros;
CREATE PROC importarRegistros

AS

BULK INSERT dbo.preAvengers FROM 'C:\tmp\registros.txt'
WITH ( FIELDTERMINATOR ='|', FIRSTROW = 1 )

INSERT INTO dbo.avengers(name, email, welcome) 
   SELECT name, email, welcome
   FROM dbo.preAvengers;

delete from dbo.preAvengers;
```
