[[#Técnicas]]
- [[#Analisar suas distribuições]]
- [[#Considerar os pontos fora da curva]]
- [[#Dividir os dados]]
- [[#Considerar a significância prática]]
- [[#Verificar a consistência ao longo do tempo]]
- [[#Confirmar e contar sua filtragem]]
[[#Processo]]
- [[#Validação, descrição e avaliação separadas]]
- [[#Confirme a configuração do experimento e da coleta de dados]]
- [[#Verificar o que não deve mudar]]
- [[#Padrão primeiro, segundo personalizado]]
- [[#Verificar a reprodutibilidade]]
- [[#Verificar a consistência com medições anteriores]]
- [[#As novas métricas precisam ser aplicadas primeiro aos dados/recursos antigos]]
- [[#Fazer hipóteses e procurar evidências]]
- [[#Benefícios da análise exploratória da iteração completa]]
- [[#Atenção aos comentários]]
[[#Mentalidade]]
- [[#A análise de dados começa com perguntas, não dados ou uma técnica]]
- [[#Seja cético e defensor]]
- [[#Correlação != Causalidade]]

## Técnicas

### Analisar suas distribuições
A maioria dos profissionais usa métricas de resumo (por exemplo, média, mediana, desvio padrão e assim por diante) para se comunicar sobre distribuições. No entanto, normalmente é necessário examinar representações de distribuição muito mais detalhadas gerando histogramas, funções de distribuição cumulativa (CDFs), gráficos quantil-quantis (Q-Q) e assim por diante. Essas representações mais avançadas permitem detectar recursos importantes dos dados, como comportamento multimodal ou uma classe significativa de outliers.

### Considerar os pontos fora da curva
Analise os pontos fora da curva com cuidado, porque eles podem ser canários na mina de carvão que indicam problemas mais fundamentais com sua análise. Não há problema em excluir valores atípicos dos seus dados ou agrupá-los em uma categoria "incomum", mas você precisa saber por que os dados foram direcionados a essa categoria.

Por exemplo, uma análise das consultas com o menor número de cliques pode revelar cliques em elementos que você não está contando. Analisar consultas com o maior número de cliques pode revelar cliques que não deveriam ser contabilizados. Por outro lado, pode haver algumas exceções que você nunca conseguirá explicar. Portanto, tenha cuidado com quanto tempo você dedica a essa tarefa.

### Dividir os dados

Dividir significa separar os dados em subgrupos e analisar os valores de métricas para cada subgrupo separadamente. Geralmente, dividimos dimensões como navegador, localidade, domínio, tipo de dispositivo e assim por diante. Se for provável que o fenômeno subjacente funcione de maneira diferente entre subgrupos, será necessário dividir os dados para confirmar se esse é mesmo o caso. Mesmo que você não espere que o corte produza resultados diferentes, analisar algumas frações para ter consistência interna oferece maior confiança de que você está medindo a coisa certa. Em alguns casos, uma parcela específica pode ter dados incorretos, uma interação do usuário corrompida ou, de alguma forma, ser fundamentalmente diferente.

Sempre que você dividir os dados para comparar dois grupos (como experimento e controle, ou mesmo "horário A" e "horário B"), você precisa estar ciente das mudanças na combinação. Uma _mudança de mix_ ocorre quando a quantidade de dados nas fatias de cada grupo é diferente. [O paradoxo de Simpson](http://wikipedia.org/wiki/Simpson's_paradox) e outras confusões podem ocorrer. Geralmente, se a quantidade relativa de dados em uma fatia for a mesma nos dois grupos, você poderá fazer uma comparação com segurança.

### Considerar a significância prática

Com um grande volume de dados, pode ser tentador se concentrar apenas na significância estatística ou nos detalhes de cada dado. Mas você precisa se perguntar: "Mesmo que seja verdade que o valor X é 0,1% maior do que o valor de Y, isso importa?" Isso pode ser especialmente importante se você não consegue entender/categorizar parte dos seus dados. Se você não consegue entender algumas strings de user agent nos registros, independentemente de elas representarem 0,1% ou 10% dos dados, há uma grande diferença na maneira como você precisa investigar esses casos.

Como alternativa, às vezes você tem um pequeno volume de dados. Muitas mudanças não parecem ser estatisticamente significativas, mas isso é diferente de declarar que elas são "neutras". Pergunte a si mesmo: "Qual a probabilidade de que ainda haja uma mudança _praticamente significativa_?"

### Verificar a consistência ao longo do tempo

Quase sempre tente dividir os dados por unidades de tempo, porque muitas perturbações nos dados subjacentes acontecem à medida que nossos sistemas evoluem com o tempo. Muitas vezes usamos dias, mas outras unidades de tempo também podem ser úteis. Durante o lançamento inicial de um recurso ou de uma nova coleta de dados, os usuários geralmente verificam cuidadosamente se tudo está funcionando conforme o esperado. No entanto, muitas falhas ou comportamentos inesperados podem surgir ao longo do tempo.

Só porque um determinado dia ou conjunto de dias é um ponto fora da curva, não significa que você precisa descartar os dados correspondentes. Use os dados como um gancho para determinar uma razão causal pelo qual esse dia ou dias são diferentes antes de descartá-los.

Analisar os dados diários também oferece uma noção da variação nos dados que, em algum momento, levaria a intervalos de confiança ou declarações de significância estatística. Geralmente, isso não substitui o cálculo rigoroso do intervalo de confiança, mas, muitas vezes, com grandes mudanças, é possível notar que elas terão significância estatística apenas nos gráficos diários.

### Confirmar e contar sua filtragem

Quase todas as análises de dados grandes começam com a filtragem de dados em vários estágios. Talvez você queira considerar apenas usuários dos EUA, pesquisas na Web ou pesquisas com anúncios. Seja qual for o caso, você precisa:

- Confirme e especifique claramente a filtragem que você está fazendo.
- Conte a quantidade de dados que estão sendo filtrados em cada etapa.

Muitas vezes, a melhor maneira de fazer isso é calcular _todas_ as métricas, mesmo para a população que você está excluindo. Então, você pode analisar esses dados para responder a perguntas como: "Que fração de consultas a filtragem de spam removeu?" Dependendo do motivo da filtragem, esse tipo de análise nem sempre é possível.

## Processo

Esta seção contém recomendações sobre como abordar seus dados, quais perguntas fazer sobre eles e o que verificar.

### Validação, descrição e avaliação separadas

Eu penso na análise de dados como tendo três estágios inter-relacionados:

1. **Validação**: acredito que os dados são autoconsistentes, que foram coletados corretamente e que representam o que eu acho que fazem?
2. **Descrição**: qual é a interpretação objetiva desses dados? Por exemplo, "Os usuários fazem menos consultas classificadas como X", "No grupo experimental, o tempo entre X e Y é 1% maior" e "Menos usuários vão para a próxima página de resultados".
3. **Avaliação**: dada a descrição, os dados nos dizem que algo bom está acontecendo para o usuário, para o Google ou para o mundo?

Ao separar esses estágios, você pode chegar a um acordo com outras pessoas mais facilmente. A descrição deve ser algo com que todos possam concordar para os dados. A avaliação provavelmente estimulará muito mais debate. Se você não separar "Descrição" e "Avaliação", é muito mais provável que veja apenas a interpretação dos dados que espera ver. Além disso, a avaliação tende a ser muito mais difícil, porque estabelecer o valor regulatório de uma métrica, geralmente por meio de comparações rigorosas com outros recursos e métricas, exige um investimento significativo.

Essas etapas não progridem de maneira linear. Ao explorar os dados, você pode avançar e voltar entre as fases, mas a qualquer momento é preciso deixar claro em que estágio você está.

### Confirme a configuração do experimento e da coleta de dados

Antes de analisar qualquer dado, entenda o contexto em que eles foram coletados. Se os dados vierem de um experimento, analise a configuração dele. Se forem da instrumentação do novo cliente, você precisa ter pelo menos um entendimento básico de como os dados são coletados. É possível que você encontre configurações incomuns ou ruins, ou restrições de população (como dados válidos somente para o Chrome). Qualquer coisa notável aqui pode ajudar você a construir e verificar as teorias mais tarde. Alguns itens a serem considerados:

- Se o experimento estiver em andamento, faça o teste por conta própria. Se isso não for possível, analise as capturas de tela/descrições do comportamento.
- Verifique se houve algo incomum no período em que o experimento ocorreu (fim de ano, grandes lançamentos etc.).
- Determinar quais populações de usuários foram submetidas ao experimento.

### Verificar o que não deve mudar

Como parte do estágio "Validação", antes de responder à pergunta do seu interesse (por exemplo, "Adicionar uma foto de um rosto aumentou ou diminuiu os cliques?"), exclua qualquer outra variabilidade nos dados que possa afetar o experimento. Exemplo:

- O número de usuários mudou?
- O número certo de consultas afetadas apareceu em todos os meus subgrupos?
- As taxas de erro mudaram?

Essas perguntas são relevantes tanto para comparações de experimento/controle quanto para análise de tendências ao longo do tempo.

### Padrão primeiro, segundo personalizado

Ao analisar novos recursos e dados, é particularmente tentador mergulhar diretamente nas métricas novas ou especiais desse novo recurso. No entanto, sempre confira as métricas padrão primeiro, mesmo que espere que elas mudem. Por exemplo, ao adicionar um novo bloco universal à página, entenda o impacto nas métricas padrão, como "cliques em resultados da Web", antes de se aprofundar nas métricas personalizadas desse novo resultado.

As métricas padrão são muito mais bem validadas e têm mais chances de serem corretas do que as métricas personalizadas. Se as métricas personalizadas não fazem sentido com as padrão, é provável que elas estejam erradas.

### Verificar a reprodutibilidade

O fracionamento e a consistência ao longo do tempo são exemplos específicos de verificação de reprodutibilidade. Se um fenômeno é importante e significativo, você precisa vê-lo em diferentes populações de usuários e em diferentes horários. Mas verificar a reprodutibilidade significa mais do que executar essas duas verificações. Se você estiver criando modelos dos dados, convém que eles sejam estáveis em pequenas perturbações nos dados subjacentes. O uso de diferentes intervalos de tempo ou subamostras aleatórias dos dados também informa o nível de confiabilidade desse modelo.

Se um modelo não for reproduzível, você provavelmente não está capturando algo fundamental sobre o processo subjacente que produziu os dados.

### Verificar a consistência com medições anteriores

Muitas vezes, você estará calculando uma métrica semelhante a coisas que foram contadas no passado. Compare suas métricas com aquelas informadas anteriormente, mesmo que elas estejam em populações de usuários diferentes.

Por exemplo, se você estiver analisando o tráfego de consulta de uma população especial e medir que o tempo médio de carregamento da página é de cinco segundos, mas as análises anteriores de todos os usuários deram um tempo de carregamento de página médio de dois segundos, é necessário investigar. Seu número pode ser o correto para esta população, mas agora você tem que fazer mais trabalho para validar isso.

Não é preciso chegar a um acordo, mas você precisa estar na mesma base. Se não estiver, presuma que esteja errado até que possa se convencer totalmente. A maioria dos dados surpreendentes acabará sendo um erro, não um insight novo incrível.

### As novas métricas precisam ser aplicadas primeiro aos dados/recursos antigos

Se você criar novas métricas (possivelmente coletando uma nova fonte de dados) e tentar aprender algo novo, não saberá se a nova métrica está certa. Ao usar as novas métricas, primeiro aplique essas informações a um recurso ou dado conhecido. Por exemplo, se você tiver uma nova métrica para a satisfação do usuário, certifique-se de que ela informe seus melhores recursos para ajudar na satisfação. Se você tiver uma métrica nova para onde os usuários direcionam a atenção para a página, verifique se ela corresponde ao que sabemos com base em estudos de rastreamento ocular ou de rotuladores sobre como as imagens afetam a atenção da página. Isso proporciona validação quando você aprende algo novo.

### Fazer hipóteses e procurar evidências

Normalmente, a análise de dados para um problema complexo é iterativa.[2](https://developers.google.com/machine-learning/guides/good-data-analysis?hl=pt-br#fn2) Você descobrirá anomalias, tendências ou outros recursos dos dados. Naturalmente, você desenvolverá teorias para explicar esses dados. Não basta desenvolver uma teoria e proclamá-la como verdadeira. Procure evidências (dentro ou fora dos dados) para confirmar/negar essa teoria. Exemplo:

- Se você notar algo que pareça uma tendência de aprendizado, veja se isso se manifesta mais fortemente com usuários de alta frequência.
- Se você acredita que uma anomalia é causada pelo lançamento de alguns recursos, verifique se a população para que o recurso foi lançado é a única afetada pela anomalia. Como alternativa, verifique se a magnitude da mudança é consistente com as expectativas do lançamento.
- Se as taxas de crescimento dos usuários mudarem em uma localidade, tente encontrar uma fonte externa que valide essa taxa de mudança.

Uma boa análise de dados terá uma história para contar. Para ter certeza de que é a história certa, você precisa contar a história para si mesmo e procurar evidências de que ela está errada. Uma maneira de fazer isso é se perguntar: "Quais experimentos eu executaria que validariam/invalidariam a história que estou contando?". Mesmo que você possa/não possa fazer esses experimentos, eles podem dar ideias de como validar com os dados que você tem.

A boa notícia é que essas teorias e possíveis experimentos podem levar a novas linhas de pesquisa que transcendem a tentativa de aprender sobre qualquer recurso ou dados específico. Depois, você entra no reino da compreensão não apenas desses dados, mas de derivar novas métricas e técnicas para todos os tipos de análises futuras.

### Benefícios da análise exploratória da iteração completa

Ao fazer a análise exploratória, faça o máximo possível de iterações de toda a análise. Normalmente, você terá várias etapas de coleta, processamento, modelagem, entre outros. Se passar muito tempo para aperfeiçoar o primeiro estágio dos indicadores iniciais, vai perder oportunidades de fazer mais iterações na mesma quantidade de tempo. Além disso, quando você finalmente olha seus dados no final, você pode fazer descobertas que mudam sua direção. Portanto, seu foco inicial não deve ser na perfeição, mas em conseguir algo razoável até o fim. Deixe anotações para você e confirme coisas como etapas de filtragem e solicitações não analisáveis ou incomuns, mas não perca tempo tentando se livrar de todas elas no início da análise exploratória.

### Atenção aos comentários

Normalmente, definimos várias métricas relacionadas ao sucesso do usuário. Por exemplo, os usuários clicaram em um resultado? Se você alimentar esses dados de volta no sistema (o que fazemos em diversos lugares), criará muitas oportunidades para confusão de avaliação.

Não é possível usar a métrica enviada ao sistema como base para avaliar a alteração. Se você veicula mais anúncios que recebem mais cliques, não pode usar "mais cliques" como base para decidir se os usuários estão mais satisfeitos, mesmo que "mais cliques" signifiquem "mais satisfeitos". Além disso, você não deve nem diminuir as variáveis que foram alimentadas e manipuladas, porque isso resultaria em mudanças na combinação que serão difíceis ou impossíveis de entender.

## Mentalidade

Esta seção descreve como trabalhar com outras pessoas e comunicar insights.

### A análise de dados começa com perguntas, não dados ou uma técnica

Há sempre uma motivação para analisar dados. Formular suas necessidades como perguntas ou hipóteses ajuda a garantir que você esteja coletando os dados que precisa coletar e que está pensando sobre as possíveis lacunas nos dados. Claro, as perguntas que você faz devem evoluir à medida que você analisa os dados. No entanto, uma análise sem uma pergunta terminará sem propósito.

Não caia na armadilha de encontrar alguma técnica favorita e só encontrar as partes dos problemas em que essa técnica funciona. Novamente, criar perguntas claras ajudará a evitar essa armadilha.

### Seja cético e defensor

Ao trabalhar com dados, você precisa se tornar o defensor dos insights que está conseguindo e o cético deles. Você encontrará alguns fenômenos interessantes nos dados que observar. Ao detectar um fenômeno interessante, faça a si mesmo as seguintes perguntas:

- Que outros dados eu poderia coletar para mostrar o quanto isso é incrível?
- O que eu poderia descobrir que invalidaria isso?"

Especialmente em casos em que você está fazendo uma análise para alguém que realmente quer uma resposta específica (por exemplo, "Meu recurso é incrível!"), é preciso ser cético para evitar erros.

### Correlação != Causalidade

Ao fazer teorias sobre dados, frequentemente queremos declarar que "X causa Y", por exemplo, "a página ficando mais lenta fez com que os usuários clicassem menos". [Mesmo o xkcd sabe](http://xkcd.com/552/) que não é possível simplesmente estabelecer a causalidade devido à correlação. Ao considerar como você validaria uma teoria da causalidade, normalmente é possível desenvolver uma boa noção do quanto uma teoria causal é confiável.

Às vezes, as pessoas tentam manter uma correlação tão significativa, afirmando que, mesmo que não haja relação causal entre A e B, deve haver algo subjacente à coincidência para que um sinal possa ser um bom indicador ou substituto do outro. Essa área é perigosa para vários problemas de teste de hipóteses. Como o [xkcd também sabe](http://xkcd.com/882/), com experimentos e dimensões suficientes, alguns dos sinais se alinharão para um experimento específico. Isso não implica que os mesmos indicadores vão se alinhar no futuro. Você tem a mesma obrigação de considerar uma teoria causal, como "há um efeito oculto C que causa A e B", para que você possa tentar validar se isso é plausível.

Um analista de dados precisa frequentemente lidar com essas perguntas causais para as pessoas que querem consumir os dados. Você deve deixar claro para esses consumidores o que você pode e não pode dizer sobre causalidade.