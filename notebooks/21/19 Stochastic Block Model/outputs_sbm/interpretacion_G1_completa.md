### Interpretación específica: G1 completa
- El criterio penalizado seleccionó $q=3$ con $L=-118.6285$ y BIC-like=250.1693.
- La modularidad diagnóstica es baja ($Q=0.0175$), lo cual es coherente con un SBM que detecta roles además de comunidades densas.
- Media diagonal de $\hat\Omega$: 0.949; media fuera de diagonal: 1.028; razón diagonal/fuera=0.923.
- Pares de bloques más intensos después de corregir por grado: C1-C2: omega=3.083, M=24, C0-C0: omega=2.846, M=26, C0-C1: omega=0.000, M=0.
- En la red completa, `C0` separa el subecosistema pagos/retail/consumo: tiene aristas internas y no se conecta con el componente tecnológico.
- `C1` y `C2` no son comunidades densas internamente; son dos lados de una estructura tecnológica disasortativa. La masa relevante está entre ambos bloques, no en sus diagonales.
- C0: 11 nodos; 13 aristas internas; $\kappa_0=26$. Nodos principales por grado: AAPL(5), MA(4), WMT(4), V(3). Lectura: bloque de pagos/retail/consumo.
  Miembros: AAPL, AVGO, BAC, BRK.B, COST, HD, JPM, MA, PG, V, WMT.
- C1: 11 nodos; 0 aristas internas; $\kappa_1=24$. Nodos principales por grado: NVDA(8), AMD(4), PLTR(4), ABBV(1). Lectura: bloque de infraestructura/IA y nodos conectados a plataformas.
  Miembros: ABBV, AMD, CVX, GE, JNJ, LLY, NFLX, NVDA, PLTR, UNH, XOM.
- C2: 8 nodos; 0 aristas internas; $\kappa_2=24$. Nodos principales por grado: AMZN(8), MSFT(6), ORCL(3), GOOGL(2). Lectura: bloque de plataformas/compradores tecnológicos.
  Miembros: AMZN, GOOG, GOOGL, META, MSFT, MU, ORCL, TSLA.
- El vínculo entre bloques más relevante es C1-C2: $m_{12}=24$ y $\hat\omega_{12}=3.083$. Nodos que más explican ese cruce: AMZN(8; grado 8), NVDA(8; grado 8), MSFT(6; grado 6), AMD(4; grado 4), PLTR(4; grado 4), ORCL(3; grado 3).