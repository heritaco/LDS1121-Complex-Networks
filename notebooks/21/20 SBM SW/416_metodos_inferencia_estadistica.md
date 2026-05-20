# Métodos basados en inferencia estadística

**Autor:** Dr. Hugo Villanueva Méndez  
**Institución:** Universidad de las Américas Puebla, Escuela de Ciencias, Departamento de Actuaría, Física y Matemáticas  
**Periodo:** Primavera 2026

> Nota: esta es una versión limpia en Markdown del PDF. Las fórmulas fueron normalizadas a sintaxis LaTeX con `$...$` para matemáticas en línea y `$$...$$` para matemáticas en display.

---

# Introducción

Dado un modelo de red, es decir, cualquier proceso capaz de generar una red, podemos ajustarlo a los datos, o sea, a una estructura de red específica, hallando los valores de los parámetros del modelo que ofrecen la mayor verosimilitud.

En esencia, nos preguntamos:

> Si esta red fue generada por este modelo, ¿cuál es nuestra mejor estimación de los valores de los parámetros del modelo que se utilizaron?

Estos ajustes de modelos a los datos suelen revelar mucha información sobre la estructura de la red.

---

# Ejemplo: red aleatoria de Poisson

Consideremos el modelo de red aleatoria Poisson. Además del tamaño de la red $n$, este modelo tiene solamente un parámetro: la probabilidad $p$ de que cualesquiera dos nodos distintos estén conectados por una arista.

Cada arista es independiente y tiene la misma probabilidad. Por tanto, la probabilidad total, o similitud, de que una red particular, definida por su matriz de adyacencia $A$, sea generada por el modelo de red aleatoria con un valor particular de $p$, es

$$
P(A\mid p)=p^m(1-p)^{\binom{n}{2}-m},
$$

donde $m$ es el número de aristas en la red.

---

# Estimación de $p$

Supongamos ahora que no conocemos el valor de $p$. Lo que conocemos son los datos, es decir, la red misma. Podemos hacer una estimación de $p$ usando

$$
P(p\mid A)=\frac{P(A\mid p)P(p)}{P(A)},
$$

donde $P(p)$ y $P(A)$ son las probabilidades a priori sobre $p$ y $A$, respectivamente.

El valor más probable de $p$ se obtiene, por definición, al maximizar esta expresión con respecto a $p$ mientras $A$ permanece constante. Como $A$ es constante, también lo es $P(A)$, de modo que el denominador no tiene efecto al maximizar.

Además, si suponemos que $P(p)$ es constante, es decir, que todos los valores de $p$ entre $0$ y $1$ son igualmente probables, entonces maximizar $P(p\mid A)$ es equivalente a maximizar la verosimilitud $P(A\mid p)$ para determinar el valor de $p$.

---

# Maximización de la verosimilitud

La verosimilitud es

$$
P(A\mid p)=p^m(1-p)^{\binom{n}{2}-m}.
$$

Para maximizarla, derivamos con respecto a $p$ e igualamos a cero:

$$
\frac{d}{dp}\left[p^m(1-p)^{\binom{n}{2}-m}\right]=0.
$$

Esto da

$$
m p^{m-1}(1-p)^{\binom{n}{2}-m}
-\left[\binom{n}{2}-m\right]p^m(1-p)^{\binom{n}{2}-m-1}=0.
$$

Por tanto,

$$
\hat p=\frac{m}{\binom{n}{2}}.
$$

Es decir, el estimador de máxima verosimilitud de $p$ es la proporción observada de aristas respecto al número máximo posible de aristas.

---

# Log-verosimilitud

Tomando logaritmos,

$$
\log P(A\mid p)=m\log(p)+\left[\binom{n}{2}-m\right]\log(1-p).
$$

Como el logaritmo es una función creciente, el máximo de la log-verosimilitud ocurre en el mismo punto que el máximo de la verosimilitud. La ventaja es que derivar la log-verosimilitud suele ser más fácil.

En este sentido, el mejor estimador de la probabilidad de aristas $p$ es el estimador obvio:

$$
\hat p=\frac{\text{número de aristas observadas}}{\text{número máximo de aristas posibles}}.
$$

---

# Detección de comunidades

Podemos usar el método de máxima similitud o máxima verosimilitud para realizar detección de comunidades. La idea es ajustar los datos de la red a un modelo que contenga estructura comunitaria.

El modelo que utilizamos es el **modelo de bloques estocásticos corregido por grado**, o **degree-corrected stochastic block model**.

En este modelo, dividimos los nodos de una red en $q$ grupos o comunidades, etiquetadas por los enteros $1,\ldots,q$. Después colocamos aristas no dirigidas entre pares de nodos con probabilidad

$$
\frac{\omega_{g_i g_j}c_i c_j}{2m},
$$

