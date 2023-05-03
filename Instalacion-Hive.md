# Instalación de Hive

![image](https://user-images.githubusercontent.com/123466051/235984587-7ce18c2b-d2a0-44c6-a3db-9238d540229b.png)


**Este servicio lo vamos a instalar en el Servidor2, por lo cual la siguiente configuración será exclusiva de ese servidor.**

## Descarga de hive y procesos previos

Lo primero que debemos hacer es descargar la versión de hive que vamos a usar en mi caso la 3.1.3.

```wget https://dlcdn.apache.org/hive/hive-3.1.3/apache-hive-3.1.3-bin.tar.gz```

Lo descomprimimos y lo movemos hacia $hadoop_home:

```tar -xzvf apache-hive-3.1.3-bin.tar.gz```

```mv apache-hive-3.1.3-bin $HADOOP_HOME/hive-3.1.3```

Necesitamos añadir las siguientes variables de entorno a nuestro ~/.bashrc:

```
export HIVE_HOME=$HADOOP_HOME/hive-3.1.3
export PATH=$HIVE_HOME/bin:$PATH
export HIVE_CONF_DIR=$HIVE_HOME/conf
```

Ahora debemos actualizar nuestras variables con el siguiente comando:

```source ~/.bashrc```

La versión que hemos descargado de hive necesita java 8 para funcionar, para ello la descargamos:

```sudo apt-get install openjdk-8-jdk```

Comprobamos que se ha descargado:

```update-alternatives --list java```

y nos debe de salir lo siguiente:

```
/usr/lib/jvm/java-11-openjdk-amd64/bin/java
/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
```

Ahora debemos cambiar la variable de java en nuestro hadoop-env.sh(```/$hadoop_home/etc/hadoop/hadoop-env.sh```)

```export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64```

## Configuración de hive(```$hive_home/conf```)

Para empezar con la configuración de hive lo primero que vamos a hacer es crear una copia de los archivos principal de configuración, estos están en ```$hive_home/conf```

```
cp hive-default.xml.template hive-site.xml
cp hive-env.sh.template hive-env.sh
cp hive-exec-log4j2.properties.template hive-exec-log4j2.properties
cp hive-log4j2.properties.template hive-log4j2.properties
```

Modificamos el fichero hive-env.sh y añadimos las siguientes líneas:

```
export HIVE_HOME=$HADOOP_HOME/hive-3.1.3
export HIVE_CONF_DIR=$HIVE_HOME/conf
```

Nos preparamos el entorno en HDFS para trabajar con hive en este:

```
hdfs dfs -rm -r /tmp
hdfs dfs -mkdir /tmp
hdfs dfs -mkdir -p /user/hive/warehouse
hdfs dfs -chmod g+w /tmp
hdfs dfs -chmod g+w /user/hive/warehouse
```

Modificamos el hive-site.xml con las siguientes líneas, ** Importante ** estas líneas deben estar al principio para poder sobrescribir los valores por defecto:

``` <property>
        <name>system:java.io.tmpdir</name>
        <value>/tmp/hive/java</value>
    </property>
    <property>
        <name>system:user.name</name>
        <value>${user.name}</value>
    </property>
```

Ahora nos dirigimos a la carpeta donde vamos a crear el schema para nuestra base de datos, en mi caso he creado una carpeta en $home para ello:

```
cd $home
mkdir Hive_Metastore
cd Hive_Metastore
```

Ahora creamos el schema:

```schematool -dbType derby -initSchema```

Una vez creado el schema debemos iniciar el servicio hive con el siguiente comando, ** Importante ** debemos realizar este comando donde hemos creado el schema:

```hiveserver2```

Este comando se quedara activo por lo tanto tendremos que abrir otra terminal para seguir trabajando


## Habilitar la conexión con el proxy user
Ahora para poder conectarnos con nuestro usuario a nuestra base de datos debemos modificar el core-site(```$hadoop_home/etc/hadoop/core-site.xml```), 
Debemos copiar las siguientes lineas, **Importante** debes modificar donde pone **tuUsuario** por el nombre de tu usuario:

```
   <property>
        <name>hadoop.proxyuser.tuUsuario.hosts</name>
        <value>*</value>
    </property>
    <property>
        <name>hadoop.proxyuser.tuUsuario.groups</name>
        <value>*</value>
    </property>
```

Ahora debemos reiniciar hadoop y parar el comando hiveserver2 y volverlo a lanzar.

Después de esto ya podríamos conectarnos con hive con el siguiente comando:

```beeline -u jdbc:hive2://ip-de-tu-servidor:10000/ -n tuUsuario```

Hive también dispone de una interfaz web para acceder a esta debemos poner en el buscador la ip de nuestro server de hive y el puerto 10002:
``
![image](https://user-images.githubusercontent.com/123466051/235991141-12308a61-77a3-4004-b60c-0c2c049f0b2f.png)





   

