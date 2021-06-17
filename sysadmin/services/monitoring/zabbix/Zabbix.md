# Zabbix

Software de monitorización elaborado en PHP....

## Instalación en CentOS 8

 ### Actualizar el sistema

```bash
dnf upgrade
```

### Instalar el repositorio

```bash
rpm -Uvh https://repo.zabbix.com/zabbix/5.0/rhel/8/x86_64/zabbix-release-5.0-1.el8.noarch.rpm
dnf clean all 
```

### Instalar el software necesario

```bash
dnf install zabbix-server-mysql zabbix-web-mysql zabbix-nginx-conf zabbix-agent mariadb-server
```

### Configurando por primera vez la base de datos

#### Habilitando al arranque y arrancando MariaDB

```bash
systemctl enable --now mariadb.service
```

#### Configurando la base de datos

__NOTA:__ _Solo hay que seguir los pasos_

```bash
mysql_secure_installation
```

#### Configurando la base de datos para Zabbix

```mysql
mysql -u root -p
mysql> CREATE DATABASE zabbix CHARACTER SET utf8 COLLATE utf8_bin;
mysql> CREATE USER zabbix@localhost identified BY 'AQUI_UNA_CONTRASEÑA';
mysql> GRANT ALL PRIVILEGES ON zabbix.* TO zabbix@localhost;
mysql> QUIT; 
```

#### Importando el esquema de base de datos

```bash
zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -u zabbix -p AQUI_UNA_CONTRASEÑA 
```

### Configurando la base de datos para el servidor

Editar el archivo `/etc/zabbix/zabbix_server.conf` y cambiar la contraseña de BBDD:

```
 DBPassword=AQUI_UNA_CONTRASEÑA
```

### Editar archivo `/etc/nginx/conf.d/zabbix.conf`

__NOTA:__ Descomentar y configurar las directivas `listen` y `server_name`

```
# listen 80;
# server_name example.com; 
```

### Escoger el huso horario `/etc/php-fpm.d/zabbix.conf`

```php
php_value[date.timezone] = Atlantic/Canary 
```

### Arrancando y habilitando Zabbix en el sistema

```bash
systemctl enable --now zabbix-server.service zabbix-agent.service nginx.service php-fpm.service
```

### Accediendo al portal de configuración

Accedemos mediante el dominio que hemos configurado anteriormente.

* Usuario: Admin
* Contraseña: zabbix

## Let's Encrypt

### Instalar el software necesario

```bash
dnf install epel-release
dnf install certbot python3-certbot-nginx
```

__NOTA:__ Teniendo el dominio apuntando al servidor y certificando en https://dnschecker.org que el resultado del registro es la IP del dominio, procedemos a generar el certificado.

## Generando el certificado

```bash
certbot --nginx -d DOMINIO -m TU_EMAIL --agree-tos --non-interactive
```

### Reiniciando el servidor web

```
systemctl restart nginx.service
```

Ya tendremos nuestro servidor web protegido via SSL.

## Firewalld

### Instalar firewalld

```bash
dnf install firewalld
```

### Habilitando al arranque e iniciándolo

```
systemctl enable --now firewalld.service
```

### Abriendo los puertos para Zabbix

```bash
firewall-cmd --add-service http --add-service https --zone public --permanent
firewall-cmd --reload
```

## Procedimiento de backup

### Exportar todas las bases de datos

```bash
mysqldump -u root --all-databases -p  > dump-$(date +%d-%m-%y).sql
```

* `-u root`: Usuario root

* `--all-databases`: Todas las bases de datos

* `-p`: Pregunta por la contraseña

* `>` : Redirige el flujo hacia el fichero salida `dump-$(date +%d-%m-%y).sql` 
* `dump-$(date +%d-%m-%y).sql`

### Comprimir los directorios esenciales

```bash
tar zcfv /root/zabbix-$(date +%d-%m-%y).tar.gz /etc/zabbix /usr/share/zabbix --acls --xattrs --selinux
```

