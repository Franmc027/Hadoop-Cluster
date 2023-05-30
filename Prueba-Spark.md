# Ejemplo de uso de Spark

Para esta prueba vamos a usar un dataset con datos de la supervivencia de los tripulantes del titanic, este dataset lo puedes descargar aquí --> [titanic.csv](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/files/11593831/titanic.csv)


Guardamos el dataset en HDFS:

```hdfs dfs -mkdir /bda```

```hdfs dfs -mkdir /bda/spark```

```hdfs dfs -mkdir /bda/spark/csv/```

```hdfs dfs -copyFromLocal titanic.csv /bda/spark/csv/titanic.csv ```

## Carga de datos en spark-shell(scala)

Cargar un dataset en scala:

```val df = spark.read.format("csv").option("header", true).option("separator", ",").load("hdfs://proyecto-argus:9000/bda/spark/csv/titanic.csv")```

Ver el contenido del dataframe:

```df.show(10)```

## Carga de datos en pyspark(python)

Cargar el dataset en python:

```df = spark.read.format("csv").option("header", True).option("separator", ",").load("hdfs://proyecto-argus:9000/bda/spark/csv/titanic.csv")```

Ver el contenido del dataframe:

```df.show(10)```

## Ejecición de script en pyspark

El escript es el siguiente:

```
from  pyspark.sql import SparkSession

spark = SparkSession.builder.appName("Primer_Script").getOrCreate()

df = spark.read.format("csv").option("header", True).option("separator", True).load("hdfs://proyecto-argus:9000/bda/spark/csv/titanic.csv")

df.show(10, False)
```

Ejecutar el script:


```spark-submit  <<nombre-script>>```


### Guardar un dataframe en HDFS

Cargamos el dataframe:

```df = spark.read.format("csv").option("header", True).option("separator", ",").load("hdfs://proyecto-argus:9000/bda/spark/csv/titanic.csv")```


Modificamos el dataframe que vamos a guardar:

```survived_clas_sex = df.groupBy(["Sex", "Pclass"]).agg({"Age": "mean", "Fare" : "mean", "Survived": "mean"})```


Lo guardamos en HDFS

```survived_clas_sex.write.mode("overwrite").parquet("hdfs://proyecto-argus:9000/bda/spark/csv/survived_clas_sex")```





  


