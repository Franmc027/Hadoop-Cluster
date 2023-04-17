# Descripción de los servicios 

Los servicios que vamos a usar son:

[HDFS](#id1)

[MapReduce](#MapReduce)

[Yarn](#Yarn)

[Hive](#Hive)

[Pig](#)

[Flume](#)

[Hue](#)

[Spark](#)

[Zookeeper](#)

[HBase](#)

[Kafka](#)

[Nifi](#)

## HDFS <a name="id1"></a>

![image](https://user-images.githubusercontent.com/123466051/232528652-5f45d047-f766-4cda-9a18-86e31b539800.png)

HDFS está diseñado para almacenar y procesar grandes conjuntos de datos en un cluster de Hadoop, y está optimizado para aplicaciones de procesamiento de datos en paralelo utilizando la tecnología de MapReduce. HDFS divide los archivos grandes en bloques más pequeños y los distribuye en varios nodos en el cluster. Cada bloque de datos se replica en varios nodos para proporcionar tolerancia a fallos y alta disponibilidad.

El diseño de HDFS se basa en los siguientes componentes:

NameNode: es el nodo maestro que gestiona el sistema de archivos. Se encarga de la asignación de bloques de datos a los nodos de datos y realiza un seguimiento de la ubicación de los bloques.

DataNode: son los nodos de almacenamiento que almacenan los bloques de datos. Se encargan de leer y escribir los datos en el disco y de enviar la información al NameNode.


## MapReduce <a name="MapReduce"></a>

![image](https://user-images.githubusercontent.com/123466051/232530114-812a64d4-b439-41fc-b089-cc8dc5fa671d.png)

MapReduce se basa en el procesamiento en paralelo de grandes conjuntos de datos a través de la división del trabajo en tareas más pequeñas, y luego la combinación de los resultados de esas tareas para producir el resultado final. Se divide en dos fases principales:

Fase de Map: en esta fase, los datos de entrada se dividen en fragmentos más pequeños y se procesan en paralelo en varios nodos del cluster. Cada nodo aplica una función de "map" a los datos de entrada para producir una lista de pares clave-valor.

Fase de Reduce: en esta fase, los pares clave-valor generados por la fase de Map se agrupan y procesan en paralelo en varios nodos del cluster. Cada nodo aplica una función de "reduce" a los datos para producir un resultado final.


## Yarn <a name="Yarn"></a>

![image](https://user-images.githubusercontent.com/123466051/232530684-6f33ab93-a12f-4b7a-8aed-dad3e7a43442.png)


Antes de la introducción de YARN, el procesamiento de datos en un cluster de Hadoop estaba limitado al modelo de MapReduce. Esto significaba que el cluster sólo podía ejecutar aplicaciones de MapReduce, lo que limitaba su versatilidad. YARN fue desarrollado para superar estas limitaciones y permitir que otras aplicaciones, además de MapReduce, se ejecuten en un cluster de Hadoop.

YARN proporciona una plataforma de programación distribuida que permite a los desarrolladores escribir aplicaciones de procesamiento de datos que se ejecutan en un cluster de Hadoop. Proporciona un administrador de recursos y un planificador que asigna los recursos del cluster a las tareas en ejecución. Esto permite que varias aplicaciones se ejecuten en el mismo cluster y compartan los mismos recursos.

La arquitectura de YARN se basa en dos componentes principales:

ResourceManager: Es el nodo maestro que administra los recursos del cluster y programar las tareas. Es responsable de asignar recursos a las aplicaciones y monitorear su estado.

NodeManager: Es el nodo esclavo que se ejecuta en cada nodo del cluster y administra los recursos locales del nodo, como la memoria y la CPU. Es responsable de iniciar y detener las tareas y reportar el estado al ResourceManager.

En resumen, YARN es un componente de Apache Hadoop que se utiliza para administrar los recursos de un cluster y programar las tareas en un entorno distribuido. Proporciona una plataforma de programación distribuida que permite a los desarrolladores escribir aplicaciones de procesamiento de datos que se ejecutan en un clúster de Hadoop.


## Hive <a name="Hive"></a>



