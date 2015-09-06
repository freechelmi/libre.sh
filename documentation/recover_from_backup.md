```
# upload the key
gpg --import .gnupg/secring.gpg
source /etc/environment
domain=example.org
docker run -it --rm --name test -h backup.container -v /root:/root -v /data/domains/$domain:/backup indiepaas/duplicity sftp://${BACKUP_DESTINATION}/$domain /backup

systemctl start service
docker run -it --rm --name mysqlinport -v /data/domains/$domain/mysql/dump.sql:/tmp/dump.sql --link mysql-$domain:db indiepaas/mysql /bin/bash
mysql -u admin -p -h db < /tmp/dump.sql
```