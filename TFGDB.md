
## Base de datos y entorno básico

El objetivo principal de esta pequeña guía es instalar DB2 LUW y configurar el entorno básico para que funcione correctamente.

## ✔️ Instalación de DB2 LUW en la máquina virtual
### ⚙️ Requisitos previos
### 1️⃣ Actualizamos el sistema operativo
Esto lo realizaremos únicamente para asegurarnos que todo lo tenemos al día y no tenemos problemas a la hora de continuar con la instalación.
```bash
  sudo apt update && sudo apt upgrade -y
```
### 2️⃣ Actualizamos el sistema operativo
Para poder utilizar DB2, necesitamos las siguientes librerias.
```bash
  sudo apt install libaio1 ksh libpam0g libstdc++6 -y
```
### 3️⃣ Creamos el grupo y usurio para instancias
```bash
  sudo groupadd db2adm
  sudo useradd -m -g db2iadm1 db2inst
  sudo passwd db2inst
```
### ⚙️ Instalación DB2 LUW
### 1️⃣ Descomprimir el paquete
El paquete en cuestión nos lo bajaremos de la página de IBM: [Descarga e instalación del servidor DB2](https://www.ibm.com/docs/es/netcoolomnibus/8.1?topic=balancing-downloading-installing-db2-server)
```bash
   tar -xvf db2_linux_x64_server.tar.gz
   cd server_t
```
El server_t se genera automáticamente con los archivos de instalación
### 2️⃣ Iniciamos el instalador 
```bash
   sudo ./db2_install
```
### ⚙️ Configuración post-configuración
### 1️⃣ Creamos la instancia principal: db2inst1
```bash
   sudo /opt/ibm/db2/V11.5/instance/db2icrt -u db2inst db2inst
```
### 2️⃣ Iniciamos la instancia
```bash
   su - db2inst
   . /home/db2inst/sqllib/db2profile
   db2start
```
## ✔️ Creación de la Base de Datos
Creamos la base de datos con nombre **TFGDB** donde vamos a almacenar los datos del proyecto
### 1️⃣ Conexión con la instancia
```bash
   sudo su - db2inst
```
### 2️⃣ Creamos la base de datos 
```bash
   db2 create database TFGDB
```
### 3️⃣ Verificar que la base de datos esta creada
```bash
   db2 list db directory
```
### 4️⃣ Conectarse a la base de datos
```bash
   db2 connect to TFGDB
```
## ✔️ Creación de instancia: pruebas
Creamos la instancia **pruebas** donde vamos a realizar pruebas respecto a los datos del proyecto
### 1️⃣ Crear usuario para la instancia
```bash
   sudo useradd -m -g db2iadm1 pruebas
   sudo passwd pruebas
```
### 2️⃣ Creamos la instancia 
```bash
   sudo /opt/ibm/db2/V11.5/instance/db2icrt -u pruebas pruebas
```
### 3️⃣ Iniciamos la instancia
```bash
   su - pruebas
   . /home/pruebas/sqllib/db2profile
   db2start
```
## 💡 Verificar instancias y base de datos
### 📌 Listar todas las instancias 
```bash
   db2ilist
```
### 📌 Listar todas las instancias 
```bash
   db2 list db directory
```
