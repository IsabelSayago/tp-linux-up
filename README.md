# TP Integrador Linux — Universidad de Palermo

## Integrantes

- Isabel Sayago
- Cesia Llaufulen
- Magali Cerisola
- Milenka Rosales
- Nicolas Cerecedo

---

## Estado del TP

### ✅ Completado

- Sección 1: Setup base.
- Sección 2.1: Actualización a Debian 12.
- Sección 2.2: Configuración de SSH.
- Sección 2.3: Apache + PHP.
- Sección 2.4: MariaDB.
- Sección 3: Red estática.
- Sección 4: Almacenamiento con disco adicional.
- Sección 5: Backup + cron.
- Sección 6: Entregables finales.

---

## División de tareas del grupo

### Isabel Sayago — Setup base y actualización del sistema

Tareas realizadas:

- Importó la máquina virtual en VirtualBox.
- Blanqueó la contraseña del usuario root.
- Configuró la contraseña de root como `palermo`.
- Configuró el hostname del servidor como `TPServer`.
- Creó el repositorio en GitHub.
- Creó el README inicial con los integrantes del grupo.
- Actualizó el sistema operativo a Debian 12.

Comandos principales utilizados:

```bash
hostnamectl set-hostname TPServer
apt update
apt full-upgrade
```

---

### Cesia Llaufulen — Red estática y SSH

Tareas realizadas:

- Configuró la red estática del servidor.
- Editó el archivo `/etc/network/interfaces`.
- Configuró los datos de red requeridos:
  - ADDRESS
  - NETMASK
  - GATEWAY
- Probó conectividad mediante `ping`.
- Instaló y configuró OpenSSH Server.
- Generó el par de claves en `/root/.ssh/`.
- Configuró el acceso SSH modificando `/etc/ssh/sshd_config`.
- Habilitó `PermitRootLogin`.
- Habilitó `PubkeyAuthentication`.
- Probó el acceso remoto por SSH.

Archivos principales modificados:

```bash
/etc/network/interfaces
/etc/ssh/sshd_config
/root/.ssh/
```

---

### Magali Cerisola — Disco, particiones, Apache y PHP

Tareas realizadas:

- Agregó un disco adicional de 10 GB en VirtualBox.
- Creó las particiones necesarias con `fdisk`.
- Configuró las particiones para:
  - `/www_dir`
  - `/backup_dir`
- Formateó las particiones en formato `ext4`.
- Configuró el montaje automático editando `/etc/fstab`.
- Generó el archivo `/opt/particion`.
- Reinició el sistema y verificó el montaje correcto.
- Instaló Apache y PHP.
- Configuró Apache para que el `DocumentRoot` apunte a `/www_dir`.
- Copió los archivos `index.php` y `logo.png` desde `/root` hacia `/www_dir`.
- Verificó que la página web se visualizara correctamente desde el navegador.

Comandos y archivos principales:

```bash
fdisk
mkfs.ext4
/etc/fstab
cat /proc/partitions > /opt/particion
apt install apache2 php
/www_dir
/backup_dir
```

---

### Milenka Rosales — MariaDB y documentación

Tareas realizadas:

- Instaló y verificó MariaDB Server.
- Copió el archivo de base de datos desde el material adicional hacia `/root/db.sql`.
- Importó o verificó la base de datos con MariaDB.
- Verificó la existencia de la base de datos `ingenieria`.
- Verificó las tablas:
  - `alumnos`
  - `modulos`
  - `notas`
- Actualizó el README con la información correspondiente a MariaDB y la división de tareas.

Comandos principales utilizados:

```bash
cp /root/Material_Adicional_TPVMCA/db.sql /root/db.sql
apt install -y mariadb-server
systemctl status mariadb
mysql < /root/db.sql
mysql -e "SHOW DATABASES;"
mysql -e "USE ingenieria; SHOW TABLES;"
```

Base de datos verificada:

```text
ingenieria
```

Tablas encontradas:

```text
alumnos
modulos
notas
```

---

### Nicolas Cerecedo — Backup, cron y entregables finales

Tareas realizadas:

