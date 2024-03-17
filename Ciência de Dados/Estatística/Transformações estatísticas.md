Vários procedimentos estatísticos são baseados na suposição de que **os dados provêm de uma distribuição normal** (em forma de sino) ou então mais ou menos simétrica. Mas, em muitas situações de **interesse prático**, a distribuição dos dados da amostra **é assimétrica** e pode conter valores atípicos.

Se quisermos utilizar tais procedimentos, o que se propõe é efetuar uma transformação das observações, de modo a se obter uma distribuição mais simétrica e próxima da normal. Uma família de transformações frequentemente utilizada é:

$$
x^{(p)} = 
\begin{cases}
x^p, &\text{se $p$ > 0} \\
ln(x), &\text{se $p$ = 0} \\
-x^p, &\text{se $p$ < 0}
\end{cases}
$$

Normalmente, o que se faz é experimentar valores de $p$ na sequência:

$$
...,–3, –2, –1, –1/2, –1/3, –1/4, 0, 1/4, 1/3, 1/2, 1, 2, 3, ...
$$

e para cada valor de p obtemos gráficos apropriados (histogramas, desenhos esquemáticos etc.) para os dados originais e transformados, de modo a escolhermos o valor mais adequado de p.

>[!tip] Qual valor de $p$ usar?
>Para dados positivos teremos, usualmente, dados assimétricos à direita. Para essas distribuições, a transformação $0 < p < 1$ é apropriada, pois valores grandes x decrescem mais, relativamente a valores pequenos. Para distribuições assimétricas à esquerda, tome $p > 1$.
