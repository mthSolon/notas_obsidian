>[!missing] MELHORAR
>O início da nota fala sobre teste qui-quadrado e depois fala sobre associação entre variáveis qualitativas. Separar em duas notas **teste qui-quadrado** e **associação entre duas variáveis qualitativas**.
>Falar sobre o coeficiente de Spearmen

>[!summary] Resumo
>O teste nos diz se há uma associação significativa entre duas variáveis.

>[!WARNING] Atenção
>Um problema com esse teste é que ele não dá a força de associação entre as duas variáveis, por esse motivo se utiliza o coeficiente de contingência para obter esse valor.  

O teste qui-quadrado é uma ferramenta estatística que nos ajuda a entender **se existe uma associação significativa entre duas variáveis categóricas.** Em outras palavras, ele nos ajuda a responder a perguntas como: "Há uma relação entre a preferência de produto A ou B e a faixa etária dos consumidores?" ou "Existe uma associação entre o gênero de uma pessoa e sua escolha de atividade física?".  
  
Vamos desmembrar isso um pouco mais:  
  
- **Variáveis Categóricas**: São características que podem ser divididas em diferentes categorias, mas não têm uma ordem intrínseca. Por exemplo, cor dos olhos (azul, castanho, verde) ou tipo de ocupação (estudante, profissional, aposentado).  
  
- **Associação Significativa**: O teste qui-quadrado nos ajuda a determinar se as frequências observadas em nossos dados são significativamente diferentes das frequências que esperaríamos se não houvesse associação real entre as variáveis.  
  
- **Como Funciona**: O teste compara as frequências observadas em uma tabela de contingência (uma tabela que mostra a distribuição conjunta das duas variáveis) com as frequências esperadas. As frequências esperadas são calculadas sob a suposição de que não há associação entre as variáveis.  
  
- **Resultado**: Se as frequências observadas não diferem significativamente das frequências esperadas, não há evidência estatística de associação. Se houver diferenças significativas, podemos concluir que há uma associação entre as variáveis.  
  
Em resumo, o teste qui-quadrado é como uma ferramenta de detetive estatístico que nos ajuda a descobrir se há uma ligação significativa entre diferentes categorias de variáveis categóricas. Ele é muito útil para analisar padrões e relações em dados que não são expressos em termos numéricos, mas sim em termos de categorias.

## Intuição matemática do qui-quadrado

Considere a seguinte tabela:

![[tabela_qui_dependente.png]]

Se as variáveis forem tratadas como independentes, teríamos a seguinte tabela:

![[tabela_qui_independente.png]]

em que todas as frequências relativas de cada coluna seriam iguais, pois o fato de uma pessoa ser da cooperativa *Produtor* não deveria influenciar de que *Estado* ela seria. A primeira tabela, portanto, mostra os valores observados $o_i$ e a segunda tabela mostra os valores esperados $e_i$.

Dessa maneira, podemos calcular os desvios de cada variável subtraindo cada valor observado $o_i$ pelo valor esperado $e_i$:

![[desvios_qui.png]]

Entretanto, os desvios acima podem enganar, pois são absolutos. Por exemplo, o maior desvio na categoria *Escola* seria o estado de *São Paulo*, mas o desvio relativo do *Paraná* é maior que o de *São Paulo*, pois apresenta um valor esperado menor que o de *São Paulo*.

Uma medida para calcular o desvio relativo pode ser descrito a seguir:
$$
\frac{(o_i - e_i)^2}{e_i},
$$
onde $o_i$ é o valor observado e $e_i$ é o valor esperado. 

A soma de todos os desvios relativos descreve uma medida de afastamento global chamada $\chi^2$ (qui-quadrado) de Pearson. **Um valor grande de $\chi^2$ indica uma associação entre as variáveis**.

Além do $\chi^2$, Pearson definiu uma medida de associação chamada de *coeficiente de contingência* dado por
$$
C = \sqrt{\frac{\chi^2}{\chi^2 + n}},
$$
onde $n$ é o tamanho da amostra. Um inconveniente do coeficiente $C$ é que ele não varia entre 0 e 1. O valor máximo de $C$ depende da quantidade de categorias da variável $X$ e da variável $Y$. Para evitar isso, costuma-se definir outro coeficiente, dado por
$$
T = \sqrt{\frac{\chi^2/n}{(r-1)(s-1)}},
$$
em que $r$ e $s$ são a quantidade de categorias de cada variável respectivamente. Esse coeficiente atinge o valor máximo igual a 1 se $r = s$.

O *coeficiente V de Cramer* também pode ser utilizado, pois varia de \[0, 1].
$$
V = \sqrt{\frac{\chi^2}{n\cdot(q-1)}}
$$
onde $q$ é o $min(i, j)$ em que $i, j$ é a quantidade de linhas e colunas respectivamente.