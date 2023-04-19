# Instalacion de Hadoop Commons y HDFS

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


Una vez echo esto empezamos a configurar el core-site y el hdfs-site.
Nos vamos al core-site.xml que esta en la $hadoop_home/etc/hadoop/ y añadimos la siguiente configuración:

```

```





