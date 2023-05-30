# Ejemplo de uso de Pig

Para esta prueba vamos a usar un dataset de Spotify, donde vamos a ver el ranking de las mejores temas y álbunes de diferentes paíeses, este dataset lo puedes descargar aquí -->[spotify-dataset.csv] (https://github.com/iesgrancapitan-CEIABD-BDA/proyecto-final-bda-2022-23-a20mocafr/files/11593790/spotify-dataset.csv)

Lo primero que vamos a haces es guardarlo dentro de nuestro hdfs

```hdfs dfs -mkdir /bda```

```hdfs dfs -mkdir /bda/pig```

```hdfs dfs -mkdir /bda/pig/spotify-sample/```

```hdfs dfs -copyFromLocal spotify-dataset.csv /bda/pig/spotify-sample/spotify-dataset.csv ```

Una vez hecho esto ya podemos entrar a pig con el comando ```pig```

Cargamos el dataset:

```SPOTIFY = load '/bda/pig/spotify-sample/spotify-dataset.csv' using PigStorage(',') as (id:int, date:chararray, position:int, song:chararray, artist:chararray, popularity:int, duration_ms:int, album_type:chararray, total_tracks:int, release_date:chararray, is_explicit:Boolean, url:chararray, country:chararray);```

Seleccionamos las columnas interesantes:

```SPOTIFY = FOREACH SPOTIFY GENERATE release_date, position, song, artist, popularity, duration_ms, album_type, is_explicit, country;```

Solo nos interesan los tops de países hispanos

```SPOTIFY_HISPANO = filter SPOTIFY by ((country == 'es') or (country == 'mx') or (country == 'ar'));```

De estos solo vamos a coger el top 100 para una campaña de publicidad

```SPOTYFY_TOP100_HISPANO = filter SPOTIFY_HISPANO by ((position <= 100));```

También queremos que estos temas no sean explicitos

```SPOTIFY_HISPANO_NO_EXPLICIT = filter SPOTYFY_TOP100_HISPANO by ((is_explicit == false))```

Y por último lo guardamos en nuestro HDFS:

```STORE SPOTIFY_HISPANO_NO_EXPLICIT  INTO 'bda/pig/spotify-sample/spotify-hispano-no-explicit';```




