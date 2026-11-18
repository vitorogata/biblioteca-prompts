# Analisar tempo de atendimento com dado faltante

## Identificação do teste

**Modelo:** ChatGPT-6 Luna
<br>
<br>
**Data da execução:** 03/11/2026
<br>
<br>
**Base:** 12 chamados de atendimento, sendo 8 encerrados e 4 em aberto com tempo
vazio. Base sintética, idêntica nos dois prompts.
<br>
<br>
**Variável alterada:** estrutura do prompt. O que falhou tem apenas o pedido; o
corrigido declara regras de cálculo, formato de saída e restrições. Modelo, base
e tarefa constantes.
<br>
<br>

## Problema e quando usar

Base de chamados quase nunca vem completa. Parte dos registros não foi encerrada
e o campo de tempo vem vazio. Calcular média sobre o total joga o resultado para
baixo, e ninguém percebe porque o número parece plausível.

Uso este prompt quando preciso de indicadores de atendimento a partir de base
com registro em aberto, e preciso que o número seja conferível por outra pessoa.

<br>

## Entrada e saída esperadas

Entrada: uma linha por chamado, com identificador, data de abertura, data de
encerramento, tempo de resolução em horas e marcação de reabertura. O período
analisado vem declarado junto à base.

Saída: tabela de indicadores com valor, numerador e denominador; lista dos
chamados em aberto; limitações da análise; e a diferença entre média e mediana.

<br>

## O prompt que falhou

    Analise os dados abaixo e me diga como está o desempenho do atendimento.

    Período analisado: 01/02/2026 a 12/02/2026

    chamado | abertura | encerramento | tempo_resolucao_h | reaberto
    CH-001 | 02/02/2026 | 02/02/2026 | 4 | N
    CH-002 | 02/02/2026 | 03/02/2026 | 24 | N
    CH-003 | 03/02/2026 | 03/02/2026 | 6 | S
    CH-004 | 04/02/2026 | 06/02/2026 | 48 | N
    CH-005 | 05/02/2026 | 05/02/2026 | 3 | N
    CH-006 | 06/02/2026 | 09/02/2026 | 72 | S
    CH-007 | 09/02/2026 | 09/02/2026 | 5 | N
    CH-008 | 10/02/2026 | 10/02/2026 | 8 | S
    CH-009 | 11/02/2026 | - | - | N
    CH-010 | 11/02/2026 | - | - | S
    CH-011 | 12/02/2026 | - | - | N
    CH-012 | 12/02/2026 | - | - | N

<br>

## Saída do prompt que falhou

    Desempenho do atendimento

    O quadro é misto: a maioria dos chamados foi encerrada, mas há sinais de
    demora em alguns casos e uma taxa relevante de reabertura.

    • 12 chamados foram abertos no período; 8 foram encerrados até o fim da base
      e 4 permaneciam abertos.
    • Entre os encerrados, o tempo médio de resolução foi de 21,25 horas e a
      mediana, 7 horas. A média é puxada para cima por dois chamados que levaram
      48 e 72 horas.
    • 6 dos 8 encerrados foram resolvidos em até 24 horas; 2 levaram mais de 24
      horas.
    • 3 dos 8 encerrados têm indicação de reabertura, ou 37,5%. Há ainda um
      chamado aberto marcado como reaberto, então são 4 registros com "S" no
      total.

    Leitura geral: a mediana de 7 horas sugere que muitos casos foram tratados
    rapidamente, mas a média e os chamados de 48 e 72 horas apontam uma cauda de
    atendimentos mais lentos. A taxa de reabertura também merece atenção, pois
    pode indicar que parte das soluções não se sustentou. Como não foi informado
    um SLA ou uma meta de qualidade, não dá para classificar formalmente o
    desempenho como dentro ou fora do esperado.

    Prioridades: verificar os chamados reabertos para identificar causas
    recorrentes e acompanhar os quatro que ainda estavam abertos no fechamento da
    base, em especial o CH-010, marcado como reaberto.

<br>

## O prompt corrigido

    Você vai calcular indicadores de atendimento a partir de uma base de
    chamados.

    Regras de cálculo:
    - Tempo médio de resolução: considerar apenas chamados encerrados, ou seja,
      com encerramento e tempo preenchidos. Chamado em aberto não entra no
      cálculo e não conta como zero.
    - Informe sempre o numerador e o denominador de cada indicador. Média sem
      denominador não é resultado.
    - Calcule também a mediana do tempo de resolução, além da média.
    - Taxa de reabertura: reabertos dividido pelo total de chamados encerrados.
    - Se o período analisado cortar chamados em andamento, registre isso como
      limitação da análise.

    Formato da saída, nesta ordem:

    1. Tabela: indicador | valor | numerador | denominador
    2. Tabela: chamados que ficaram em aberto, com chamado e data de abertura
    3. Limitações da análise: até três linhas
    4. Divergência entre média e mediana: uma linha

    Regras:
    - Não emita juízo de valor como "bom", "satisfatório" ou "preocupante" sem um
      critério declarado. Se não houver meta na base, diga que não há meta.
    - Não estime valor ausente. Campo vazio é dado faltante, não zero.
    - Não escreva introdução, conclusão nem recomendação de melhoria.

    Período analisado: 01/02/2026 a 12/02/2026

    chamado | abertura | encerramento | tempo_resolucao_h | reaberto
    CH-001 | 02/02/2026 | 02/02/2026 | 4 | N
    CH-002 | 02/02/2026 | 03/02/2026 | 24 | N
    CH-003 | 03/02/2026 | 03/02/2026 | 6 | S
    CH-004 | 04/02/2026 | 06/02/2026 | 48 | N
    CH-005 | 05/02/2026 | 05/02/2026 | 3 | N
    CH-006 | 06/02/2026 | 09/02/2026 | 72 | S
    CH-007 | 09/02/2026 | 09/02/2026 | 5 | N
    CH-008 | 10/02/2026 | 10/02/2026 | 8 | S
    CH-009 | 11/02/2026 | - | - | N
    CH-010 | 11/02/2026 | - | - | S
    CH-011 | 12/02/2026 | - | - | N
    CH-012 | 12/02/2026 | - | - | N

