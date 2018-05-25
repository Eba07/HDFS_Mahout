ENTORNO

Ubuntu 17.10 </br>
Oracle Java SDK 1.8.0_71 </br>
Apache Hadoop 2.9.0

INSTALACIÓN Y CONFIGURACIÓN DE MAHOUT
Seguimos los siguientes pasos:
-	Descargar la libreria Mahout desde la página de Apache Mahout:  http://mahout.apache.org/
-	Descomprimir el archivo binario de mahout:
  $ sudo tar -zxvf apache-mahout-distribution-0.13.0.tar.gz
- Mover la carpeta descomprimida a la carpeta /home/bigdata/mahout que hemos creado previamente:</br>
  $ mkdir /home/bigdata/mahout</br>
  $ sudo mv apache-mahout-distribution-0.13.0 /home/bigdata/mahout
-	Editar la configuración añadiendo las siguientes líneas al fichero ~/.bashrc y ejecutar los cambios:
```
# MAHOUT VARIABLES START	
export MAHOUT_HOME=/home/bigdata/mahout
export PATH=$PATH:$MAHOUT_HOME/bin
# MAHOUT VARIABLES END
```

$ cd /home/bigdata/mahout </br>
$ sudo nano ~/.bashrc </br>
$ source ~/.bashrc

DESCARGAR Y SUBIR LA DATA A HDFS:
-	Crear la carpeta dato donde descargaremos el fichero de datos desde : http://archive.ics.uci.edu/ml/databases/synthetic_control/synthetic_control.data 

$ mkdir dato </br>
$ cd dato </br>
$ wget http://archive.ics.uci.edu/ml/databases/synthetic_control/synthetic_control.data
-	Verificar la estructura de los datos, son 600 filas en 60 columnas.
$ vi synthetic_control.data
-	Iniciamos los demonios de hadoop </br>
$ start-dfs.sh </br>
$ start-yarn.sh
-	Subir el fichero synthetic_control.data a la carpeta testdata que creamos en HDFS. </br>
$ hdfs dfs -mkdir testdata </br>
$ hdfs dfs -put /home/bigdata/dato/synthetic_control.data testdata

CLUSTERIZACIÓN USANDO CANOPY CLUSTERING

-	Ejecutar el algoritmo Canopy de Mahout. </br>

$MAHOUT_HOME/bin/mahout  org.apache.mahout.clustering.syntheticcontrol.canopy.Job

-	Se generan 6 clústers en un tiempo de ejecución de 1.2 minutos aproximadamente. 
-	Revisamos el resultado obtenido que se encuentra en la carpeta output en HDFS. El formato de los archivos está en un formato no legible.</br>

$ hdfs dfs -ls output

-	Mahout tiene una utilidad conocida como clusterdump que lo convierte en formato legible. Para usarlo copiamos el resultado a local en la carpeta canopyoutput. </br>
$ mkdir canopyoutput </br>
$ hadoop fs -get output canopyoutput </br>
$ mahout clusterdump --input output/clusters-0-final --pointsDir output/clusteredPoints --output canopýoutput/clusteranalyze.txt

-	Revisamos la salida transformada que se encuentra en el fichero canopýoutput/clusteranalyze.txt </br>
$ nano canopýoutput/clusteranalyze.txt

-“C-0”, es el nombre de un clúster y r el radio del clúster, entre otros datos que servirán para el análisis.

CLUSTERIZACIÓN USANDO EL ALGORITMO K-MEANS

-	Corremos el algoritmo k-means clustering de Mahout. </br>

$MAHOUT_HOME/bin/mahout org.apache.mahout.clustering.syntheticcontrol.kmeans.Job

-	El algoritmo ha generado 6 clústers en un tiempo de 5.6 minutos aproximadamente.
-	Revisamos el resultado obtenido que se encuentra en la carpeta output en HDFS. </br>
$ hdfs dfs -ls output
 
-	Observamos que la salida del clúster está en formato SequenceFile que no es legible para humanos.  Usaremos el programa  clusterdump  de Mahout que permite descargar los centroides del cluster y puntos asociados, proporciona un fichero en formato legible.
-	Grabamos el resultado a local en el fichero  kmeansoutput/clusteranalyze.txt </br>
$ mkdir kmeansoutput </br>
$ hadoop fs -get output kmeansoutput </br>
$ mahout clusterdump --input output/clusters-10-final --pointsDir output/clusteredPoints --output kmeansoutput/clusteranalyze.txt
 
-	Revisamos la salida transformada que se encuentra en el fichero kmeansoutput/clusteranalyze.txt, donde tendremos la información de los clústers, su radio y los puntos que lo conforman para su análisis. </br>
$ nano kmeansoutput/clusteranalyze.txt









