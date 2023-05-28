# Instalación de Spark

![image](https://github.com/Franmc027/Hadoop-Cluster/assets/123466051/4db29264-6f0e-4764-9374-c585fdc59f3a)


**Este servicio lo vamos a instalar en el Servidor3, por lo cual la siguiente configuración será exclusiva de ese servidor.**


## Instalación y configuración

Lo primero que deberemos hacer es descargar la versión estable más reciente desde la página web oficial de Spark:

```wget https://www.apache.org/dyn/closer.lua/spark/spark-3.4.0/spark-3.4.0-bin-hadoop3.tgz```

Una vez hecho esto debemos descomprimir el archivo y moverlo hacia nuestro $HADOOP_HOME:

```tar -xzvf spark-3.4.0-bin-hadoop3.tar.gz```


```mv spark-3.4.0-bin-hadoop3 $HADOOP_HOME/spark-3-0-4```

Ahora modificamos el ```~/.bashrc``` y añadimos las siguientes líneas:

```
export SPARK_HOME=/home/fmoya/hadoop-3.3.4/spark-3-4-0
export PATH=$PATH:$SPARK_HOME/bin
```

Una vez tenemos esto solo tenemos que dirigir a los archivos de configuración de spark en ```$SPARK_HOME/conf```.

Copiar el arhivo ```spark-env.sh.template``` y crear el archivo ```spark-env.sh``` donde pondremos unos parámetros de configuración:

```cp spark-env.sh.template spark-env.sh```

Ahora entramos dentro del spark-env.sh y colocamos la siguiente configuración:

```
export HADOOP_CONF_DIR=/home/fmoya/hadoop-3.3.4/etc/hadoop
export YARN_CONF_DIR=/home/fmoya/hadoop-3.3.4/etc/hadoop
export PYSPARK_PYTHON=python3
```


