# Instalación de Flume


![flume](https://github.com/Franmc027/Hadoop-Cluster/assets/123466051/61cc7ace-7772-4a87-80ba-e37c7c89576f)

**Este servicio lo vamos a instalar en el Servidor4, por lo cual la siguiente configuración será exclusiva de ese servidor.**


Lo primero que debemos hacer es descargar java8, ya que es la versión que necesita Flume.

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

Una vez hecho esto reiniciamos hadoop desde el servidor1, una vez hecho esto debemos descargar Flume.

```wget https://dlcdn.apache.org/flume/1.11.0/apache-flume-1.11.0-bin.tar.gz```

Lo descomprimimos

```tar -xzvf apache-flume-1.11.0-bin.tar.gz```

Lo movemos a nuestro $hadoop_home

```mv apache-flume-1.11.0-bin $HADOOP_HOME/flume-1.11```

Editamos nuestro ```~/.bashrc``` y añadimos:

```
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export FLUME_HOME=$HADOOP_HOME/flume-1.11
export PATH=$FLUME_HOME/bin:$PATH
```

Ahora nos vamos a la carpeta de configuración de Flume(```$FLUME_HOME/conf```)

```
cp flume-conf.properties.template flume-conf.properties
cp flume-env.sh.template flume-env.sh
```

Despues de haber hesto verificamos que funcione todo, verificando la versión de nuestro flume:

```
flume-ng version
```



