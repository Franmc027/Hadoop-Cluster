# Descripción de los servicios 

Los servicios que vamos a usar son:

[HDFS](#id1)

[MapReduce](#id2)

[Yarn](#id3)

[Hive](#id4)

[Pig](#id5)

[Flume](#id6)

[Hue](#id7)

[Spark](#id8)

[Zookeeper](#id9)

[HBase](#id10)

[Kafka](#id11)

[Nifi](#id12)

## HDFS <a name="id1"></a>

![image](https://user-images.githubusercontent.com/123466051/232534226-15a6cc3a-5d11-42e1-a397-106f81cbb745.png)

HDFS está diseñado para almacenar y procesar grandes conjuntos de datos en un cluster de Hadoop, y está optimizado para aplicaciones de procesamiento de datos en paralelo utilizando la tecnología de MapReduce. HDFS divide los archivos grandes en bloques más pequeños y los distribuye en varios nodos en el cluster. Cada bloque de datos se replica en varios nodos para proporcionar tolerancia a fallos y alta disponibilidad.

El diseño de HDFS se basa en los siguientes componentes:

NameNode: es el nodo maestro que gestiona el sistema de archivos. Se encarga de la asignación de bloques de datos a los nodos de datos y realiza un seguimiento de la ubicación de los bloques.

DataNode: son los nodos de almacenamiento que almacenan los bloques de datos. Se encargan de leer y escribir los datos en el disco y de enviar la información al NameNode.


## MapReduce <a name="id2"></a>

![image](https://user-images.githubusercontent.com/123466051/232530114-812a64d4-b439-41fc-b089-cc8dc5fa671d.png)

MapReduce se basa en el procesamiento en paralelo de grandes conjuntos de datos a través de la división del trabajo en tareas más pequeñas, y luego la combinación de los resultados de esas tareas para producir el resultado final. Se divide en dos fases principales:

Fase de Map: en esta fase, los datos de entrada se dividen en fragmentos más pequeños y se procesan en paralelo en varios nodos del cluster. Cada nodo aplica una función de "map" a los datos de entrada para producir una lista de pares clave-valor.

Fase de Reduce: en esta fase, los pares clave-valor generados por la fase de Map se agrupan y procesan en paralelo en varios nodos del cluster. Cada nodo aplica una función de "reduce" a los datos para producir un resultado final.


## Yarn <a name="id3"></a>

![image](https://user-images.githubusercontent.com/123466051/232530684-6f33ab93-a12f-4b7a-8aed-dad3e7a43442.png)


Antes de la introducción de YARN, el procesamiento de datos en un cluster de Hadoop estaba limitado al modelo de MapReduce. Esto significaba que el cluster sólo podía ejecutar aplicaciones de MapReduce, lo que limitaba su versatilidad. YARN fue desarrollado para superar estas limitaciones y permitir que otras aplicaciones, además de MapReduce, se ejecuten en un cluster de Hadoop.

YARN proporciona una plataforma de programación distribuida que permite a los desarrolladores escribir aplicaciones de procesamiento de datos que se ejecutan en un cluster de Hadoop. Proporciona un administrador de recursos y un planificador que asigna los recursos del cluster a las tareas en ejecución. Esto permite que varias aplicaciones se ejecuten en el mismo cluster y compartan los mismos recursos.

La arquitectura de YARN se basa en dos componentes principales:

ResourceManager: Es el nodo maestro que administra los recursos del cluster y programar las tareas. Es responsable de asignar recursos a las aplicaciones y monitorear su estado.

NodeManager: Es el nodo esclavo que se ejecuta en cada nodo del cluster y administra los recursos locales del nodo, como la memoria y la CPU. Es responsable de iniciar y detener las tareas y reportar el estado al ResourceManager.

En resumen, YARN es un componente de Apache Hadoop que se utiliza para administrar los recursos de un cluster y programar las tareas en un entorno distribuido. Proporciona una plataforma de programación distribuida que permite a los desarrolladores escribir aplicaciones de procesamiento de datos que se ejecutan en un clúster de Hadoop.


## Hive <a name="id4"></a>

![image](https://user-images.githubusercontent.com/123466051/232532222-aa156ba2-ee33-478d-bf67-45d13424083b.png)


Apache Hive es un framework de procesamiento de datos de código abierto basado en Apache Hadoop. Proporciona una capa de abstracción sobre los datos almacenados en un cluster de Hadoop y permite a los usuarios consultar y analizar datos utilizando SQL-like declarativo llamado HiveQL.

Hive se utiliza para procesar grandes conjuntos de datos en un entorno distribuido utilizando un lenguaje de consulta SQL-like que es familiar para muchos usuarios. HiveQL permite a los usuarios escribir consultas SQL-like y Hive traduce esas consultas en tareas MapReduce que se ejecutan en el cluster de Hadoop. Hive también admite la ejecución de tareas MapReduce personalizadas y permite a los usuarios integrar fácilmente sus propias funciones de MapReduce.


## Pig <a name="id5"></a>

![image](https://user-images.githubusercontent.com/123466051/232532567-ac9d4a45-ffa4-495e-a7aa-5323055b89c7.png)


Apache Pig es una plataforma de procesamiento de datos de alto nivel que se ejecuta sobre Hadoop. Permite a los usuarios escribir programas en un lenguaje de alto nivel llamado Pig Latin que luego se compila en código MapReduce, que se puede ejecutar en un cluster de Hadoop.

Pig Latin es un lenguaje de programación de alto nivel que se utiliza para procesar grandes conjuntos de datos de forma paralela. Pig Latin es similar a SQL, pero se enfoca en operaciones de transformación de datos y no en la gestión de la estructura de datos. Las operaciones en Pig Latin se pueden encadenar para crear flujos de trabajo complejos.

Pig proporciona una serie de operadores y funciones incorporadas que permiten a los usuarios realizar operaciones de transformación de datos, filtrado y agrupación, así como operaciones avanzadas como unión, agregación y ordenamiento. Además, Pig también admite la integración con otros frameworks como Hive y HBase.

La ventaja de Pig es que permite a los usuarios trabajar con grandes conjuntos de datos de una manera simple y eficiente, sin tener que preocuparse por los detalles de implementación de MapReduce. Pig se puede utilizar en una variedad de aplicaciones, como análisis de datos, minería de datos y procesamiento de lenguaje natural, entre otros.


## Flume <a name="id6"></a>

![image](https://user-images.githubusercontent.com/123466051/232532842-1d496054-fdc7-4fbe-8e44-19877d3a7599.png)

Apache Flume es un servicio de recolección de datos distribuido y confiable que se utiliza para mover grandes cantidades de datos desde diferentes orígenes hacia diferentes destinos en un entorno distribuido. Flume está diseñado para manejar datos de registro, pero también se puede utilizar para transportar otros tipos de datos.

Flume permite la ingesta de datos desde diversas fuentes, como servidores web, bases de datos, sistemas de archivos, etc., y los entrega a diferentes destinos, como HDFS, HBase, Apache Solr, bases de datos relacionales, etc. Flume utiliza un modelo de agente para la recolección de datos, donde cada agente consta de tres componentes principales: fuente, canal y destino.

La fuente es responsable de recopilar los datos de una determinada fuente de datos y transmitirlos al canal.
El canal es responsable de almacenar temporalmente los datos hasta que se entreguen a los destinos.
El destino es responsable de enviar los datos a su destino final, como HDFS o HBase.
Flume también proporciona una arquitectura escalable y de alta disponibilidad que permite a los usuarios agregar nuevos nodos a medida que aumenta el volumen de datos. Además, Flume es compatible con la mayoría de los sistemas de datos y se integra fácilmente con otros componentes del ecosistema de Hadoop.

En resumen, Flume es una herramienta esencial para el procesamiento de datos en tiempo real en un entorno distribuido y es ampliamente utilizado en diversas aplicaciones, como análisis de registros, minería de datos, análisis de datos en tiempo real, etc.


## Hue <a name="id7"></a>

![image](https://user-images.githubusercontent.com/123466051/232533144-3b51de80-6b61-453e-a8ba-1aacc77305d3.png)


Hue (Hadoop User Experience) es una interfaz web de código abierto que proporciona una experiencia de usuario intuitiva y fácil de usar para interactuar con diferentes componentes del ecosistema de Hadoop, como Hive, Pig, HBase, Oozie, Spark, etc.

Hue es una herramienta que permite a los usuarios trabajar con Hadoop sin tener que escribir código en línea de comandos. Hue proporciona una interfaz gráfica de usuario que permite a los usuarios interactuar con los datos almacenados en HDFS y en otros sistemas de almacenamiento, como HBase y Amazon S3.

Además, Hue también proporciona una serie de herramientas de administración de clústeres que permiten a los administradores de sistemas monitorear y administrar diferentes aspectos del clúster, como el estado del trabajo, el uso de recursos, etc. Los usuarios también pueden ejecutar consultas y scripts de Hive y Pig, programar flujos de trabajo con Oozie y crear gráficos y visualizaciones con Spark.

En resumen, Hue es una herramienta valiosa para los usuarios y administradores de clústeres de Hadoop, ya que proporciona una interfaz fácil de usar y una amplia gama de herramientas que simplifican el trabajo
 con Hadoop.


## Spark <a name="id8"></a>

![image](https://user-images.githubusercontent.com/123466051/232533339-02f29c6a-5978-4eef-add6-20b50295371d.png)


A diferencia de Hadoop MapReduce, que está diseñado para procesar grandes volúmenes de datos en lotes (batch), Spark está diseñado para procesar datos de manera interactiva y en tiempo real. Además, Spark proporciona una API unificada para el procesamiento de datos en lotes, en tiempo real, en streaming y de aprendizaje automático, lo que lo hace más flexible y fácil de usar que otras soluciones de procesamiento de datos.

Spark se basa en una arquitectura de computación distribuida llamada Resilient Distributed Datasets (RDD), que permite a los desarrolladores escribir código que se ejecuta en paralelo en múltiples nodos de un clúster. Spark utiliza la memoria para almacenar los datos intermedios en lugar de escribirlos en el disco, lo que lo hace significativamente más rápido que MapReduce.

Las aplicaciones de Spark se pueden escribir en varios lenguajes de programación, incluyendo Java, Scala, Python y R. Además, Spark se integra con una amplia variedad de herramientas y bibliotecas, incluyendo Hadoop, Hive, Pig, Kafka y Cassandra, lo que lo hace fácil de usar en entornos existentes.

En resumen, Spark es una plataforma de procesamiento de datos de alto rendimiento y flexible que está diseñada para procesar datos a gran escala de manera interactiva, en tiempo real y en diferentes formatos.


## ZooKeeper <a name="id9"></a>

![image](https://user-images.githubusercontent.com/123466051/232533517-81259be6-5068-406f-93a4-db16d925318b.png)


ZooKeeper es un servicio de coordinación distribuida de código abierto que proporciona un conjunto de herramientas para la construcción de sistemas distribuidos altamente disponibles y escalables. Fue desarrollado originalmente por Yahoo y ahora es mantenido por la Apache Software Foundation.

ZooKeeper se utiliza comúnmente en sistemas distribuidos para gestionar la configuración, la sincronización y el descubrimiento de servicios, así como para la elección de líderes y la gestión de bloqueos. Proporciona un conjunto de abstracciones de datos distribuidos, como árboles de directorios, nodos efímeros y semáforos distribuidos, que permiten a los desarrolladores construir sistemas distribuidos altamente disponibles y escalables de manera más fácil.

Una de las características más importantes de ZooKeeper es su capacidad para ofrecer garantías de ordenación y consistencia en el acceso a los datos. Esto se logra mediante el uso de un protocolo de consenso llamado Zab, que asegura que todas las operaciones de lectura y escritura se ejecuten en el mismo orden en todos los nodos del clúster.



## HBase <a name="id10"></a>

![image](https://user-images.githubusercontent.com/123466051/232533727-789f3c5d-b1d3-4b7b-83c3-8fb422ce4493.png)


HBase es una base de datos NoSQL distribuida y escalable que está integrada con Hadoop Common. Hadoop Common es una biblioteca compartida utilizada por otros componentes de Hadoop para acceder al sistema de archivos Hadoop.

HBase se basa en el modelo de datos de Bigtable de Google y está diseñado para manejar grandes cantidades de datos no estructurados o semiestructurados. Es una base de datos columnar orientada a columnas, lo que significa que los datos se almacenan de forma horizontal en filas, pero las columnas se agrupan lógicamente en familias de columnas. Además, HBase se ejecuta en clústeres de servidores y utiliza HDFS (Hadoop Distributed File System) como almacenamiento subyacente para los datos.

Hadoop Common y HBase trabajan juntos para proporcionar una plataforma de procesamiento de datos escalable y de alta disponibilidad. Hadoop Common se encarga del acceso a los datos y del procesamiento en paralelo, mientras que HBase proporciona una capa de almacenamiento NoSQL para los datos estructurados o semiestructurados. Juntos, Hadoop Common y HBase permiten a los usuarios procesar grandes cantidades de datos de manera distribuida, escalable y tolerante a fallos.

HBase se utiliza comúnmente en aplicaciones que requieren un alto rendimiento de lectura y escritura, como la indexación y búsqueda de datos, el procesamiento de registros y la recopilación de datos en tiempo real. También se utiliza en proyectos de análisis de datos como Apache Phoenix, que proporciona una capa de SQL para HBase, lo que permite a los usuarios interactuar con los datos utilizando consultas SQL familiares.

En resumen, HBase es una base de datos NoSQL distribuida y escalable que está integrada con Hadoop Common y se utiliza para almacenar y procesar grandes cantidades de datos estructurados o semiestructurados en clústeres de servidores.


## Kafka <a name="id11"></a>

![image](https://user-images.githubusercontent.com/123466051/232533867-3ce8fe17-8e57-4290-aa7c-b55f25057c27.png)


Kafka es una plataforma de procesamiento de datos de código abierto que se utiliza para la transmisión de datos en tiempo real y la gestión de eventos. Fue desarrollada por LinkedIn y ahora es mantenida por la Apache Software Foundation.

Kafka se basa en la arquitectura de registro de commit (commit log), que es una estructura de datos de registro inmutable y ordenada que almacena todas las operaciones de escritura en un sistema distribuido. Kafka permite la publicación y suscripción de flujos de datos en tiempo real en clústeres de servidores distribuidos.

La plataforma Kafka se compone de dos componentes principales: los productores y los consumidores. Los productores son responsables de la publicación de datos en el clúster de Kafka, mientras que los consumidores se suscriben a los flujos de datos y reciben las actualizaciones en tiempo real. Kafka también proporciona un sistema de colas de mensajes llamado "topic" para el almacenamiento



## Nifi <a name="id12"></a>

![image](https://user-images.githubusercontent.com/123466051/232534037-38532510-835c-419c-b609-e8e688ee6a30.png)


NiFi se basa en un modelo de programación visual en el que los usuarios pueden diseñar flujos de trabajo gráficamente, utilizando componentes predefinidos que representan fuentes de datos, procesadores y destinos de datos. Los flujos de trabajo se pueden diseñar, implementar y administrar a través de una interfaz de usuario web.

La plataforma NiFi se utiliza para automatizar el flujo de datos en tiempo real entre sistemas heterogéneos, lo que permite a los usuarios integrar fácilmente fuentes de datos dispares y distribuir datos de manera eficiente a través de sistemas y dispositivos. NiFi se puede utilizar en una variedad de casos de uso, como la ingestión de datos, la transformación de datos, la integración de sistemas, la monitorización de eventos y la automatización de procesos empresariales.

Entre las características principales de NiFi se incluyen su capacidad para procesar datos en tiempo real, su arquitectura escalable y tolerante a fallos, su amplia gama de conectores de fuente y destino de datos, su capacidad para realizar transformaciones de datos y enriquecimiento de datos en tiempo real, y su facilidad de uso para diseñar flujos de trabajo complejos.

En resumen, Apache NiFi es una plataforma de procesamiento de datos de código abierto que permite a los usuarios automatizar el flujo de datos en tiempo real entre sistemas de software, dispositivos y usuarios de manera eficiente, escalable y tolerante a fallos.









