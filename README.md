# Docker MSSQL

## Odtworzenie kopi

Przed odtworzeniem backupu trzeba utworzyć dwa pliki w katalogu `data`:

- `baza.mdf`
- `baza_log.ldf`

Polecenie to odtworzenie kopi z folderu backup:

```sql
DECLARE @backupName VARCHAR(100);
DECLARE @olddbaName VARCHAR(100);
DECLARE @newdbaName VARCHAR(100);
DECLARE @SQL NVARCHAR(MAX);

SET     @backupName  = 'kopia.bak';
SET     @olddbaName  = 'NazwaBazy';
SET     @newdbaName  = @olddbaName;
-- SET     @newdbaName  = @olddbaName + '_new';

SET @SQL =
N'RESTORE DATABASE ' + @olddbaName + ' FROM DISK = ''/var/opt/mssql/backup/' + @backupName + ''' WITH MOVE ''' + @olddbaName + ''' TO ''/opt/var/mssql/data/' + @newdbaName + '.mdf'', MOVE ''' + @olddbaName + '_log'' TO ''/opt/var/log/mssql/data/' + @newdbaName + '_Log.ldf'''
EXEC sp_executesql @SQL
```

## Założenia

- Konfiguracja w pliki `.env`

## Uruchamianie

```
docker compose build
docker compose up
```
