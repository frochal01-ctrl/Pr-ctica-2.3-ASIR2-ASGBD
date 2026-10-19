# Instalar clientes para tres SGBD

## 1. Clientes para Oracle Database (en Mint/Debian)

### 1.1 Cliente gráfico: SQL Developer  

Instala un JDK compatible con la versión de SQL Developer que descargues.  

```bash
sudo apt update
sudo apt install default-jdk unzip
java --version
```
<img src="image/java.png">

Descarga el ZIP de SQL Developer para Linux.

<img src="image/client.png">

Instalar el cliente:

```bash
sudo unzip NOMBRE_DEL_ARCHIVO_SQLDEVELOPER.zip -d /opt/
/opt/sqldeveloper/sqldeveloper.sh
```  
<img src="image/clineteini.png">

Crear lanzador:

<img src="image/lanzador.png">

Crea una conexión a Oracle con el usuario `orauser`, puerto `1521` y nombre de servicio `FREEPDB1`.

<img src="image/configuracion_orace.png">
<img src="image/conectadooracle.png">  

### 1.2 Cliente gráfico: VS Code y extensión SQL Developer

```bash
cd ~/Descargas
sudo apt install ./NOMBRE_DEL_ARCHIVO_CODE.deb
```
<img src="image/viins.png.png">  

Instalar extensión Oracle SQL Developer:

<img src="image/exins.png">

Conexión a la base de datos:

<img src="image/COCON.png">
<img src="image/coneshecha.png">

### 1.3 Cliente de terminal: SQL*Plus

Descargar SQL*Plus:

```bash
mkdir -p ~/oracle-client
unzip NOMBRE_BASIC.zip -d ~/oracle-client
unzip NOMBRE_SQLPLUS.zip -d ~/oracle-client
ls ~/oracle-client
```
<img src="image/com1.png">

Configurando rutas:

```bash
export LD_LIBRARY_PATH="$HOME/oracle-client/instantclient_XX_X:$LD_LIBRARY_PATH"
export PATH="$HOME/oracle-client/instantclient_XX_X:$PATH"
sqlplus -v
sqlplus orauser@//localhost:1521/FREEPDB1
```
<img src="image/com2.png">

### 1.4 Cliente de terminal: SQLcl

```bash
cd ~/Descargas
unzip NOMBRE_DEL_ARCHIVO_SQLCL.zip -d ~/sqlcl
~/sqlcl/sqlcl/bin/sql -version
```
<img src="image/sqlc.png">

Para poder ejecutar `sql` desde cualquier terminal, añade esta línea a `~/.bashrc`:

```bash
export PATH="$HOME/sqlcl/sqlcl/bin:$PATH"
```
<img src="image/ruta.png">

Prueba la conexión con `orauser` y `FREEPDB1`:

<img src="image/sqlcdf.png">

---

## 2. Clientes para PostgreSQL

### 2.1 Cliente de terminal: psql

```bash
sudo apt update
sudo apt install postgresql-client
psql --version
psql -h localhost -U pguser -d dbpg -W
```
<img src="image/com3.png">

### 2.2 Cliente gráfico: pgAdmin 4

```bash
sudo apt install curl gnupg lsb-release
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /etc/apt/keyrings/packages-pgadmin-org.gpg
sudo sh -c 'echo "deb [signed-by=/etc/apt/keyrings packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list'
sudo apt update
sudo apt install pgadmin4-desktop
```
<img src="image/com4.png">

Configuración de conexión por pgAdmin:

<img src="image/conesionporpgAdmin .png">

Conexión exitosa por pgAdmin:

<img src="image/conesionadexi.png">  

---

## 3. Clientes para MariaDB

### 3.1 Cliente de terminal: mariadb 

```bash
sudo apt update
sudo apt install mariadb-client
mariadb --version
mariadb -h localhost -u muser -p dbm
```
<img src="image/conemaria.png"> 

### 3.2 Cliente web: phpMyAdmin

```bash
sudo apt update
sudo apt install apache2 php php-mysql php-mbstring php-zip php-gd php-curl phpmyadmin
sudo phpenmod mbstring
sudo systemctl restart apache2
```
<img src="image/conphp.png">

Conexión con MariaDB con phpMyAdmin:

<img src="image/conephp.png">

---

## 4. Clientes para varios SGBD

### 4.1 DBeaver Community

```bash
cd ~/Descargas
sudo apt install ./NOMBRE_DEL_ARCHIVO_DBEAVER.deb
```
<img src="image/instaladbe.png">

Conexión con las tres bases de datos usando DBeaver:

<img src="image/treaconeex.png">

### 4.2 Adminer

```bash
sudo apt install php-cli
wget https://www.adminer.org/latest.php -O adminer.php
php -S 127.0.0.1:8080 adminer.php
```
<img src="image/serphp.png">

Conexión con Adminer:

<img src="image/cophpexe.png">

---

## 5. Incidencias

Un problema con MariaDB es que pedía SSL. Lo he arreglado poniendo un parámetro llamado `ssl=no`.

---

## 6. Fuentes consultadas

*   [Práctica Instalar Clientes 3 SGBD - Informática IES Albarregas](https://informatica.iesalbarregas.com/pluginfile.php/15395/mod_assign/introattachment/0/Practica_Instalar_Clientes_3_SGBD.pdf?forcedownload=1)