donde:

- $g_i$ y $g_j$ son los grupos a los cuales pertenecen los nodos $i$ y $j$;
- $c_i$ es el grado promedio deseado del nodo $i$;
- el grado real puede variar alrededor de $c_i$;
- solamente la media se fija en $c_i$;
- $\omega_{rs}$ es un factor que modifica la probabilidad de una arista entre nodos de los grupos $r$ y $s$.

---

# Matriz de parámetros comunitarios

La matriz de parámetros

$$
\Omega=(\omega_{rs})_{r,s=1}^q
$$

controla la estructura comunitaria.

Si las entradas diagonales $\omega_{rr}$ son mayores que las entradas fuera de la diagonal, la red tendrá una estructura de comunidad **asortativa**, donde las conexiones son más probables dentro de los grupos que entre grupos.

Sin embargo, el modelo también puede capturar estructuras **disasortativas**, donde las entradas diagonales son menores que las no diagonales.

---

# Restricción sobre los parámetros $\omega_{rs}$

No tenemos libertad total para elegir los parámetros $\omega_{rs}$ si queremos que $c_i$ sea el grado esperado del nodo $i$.

El grado esperado del nodo $i$ es la suma del número esperado de aristas desde ese nodo hacia todos los demás nodos. Si $g_i$ denota el grupo al que pertenece el nodo $i$, entonces el grado esperado es

$$
\sum_j \omega_{g_i g_j}\frac{c_i c_j}{2m}
=\frac{c_i}{2m}\sum_j \omega_{g_i g_j}c_j.
$$

Si queremos que esta expresión sea igual a $c_i$, debemos tener

$$
\sum_j \omega_{r g_j}c_j=2m
$$

para cada grupo $r$.

---

# Reescritura con la delta de Kronecker

La restricción anterior impone $q$ restricciones lineales separadas sobre los valores de $\omega_{rs}$, una para cada grupo.

Podemos reescribir el lado izquierdo como

$$
\sum_j \omega_{r g_j}c_j
=\sum_{j,s}\omega_{rs}\delta_{g_j s}c_j
=\sum_s\omega_{rs}\kappa_s,
$$

donde $\delta_{ij}$ es la delta de Kronecker y

$$
\kappa_s=\sum_j \delta_{g_j s}c_j.
$$

La cantidad $\kappa_s$ es la suma de los grados promedio $c_j$ de todos los nodos del grupo $s$.

Por tanto, las restricciones quedan como

$$
\sum_s\omega_{rs}\kappa_s=2m.
$$

---

# Formulación Poisson del modelo

Esto define completamente el modelo de bloques estocásticos corregido por grado.

En lugar de colocar una única arista entre cualquier par de nodos, colocamos un número de aristas distribuido según una distribución de Poisson con media

$$
\omega_{g_i g_j}\frac{c_i c_j}{2m},
$$

para $i\neq j$, o la mitad de este valor cuando $i=j$.

Esto permite tener multiaristas. Aunque no es común en muchas redes, usualmente el valor

$$
\omega_{g_i g_j}\frac{c_i c_j}{2m}
$$

es pequeño cuando $m$ es grande, por lo que la probabilidad de tener dos o más aristas entre un par de nodos es muy pequeña.

---

# Conjuntos de parámetros del modelo

El modelo de bloques estocásticos corregido por grado tiene tres conjuntos de parámetros.

Primero, la matriz de tamaño $q\times q$ con elementos $\omega_{rs}$, denotada por

$$
\Omega.
$$

Esta matriz es simétrica.

Segundo, las cantidades $c_i$, que podemos pensar como un vector

$$
c=(c_1,\ldots,c_n).
$$

Tercero, hay un grupo escondido de parámetros: los grupos $g_i$ a los cuales pertenecen los nodos. Estos forman el vector

$$
g=(g_1,\ldots,g_n).
$$

---

# Verosimilitud del modelo corregido por grado

Podemos escribir la probabilidad de que una red con matriz de adyacencia $A$ sea generada por el modelo de bloques estocásticos corregido por grado como

$$
P(A\mid \Omega,c,g)
=
\prod_{i<j}
\frac{\left(\omega_{g_i g_j}\frac{c_i c_j}{2m}\right)^{A_{ij}}}{A_{ij}!}
\exp\left(-\omega_{g_i g_j}\frac{c_i c_j}{2m}\right)
\prod_i
\frac{\left(\omega_{g_i g_i}\frac{c_i^2}{4m}\right)^{A_{ii}/2}}{(A_{ii}/2)!}
\exp\left(-\omega_{g_i g_i}\frac{c_i^2}{4m}\right).
$$

Esta expresión es el producto de distribuciones Poisson, una para cada par de nodos $i,j$, y representa la probabilidad de observar los valores específicos $A_{ij}$ de la matriz de adyacencia.

