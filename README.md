# Hadoop_Mahout

USO DE MAHOUT

OBJETIVO : Clusterización  de un conjunto de datos de series temporales (synthetic_control.data).

ALGORITMOS:
Mahout es una librería de software libre escrita en Java y optimizada para funcionar sobre Hadoop. Mahout permite implementar algoritmos de Machine learning.
Para el caso usaremos dos algoritmos implementados en Mahout. 
-	Canopy Clustering, es un método muy simple, rápido y acertado para agrupar objetos en clústers. Representa los puntos en un espacio multidimensional. Frecuentemente usado antes de usar K-means. 
-	Algoritmo k- means clustering, algoritmo simple de agrupación de objetos. Los objetos deben representarse como un conjunto de características numéricas.

DATA:
synthetic_control.data.  Es un conjunto de datos que contiene 600 ejemplos de gráficos de control sintéticamente generados. Hay seis clases diferentes de cuadros de control: Normal, Cíclico, Tendencia creciente, Tendencia decreciente, Cambio hacia arriba, Cambio hacia abajo. Los gráficos de control son herramientas que sirven para determinar si un proceso de fabricación o comercial se encuentra en estado de control estadístico.  
