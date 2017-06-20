# Apache Tomcat

## Definición 
Funciona como un contenedor de servlets desarrollado bajo el proyecto Jakarta en la Apache Software Foundation. Tomcat implementa las especificaciones de los servlets y de JavaServer Pages (JSP) de Oracle Corporation (aunque creado por Sun Microsystems). 
## Rol en geonetwork 
Geonetwork al ser una herramienta de uso libre ya desarrollada en JAVA permite la instalación y configuración en un contenedor de aplicaciones (apache Tomcat) que a su vez está instalado en el servidor, es decir para que Geonetwork funcione es necesario estar desplegado en Tomcat o en una aplicación similar.

## Configuraciones para geonetwork 
Una vez instalado apache Tomcat es necesario configurarlo para que permita ejecutar aplicaciones que solicitan más memoria de la que viene por default, este proceso se realiza a través del archivo ubicado en /etc/default/tomcat7/bin/setenv.sh allí agregar o editar la siguiente línea: JAVA_OPTS = "$JAVA_OPTS -Xms128m -Xmx512m -server" De esta forma se configurarán 512mb para su ejecución siendo esto suficiente para un correcto despliegue, es necesario conocer el usuario administrador que nos permitirá gestionar las instancias de geonetwork en apache tomcat, para realizar este proceso se debe: Ir la carpeta de instalación de apache tomcat vx (siendo x la versión de tomcat puede ser 7, 8 o 9 se recomienda 7 u 8 por temas de compatibilidad), ingresar en la carpeta conf y allí localizar el archivo tomcat-users.xml el cual contendrá los usuario y permisos del mismo

Si es una nueva instalación posiblemente estarán comentados los usuarios, agregar la información indicada a continuación antes de asegurándose que aparezca la siguiente información:

## Cambios de configuraciones antes del despliegue
En caso que se desee modificar la información y configuraciones de la automatización es necesario ingresar a:
branch / allin / ansible / group_vars /  tag_Name_appserver / tomcat
desde aquí se podrán modificar las siguientes opciones
* version actualmente **apache-tomcat-7.0.78**
* java_vm_ms actualmente **1024M** es posible aumentar la capacitad en caso de ser necesario a **2048M** 2GB memoria
* java_vm_mx actualmente **1024M** es posible aumentar la capacitad en caso de ser necesario a **2048M** 2GB memoria
* admin_user actualmente **admin** es posible cualquier nombre de usuario por ejemplo **usu4r104dmn1str4d0r**
* admin_password actualmente **admin** es posible cualquier contraseña por ejemplo **c0ntr4s3n4+c0mpl3j4**


## Configuraciones posteriores. 
Normalmente no se deberían cambiar estas configuraciones pero si en algún momento se necesita sería esta última la única opción a cambiar o el usuario o contraseña de tomcat, es posible agregar algunos roles más en caso de ser necesario. 

# Apache Http Server - Servidor Web

## Definición

Es un servidor web HTTP de código abierto, para plataformas Unix (BSD, GNU/Linux, etc.), Microsoft Windows, Macintosh y otras, que implementa el protocolo HTTP/1.12 y la noción de sitio virtual. El servidor Apache es desarrollado y mantenido por una comunidad de usuarios bajo la supervisión de la Apache Software Foundation dentro del proyecto HTTP Server (httpd).

## Rol en Geonetwork 
Para poder acceder a Geonetwork es necesario ingresar a una página web a través de un navegador como google Chrome o similar por tal motivo para permitir esta comunicación y esta disponibilidad vía web fue necesario instalar este servidor de aplicaciones web con el fin de agregar las funcionabilidades de ssl, proxis y ftp con el fin de asegurar la seguridad con los módulos activados de apache http. Configuraciones para geonetwork Una vez instalado es necesario activar los módulos de:

