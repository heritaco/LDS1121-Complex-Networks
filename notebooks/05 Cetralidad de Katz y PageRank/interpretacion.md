* **Grado**: detecta “hubs” por **cantidad de relaciones directas** (proveen a muchos o compran de muchos, según uses out/in-degree en dirigido). Es la centralidad más “local”.

* **Eigenvector**: no solo cuenta cuántos vecinos tienes, sino **qué tan importantes son tus vecinos**. En redes disconexas suele **concentrarse en la componente más “potente”** (la que tiene un núcleo más interconectado); por eso nodos de la otra componente pueden caer mucho.

* **Katz**: se parece a eigenvector pero es más “tolerante” con nodos periféricos (da crédito por caminos más largos). Aun así, **si no hay puente entre componentes**, Katz reparte importancia **por separado** dentro de cada una.

* **PageRank (dirigido)**: tiende a favorecer nodos que **reciben** muchas conexiones (clientes “importantes” para muchos proveedores) y/o están en rutas frecuentes del flujo. Si lo corres sobre una versión no dirigida, se comporta muy parecido a “grado”, porque caminar aleatoriamente en un grafo no dirigido termina visitando más a los nodos con más conexiones.




# alhpa


-   La red tiene un núcleo muy dominante (o pesos grandes)  : cuando hay muchos enlaces fuertes concentrados (personajes que comparten muchas escenas), el “feedback” de Katz se dispara si $\alph$ es grande. Por eso tu rutina tuvo que bajarlo hasta un valor pequeño para que el cálculo sea estable.

  

-   Con (\alpha) tan pequeño, Katz se vuelve más local  : la centralidad queda determinada principalmente por conexiones cercanas (vecinos directos y, a lo mucho, vecindario inmediato). En consecuencia,   Katz tiende a parecerse más a grado/eigenvector   y el ranking cambia poco (que es justo lo que observaste en Star Wars: casi todo coincide).

  

-   Si la red fuera más “suave” (menos núcleo o pesos más bajos)  , normalmente podrías usar un (\alpha) mayor sin problemas y Katz diferenciaría más “influencia de largo alcance”. Aquí no: la estructura/pesos hacen que el umbral de estabilidad sea bajo.