<br>

## Saída do prompt corrigido

    indicador | valor | numerador | denominador
    Tempo médio de resolução (h) | 21,25 h | soma dos tempos de resolução = 170 h | 8 chamados encerrados com encerramento e tempo preenchidos
    Mediana do tempo de resolução (h) | 7 h | soma dos dois valores centrais = 6 h + 8 h = 14 h | 2 valores centrais
    Taxa de reabertura | 37,5% | 3 chamados reabertos entre os encerrados | 8 chamados encerrados

    chamado | data de abertura
    CH-009 | 11/02/2026
    CH-010 | 11/02/2026
    CH-011 | 12/02/2026
    CH-012 | 12/02/2026

    Limitações da análise

    Quatro chamados permaneciam em aberto no fim do período e foram excluídos dos
    cálculos de resolução. Como o período termina em 12/02/2026, chamados ainda em
    andamento nessa data podem ter resolução posterior não capturada. A base não
    informa meta de atendimento.

    Divergência entre média e mediana

    A média (21,25 h) supera a mediana (7 h) em 14,25 h; os tempos mais longos,
    especialmente 48 h e 72 h, elevam a média.

<br>

## Por que está estruturado assim

A regra de excluir chamado em aberto do cálculo é a que evita o erro mais
custoso. Se os quatro registros sem tempo entrassem como zero, a média cairia de
21,25 h para 14,17 h e a operação pareceria 33% mais rápida do que é. Número
errado com aparência plausível é pior que número ausente.

Exigir numerador e denominador em colunas separadas é o que torna a conta
conferível. Na saída do prompt que falhou, o valor 21,25 h aparece correto, mas
quem lê não sabe sobre quantos registros ele foi calculado sem reconstruir a
conta. Aqui o denominador está na mesma linha do indicador.

A mediana ao lado da média existe para expor a cauda. A diferença de 14,25 h
entre as duas não é detalhe estatístico: com média de 21,25 h e mediana de 7 h,
o atendimento típico é rápido e a média está sendo puxada por dois casos. Quem
acompanha só a média vai perseguir um problema que não existe na maioria dos
chamados.

A proibição de juízo de valor sem critério declarado resolve uma tentação do
modelo: transformar dado em avaliação. Sem meta na base, "desempenho
satisfatório" é opinião disfarçada de análise.

A proibição de recomendação fecha o mesmo tipo de vazamento, por outra porta. A
saída do prompt que falhou termina com uma lista de prioridades que não sai de
nenhum dado da base — é o modelo opinando sobre gestão, não sobre os números.

<br>

## Modo de falha conhecido

**Quebra de tabela em volume.** O formato funciona com 12 registros e tende a
degradar em bases de centenas, quando o modelo resume as linhas em prosa no meio
da tabela. Não testei esse limite: a base deste arquivo é pequena demais para
afirmar onde quebra. A hipótese a testar é lote de 25, mesma lógica do arquivo de
classificação.

**Definição da taxa de reabertura é escolha, não fato.** Aqui fixei reabertos
sobre encerrados, que dá 37,5%. Sobre o total de 12, daria 25%. As duas respostas
são defensáveis e produzem números diferentes para a mesma base. Quem lê o
relatório precisa saber qual foi usada, senão compara indicadores incompatíveis
entre meses.

**Reabertura sem contagem.** O campo `reaberto` marca S ou N, não quantas vezes.
Um chamado reaberto três vezes conta igual a um reaberto uma vez. Se a base
tiver essa informação, ela precisa entrar no prompt.

**Média e mediana com n ímpar.** A mediana aqui usa dois valores centrais porque
são 8 registros. Com número ímpar, o cálculo é outro, e modelos erram com
frequência a escolha do elemento central.

**Borda da janela.** Quando o período termina com chamados recém-abertos, a
leitura correta é limitação, não atraso. O prompt vago tratou como pendência
operacional. A regra que corrige isso está no prompt, mas depende de o modelo
olhar a data de abertura — em base maior ele pode não olhar.

<br>

## Conclusão

Neste teste, o prompt estruturado não calculou melhor. Calculou igual, e entregou
em formato que se pode usar.

As duas versões acertaram média (21,25 h), mediana (7 h), taxa de reabertura
(37,5%) e denominador. O modelo vago inclusive declarou que não havia meta na
base para julgar o desempenho, o que eu não esperava. A diferença ficou em três
pontos: saída em tabela com numerador e denominador, leitura correta da borda da
janela como limitação, e ausência de recomendação não pedida.

A regra geral que fica: estrutura de prompt não serve só para corrigir erro do
modelo. Serve para definir o formato do artefato. Quando a análise vai ser lida
por outra pessoa ou comparada com outro período, o formato é metade do
resultado — e é a metade que o pedido vago não controla.

Um sinal prático de que a análise está pronta para circular: cada número tem
denominador na mesma linha, e cada definição controversa está declarada. Se falta
uma das duas, o número vai ser interpretado de formas diferentes por leitores
diferentes.
