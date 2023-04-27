# Instalacion de Hadoop Commons (HDFS - YARN - MAPREDUCE)

Para nuestro clúster vamos usar la version 3.3.4 de Hadoop.

Para la instalacion de esto primero debemos de instalar la versión recomendada de Java:

```sudo apt-get install openjdk-11-jdk ```


Despues descargamos Apache Hadoop:

```wget https://downloads.apache.org/hadoop/common/hadoop-3.3.4/hadoop-3.3.4.tar.gz```

Una vez echo esto lo descomprimimos

```tar -xzf hadoop-3.3.4.tar.gz```

Entramos dentro 

```cd hadoop-3.3.4```

Modificamos el archivo etc/hadoop/hadoop-env.sh, para definir nuestra version de Java

```export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/```

![image](https://user-images.githubusercontent.com/123466051/233122306-dfbf5530-102a-4da0-ab20-396adf2475f7.png)


Para mas comodidad, vamos a añadir las siguientes variables a ~/.bashrc, para poder utilizar los comandos de hdfs desde cualquier lado.

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

También deberíamos modificar el archivo /etc/hosts para mas comodidad, para ello copiar lo siguinte en el archivo, modifica las ip con tu configuración **Importante** las tres ultimas ip tienen que tener el nombre de tus servidores:


```
192.168.12.220 proyecto-argus

192.168.12.220 servidor1
192.168.12.221 servidor2
192.168.12.222 servidor3

192.168.12.220 220-bda-fmc-servidor1
192.168.12.221 221-bda-dmc-servidor2
192.168.12.222 222-bda-fmc-servidor3

```

Antes de empezar debemos poder conectarnos vía ssh desde el servidor1 hacia los servidores 2, 3 y a si mismo sin contraseña, para ello haremos lo siguiente.

Primero debemos entrar ~/.ssh/

``` cd $home/.ssh ```

Una vez estemos allí debemos crear unas claves para poder entrar sin necesidad de contraseña. **Importante** debemos crear estas claves, sin ninguna contraseña encriptada, para que no nos pida esta cuando vallamos a conectarnos.

```ssh-keygen -b 4096```

Esto nos generará 2 claves una privada y otra pública, lo primero que tenemos que hacer es poner esa clave pública claves autorizadas. para poder conectarnos a nosotros mismo sin contraseña:

```cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys```

Ahora tenemos que hacer lo mismo en los servidores 2 y 3.
Nos pasamos la clave al servidor 2 y 3 con el comando SCP, una vez en el servidor2  y servidor3 debemos realizar el mismo comando que antes:

```cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys```

y ya nos podríamos conectar por ssh sin contraseña



Una vez hecho esto empezamos a configurar el core-site y el hdfs-site.
Nos vamos al core-site.xml que esta en la $hadoop_home/etc/hadoop/ y añadimos la siguiente configuración:

```
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://proyecto-argus:9000</value>
    </property>
</configuration>
```

Ahora nos dirigimos al hdfs-site.xml, donde pondremos la configuración de nuestro HDFS en nuestro caso tendremos un factor de réplica de 2.

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



