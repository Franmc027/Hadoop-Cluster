# Instalación de Kafka con Zookeeper

![image](https://github.com/Franmc027/Hadoop-Cluster/assets/123466051/7994c06e-3038-49ef-b61e-f9f39385dae2)

**Este servicio lo vamos a instalar en el Servidor4, por lo cual la siguiente configuración será exclusiva de ese servidor.**

## Instalación 

Lo primero que vamos a hacer es descargar desde la web oficial la ultima version estable de Kafka (esta ya viene con Zookeeper integrado)

```wget https://downloads.apache.org/kafka/3.4.0/kafka-3.4.0-src.tgz```

Descomprimimos y lo movemos a la carpeta nuestra

```tar -xzvf kafka-3.4.0-src.tgz```

```mv kafka-3.4.0-src $HADOOP_HOME/kafka-3-4-0```

Añadimos las siguientes lineas a nuestro ```~/.bashr```

```
export KAFKA_HOME=$HADOOP_HOME/kafka-3-4-0
export PATH=$KAFKA_HOME/bin:$PATH
```
 Lo actualizamos:
 
 ```source ~/.bashrc```
 
 ## Configuración
 
 Empezamos a configurar Kafka, para ello nos vamos ```$KAFKA_HOME/config```. Lo primero que vamos a hacer es entrar en ```Zookeeper.properties```
 
 En mi caso e cambiado solo la dirección de los logs para no perderlos cadavez que se apaga, para ello cambiamos la ruta de estos en mi caso:
 
 ```dataDir=/home/fmoya/zookeeper-log/zookeeper```


Despues de esto nos vamos al archivo ```server.properties```

- Descomentamos la siguiente linea y colocalmos la ip de la maquina donde va a estar este kafaka:
```listeners=PLAINTEXT://192.168.12.223:9092```
 
 - Modificamos la línea donde proporcionamos donde va a escuchar Zookeeper:
 ```zookeeper.connect=192.168.12.223:2181```
 
 - También como antes hemos echo en el archivo de zookeeper.properties voy a cambiar la direcion de los logs:
 ```log.dirs=/home/fmoya/kafka-logs```
 
 Una vez echo esto debemos iniciar los procesos en el siguiente orden (para ello deberemos ocupar 2 terminales o lanzarlos en segundo plano con &):
 
 - Iniciamos Zookeeper(le debemos pasar donde esta el archivo de configuración como argumento):
    ``` zookeeper-server-start.sh $KAFKA_HOME/config/zookeeper.properties ```
    
 - Iniciamos Kafka(le debemos pasar donde esta el archivo de configuración como argumento):
   ```kafka-server-start.sh $KAFKA_HOME/config/server.properties```
 
 Ya tendriamos kafka iniciado, para comprobar que esta funcionando vamos a crear un topic:
 
 ```kafka-topics.sh --create --bootstrap-server 192.168.12.223:9092 -topic prueba```
 
 Para comprobar que se ha creado vamos a listar todos los topics
 
 ``` kafka-topics.sh --list --bootstrap-server 192.168.12.223:9092```
 
 
 
 






