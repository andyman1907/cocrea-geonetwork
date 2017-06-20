#Apache Tomcat

##Definición Funciona como un contenedor de servlets desarrollado bajo el proyecto Jakarta en la Apache Software Foundation. Tomcat implementa las especificaciones de los servlets y de JavaServer Pages (JSP) de Oracle Corporation (aunque creado por Sun Microsystems). ##Rol en geonetwork Geonetwork al ser una herramienta de uso libre ya desarrollada en JAVA permite la instalación y configuración en un contenedor de aplicaciones (apache Tomcat) que a su vez está instalado en el servidor, es decir para que Geonetwork funcione es necesario estar desplegado en Tomcat o en una aplicación similar.

##Configuraciones para geonetwork Una vez instalado apache Tomcat es necesario configurarlo para que permita ejecutar aplicaciones que solicitan más memoria de la que viene por default, este proceso se realiza a través del archivo ubicado en /etc/default/tomcat7/bin/setenv.sh allí agregar o editar la siguiente línea: JAVA_OPTS = "$JAVA_OPTS -Xms128m -Xmx512m -server" De esta forma se configurarán 512mb para su ejecución siendo esto suficiente para un correcto despliegue, es necesario conocer el usuario administrador que nos permitirá gestionar las instancias de geonetwork en apache tomcat, para realizar este proceso se debe: Ir la carpeta de instalación de apache tomcat vx (siendo x la versión de tomcat puede ser 7, 8 o 9 se recomienda 7 u 8 por temas de compatibilidad), ingresar en la carpeta conf y allí localizar el archivo tomcat-users.xml el cual contendrá los usuario y permisos del mismo

Si es una nueva instalación posiblemente estarán comentados los usuarios, agregar la información indicada a continuación antes de asegurándose que aparezca la siguiente información:

##Configuraciones posteriores. Normalmente no se deberían cambiar estas configuraciones pero si en algún momento se necesita sería esta última la única opción a cambiar o el usuario o contraseña de tomcat, es posible agregar algunos roles más en caso de ser necesario. #Apache Http Server - Servidor Web

##Definición

Es un servidor web HTTP de código abierto, para plataformas Unix (BSD, GNU/Linux, etc.), Microsoft Windows, Macintosh y otras, que implementa el protocolo HTTP/1.12 y la noción de sitio virtual. El servidor Apache es desarrollado y mantenido por una comunidad de usuarios bajo la supervisión de la Apache Software Foundation dentro del proyecto HTTP Server (httpd).

##Rol en Geonetwork Para poder acceder a Geonetwork es necesario ingresar a una página web a través de un navegador como google Chrome o similar por tal motivo para permitir esta comunicación y esta disponibilidad vía web fue necesario instalar este servidor de aplicaciones web con el fin de agregar las funcionabilidades de ssl, proxis y ftp con el fin de asegurar la seguridad con los módulos activados de apache http. Configuraciones para geonetwork Una vez instalado es necesario activar los módulos de:

ssl
headers
proxy
proxy_ajp
proxy_connect
proxy_ftp
proxy_html
proxy_http
rewrite
xml2enc
Para llevar a cabo este proceso es necesario retirar el carácter # del archivo conf/httpd.conf

##Configuraciones posteriores Normalmente no se deberían modificar estas configuraciones pero si en el algún momento se desea cambiar sus ajustes será necesario volver a ponerle el carácter # para así deshabilitar cada funcionabilidad.

#Solr - Software de indexamiento ##Definición Es un motor de búsqueda de código abierto basado en la biblioteca Java del proyecto Lucene, con APIs en XML/HTTP y JSON, resaltado de resultados, búsqueda por facetas, caché, y una interfaz para su administración. Básicamente se encarga de organizar la toda la información que genera Geonetwork para que sea encontrada de una forma más eficiente que si se buscara a través de la base de datos, este motor tiene en cuenta las búsquedas más frecuentes para disponer de la información más rápido.

##Configuraciones para Geonetwork Ya viene integrado, no necesita ninguna configuración.

##Configuraciones posteriores.

Ninguna configuración posterior. #MySQL - Base de datos

##Definición

Es un sistema de gestión de bases de datos relacional desarrollado bajo licencia dual GPL/Licencia comercial por Oracle Corporation y está considerada como la base datos open source más popular del mundo,1 2 y una de las más populares en general junto a Oracle y Microsoft SQL Server, sobre todo para entornos de desarrollo web.

##Configuraciones para Geonetwork

Después de la instalación del motor es necesario crear una base de datos llamada geonetwork con un usuario geonet y una contraseña geonetwork Posterior a esto se configura en los procesos posteriores usando ansible estos datos en geonetwork

##Configuraciones posteriores

De ser necesario se cambiaría el nombre de la base de datos, el usuario o la contraseña sin embargo esto puede acarrear perdida de información o segmentación de la misma.

