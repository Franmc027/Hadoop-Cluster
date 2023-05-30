# Ejemplo de uso de Flume

Vamos a crear un agente sencillo, este va a mirar un directorio y cuando un nuevo archivo aparezca lo guardará en una carpeta de HDFS. El agente es el siguiente:

```
# Nombramos los componentes del agente
spooldir.sources = spooldir_source
spooldir.channels = memory_channel
spooldir.sinks = hdfs_sink

# Configuramos las propiedades source
spooldir.sources.spooldir_source.type = spooldir
spooldir.sources.spooldir_source.spoolDir = /home/fmoya/flume-files/input
spooldir.sources.spooldir_source.fileHeader = true
spooldir.sources.spooldir_source.basenameHeaderKey = fileName

# Configuramos las propiedades channel
spooldir.channels.memory_channel.type = memory
spooldir.channels.memory_channel.capacity = 10000
spooldir.channels.memory_channel.transactionCapacity = 10000

# Configuramos las propiedades sink
spooldir.sinks.hdfs_sink.type = hdfs
spooldir.sinks.hdfs_sink.hdfs.path = hdfs://proyecto-argus:9000/bda/flume/spooldir
spooldir.sinks.hdfs_sink.writeFormat = Text
spooldir.sinks.hdfs_sink.fileType = DataStream
spooldir.sinks.hdfs_sink.hdfs.filePrefix = spooldir-

# Vinculamos source con sink a través de channel
spooldir.sources.spooldir_source.channels = memory_channel
spooldir.sinks.hdfs_sink.channel = memory_channel
```
Lanzamos el agente:

```flume-ng agent -n spooldir --conf ./ -f prueba-hdfs.conf```

