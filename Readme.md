**Symbols and Assumptions:**

- Number of layers: $L$

- Neuron count in each layer: $[n_0, n_1, ..., n_L]$

- Input/output dimension: $n_0=d_{in}$, $n_L=d_{out}$

- Spline parameters: $D_{spline}=G+K+1$ (where $G$ = number of grid intervals, $K$ = spline order)

- Total number of edges: $N_{edges}=\sum_{l=0}^{L-1}(n_l\times n_{l+1})$

- Number of pre-output layer nodes: $N_{nodes}=\sum_{l=0}^{L-1} n_l$

- $F_{act}$: FLOPs for the non-linear activation function used in MLP or KAN (e.g., SiLU)

- $C_{spline}$: Core B-spline complexity per edge per sample:

  $C_{spline} = 9 \times K \times (G + 1.5 \times K) + 2 \times G - 2.5 \times K$

- Weight generation FLOPs $C_{meta\_gen} = 2 d_{hidden} + F_{act} d_{hidden} + 2 d_{hidden} (G+K+1)$

Table 1 FLOPs Comparison Summary

| Model   | Forward FLOPs                                                | Backward FLOPs                              | Total FLOPs                                                  |
| ------- | ------------------------------------------------------------ | ------------------------------------------- | ------------------------------------------------------------ |
| KAN     | $F_{act} N_{nodes} + N_{edges} C_{spline}$                   | $2N_{node}(K^2 + GK)+3N_{edges} D_{spline}$ | $F_{act} N_{nodes} + N_{edges}  C_{spline}+2N_{node}(K^2 + GK)+3N_{edges}D_{spline}$ |
| MetaKAN | $F_{act} N_{nodes} + N_{edges} C_{spline}+N_{edges}  C_{meta\_gen}$ | $2N_{edges}+ 2C_{meta\_gen}$                | $F_{act} N_{nodes} + N_{edges} C_{spline}+(2N_{edges}+4d_{hidden}) D_{spline}$ |

