



# Medidas de centralidad: qué miden + diferencia entre grafo no dirigido vs dirigido

## Grado
**Qué mide:** “popularidad local” = **cantidad de relaciones directas** (hubs por conexiones inmediatas).

- **No dirigido:** un solo grado $k(v)$ = número de vecinos (cada arista suma 1 a ambos extremos).
- **Dirigido:** se separa en
  - **out-degree** $k^{out}(v)$ = enlaces que **salen** de $v$,
  - **in-degree** $k^{in}(v)$ = enlaces que **entran** a $v$.
  Un “hub” puede ser **de salida** (alto $k^{out}$) o **de entrada** (alto $k^{in}$), y son roles distintos.

  
**Fórmula:**
- **No dirigido:** $$k(v)=\sum_{u\in V} A_{vu}.$$
- **Dirigido:** $$k^{out}(v)=\sum_{u\in V} A_{vu},\qquad k^{in}(v)=\sum_{u\in V} A_{uv}.$$



## Eigenvector
**Qué mide:** “estar conectado a nodos importantes” = no solo cuántos vecinos tienes, sino **qué tan centrales son tus vecinos** (se asocia a estructura núcleo–periferia).

- **No dirigido:** se aplica sobre una matriz simétrica; premia pertenecer al **núcleo** (vecinos que también son centrales).
- **Dirigido:** hay dos variantes naturales según el rol que quieras:
  - **prestigio/recepción:** eigenvector de $A^\top$ (ser apuntado por nodos centrales),
  - **influencia/emisión:** eigenvector de $A$ (apuntar hacia nodos centrales).
  En redes disconexas suele concentrarse en la componente con mayor “potencia” espectral.

**Fórmula:**
- **No dirigido (principal):** $$Ax=\lambda x,\qquad x\ge 0,\ \lambda=\rho(A).$$
- **Dirigido (dos roles):** $$Ax=\lambda x\ \ (\text{emisión}),\qquad A^\top x=\lambda x\ \ (\text{recepción}).$$
- 
## Katz
**Qué mide:** “influencia/accesibilidad por caminatas” = suma de **caminos de todas las longitudes** con descuento $\alpha^k$ (más global que grado; más tolerante que eigenvector).

- **No dirigido:** cuenta caminatas sin orientación; interpreta “alcance global” en la red con descuento por longitud.
- **Dirigido:** depende de la orientación:
  - Katz sobre $A$ favorece nodos con capacidad de **alcanzar** a muchos (salidas por caminos dirigidos),
  - Katz sobre $A^\top$ favorece nodos que son **alcanzados** por muchos (entradas por caminos dirigidos).
  Si no hay puentes entre componentes, Katz se reparte **por componente** (no hay transferencia entre componentes).


**Fórmula:**
$$c(\alpha)=\sum_{k=1}^{\infty}\alpha^k A^k\mathbf{1}=\left[(I-\alpha A)^{-1}-I\right]\mathbf{1},\qquad 0<\alpha<\frac{1}{\rho(A)}.$$

* **Interpretación de $\alpha$ en Katz**: $\alpha$ es el **descuento por longitud de camino** (cada salto extra multiplica por $\alpha$). Katz converge si $0<\alpha<\alpha_c$ con $\alpha_c=1/\rho(A)$ (radio espectral). Es más claro pensar en $\eta=\alpha\rho(A)\in(0,1)$:

  * **$\alpha$ pequeño (local)**: $\eta\lesssim 0.2$. Dominan caminos cortos; Katz $\approx \alpha A\mathbf{1}$, muy parecido a **grado**. Ranking estable.

  * **$\alpha$ mediano (meso-escala)**: $0.2\lesssim \eta\lesssim 0.8$. Pesan rutas de 2–5 saltos; premia estar **cerca de nodos importantes**, no solo ser hub directo.

  * **$\alpha$ grande (global/casi crítico)**: $\eta\gtrsim 0.8$ (cerca de $\alpha_c$). Caminos largos pesan mucho; Katz se vuelve parecido a **eigenvector** y más **sensible** (puede “dominar” la componente con mayor $\rho(A)$ en redes disconexas).

