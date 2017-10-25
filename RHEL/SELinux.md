# Activación y monitorización SELinux

__SELinux__
:Protejer datos de usuario de los servicios del sistema comprometidos.
Basado en Objetos.

Para mostrar el modo actual de _SELinux_ `getenforce`

Opción `-Z` con `ls` y `ps`

Para ver variables (booleanas) `getsetbool -a`

## Conceptos básicos

### Apache sin SELinux

* Se ha de abrir cortafuegos para permitir acceso web _anónimo_
* Se ha de permitir acceso a usuario:grupo
    - Lectura sobre `/var/www/html`
    - Escritura sobre `/tmp`, `/var/tmp` y otros

### Apache con SELinux

* Las reglas de SELinux determinan qué procesos pueden acecder a qué ficheros, directorios, puertos
* Cada fichero, proceso, directorio, puerto tiene un __contexto__    
    - __Contexto__: el nombre de la política SELinux
    - __Por defecto__: la política es _no permitir_ interacción a no ser que la regla permita acceso.

#### Contextos (etiquetas)

* User
* Role
* Type
* Sensitivity
* Política _dirigida_ (targeted) basa sus reglas en el contexto _type_ 
    - normalmente comienzan con `_t`
* Contexto _type_ para:
    - Servidor web: `http_t`
    - Ficheros, directorios en `/var/www/html`: `httpd_sys_content_t`
    - Ficheros, directorios en `/tmp` y `/var/tmp`: `tmp_t`
    - Puertos web: `http_port_t`

#### Políticas

* Permitir a _Apache_ (proceso servidor web `http_t`) acecder a ficheros/directorios con _contexto_ en `/var/www/html` y otros (`httpd_sys_content_t`)
* Contiene un _no permitir_ para ficheros en `/tmp` y `/var/tmp`
* Contiene reglas para sistemas de ficheros remotos

#### Comandos

```
# ps axZ
# systemctl start httpd
# ps -ZC http
# ls -Z /home
# ls -Z /var/www
```

### Modos

Podemos usar los _SELinux modes_ para desactivarlo temporalmente

#### Enforcing mode

* SELinux deniega acceso al servidor web que intenta leer ficheros con contexto `tmp_t`
* SELinux registra y protege

#### Permissive mode

* Se utiliza para resolver problemas
* Se permiten todas las interacciones
* Se registran interacciones que se habrían denegado en _enforcing mode_
* Se usa para permitir temporalmente acceso a contenido bloqueado por SELinux
* No se requieren reinicios para pasar entre modos _permissive_ y _enforce_

#### Disable mode

* Se desactiva completamente SELinux
* Es necesario reinicio
* Es recomendable usar _permissive_ antes que _disable_ mode

Para mostrar el modo actual `getenforce`

### SELinux Booleans

__Switches__ que cambian el comportamiento de las políticas de SELinux

* Las reglas que se pueden activar/desactivar
* Se pueden usar para afinar políticas para crear ajustes selectivos

Usar `getsetbool` para mostrar las _SELinux Booleans_ y sus valores. Con `-a` se muestran todas.

### Cambiar entre modes

Con el comando `setenforce`

* Se puede desactivar temporalmente SELinux
* Se puede cambiar temporalmente entre _enforcing_ y _permisive_

__Pasando parámetros__

* Se pueden pasar parámetros al _kernel_ en tiempo de arranque
* Pasando `enforcing=0` hacemos que el sistema arranque en modo _permissive_
* Con `enforcing=1` arranca en modo _enforcing_
* Pasando `selinux=0` desactivamos SELinux. `selinux=1` lo activa.

#### Modo por defecto

Se configura en `/etc/selinux/config`. 

Parámetros pasado en el arranque prevalecen sobre lo definido aquí.

--
