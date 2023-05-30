# Ejemplo de uso de Kafka con Nifi

Para esta prueba lo primero que debemos hacer es tener iniciado Kafka, Zookeeper y nifi como explicamos en los archivos de instalación anteriores. Después entramos a la siguiente dirección con nuestro navegador

```https://ip-servidor-nifi:8443```

## Primer ejemplo

El primer flujo que vamos a crear, va a contener dos caminos, el primero va a generar un archivo de forma automática y este será almacenado en un topic de kafka, el 
segundo mirara un directorio y los archivos nuevos que se generen en este lo almacenara en un topic de kafka para ello necesitaremos los 
siguientes procesos:

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/f592c918-6584-4bf1-9a46-57920d1870d5)

La configuración de estos es:

GenerateFlowFile-->

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/6a4e2d73-c698-4f2c-ae30-ac3b9ac5d0f3)

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/ae129d21-42ba-4b25-b3f4-c5161a0043a2)

Kafka1(kafka de la izquierda)-->

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/8f905920-3c39-4686-9ee3-961a3f34da62)


![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/e0d21804-4b94-4543-befa-e4a0896e94a1)

GetFile-->

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/30df8c56-315b-4cf8-8e2c-6899df463e2b)


![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/992027ca-7bd5-449e-bd68-5a6c93eed466)


Kafka2(kafka de la derecha)-->

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/3b675ade-16ea-4db5-9320-946ba1dbb3b4)

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/c5ea0588-0b9c-4f41-b7a7-c995f6724ea6)

LogAttribute -->

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/b1588401-6823-4b84-bb5e-4fe03378daf3)

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/2c81a14e-9a02-4159-a535-9732d24fa3cc)

## Segundo ejemplo

En el segundo ejemplo vamos a recoger mensajes de un topic de kafka y guardarlos en un archivo en local


![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/7ffc8aeb-7912-449e-a949-389cdcc07a56)

Kafka -->

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/ad8caf9d-6c02-4de1-bf23-1f17b0cac38c)

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/34417b90-b461-4a7d-888f-398eeb52852f)

PutFile -->

![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/011305ff-c0bb-4c55-8a0a-b37c3b81b9d1)


![image](https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/assets/101642915/83ad3946-dcb0-4d9e-a4c3-c4e6790cf72d)