* ssl
* headers
* proxy
* proxy_ajp
* proxy_connect
* proxy_ftp
* proxy_html
* proxy_http
* rewrite
* xml2enc
Para llevar a cabo este proceso es necesario retirar el carácter # del archivo conf/httpd.conf

## Cambios de configuraciones antes del despliegue
si se desea inactivar o agregar más módulos de los nombrados en el punto anterior es necesario acceder a:
branch / allin / ansible / roles / webserver / tasks / main.yml
desde la línea 22 a la 29 es posible agregar otros módulos que se podrán consultar desde el siguiente link (https://httpd.apache.org/docs/2.2/es/mod/) lo que permitirá agregar más funcionalidades.

## Configuraciones posteriores 
Normalmente no se deberían modificar estas configuraciones pero si en el algún momento se desea cambiar sus ajustes será necesario volver a ponerle el carácter # para así deshabilitar cada funcionabilidad.

# Solr -Software de indexamiento 

## Definición 

Es un motor de búsqueda de código abierto basado en la biblioteca Java del proyecto Lucene, con APIs en XML/HTTP y JSON, resaltado de resultados, búsqueda por facetas, caché, y una interfaz para su administración. Básicamente se encarga de organizar la toda la información que genera Geonetwork para que sea encontrada de una forma más eficiente que si se buscara a través de la base de datos, este motor tiene en cuenta las búsquedas más frecuentes para disponer de la información más rápido.

## Configuraciones para Geonetwork 
Ya viene integrado, no necesita ninguna configuración.

## Cambios de configuraciones antes del despliegue
Para cambiar los ajustes principales ingresar a la ruta:
branch / allin / ansible / group_vars /  tag_Name_solrserver
solr_user: actualmente  **solr**
solr_connect_host: actualmente **localhost**
solr_port: **8983**
solr_xms:**256M**
solr_xmx: **512M**
solr_timezone: actualmente **"UTC"** dependiendo de la zona horaria se puede usar **"UTC-5"** para Colombia
solr_log_file_path: actualmente **/var/log/solr.log** es posible cambiarla por una ruta diferente dependiendo de la necesidad, tener en cuenta que esta es una ruta linux por lo tanto debe respetar estas su sintaxis.

## Configuraciones posteriores.

Ninguna configuración posterior. 
# MySQL - Base de datos

## Definición

Es un sistema de gestión de bases de datos relacional desarrollado bajo licencia dual GPL/Licencia comercial por Oracle Corporation y está considerada como la base datos open source más popular del mundo,1 2 y una de las más populares en general junto a Oracle y Microsoft SQL Server, sobre todo para entornos de desarrollo web.

## Configuraciones para Geonetwork

Después de la instalación del motor es necesario crear una base de datos llamada geonetwork con un usuario geonet y una contraseña geonetwork Posterior a esto se configura en los procesos posteriores usando ansible estos datos en geonetwork

## Cambios de configuraciones antes del despliegue
Para cambiar los ajustes principales ingresar a la ruta:
branch / allin / ansible / group_vars /  tag_Name_dbserver
es posible cambiar el nombre de usuario, contraseña,  base de datos, codificación, puerto, timeout de las querys de la siguiente manera:
* name: actualmente **defaultuser** se puede cambiar por ejemplo por el **usu4r10g30n3tw0rk**
* password: actualmente **default1** se puede cambiar por ejemplo por **c0ntr4s3n4g30n3tw0rk**
* name: actualmente **geonetworkdb** se puede cambiar por cualquier otro nombre ejemplo **dbg30n3tw0rk**
* mysql_port: actualmente  **"3306"** se puede cambiar por cualquier otro por ejemplo **3309**
* mysql_wait_timeout: actualmente  **"28800"** este tiempo está representado en milisegundos se puede aumentar o disminuir por ejemplo **20000**

## Configuraciones posteriores

De ser necesario se cambiaría el nombre de la base de datos, el usuario o la contraseña sin embargo esto puede acarrear perdida de información o segmentación de la misma.

