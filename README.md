# GLPI Tools

### Features

- Backup of GLPI with retention (Files and SQL)
- Restore from backups
- Update GLPI from official sources
- Fix file permissions
- Easy removal of the installation file after an update
- Backup automation

### Usage

Backup GLPI
```bash
./glpitools.sh backup
```

Restore GLPI
```bash
./glpitools.sh restore
```

Update GLPI
```bash
./glpitools.sh update
```

Fix permissions
```bash
./glpitools.sh fix-permissions
```

Remove Install file
```bash
./glpitools.sh installfile
```

### Installation and Configuration

Dependencies
```bash
apt install curl git
```

Create directories
```bash
mkdir /backup  
mkdir /backup/glpi
```

Download and install glpitools
```bash
cd /opt/  
git clone https://github.com/goronu/glpitools
cd ./glpitools
```

### Configure glpitools

Edit script file
```bash
nano glpitools.sh
```
Set the following parameters:

- `BACKUP_DIR`        # Backup directory
- `GLPI_DIR`          # GLPI installation path
- `DB_NAME`           # Database name
- `DB_USER`           # MySQL/MariaDB user
- `DB_PASS`           # MySQL/MariaDB password
- `RETENTION_DAYS`    # Number of days before old backups are deleted
- `GLPI_DOWNLOAD_URL` # GLPI source URL
- `APACHE_USER`       # Apache/Nginx user (can be www-data, apache, nginx, etc.)

### Automate Backups

Open the CRON file:
```bash
crontab -e
```

Add the following line:
```bash
0 2 * * * /opt/glpitools/glpitools.sh backup >> /var/log/glpitools_backup.log 2>&1
