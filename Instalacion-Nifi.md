# Instalación de NIFI

![image](https://github.com/Franmc027/Hadoop-Cluster/assets/123466051/a0c6182b-915f-44fb-a42d-c9d0a3f90731)

**Este servicio lo vamos a instalar en el Servidor4, por lo cual la siguiente configuración será exclusiva de ese servidor.**

## Instalación

Descargamos la última versión de NIFI:

``` wget https://dlcdn.apache.org/nifi/1.21.0/nifi-1.21.0-bin.zip```

Descomprimimos el zip:

```unzip nifi-1.21.0-bin.zip```

Lo movemos a $HADOOP_HOME:

```mv nifi-1.21.0 $HADOOP_HOME/nifi-1-21-0```

Modificamos  nuestro  bashrc (```nano ~/.bashrc```) y añadimos al final:

```
export NIFI_HOME=$HADOOP_HOME/nifi-1-21-0
export PATH=$NIFI_HOME/bin:$PATH
```

## Configuración

Nos dirigimos a la carpeta conf (```cd $NIFI_HOME/conf```) y modificamos las siguientes líneas del archivo nifi.properties

```
nifi.web.https.host=192.168.12.223
nifi.web.https.port=8443
```
Esto nos da acceso a la aplicación web de nifi por el puerto indicado.

Iniciamos nifi con:

```nifi.sh start```

Para poder entrar a la interfaz web nos va a pedir un usuario y una contraseña, para establecer este realizamos el siguiente comando:

``` nifi.sh set-single-user-credentials usuario contraseña```

Ya podríamos entrar a la interfaz web escribiendo la siguiente url en nuestro buscador:

```https:192.168.12.223:8443```



