## Configuraciones

```

exec sp_configure
go
exec sp_configure 'xp_cmdshell', 1
-- Configuration option 'xp_cmdshell' changed from 0 to 1. Run the RECONFIGURE statement to install.
go
reconfigure
go
