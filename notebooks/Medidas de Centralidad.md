# Medidas de centralidad: qué miden + fórmula + diferencia entre grafo no dirigido vs dirigido

## Grado
**Qué mide:** “popularidad local” = **cantidad de relaciones directas**.

**Fórmula:**
- **No dirigido:** $$k(v)=\sum_{u\in V} A_{vu}.$$
- **Dirigido:** $$k^{out}(v)=\sum_{u\in V} A_{vu},\qquad k^{in}(v)=\sum_{u\in V} A_{uv}.$$

**No dirigido vs dirigido:**
- **No dirigido:** un solo grado $k(v)$ (cada arista suma 1 a ambos extremos).
- **Dirigido:** se separa en out-degree (salen) e in-degree (entran).

---

## Eigenvector
**Qué mide:** “estar conectado a nodos importantes”.

**Fórmula:**
- **No dirigido (principal):** $$Ax=\lambda x,\qquad x\ge 0,\ \lambda=\rho(A).$$
- **Dirigido (dos roles):** $$Ax=\lambda x\ \ (\text{emisión}),\qquad A^\top x=\lambda x\ \ (\text{recepción}).$$

**No dirigido vs dirigido:**
- **No dirigido:** $A$ simétrica; suele reflejar “núcleo”.
- **Dirigido:** cambia según uses $A$ (influencia) o $A^\top$ (prestigio).

---

## Katz
**Qué mide:** influencia/accesibilidad por **caminatas** (caminos de todas las longitudes con descuento).

**Fórmula:**
$$c(\alpha)=\sum_{k=1}^{\infty}\alpha^k A^k\mathbf{1}=\left[(I-\alpha A)^{-1}-I\right]\mathbf{1},\qquad 0<\alpha<\frac{1}{\rho(A)}.$$

**No dirigido vs dirigido:**
- **No dirigido:** caminatas sin orientación.
- **Dirigido:** con $A$ enfatiza “alcanzar” (salidas); con $A^\top$ enfatiza “ser alcanzado” (entradas).

---

## PageRank
**Qué mide:** “importancia por flujo” = probabilidad estacionaria de un paseo aleatorio con reinicio.

**Fórmula (forma estándar):**
$$p=\alpha P^\top p+(1-\alpha)v,$$
donde $P$ es la matriz de transición (p. ej. $$P=D_{out}^{-1}A$$ en dirigido, con ajuste de dangling nodes), $v$ es el vector de teleportación ($v_i\ge 0$, $\sum_i v_i=1$) y $\alpha\in(0,1)$.

**No dirigido vs dirigido:**
- **No dirigido:** típicamente $$p_i\propto k(i)$$ (se parece a grado).
- **Dirigido:** favorece nodos que **reciben** enlaces desde nodos importantes y/o están en rutas frecuentes.

---

## Hubs y Authorities (HITS)
**Qué mide:** roles complementarios en dirigido: *hubs* apuntan a buenas *authorities*.

**Fórmula:**
$$a \propto A^\top h,\qquad h \propto A a.$$
Equivalente:
$$A^\top A\,a=\lambda a,\qquad A A^\top\,h=\lambda h.$$

**No dirigido vs dirigido:**
- **No dirigido:** hub/authority tienden a colapsar (no hay roles distintos claros).
- **Dirigido:** hub alto = apunta a authorities fuertes; authority alta = recibe de hubs fuertes.

---

## Closeness (cercanía)
**Qué mide:** “rapidez de acceso” vía distancias de caminos más cortos.

**Fórmula:**
- **Closeness estándar (red conectada):**
$$C_C(v)=\frac{n-1}{\sum_{u\ne v} d(v,u)}.$$
- **Closeness armónica (útil si hay desconexión):**
$$C_H(v)=\sum_{u\ne v}\frac{1}{d(v,u)},\qquad \text{con } \frac{1}{\infty}=0.$$

**No dirigido vs dirigido:**
- **No dirigido:** $d(v,u)$ sin orientación.
- **Dirigido:** distingue
  - **out-closeness:** usa $$d^{\rightarrow}(v,u)$$ (alcanzar siguiendo dirección),
  - **in-closeness:** usa $$d^{\rightarrow}(u,v)$$ (ser alcanzado).

---

## Betweenness (intermediación)
**Qué mide:** “puente/control” = cuántos caminos más cortos pasan por el nodo.

**Fórmula:**
$$C_B(v)=\sum_{\substack{s\ne v\ne t\\ s\ne t}}\frac{\sigma_{st}(v)}{\sigma_{st}},$$
donde $\sigma_{st}$ es el número de caminos más cortos entre $s$ y $t$, y $\sigma_{st}(v)$ los que pasan por $v$ (a veces se normaliza por $(n-1)(n-2)$ o equivalente).

**No dirigido vs dirigido:**
- **No dirigido:** caminos más cortos sin orientación.
- **Dirigido:** caminos más cortos respetando dirección; puede cambiar mucho quién es “puente”.