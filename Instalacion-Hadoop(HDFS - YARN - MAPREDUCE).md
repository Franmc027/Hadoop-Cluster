# Instalación de Hadoop Commons (HDFS - YARN - MAPREDUCE)

Para nuestro clúster vamos a usar la versión 3.3.4 de Hadoop.

***Importante esta configuración se realizará en el servidor1, y despues deberas replicarla en los servidores workers(servidor2, 3 y 4)***

Para la instalación de esto primero debemos de instalar la versión recomendada de Java:

```sudo apt-get install openjdk-11-jdk ```

## Descargar y descomprimir Hadoop

En nuestro caso utilizaremos la versión 3.3.4, para descargarla realizamos el siguiente comando:

```wget https://downloads.apache.org/hadoop/common/hadoop-3.3.4/hadoop-3.3.4.tar.gz```

Una vez hecho esto lo descomprimimos

```tar -xzf hadoop-3.3.4.tar.gz```

Entramos dentro 

```cd hadoop-3.3.4```

Modificamos el archivo etc/hadoop/hadoop-env.sh, para definir nuestra versión de Java

```export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/```

![image](https://user-images.githubusercontent.com/123466051/233122306-dfbf5530-102a-4da0-ab20-396adf2475f7.png)

## Variables ~/.bashrc

Para más comodidad, vamos a añadir las siguientes variables a ~/.bashrc, para poder utilizar los comandos de hdfs desde cualquier lado.

```
export HADOOP_HOME=$HOME/hadoop-3.3.4 

export HADOOP_INSTALL=$HADOOP_HOME 

export HADOOP_MAPRED_HOME=$HADOOP_HOME 

export HADOOP_COMMON_HOME=$HADOOP_HOME 

export HADOOP_HDFS_HOME=$HADOOP_HOME 

export HADOOP_YARN_HOME=$HADOOP_HOME 

export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native 

export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin 

export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
```

![image](https://user-images.githubusercontent.com/123466051/233123499-78299819-da75-406b-88ed-7bce27ce25b8.png)

Para comprobar de que todo va correctamente ejecutamos el siguiente comando:

``` hadoop ```


## Modificación del archivo /etc/hosts

También deberíamos modificar el archivo /etc/hosts para mas comodidad, para ello copiar lo siguinte en el archivo, modifica las ip con tu configuración **Importante** las tres últimas ip tienen que ir acompañadas de el nombre de tus servidores:


```
192.168.12.220 proyecto-argus

192.168.12.220 servidor1
192.168.12.221 servidor2
192.168.12.222 servidor3
192.168.12.223 servidor4


192.168.12.220 220-bda-fmc-servidor1
192.168.12.221 221-bda-dmc-servidor2
192.168.12.222 222-bda-fmc-servidor3
192.168.12.223 222-bda-fmc-servidor4


```

## Conexión por ssh sin contraseña entre servidores

Antes de empezar debemos poder conectarnos vía ssh desde el servidor1 hacia los servidores 2, 3 y a si mismo sin contraseña, para ello haremos lo siguiente.

Primero debemos entrar ~/.ssh/

``` cd $home/.ssh ```

Una vez estemos allí debemos generar unas claves para poder entrar sin necesidad de contraseña. **Importante** debemos crear estas claves, sin ninguna contraseña encriptada, para que no nos pida esta cuando vallamos a conectarnos.

```ssh-keygen -b 4096```

Esto nos generará 2 claves, una privada y otra pública, lo primero que tenemos que hacer es poner esa clave pública claves autorizadas. Para poder conectarnos a nosotros mismo sin contraseña:

```cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys```

Ahora tenemos que hacer lo mismo en los servidores 2 , 3 Y 4.
Nos pasamos la clave al servidor 2 y 3 con el comando SCP, una vez en el servidor2  y servidor3 debemos realizar el mismo comando que antes:

```cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys```

y ya nos podríamos conectar por ssh sin contraseña


## Configuración del core-site.xml

Una vez hecho esto empezamos a configurar el core-site y el hdfs-site.
Nos vamos al core-site.xml que está en la $hadoop_home/etc/hadoop/ y añadimos la siguiente configuración:

```
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://proyecto-argus:9000</value>
    </property>
</configuration>
```

## Configuracion HDFS-site.xml

Ahora nos dirigimos a /$home_hadoop/etc/hadoop/hdfs-site.xml, donde pondremos la configuración de nuestro HDFS en nuestro caso tendremos un factor de réplica de 2.

```
<configuration>

<property>
    <name>dfs.namenode.name.dir</name>
    <value>/home/fmoya/hadoop_data/hdfs/namenode</value>
  </property>

  <property>
    <name>dfs.datanode.data.dir</name>
    <value>/home/fmoya/hadoop_data/hdfs/datanode</value>
  </property>

  <property>
    <name>dfs.replication</name>
    <value>2</value>
  </property>

</configuration>
```

## Mapred-site.xml

Ahora nos dirigimos a /$home_hadoop/etc/hadoop/Mapred-site.xml y copiamos la siguiente configuración:

```
<configuration>
    <property>
            <name>mapreduce.framework.name</name>
            <value>yarn</value>
    </property>
</configuration>
```


## Yarn-site.xml

Lo primero que tenemos que hacer es conseguir el classpaht para ello realizamos este comando:

```echo `hadoop classpath` ```

Nos dirigimos a /$home_hadoop/etc/hadoop/yarn-site.xml y copiamos la siguiente configuración, debes cambiar el parametro yarn.resourcemanager.hostname con la ip de tu resourcemanager, en mi caso es el server1, también debes modificar el parámetro yarn.application.classpath con la salida del comando anterior:

```
<configuration>
    <property>
        <name>yarn.webapp.ui2.enable</name>
        <value>true</value>
    </property>

    <property>
            <name>yarn.acl.enable</name>
            <value>0</value>
    </property>

    <property>
            <name>yarn.resourcemanager.hostname</name>
            <value>192.168.12.220</value>
    </property>
	
    <property>
        <name>yarn.application.classpath</name>
        <value>/home/fmoya/hadoop-3.3.4/etc/hadoop:/home/fmoya/hadoop-3.3.4/share/hadoop/common/lib/*:/home/fmoya/hadoop-3.3.4/share/hadoop/common/*:/home/fmoya/hadoop-3.3.4/share/hadoop/hdfs:/home/fmoya/hadoop-3.3.4/share/hadoop/hdfs/lib/*:/home/fmoya/hadoop-3.3.4/share/hadoop/hdfs/*:/home/fmoya/hadoop-3.3.4/share/hadoop/mapreduce/*:/home/fmoya/hadoop-3.3.4/share/hadoop/yarn:/home/fmoya/hadoop-3.3.4/share/hadoop/yarn/lib/*:/home/fmoya/hadoop-3.3.4/share/hadoop/yarn/*</value>
    </property>

    <property>
            <name>yarn.nodemanager.aux-services</name>
            <value>mapreduce_shuffle</value>
    </property>
</configuration>

```

## Workers

Ahora como en nuestra configuración de clúster vamos a tener un servidor principal y varios workers, tenemos que modificar el archivo /$hadoop_home/etc/hadoop/workers,
este archivo nos indicara cuáles van a ser los servidores donde pondremos los datanodes y los nodemanagers, en nuestro caso el archivo es el siguiente:

```
servidor2
servidor3
servidor4
```

## Configuracíon servidores workes

Debemos hacer el proceso anterior en todos los nodos workes que tengamos, en mi caso en el servidor 2, 3 y 4.

## Lanzamiento de HDFS y YARN

Una vez echo todo lo anterior, ya podemos iniciar estos dos servicios, esto se debe realizar desde el servidor master(servidor1):

``` start-dfs.sh ```

``` start-yarn.sh ```

Una vez realizado esto podremos entrar a la interfaz web de estos servicios:

HDFS:
    ```
    IP-SERVER1:9870 --> Ejemplo: 192.168.12.220:9870
    ```
    
![image](https://user-images.githubusercontent.com/123466051/235992798-56ddf13b-16be-44c0-ba54-6821efbcaef6.png)


![image](https://github.com/Franmc027/Hadoop-Cluster/assets/123466051/4aa64f4d-9385-47d4-8adc-5e8fadd07301)


    
YARN
    ```
    IP-SERVER1:8088/ui2 --> Ejemplo: 192.168.12.220:8088/ui2
    ```
![image](https://user-images.githubusercontent.com/123466051/235992939-9aa9d30d-04e1-4af8-b265-c413e8f10245.png)





