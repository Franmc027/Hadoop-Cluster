# Instalación de Pig

![image](https://user-images.githubusercontent.com/123466051/235997235-4140061b-1324-47b6-b4b0-6ea1d42fc5f4.png)

**Este servicio lo vamos a instalar en el Servidor2, por lo cual la siguiente configuración será exclusiva de ese servidor.**

Lo primero que vamos ha hacer es instalar la version de pig que vamos a usar, en mi caso la versión 0.17.0:

```wget https://downloads.apache.org/pig/pig-0.17.0/pig-0.17.0.tar.gz```


Lo desempaquetamos y lo movemos a $hadoop_home

```
tar -xzvf pig-0.17.0.tar.gz
mv pig-0.17.0 $HADOOP_HOME/pig-0.17.0
```

