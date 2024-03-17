>[!missing] MELHORAR
>Ver a seção de Target Encoder da documentação do scikit-learn, lá possui informações valiosas sobre a parte matemática do encoder.

>[!tip] Casos de uso
>Target encoding é ótimo para:
>- **Features com alta cardinalidade**: uma feature com um alto número de categorias pode se tornar um problema na hora de codificar, um *one-hot encoding* geraria muitas colunas. Outras alternativas, como *Ordinal Encoder*, podem não ser apropriadas para a feature. O Target Encoder deriva valores das categorias utilizando a propriedade mais importante da feature que é sua relação com o target.
>- **Features motivadas pelo domínio**: por experiência prévia, você pode suspeitar que uma feature categórica pode ser importante mesmo se ela marcou baixo em alguma métrica. O Target Encoder pode ajudar a revelar a verdadeira informatividade da feature.

**Target encoding** é qualquer tipo de encoding que substitui os valores categóricos por algum número derivado do *target*. Por exemplo:

| marca       | preço | marca_encoded |
| ----------- | ----- | ------------- |
| alfa-romero | 13495 | 15498.333333  |
| alfa-romero | 16500 | 15498.333333  |
| alfa-romero | 16500 | 15498.333333  |
| audi        | 13950 | 17859.166667  |
| audi        | 17450 | 17859.166667  |
| audi        | 15250 | 17859.166667  |
| audi        | 17710 | 17859.166667  |
| audi        | 18920 | 17859.166667  |
| audi        | 23875 | 17859.166667  |
| bmw         | 16430 | 16430         |
Cada marca foi substituída pela média do preço por cada marca.

>[!info] Info
>A média foi usada na tabela acima, mas é possível utilizar outras métodos, como a probabilidade da categoria.

## Problemas

1. **O primeiro problema é categorias desconhecidas**. Target encodings criam um risco de overfitting, o que significa que eles precisam ser treinados em um split de encoding independente. Quando você junta os encodings de splits futuros, o Pandas irá preencher os valores faltantes para qualquer categoria que não esteja presente no split do encoding. Você deve imputar esses valores faltantes de alguma maneira.
2. **O segundo problema são as categorias raras**. Quando uma categoria ocorre poucas vezes no dataset, qualquer estatística calculada no seu grupo não irá representá-la muito bem. Por exemplo, a marca *bmw* aparece apenas uma vez na tabela, a média calculada para a marca foi apenas o valor *preço* daquele único veículo que não irá representar muito bem qualquer outra *bmw* no futuro. **Aplicar Target Encoding em categorias raras pode levar ao overfitting**.

## Solução
A solução para esses problemas é utilizar uma técnica chamada de **smoothing**. A ideia é misturar a média dos valores da categoria com a média dos valores de todas as categorias: `encoding = weight * in_category + (1 - weight) * overall` onde `weight` é um valor entre 0 e 1 calculado frequência da categoria. Categorias raras recebem um peso menor na sua média, enquanto categorias faltantes irão receber apenas a média geral.

Um método fácil para determinar o valor de `weight` é computar uma **m-estimate**:
`weight = n / (n + m)` onde `n` é o total de vezes que a categoria ocorre nos dados. O parâmetro `m` determina o fator **smoothing**. Valores grandes de `m` colocam mais peso na estimativa geral.

![[m-estimate.png]]

Quando for escolher o valor de `m`, considere quão ruidosa você espera as categorias estarem. O preço do veículo varia muito para cada marca? Você precisa de muitos dados para ter boas estimativas? Se sim, é melhor usar um valor grande para `m`; se a média do preço para cada marca for relativamente estável, um valor pequeno pode ser usado.