El primer producto representa las aristas que no son lazos. El segundo producto cuenta los lazos.

---

# Log-verosimilitud completa

Aplicando logaritmo,

$$
\begin{aligned}
\log P(A\mid \Omega,c,g)
=&\sum_{i<j}\left[
A_{ij}\log\left(\omega_{g_i g_j}\frac{c_i c_j}{2m}\right)
-\log(A_{ij}!)
-\omega_{g_i g_j}\frac{c_i c_j}{2m}
\right]\\
&+\sum_i\left[
\frac{1}{2}A_{ii}\log\left(\omega_{g_i g_i}\frac{c_i^2}{4m}\right)
-\log\left((A_{ii}/2)!\right)
-\omega_{g_i g_i}\frac{c_i^2}{4m}
\right].
\end{aligned}
$$

El objetivo es maximizar esta expresión. Por tanto, podemos ignorar los términos constantes que no dependen de los parámetros.

---

# Log-verosimilitud simplificada

Después de simplificar, obtenemos

$$
\log P(A\mid \Omega,c,g)
=
\frac{1}{2}\sum_{ij}\left[
A_{ij}\log\left(\omega_{g_i g_j}\frac{c_i c_j}{2m}\right)
-\omega_{g_i g_j}\frac{c_i c_j}{2m}
\right]
+\text{constantes}.
$$

---

# Expansión del término logarítmico

Notemos que

$$
\begin{aligned}
\sum_{ij}A_{ij}\log\left(\omega_{g_i g_j}\frac{c_i c_j}{2m}\right)
=&\sum_{ij}A_{ij}\log\omega_{g_i g_j}
+\sum_{ij}A_{ij}\log c_i\\
&+\sum_{ij}A_{ij}\log c_j
-\sum_{ij}A_{ij}\log(2m).
\end{aligned}
$$

Como

$$
k_i=\sum_j A_{ij}
$$

es el grado del nodo $i$, y

$$
\sum_{ij}A_{ij}=2m,
$$

entonces

$$
\begin{aligned}
\sum_{ij}A_{ij}\log\left(\omega_{g_i g_j}\frac{c_i c_j}{2m}\right)
=&\sum_{ij}A_{ij}\log\omega_{g_i g_j}
+\sum_i k_i\log c_i\\
&+\sum_j k_j\log c_j
-2m\log(2m).
\end{aligned}
$$

---

# Definición de $m_{rs}$

Además,

$$
\sum_{ij}A_{ij}\log\omega_{g_i g_j}
=
\sum_{ijrs}\delta_{g_i r}\delta_{g_j s}A_{ij}\log\omega_{rs}
=
\sum_{rs}m_{rs}\log\omega_{rs},
$$

donde

$$
m_{rs}=\sum_{ij}\delta_{g_i r}\delta_{g_j s}A_{ij}.
$$

Por tanto,

$$
\log P(A\mid \Omega,c,g)
=
\sum_i k_i\log c_i
+\frac{1}{2}\sum_{rs}m_{rs}\log\omega_{rs}
-\frac{1}{2}\sum_{ij}\omega_{g_i g_j}\frac{c_i c_j}{2m}
+\text{constantes}.
$$

---

# Maximización respecto a $c_i$

Diferenciando respecto a $c_i$,

$$
\frac{\partial \log P}{\partial c_i}
=
\frac{k_i}{c_i}
-\sum_j \omega_{g_i g_j}\frac{c_j}{2m}.
$$

Por la restricción del modelo,

$$
\sum_j \omega_{g_i g_j}c_j=2m.
$$

Entonces

$$
\frac{\partial \log P}{\partial c_i}
=
\frac{k_i}{c_i}-1.
$$

Igualando a cero,

$$
\frac{k_i}{c_i}-1=0,
$$

obtenemos

$$
\hat c_i=k_i.
$$

Es decir, la mejor elección para los parámetros del grado esperado $c_i$ es justamente el grado observado $k_i$ en la red.

---

# Maximización respecto a $\omega_{rs}$

Para derivar respecto a $\omega_{rs}$, notemos que

$$
\sum_{ij}\omega_{g_i g_j}\frac{c_i c_j}{2m}
=
\sum_{ijrs}\delta_{g_i r}\delta_{g_j s}\omega_{rs}\frac{c_i c_j}{2m}
=
\sum_{rs}\omega_{rs}\frac{\kappa_r\kappa_s}{2m}.
$$

Por tanto,

$$
\log P(A\mid \Omega,c,g)
=
\sum_i k_i\log c_i
+\frac{1}{2}\sum_{rs}\left[
 m_{rs}\log\omega_{rs}
-\omega_{rs}\frac{\kappa_r\kappa_s}{2m}
\right]
+\text{constantes}.
$$

