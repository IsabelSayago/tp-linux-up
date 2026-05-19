# TP Integrador Linux — Universidad de Palermo

## Integrantes

- Isabel Sayago
- Cesia Llaufulen
- Magali Cerisola
- Milenka Rosales
- Nicolas Cerecedo

## Estado del TP

### ✅ Completado

- Sección 1: Setup base (hostname TPServer, password palermo)
- Sección 2.1: Actualización a Debian 12 (bookworm)
- Sección 2.2: SSH configurado con clave pública/privada
- Sección 2.3: Apache + PHP
- Sección 2.4: MariaDB
- Sección 3: Red estática configurada (ADDRESS, NETMASK, GATEWAY)
- Sección 4: Almacenamiento (disco 10 GB, particiones /www_dir y /backup_dir)

### 🔄 En progreso

- Sección 5: Backup + cron
- Sección 6: Entregables finales

### ⏳ Pendiente

- Sección 5: Backup + cron
- Sección 6: Entregables finales


:O
## Configuración de MariaDB

Se instaló y verificó MariaDB Server en la VM.

El archivo de base de datos utilizado fue: /root/db.sql

El archivo original estaba en: /root/Material_Adicional_TPVMCA/db.sql

Comandos utilizados:

- cp /root/Material_Adicional_TPVMCA/db.sql /root/db.sql
- apt update
- apt install -y mariadb-server
- systemctl status mariadb
- mysql < /root/db.sql

La base de datos verificada fue: ingenieria

Tablas encontradas:

- alumnos
- modulos
- notas

Comandos de verificación:

- mysql -e "SHOW DATABASES;"
- mysql -e "USE ingenieria; SHOW TABLES;"

## División de tareas

### Milenka Rosales / Nicolas Cerecedo

- Instaló y verificó MariaDB Server.
- Copió el archivo db.sql a /root/db.sql.
- Verificó la base de datos ingenieria.
- Verificó las tablas alumnos, modulos y notas.
- Actualizó el README con el estado del TP.

## Backup y cron

Se creó el script `/opt/scripts/backup_full.sh` para realizar backups comprimidos en formato `.tar.gz`.

El script permite recibir dos argumentos:

- Origen
- Destino

También incluye la opción de ayuda:

- `/opt/scripts/backup_full.sh -help`

Pruebas realizadas manualmente:

- `/opt/scripts/backup_full.sh /var/log /backup_dir`
- `/opt/scripts/backup_full.sh /www_dir /backup_dir`

Archivos generados en `/backup_dir`:

- `log_bkp_20260519.tar.gz`
- `www_dir_bkp_20260519.tar.gz`

Se configuraron las siguientes tareas en el crontab de root:

- `0 0 * * * /opt/scripts/backup_full.sh /var/log /backup_dir`
- `0 23 * * 1,3,5 /opt/scripts/backup_full.sh /www_dir /backup_dir`

Se verificó que el servicio cron esté activo con:

- `systemctl status cron`

## Entregables finales

Se generaron los archivos comprimidos solicitados:

- `root.tar.gz`
- `etc.tar.gz`
- `opt.tar.gz`
- `www_dir.tar.gz`
- `backup_dir.tar.gz`

También se comprimió `/var` y se dividió en partes de 50 MB:

- `var.tar.gz.part_aa`
- `var.tar.gz.part_ab`
- `var.tar.gz.part_ac`
