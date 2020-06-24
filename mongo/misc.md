Creating mongo dump as archive

```
mongodump 
--host "localhost:{$port}" 
--db $db_name 
--excludeCollection=$exclude_collection1 
--excludeCollection=$exclude_collection2 
--gzip 
--archive=$archive_name.gzip
```