Derivando con respecto a $\omega_{rs}$ e igualando a cero,

$$
\frac{m_{rs}}{\omega_{rs}}-\frac{\kappa_r\kappa_s}{2m}=0.
$$

Por tanto,

$$
\hat\omega_{rs}=\frac{2m\,m_{rs}}{\kappa_r\kappa_s}.
$$

---

# Verificación de la restricción

Recordemos que los $\omega_{rs}$ deben cumplir la restricción

$$
\sum_s\omega_{rs}\kappa_s=2m.
$$

Sustituyendo el estimador $\hat\omega_{rs}$,

$$
\sum_s\hat\omega_{rs}\kappa_s
=
\sum_s\frac{2m\,m_{rs}}{\kappa_r\kappa_s}\kappa_s
=
\frac{2m}{\kappa_r}\sum_s m_{rs}.
$$

Usando la definición de $m_{rs}$,

$$
\sum_s m_{rs}
=
\sum_{ijs}\delta_{g_i r}\delta_{g_j s}A_{ij}
=
\sum_{ij}\delta_{g_i r}A_{ij}
=
\sum_i\delta_{g_i r}k_i
=
\sum_i\delta_{g_i r}c_i
=\kappa_r.
$$

Entonces

$$
\sum_s\hat\omega_{rs}\kappa_s
=
\frac{2m}{\kappa_r}\kappa_r
=2m.
$$

Por tanto, las restricciones para $\omega_{rs}$ se cumplen.

---

# Probabilidad perfilada

Sustituyendo los parámetros estimados $\hat c_i=k_i$ y

$$
\hat\omega_{rs}=\frac{2m\,m_{rs}}{\kappa_r\kappa_s},
$$

obtenemos la probabilidad perfilada, o log-verosimilitud perfilada:

$$
L=rac{1}{2}\sum_{rs}m_{rs}\log\left(\frac{m_{rs}}{\kappa_r\kappa_s}\right)+\text{constantes}.
$$

Esta expresión da el valor de máxima verosimilitud después de maximizar respecto a los parámetros continuos $c$ y $\Omega$.

Todavía falta maximizar respecto a $g$. Para cualquier asignación particular $g$ de nodos en grupos, calculamos $m_{rs}$, $\kappa_r$ y $\kappa_s$, los sustituimos en la expresión de $L$ y obtenemos un valor. Entonces buscamos la asignación $g$ que maximice $L$.

---

# Resumen operativo

El procedimiento de detección de comunidades basado en inferencia estadística es:

1. Elegir un número de grupos $q$.
2. Proponer una asignación de grupos $g=(g_1,\ldots,g_n)$.
3. Calcular los grados observados $k_i$.
4. Usar el estimador de máxima verosimilitud

$$
\hat c_i=k_i.
$$

5. Calcular

$$
\kappa_r=\sum_i\delta_{g_i r}k_i.
$$

6. Calcular

$$
m_{rs}=\sum_{ij}\delta_{g_i r}\delta_{g_j s}A_{ij}.
$$

7. Estimar

$$
\hat\omega_{rs}=\frac{2m\,m_{rs}}{\kappa_r\kappa_s}.
$$

8. Evaluar la log-verosimilitud perfilada

$$
L(g)=\frac{1}{2}\sum_{rs}m_{rs}\log\left(\frac{m_{rs}}{\kappa_r\kappa_s}\right)+\text{constantes}.
$$

9. Buscar la asignación $g$ que maximice $L(g)$.

---

# Interpretación conceptual

El modelo de bloques estocásticos corregido por grado separa dos efectos:

1. **Heterogeneidad de grados:** algunos nodos tienen más conexiones simplemente porque son nodos de alto grado. Esto se captura con $c_i$.
2. **Estructura comunitaria:** algunos grupos se conectan más entre sí o dentro de sí mismos. Esto se captura con $\omega_{rs}$.

La corrección por grado evita confundir nodos populares con comunidades reales. En otras palabras, no basta con que dos nodos tengan muchas conexiones; el modelo pregunta si sus conexiones son más probables de lo que esperaríamos dadas sus propensiones individuales de grado.

---

# Núcleo matemático

El núcleo del método es la optimización

$$
\max_g L(g),
$$

con

$$
L(g)=\frac{1}{2}\sum_{rs}m_{rs}\log\left(\frac{m_{rs}}{\kappa_r\kappa_s}\right)+\text{constantes}.
$$

Aquí:

- $g$ es la asignación de nodos a comunidades;
- $m_{rs}$ mide cuántas aristas conectan el grupo $r$ con el grupo $s$;
- $\kappa_r$ mide la suma de grados del grupo $r$;
- $L(g)$ mide qué tan plausible es la partición comunitaria bajo el modelo corregido por grado.

