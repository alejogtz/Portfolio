# Setup JSF Project on Netbeans on Windows 10.
> Official documentation of JEE made by Oracle can be found at this [url][2]

## JEE Installation 
> **Only if** you do not have installed by default. This may be selected when start netbeans installation.

**Add new Configuration Center**

<!-- <details> <summary>Open NetBeans and following next steps</summary> -->


Go to `Tools > Plugins > Settings` and click on `add` button for fill form with these values:

[![01.jpg](https://i.postimg.cc/sg5nkNYz/01.jpg)](https://postimg.cc/LJ6BfvQQ)

	name: <Whatever you want> JEE
	url: https://updates.netbeans.org/netbeans/updates/8.2/uc/final/distribution/catalog.xml.gz

After that, check this plugins for being installed on `Avalaible Plugins` tab. (In this case I've already installed :'D)

[![02.jpg](https://i.postimg.cc/43NSp1cT/02.jpg)](https://postimg.cc/yDtjHcnf)

Plugins will begin to be installed and when it finished just restart IDE and you'll be avalaible for creating JJE projects.

<!-- </details> -->

## Glassfish Installation

Download `Derby 4.1.Zip` which is the stable versión

	# curl -O -L http://download.oracle.com/glassfish/4.1/release/glassfish-4.1.zip --insecure
	$ curl -L http://download.oracle.com/glassfish/4.1/release/glassfish-4.1.zip --insecure -o glassfish-4.1.zip
	
> More versions can be found on [Oracle Page](https://download.oracle.com/glassfish/4.1/release/index.html)

> if you not specified `-o` arg `curl` print on tty by default ;'), so, dont forge specify it :'v
	
Unzip glassfish zip on `/apt/` or custom third party apps folder
	
	$ unzip glassfish-4.1.zip -d C:\MyApps\Servers
	
Move into server folder and start server

	$ cd C:\MyApps\Servers\glassfish4\
	

Open netbeans and add new Server on Services Tab. (*This tab can be opened by press `Ctrl + 5` or in Netbeans tab `Window > Services`*)

[![03.jpg](https://i.postimg.cc/hGTNDGVX/03.jpg)](https://postimg.cc/QBNfSh4D)

[![04.jpg](https://i.postimg.cc/rpNgZRSN/04.jpg)](https://postimg.cc/mchQtDpP)

[![05.jpg](https://i.postimg.cc/yNjXy4Hf/05.jpg)](https://postimg.cc/DWWX7Nms)
	
On configuration field you can fill them considering the next advices.

- `Domain`: A domain contains a group of GlassFish Server instances that are administered together. Each domain has a domain administration server (DAS) that hosts administrative applications.

**Creating a Domain**
This example creates a domain named domain1 . When you type the command, you might be prompted for login information.

```bash
$ asadmin> create-domain --adminport 4848 domain1
	Enter admin user name[Enter to accept default]>
	Using port 4848 for Admin.
	Default port 8080 for HTTP Instance is in use. Using 1161
	Using default port 7676 for JMS.
	Using default port 3700 for IIOP.
	Using default port 8081 for HTTP_SSL.
	Using default port 3820 for IIOP_SSL.
	Using default port 3920 for IIOP_MUTUALAUTH.
	Default port 8686 for JMX_ADMIN is in use. Using 1162
	Distinguished Name of the self-signed X.509 Server Certificate is:
	[CN=moonbeam.gateway.2wire.net,OU=GlassFish,O=Oracle Corp.,L=Redwood Shores,ST
	California,C=US]
	Domain domain1 created.
	Command create-domain executed successfully
```
To start the Administration Console in a browser, enter the URL in the following format:
	
	http://hostname:5000

For this example, the domain's log files, configuration files, and deployed applications
now reside in the following directory:

	domain-root-dir/mydomain

- `Host`: 
-`Loopback`:
-`DAS Port`:
-`HTTP Port`:
-`Tarjet`:
-`Username`: 
-`Password`:

> Full informacion of glassfish administration can be found on [official PDF][1] in their glassfish website

> Review [Page 33][1] for more details about fields and their meanings. xD


### Glassfish CLI Cheatsheet

**Start Server**

To Start GlassFish Server Using NetBeans IDE
1. Click the Services tab.
2. Expand Servers.
3. Right-click the GlassFish Server instance and select Start.

To Start GlassFish Server Using the Command Line, open a terminal window or command prompt and execute the following:
```bash	
# cd C:\MyApps\Servers\GlassFish4\bin # Here is also an asadmin.bat file xD
$ cd C:\MyApps\Servers\GlassFish4\glassfish\bin

$ asadmin start-domain --verbose
$ asadmin stop-domain domain1
```
> For more details visit [Oracle Page](https://docs.oracle.com/javaee/7/tutorial/usingexamples002.htm)

> fix error message `GlassFish requires Java SE version 6.  Your JDK is version 0`
> edit `asenv.conf` in `PATH_TO_YOUR_GLASSFISH/glassfish/config` folder, go to end of lines and add `set AS_JAVA=/PATH_TO_YOUR_JAVA/Java/JavaVirtualMachines/jdk-YOUR-VERSION.jdk` following the answer on [stackoverflow](https://stackoverflow.com/questions/47490645/glassfish-requires-java-se-version-6-your-jdk-is-version-0-mac)

**List Domains**

	asadmin> list-domains
	Name: domain1 Status: Running
	Name: domain4 Status: Not Running
	Name: domain6 Status: Not Running
	Command list-domains executed successfully

If you want to log in to another domain, invoke
> For More details review page 38 of de [official pdf][1]

	$ asadmin login with new values for --host and --port
	
**Starting and Stopping the Java DB Server**

GlassFish Server includes the Java DB database server.

To start the Java DB server from the command line, open a terminal window or command prompt and execute:

	$ asadmin start-database
	
	$ asadmin stop-database

> Visit Oracle Java Documentation for more [details](https://docs.oracle.com/javaee/7/tutorial/usingexamples004.htm)
## Glassfish Configuration With Derby

Move into glassfish admin folder
	
	$ cd C:\MyApps\Servers\GlassFish4\glassfish\bin
	
Execute as admin (*This example starts Derby on the host host1 and port 5001.*)
```bash
# Start Database
$ asadmin
asadmin > start-database --dbhost host1 --dbport 5001 --terse=true
Starting database in the background. 
Log redirected to /opt/SUNWappserver/databases/javadb.log.
Command start-database executed successfully.

# Stop Database
asadmin> stop-database --dbhost=localhost --dbport=5001
```	

**Create a Database**

> Following steps from [Oracle GlassFish Administration Guide ](https://docs.oracle.com/cd/E18930_01/html/821-2416/ggkon.html)

Move into database administration folder

	$ cd C:\MyApps\Servers\glassfish4\javadb\bin
	.
	├── NetworkServerControl
	├── NetworkServerControl.bat
	├── dblook
	├── dblook.bat
	├── derby_common.bat
	├── ij
	├── ij.bat
	├── setEmbeddedCP
	├── setEmbeddedCP.bat
	├── setNetworkClientCP
	├── setNetworkClientCP.bat
	├── setNetworkServerCP
	├── setNetworkServerCP.bat
	├── startNetworkServer
	├── startNetworkServer.bat
	├── stopNetworkServer
	├── stopNetworkServer.bat
	├── sysinfo
	└── sysinfo.bat

	0 directories, 19 files
	
And open `ij.bat` for [Interactive JDBC scripting tool](https://docs.oracle.com/cd/E18930_01/html/821-2416/ggkon.html#gharl)

	$ .\ij.bat
	ij> <here your commands>
	
	# Type help to see command information.

<details>
	<summary>Comandos que soporta Interactive JDBC scripting tool</summary>

```bash
 Los comandos soportados son los siguientes:

  PROTOCOL 'protocolo JDBC' [ AS ident ];
                               -- define un protocolo con nombre o por defecto
  DRIVER 'clase para el controlador';   -- carga la clase con nombre
  CONNECT 'URL de la base de datos' [ PROTOCOL namedProtocol ] [ AS connectionName 
  ...
  ...
 Cualquier comando no reconocido se trata potencialmente como un comando SQL-J y se ejecuta directamente.
``` 
</details>

> A well documented page using `ij` that show examples of how to use it can be found on [`Here`](https://www.javacodegeeks.com/2018/05/apache-derby-database-users-and-permissions.html)

**Steps for creation and using netbeans'sql editor are in [NetBeans Documentation Website](https://netbeans.apache.org/kb/docs/ide/java-db.html )**

> Before configurate on glassfish connection pools and resources you must already have configurated __Derby__ or __MySql__ Database Server.

## Setup MySQL driver

An existed MySql Driven can be found in your NetBeans Programam. Open NetBeans 
- Expand `Tools` menu.
- Clik on `Libraries`
- Find `MySQL JDBC Driver` and copy Library classpath location.

**Copy** driver on domain/lib folder of glassfish.

```bash
# cd C:\Program Files\NetBeans 8.2\ide\modules\ext\mysql-connector-java-5.1.23-bin.jar
$ cd $NETBEANS_INSTALLATION/ide/modules/ext/

# cp mysql-connector-java-5.1.23-bin.jar C:\MyApps\Servers\glassfish4\glassfish\domains\domain1\lib\mysql-connector-java-5.1.23-bin.jar
$ cp mysql-connector-java-5.1.23-bin.jar $GLASSFISH_DOMAIN_FOLDER/lib/
```

**or** Download it from archive repository.

```bash
$ curl -sSL -O https://downloads.mysql.com/archives/get/p/3/file/mysql-connector-java-5.1.49.zip

```

## Glassfish Configuration With MySql


### Connection Pool and Resource on Glassfish Admin Console


# Interesting topics 
**Interesting topics of Oracle Documentation and Glassfish administration**

* The following topics are addressed [here][3]:
	* Required Software
	* Starting and Stopping GlassFish Server
	* Starting the Administration Console
	* Starting and Stopping the Java DB Server
	* Building the Examples
	* Tutorial Example Directory Structure
	* Java EE 7 Maven Archetypes in the Tutorial
	* Getting the Latest Updates to the Tutorial
	* Debugging Java EE Applications

* Oracle GlassFish Administration Guide [Here][4]

* PDF Version of Oracle JEE Tutorial can be foun [Here][6]

[1]: https://javaee.github.io/glassfish/doc/5.0/administration-guide.pdf
[2]: https://docs.oracle.com/javaee/7/tutorial/index.html
[3]: https://docs.oracle.com/javaee/7/tutorial/usingexamples.htm#GFIUD
[4]: https://docs.oracle.com/cd/E18930_01/html/821-2416/ggkon.html
[5]: https://db.apache.org/derby/docs/10.0/manuals/develop/develop101.html
[6]: https://docs.oracle.com/javaee/7/JEETT.pdf

























