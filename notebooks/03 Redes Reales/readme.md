**Instrucciones de la actividad**

Revisa el siguiente cuaderno de trabajo



Redes reales.ipynb


Elige una base de datos y usa NetworkX para hacer un primer análisis de una red real; puedes usar, por ejemplo, una base de datos de las siguientes páginas:



https://networkrepository.com/index.php
https://snap.stanford.edu/data/#citnets
https://toreopsahl.com/datasets/
https://networkdata.ics.uci.edu/
https://www.re3data.org/
https://www.web-of-life.es/map.php
https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/T4HBA3
http://www-personal.umich.edu/~mejn/netdata/
https://math.nist.gov/MatrixMarket/
 

Responde ¿qué datos son? ¿cómo están relacionados los nodos? ¿cuántos son? ¿cuántas aristas tienen? 



Realiza tres visualizaciones distintas cambiando opciones como diseño (layout), forma, tamaño o color de nodos, color de aristas, etc.
Genera la matriz de adyacencia de la red.
Utiliza la función "subgraph" para extraer una subred de 8 nodos y visualizarla.
Realiza una lista de grados: Identifica los nodos con mayor y con menor grado
Encuentra el grado promedio
Encuentra la densidad: ¿consideras que la red es dispersa o densa?
Encuentra la cantidad de componentes
Calcula la distancia entre algunos nodos, por ejemplo, entre los de mayor y menor grado.
Calcula el diámetro, en caso de que la red sea disconexa, calcular el diámetro de cada componente
Calcula la conectividad por aristas y por nodos entre algunos pares de nodos (por ejemplo entre los de mayor y menor grado)
Encuentra un conjunto mínimo de nodos de corte.
Calcula su matriz Laplaciana (omite direcciones si es necesario), sus eigenvalores y sus eigenvectores (el espectro). Verifica que la multiplicidad del eigenvalor cero es la misma que la cantidad de componentes 