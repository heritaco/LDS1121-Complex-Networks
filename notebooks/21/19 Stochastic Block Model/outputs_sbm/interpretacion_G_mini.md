### Interpretación específica: G_mini
- El criterio penalizado seleccionó $q=3$ con $L=-59.3577$ y BIC-like=130.0679.
- La modularidad diagnóstica es baja ($Q=0.0671$), lo cual es coherente con un SBM que detecta roles además de comunidades densas.
- Media diagonal de $\hat\Omega$: 0.815; media fuera de diagonal: 1.128; razón diagonal/fuera=0.722.
- Pares de bloques más intensos después de corregir por grado: C1-C2: omega=3.385, M=13, C0-C0: omega=2.444, M=18, C0-C1: omega=0.000, M=0.
- En la minired, el patrón se vuelve más nítido: `C0` conserva el núcleo pagos/retail, mientras `C1` y `C2` separan plataformas tecnológicas e infraestructura/IA.
- La eliminación de nodos hoja no cambia la historia principal; reduce ruido periférico y deja el patrón bipartito tecnológico más visible.
- C0: 7 nodos; 9 aristas internas; $\kappa_0=18$. Nodos principales por grado: MA(4), AAPL(3), V(3), BAC(2). Lectura: bloque de pagos/retail/consumo.
  Miembros: AAPL, BAC, COST, HD, MA, V, WMT.
- C1: 5 nodos; 0 aristas internas; $\kappa_1=13$. Nodos principales por grado: AMZN(3), MSFT(3), ORCL(3), GOOGL(2). Lectura: bloque de plataformas/compradores tecnológicos.
  Miembros: AMZN, GOOGL, MSFT, ORCL, TSLA.
- C2: 3 nodos; 0 aristas internas; $\kappa_2=13$. Nodos principales por grado: NVDA(5), AMD(4), PLTR(4). Lectura: bloque de infraestructura/IA y nodos conectados a plataformas.
  Miembros: AMD, NVDA, PLTR.
- El vínculo entre bloques más relevante es C1-C2: $m_{12}=13$ y $\hat\omega_{12}=3.385$. Nodos que más explican ese cruce: NVDA(5; grado 5), AMD(4; grado 4), PLTR(4; grado 4), AMZN(3; grado 3), MSFT(3; grado 3), ORCL(3; grado 3).