## PageRank
**Qué mide:** “importancia por flujo” = probabilidad estacionaria de un **paseo aleatorio con reinicio** (qué tan frecuente “caes” en un nodo siguiendo enlaces).

- **No dirigido:** se vuelve muy parecido a grado (el paseo aleatorio visita más a nodos con más conexiones).
- **Dirigido:** favorece nodos que **reciben** enlaces desde nodos importantes y/o están en rutas frecuentes del flujo; la dirección determina quién acumula masa.
- 
**Fórmula (forma estándar):**
$$p=\alpha P^\top p+(1-\alpha)v,$$
donde $P$ es la matriz de transición (p. ej. $$P=D_{out}^{-1}A$$ en dirigido, con ajuste de dangling nodes), $v$ es el vector de teleportación ($v_i\ge 0$, $\sum_i v_i=1$) y $\alpha\in(0,1)$.



## Hubs y Authorities (HITS)
**Qué mide:** “roles complementarios” en dirigido:
- **Hub:** nodo que **apunta** a buenas autoridades.
- **Authority:** nodo que **recibe** de buenos hubs.

- **No dirigido:** la distinción pierde sentido (al no haber orientación, hub/authority tienden a colapsar en un mismo rol).
- **Dirigido:** es donde HITS es informativo:
  - **Hub** alto = muchos enlaces salientes hacia **authorities** fuertes,
  - **Authority** alta = muchos enlaces entrantes desde **hubs** fuertes.


- **Fórmula:**
$$a \propto A^\top h,\qquad h \propto A a.$$
Equivalente:
$$A^\top A\,a=\lambda a,\qquad A A^\top\,h=\lambda h.$$

## Closeness (cercanía)
**Qué mide:** “rapidez de acceso” = qué tan cerca está un nodo del resto vía **distancias de caminos más cortos** (alto closeness ⇒ llega en pocas etapas).

- **No dirigido:** distancias geodésicas estándar (sin orientación).
- **Dirigido:** hay dos nociones:
  - **out-closeness:** qué tan rápido $v$ puede **alcanzar** a otros siguiendo direcciones,
  - **in-closeness:** qué tan rápido otros pueden **alcanzar** a $v$.
  En redes disconexas conviene usar **closeness armónica** (maneja distancias infinitas mejor que el closeness estándar).

**Fórmula:**
- **Closeness estándar (red conectada):**
$$C_C(v)=\frac{n-1}{\sum_{u\ne v} d(v,u)}.$$
- **Closeness armónica (útil si hay desconexión):**
$$C_H(v)=\sum_{u\ne v}\frac{1}{d(v,u)},\qquad \text{con } \frac{1}{\infty}=0.$$


## Betweenness (intermediación)
**Qué mide:** “control/puente” = fracción de **caminos más cortos** entre pares que pasan por el nodo (detecta brokers y cuellos de botella).

- **No dirigido:** cuenta intermediación sobre caminos más cortos sin orientación.
- **Dirigido:** cuenta intermediación sobre caminos más cortos **respetando dirección**; un nodo puede ser puente en sentido dirigido aunque no lo sea en el no dirigido. Si la red está en componentes separadas, la intermediación “entre componentes” es 0.


**Fórmula:**
$$C_B(v)=\sum_{\substack{s\ne v\ne t\\ s\ne t}}\frac{\sigma_{st}(v)}{\sigma_{st}},$$
donde $\sigma_{st}$ es el número de caminos más cortos entre $s$ y $t$, y $\sigma_{st}(v)$ los que pasan por $v$ (a veces se normaliza por $(n-1)(n-2)$ o equivalente).

# $\alpha$ de Katz:

