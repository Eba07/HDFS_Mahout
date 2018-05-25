ENTORNO

Ubuntu 12.04 64 bits
Oracle Java SDK 1.8
Apache Hadoop 2.2.0

INSTALACIÓN Y CONFIGURACIÓN DE MAHOUT
Seguimos los siguientes pasos:
-	Descargar la libreria Mahout desde la página de Apache Mahout:  http://mahout.apache.org/
-	Descomprimir el archivo binario de mahout:
  $ sudo tar -zxvf apache-mahout-distribution-0.13.0.tar.gz
- Mover la carpeta descomprimida a la carpeta /home/bigdata/mahout que hemos creado previamente:
  $ mkdir /home/bigdata/mahout
  $ sudo mv apache-mahout-distribution-0.13.0 /home/bigdata/mahout
-	Editar la configuración añadiendo las siguientes líneas al fichero ~/.bashrc y ejecutar los cambios:

# MAHOUT VARIABLES START	
export MAHOUT_HOME=/home/bigdata/mahout
export PATH=$PATH:$MAHOUT_HOME/bin
# MAHOUT VARIABLES END

$ cd /home/bigdata/mahout
$ sudo nano ~/.bashrc


