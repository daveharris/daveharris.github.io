---
layout: post
title: MySQL Backup Script
tags:
- MySQL
---

This is
a convienct place for me to put stuff that I (or you!) may need in the
future. While working at [Fronde](http://fronde.com) I wrote this little
backup script for the wiki we were using. It is meant to be run on a
cron job daily. It makes daily backups and every Friday copies that
backup to elsewhere (preferably off disk or off site) and deletes that
past week's daily backups. Before I get flamed in the comments I know
that there is [AutoMySQLBackup](http://sourceforge.net/projects/automysqlbackup/)
but that is huge and very complicated and I wanted to write it myself!

    #!/bin/bash
    # Wiki Database backup script

    # Set up the variables
    DB_USERNAME="username"
    DB_PASSWORD="password"
    DB_HOST="localhost"
    DB_NAME="wikidb"
    BACKUP_DIR="~/wiki_backups"
    ARCHIVE_DIR="~/wiki_backups/archive"
    DATE=$(date '+%Y-%m-%d')
    OUTPUT_FILENAME="${BACKUP_DIR}/wiki_${DATE}.sql"
    ERROR_FILENAME="${BACKUP_DIR}/error_log_${DATE}.txt"
    ARCHIVE_FILENAME="${ARCHIVE_DIR}/wiki_${DATE}.sql"
    MYSQLDUMP="/usr/local/mysql/bin/mysqldump"

    # Dump the wiki db to a file
    ${MYSQLDUMP} -ac --add-drop-table -u ${DB_USERNAME} --password=${DB_PASSWORD} \
        -h ${DB_HOST} -r ${OUTPUT_FILENAME} ${DB_NAME} &> ${ERROR_FILENAME} 

    # If there are errors, then do stuff here...
    STATUS_CODE="$?"
    if [ ${STATUS_CODE} = 2 ]; then

    fi

    # If the error log is empty, delete it
    numLines=$(cat ${ERROR_FILENAME} | wc -l | sed 's/\ //g')
    if [ ${numLines} = 0 ]; then
      rm ${ERROR_FILENAME}
    fi

    # If today is Friday, put a weekly backup in archives and delete daily backups
    if [ $(date +%A) = "Friday" ]; then
      cp -f ${OUTPUT_FILENAME} ${ARCHIVE_FILENAME}
      rm ${BACKUP_DIR}/*.sql
      #echo $(cat ${BACKUP_DIR}/wiki_${DATE}.sql)
    fi