- Creó el directorio `/opt/scripts`.
- Creó el script `/opt/scripts/backup_full.sh`.
- Configuró el script para recibir dos argumentos:
  - origen
  - destino
- Agregó la opción de ayuda `-help`.
- Validó que el directorio de origen exista.
- Validó que el directorio de destino exista.
- Validó que el destino esté montado.
- Validó que `/www_dir` esté montado cuando se usa como origen.
- Dio permisos de ejecución al script.
- Probó manualmente los backups antes de configurar cron.
- Configuró las tareas programadas en el crontab de root.
- Verificó que el servicio `cron` estuviera activo.
- Generó los archivos comprimidos solicitados.
- Comprimió `/var` y lo dividió en partes de 50 MB.
- Copió los entregables finales al repositorio.
- Realizó commit y push al repositorio de GitHub.

Script creado:

```bash
/opt/scripts/backup_full.sh
```

Permisos asignados:

```bash
chmod +x /opt/scripts/backup_full.sh
```

Pruebas manuales realizadas:

```bash
/opt/scripts/backup_full.sh -help
/opt/scripts/backup_full.sh /var/log /backup_dir
/opt/scripts/backup_full.sh /www_dir /backup_dir
```

Tareas configuradas en cron:

```bash
0 0 * * * /opt/scripts/backup_full.sh /var/log /backup_dir
0 23 * * 1,3,5 /opt/scripts/backup_full.sh /www_dir /backup_dir
```

Verificación del servicio cron:

```bash
systemctl status cron
```

---

## Configuración de MariaDB

Se instaló y verificó MariaDB Server en la VM.

El archivo de base de datos utilizado fue:

```bash
/root/db.sql
```

El archivo original se encontraba en:

```bash
/root/Material_Adicional_TPVMCA/db.sql
```

Durante la importación, MariaDB informó que la base `ingenieria` ya existía. Luego se verificó directamente su contenido.

Base de datos verificada:

```text
ingenieria
```

Tablas encontradas:

```text
alumnos
modulos
notas
```

---

## Backup y cron

Se creó el script `/opt/scripts/backup_full.sh` para realizar backups comprimidos en formato `.tar.gz`.

El script permite recibir dos argumentos:

- Origen.
- Destino.

También incluye la opción de ayuda:

```bash
/opt/scripts/backup_full.sh -help
```

Pruebas realizadas manualmente:

```bash
/opt/scripts/backup_full.sh /var/log /backup_dir
/opt/scripts/backup_full.sh /www_dir /backup_dir
```

Archivos generados en `/backup_dir`:

```text
log_bkp_20260519.tar.gz
www_dir_bkp_20260519.tar.gz
```

Tareas configuradas en el crontab de root:

```bash
0 0 * * * /opt/scripts/backup_full.sh /var/log /backup_dir
0 23 * * 1,3,5 /opt/scripts/backup_full.sh /www_dir /backup_dir
```

Se verificó que el servicio `cron` estuviera activo.

---

## Entregables finales

Se generaron los archivos comprimidos individuales solicitados:

```text
root.tar.gz
etc.tar.gz
opt.tar.gz
www_dir.tar.gz
backup_dir.tar.gz
```

También se comprimió `/var` y se dividió en partes de 50 MB.

Comando utilizado:

```bash
tar -czvf - /var | split -b 50M - var.tar.gz.part_
```

Archivos generados:

```text
var.tar.gz.part_aa
var.tar.gz.part_ab
var.tar.gz.part_ac
```

---

## Estado final del servidor

El servidor quedó configurado con:

- Debian 12.
- Hostname `TPServer`.
- Red estática configurada.
- SSH habilitado.
- Disco adicional con particiones montadas en `/www_dir` y `/backup_dir`.
- Apache + PHP funcionando con `DocumentRoot` en `/www_dir`.
- MariaDB instalado y verificado.
- Base de datos `ingenieria` con tablas cargadas.
- Script de backup funcional.
- Cron configurado.
- Entregables finales comprimidos y subidos al repositorio.

---

## Repositorio

Repositorio utilizado para la entrega:

```text
https://github.com/IsabelSayago/tp-linux-up
```
