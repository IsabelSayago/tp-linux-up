# TP Integrador Linux — Universidad de Palermo

## Integrantes
- Isabel Sayago
- Cesia Llaufulen
- Magali Cerisola
- Milenka Rosales
- Nicolas Cerecedo

## Descripción
Trabajo práctico integrador grupal sobre configuración de un servidor GNU/Linux Debian 12. La VM corre en la computadora de Isabel Sayago y los demás integrantes se conectan remotamente mediante SSH a través de Tailscale, una VPN que permite conectar dispositivos en redes distintas de forma segura.

## Infraestructura
- **VM hosteada por:** Isabel Sayago
- **Sistema operativo:** Debian GNU/Linux 12 (bookworm)
- **Conexión remota:** Tailscale + SSH
- **IP Tailscale de la VM:** 100.127.21.62
- **Hostname:** TPServer

## Configuración de acceso remoto
Para que los integrantes pudieran trabajar en la VM desde sus casas sin estar en la misma red, se utilizó Tailscale. Isabel configuró la VM localmente en VirtualBox, instaló Tailscale tanto en su Windows como dentro de la VM, y agregó a cada integrante a su red de Tailscale. Cada uno se conectó por SSH usando:

```
ssh root@100.127.21.62
```

ssh root@100.127.21.62

## División de tareas
| Integrante | Secciones |
|---|---|
| Isabel Sayago | Sección 1 (Setup base), Sección 6 (Entregables GitHub) |
| Cesia Llaufulen | Sección 2.1 (Actualización SO), Sección 2.2 (SSH) |
| Magali Cerisola | Sección 3 (Red estática), Sección 2.3 (Apache + PHP), Sección 4 (Almacenamiento) |
| Milenka Rosales | Sección 2.4 (MariaDB) |
| Nicolas Cerecedo | Sección 5 (Backup + cron) |

## Estado actual
### ✅ Completado
- Sección 1: Setup base (hostname TPServer, password palermo)
- Sección 2.1: Actualización a Debian 12 (bookworm)
- Sección 2.2: SSH configurado con clave pública/privada
- Sección 2.3: Apache + PHP instalado y funcionando
- Sección 2.4: MariaDB instalada con base de datos ingenieria (tablas: alumnos, modulos, notas)
- Sección 3: Red estática configurada (ADDRESS, NETMASK, GATEWAY)
- Sección 4: Disco de 10 GB agregado, particiones /www_dir (3 GB) y /backup_dir (6 GB) creadas y montaje automático configurado
- Sección 5: Script backup_full.sh creado y cron configurado
- Sección 6: Entregables comprimidos y subidos a GitHub
