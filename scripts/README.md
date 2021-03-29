# Backup Scripts
Shell script for backing up a whole docker-volume as a tar and restoring a new docker-volume from an existing tar [[credit](https://github.com/JorgenRingen/docker-backup-volume)]

##### Backing up a docker-volume
```
sh backup-docker-volume.sh my_docker_volume /home/myself/backups
```

##### Restoring a docker volume
```
sh restore-docker-volume.sh my_restored_docker_volume /home/myself/backups/my_docker_volume_backup.tar.gz
```