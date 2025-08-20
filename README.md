# jenkins-nexus-installation-local

Instalar Jenkins en Windows:
1. Java 17 instalado en windows.
2. Configurar puerto 8080.
3. C:\Program Files\Jenkins> jenkins.exe start --> ejecutamos en el cmd para arrancar el servicio Jenkins.
C:\Program Files\Jenkins>jenkins.exe start
2024-06-10 18:48:20,991 INFO  - Starting the service with id 'jenkins'
2024-06-10 18:48:21,977 INFO  - The service with ID 'jenkins' has already been started
- java -jar jenkins.war -> Nos pide una password de administrador que tenemos que copiar para entrar en modo local vía web.
4. Para entrar en modo local -> http://localhost:8080 -> 8080 el puerto que hemos asociado a jenkins. Copiamos la contraseña que está situada en la ruta C:\Program Files\Jenkins\jenkins.err -> archivo de texto donde aparece la contraseña.
Usuario: admin
Contraseña: xxxx
e-mail: xxxx



Instalar Nexus en Windows:
1. Descargamos el archivo zip de Nexus y lo extraemos.
Hay detalles básicos sobre los directorios:
nexus-version -> bin — binarios ejecutables/script 
nexus-version -> etc — archivos de configuración
2. Nexus Repo usa:
- La configuración de integración existe en /etc/fabric
- El servidor Jetty y la configuración existen en /etc/jetty
- Sus paquetes se ejecutan en karaf y la configuración se encuentra en /etc/karaf
- El inicio de sesión utilizado para el registro y la configuración se encuentra en /etc/logback
- Para configurar SSL, necesita cambios en /etc/ssl
- La configuración básica de Nexus está disponible en nexus-default.properties. No debe modificarse. En caso de que se necesiten cambios, cree un archivo llamado 'nexus.properties' y colóquelo como /etc/nexus.properties.
3. Para iniciar nexus:
- Tener java 11 instalado
- En el cmd(importante ejecutarlo como administrador) escribimos la ruta donde está nexus.exe
- Instalamos el servicio nexus con nexus.exe /install, y lo podemos iniciar con nexus.exe /start
- Una vez hecho esto, cerramos el cmd y nos conectamos localmente vía web – http://localhost:8081 y entramos a Nexus
- Iniciamos sesión con el administrador – la contraseña se encuentra en C:\Users\6002336\Downloads\nexus-3.42.0-01-win64\sonatype-work\nexus3\admin.password
Nombre de usuario: admin
Contraseña nueva: xxxx


Instalar Jenkins en Linux:
1. Primero ejecutamos los comandos sudo apt update y apt upgrade para actualizar los paquetes del sistema.
2. Agregue la clave del repositorio al sistema:
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
3. A continuación, vamos a anexar la dirección del repositorio de paquetes de Debian a sources.list del servidor:
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
4. Ejecutar el siguiente comando si no funcionan los 2 anteriores: 
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys
5. Instalaremos Jenkins y sus dependencias:
sudo apt install jenkins
6. Iniciamos Jenkins utilizando systemctl:
sudo systemctl start jenkins
7. Debido a que systemctl no muestra un resultado de estado, utilizaremos el comando status para verificar que Jenkins se haya iniciado de forma correcta:
sudo systemctl status jenkins
8. Editamos el siguiente archivo: 
sudo nano /usr/lib/systemd/system/jenkins.service
9. Descomente la línea y configúrela de la siguiente manera:
TimeoutStartSec=infinity
10. Luego ejecute estos comandos:
systemctl daemon-reload
systemctl start jenkins
11. De manera predeterminada, Jenkins se ejecuta en el puerto 8080. Utilizaremos ufw para abrir ese puerto:
sudo ufw allow 8080
12. Nota: Si el firewall está desactivado, los siguientes comandos lo activarán y permitirán OpenSSH:
sudo ufw enable
13. Compruebe el estado de ufw para confirmar las nuevas reglas:
sudo ufw status
14. Observará que se permite el tráfico desde cualquier lugar al puerto 8080:
15. Para configurar su instalación, visite Jenkins en su puerto predeterminado, 8080, utilizando su nombre de dominio o dirección IP: http://10.0.10.2:8080
16. Debería ver la pantalla Unlock Jenkins (Desbloquear Jenkins), que muestra la ubicación de la contraseña inicial:
17. En la ventana de la terminal, utilice el comando cat para mostrar la contraseña:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Copie la contraseña alfanumérica de 32 caracteres de la terminal, péguela en el campo Administrator password y luego haga clic en Continue.
Usuario: administrador
contraseña: xxxx
Usuario: administrador
contraseña: xxxx
