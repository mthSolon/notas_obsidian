>[!missing] MELHORAR
>Colocar a intuição matemática, exemplos etc.

>[!summary] Resumo
>Teste estatístico para observar se uma distribuição de dados segue alguma distribuição específica ou se difere de forma significativa dessa distribuição  

> [!important] Importante
> Ajuda a ver se alguma variável previamente observada teve sua distribuição mudada (Data Drift).  

Existem três tipos de desvios:  
1. Desvio sazonal (de tempos em tempos, como a black friday).  
2. Desvio súbito.  
3. Desvio gradual.  

## Fórmula

![[kilmogorov-smirnov.png]]

Com a formula acima, o teste calcula uma estatística chamada KS. A estatística KS vai nos retornar um valor numérico que representa a maior diferença absoluta entre as distribuições acumuladas. Por exemplo, se o valor for 0.1, significa que há uma diferença de 0.1 entre as distribuições. ==**Quanto maior for esse valor, maior é a diferença entre as distribuições**==, o que indica que a distribuição sofreu uma modificação em seu padrão, logo, há uma grande chance de ter ocorrido um data drift.  
  
Ao utilizar essa estatística, podemos fazer um teste estatístico para avaliar se as duas amostras de notas são realmente diferentes, ou seja, se houve data drift ou se podem ter mantido o padrão. Para isso, comparamos o valor obtido com um valor crítico (geralmente, 0.05). Se o valor estiver abaixo desses limites, é bem provável que as notas não possuam a mesma distribuição.

## Tipos de drift

![[tipos_de_drift.png]]

## Tabela de quantis do teste estatístico de Kolmogorov  

![[quantis_para_kilmogorov_teste_estatistico.png]]
