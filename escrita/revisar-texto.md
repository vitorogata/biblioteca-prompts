# Revisar texto

## Identificação do teste

**Modelo:** ChatGPT-6 Luna
<br>
**Data da execução:** 03/11/2026
<br>
**Base:** um texto de 101 palavras (resumo de perfil no LinkedIn), idêntico nos dois prompts
<br>
**Variável alterada:** estrutura do prompt. O que falhou tem apenas o pedido; o corrigido tem cinco regras e a exigência de lista de mudanças. Modelo, texto e tarefa constantes.

## Problema e quando usar

Peço revisão para IA e recebo um texto melhor escrito que não parece meu: frases
mais longas, vocabulário mais formal, tudo com o mesmo ritmo. Serve para texto
genérico, não para currículo nem para mensagem que eu assino.

Uso este prompt quando o texto precisa melhorar sem perder a característica que
faz ele parecer escrito por uma pessoa.

## Entrada e saída esperadas

Entrada: o texto e o contexto de uso, como currículo, mensagem ou documentação
técnica.

Saída: o texto revisado, seguido de uma lista curta do que mudou e por quê, com o
trecho original ao lado.

## O prompt que falhou

    Melhore este texto para o resumo do meu perfil no LinkedIn.

    Texto:
    Entrei na UFABC pensando em projeto mecânico e saí interessado em processo. No
    meio do curso de Engenharia de Gestão comecei a gostar mais de organizar fluxo e
    dado do que de desenhar peça, e hoje é isso que eu faço: análise de processos,
    documentação e, mais recentemente, conciliação de dados com Python. Gosto de
    pegar processo bagunçado e deixar ele com regra escrita, do jeito que a próxima
    pessoa consegue repetir sem me chamar. Aprendi Python sozinho, na maior parte
    resolvendo problema que apareceu no trabalho. Não tenho certificação nenhuma de
    programação, o que eu tenho é script que roda.

## Saída do prompt que falhou

    Minha trajetória na UFABC começou com interesse em projetos mecânicos, mas, ao
    longo do curso de Engenharia de Gestão, descobri que me identificava mais com
    processos e dados. Hoje, trabalho com análise de processos, documentação e
    conciliação de dados com Python. Gosto de organizar processos complexos e
    transformá-los em rotinas claras, documentadas e replicáveis, para que outras
    pessoas consigam executá-las com autonomia. Aprendi Python de forma autodidata,
    resolvendo demandas reais do trabalho e desenvolvendo scripts para problemas
    concretos.

## O prompt corrigido

    Revise o texto abaixo para o resumo do meu perfil no LinkedIn.

    Regras:
    - Mantenha o tamanho aproximado. Se precisar cortar, corte redundância,
      não informação.
    - Mantenha as palavras que já são específicas do autor, mesmo que exista
      sinônimo mais elegante.
    - Não acrescente informação que não está no texto.
    - Não introduza metáfora, imagem ou opinião.
    - Frases curtas são aceitáveis. Não alongue para soar mais formal.

    Depois do texto revisado, liste em até cinco itens: o trecho original, o
    que mudou e o motivo.

    Texto:
    Entrei na UFABC pensando em projeto mecânico e saí interessado em processo. No
    meio do curso de Engenharia de Gestão comecei a gostar mais de organizar fluxo e
    dado do que de desenhar peça, e hoje é isso que eu faço: análise de processos,
    documentação e, mais recentemente, conciliação de dados com Python. Gosto de
    pegar processo bagunçado e deixar ele com regra escrita, do jeito que a próxima
    pessoa consegue repetir sem me chamar. Aprendi Python sozinho, na maior parte
    resolvendo problema que apareceu no trabalho. Não tenho certificação nenhuma de
    programação, o que eu tenho é script que roda.

## Saída do prompt corrigido

    Entrei na UFABC pensando em projeto mecânico e saí interessado em processo. No
    meio do curso de Engenharia de Gestão, comecei a gostar mais de organizar fluxo
    e dado do que de desenhar peça. Hoje, é isso que faço: análise de processos,
    documentação e, mais recentemente, conciliação de dados com Python. Gosto de
    pegar processo bagunçado e deixar ele com regra escrita, de um jeito que a
    próxima pessoa consiga repetir sem me chamar. Aprendi Python sozinho, na maior
    parte das vezes resolvendo problemas que apareceram no trabalho. Não tenho
    certificação nenhuma de programação. O que eu tenho é script que roda.

    • Original: "No meio do curso de Engenharia de Gestão comecei..."
      Mudou: acrescentei uma vírgula após "Gestão".
      Motivo: separar a expressão inicial e facilitar a leitura.
    • Original: "..., e hoje é isso que eu faço:"
      Mudou: separei em duas frases: "... de desenhar peça. Hoje, é isso que faço:"
      Motivo: deixar a frase mais direta e curta.
    • Original: "do jeito que a próxima pessoa consegue repetir"
      Mudou: "de um jeito que a próxima pessoa consiga repetir"
      Motivo: ajustar a construção sem mudar a ideia.
    • Original: "na maior parte resolvendo problema que apareceu no trabalho"
      Mudou: "na maior parte das vezes resolvendo problemas que apareceram no trabalho"
      Motivo: ajustar a expressão e a concordância.
    • Original: "Não tenho certificação nenhuma de programação, o que eu tenho é script que roda."
      Mudou: dividi em duas frases.
      Motivo: evitar a junção de duas orações independentes e preservar o fechamento enfático.

## Por que ficou estruturado assim

As cinco regras entraram juntas, então este teste não isola qual delas agiu. O que
ele permite afirmar é quais regras teriam bloqueado o que aconteceu.

A regra de manter o tamanho aproximado teria bloqueado o corte: o resultado do
pedido vago ficou com 78 palavras contra 101 do original, e perdeu uma frase
inteira. A regra de manter as palavras específicas do autor teria bloqueado a
troca de vocabulário: "bagunçado" virou "complexos", "sozinho" virou "de forma
autodidata", "sem me chamar" virou "com autonomia".

A regra de não acrescentar informação não foi a decisiva neste teste. O modelo não
inventou número, credencial nem resultado. Ele acrescentou adjetivo avaliativo —
"processos complexos", "demandas reais", "rotinas claras, documentadas e
replicáveis" —, mas nenhuma afirmação factual nova. O erro principal foi por
subtração, não por adição.

Pedir a lista de mudanças com o original ao lado transforma a revisão em algo
auditável. Eu leio a lista antes do texto e descarto a alteração que não concordo.
Sem essa lista, aceito o texto inteiro sem saber o que mudou.

A instrução de manter o tamanho aproximado existe porque, sem ela, o modelo trata
"melhorar" como "reescrever". Neste teste ele reescreveu para menos.

## Modo de falha conhecido

**Remoção da frase de assinatura.** Sem instrução de preservação, o modelo apaga a
frase que mais identifica o autor. Neste teste desapareceu "Não tenho certificação
nenhuma de programação, o que eu tenho é script que roda", e o parágrafo final
perdeu o fecho de personalidade. Como perceber rápido: conte as frases do original
e do resultado. Se o resultado tem menos frases, houve corte.

**Troca do concreto pelo abstrato.** O modelo substitui o detalhe verificável por
categoria genérica: "problema que apareceu no trabalho" virou "demandas reais do
trabalho", "processo bagunçado" virou "processos complexos". Nenhuma palavra é
falsa, mas o texto deixa de dizer algo específico. Como perceber: procure no
resultado as palavras concretas do original. As que desapareceram são o
diagnóstico.

**Adjetivo avaliativo sem fato novo.** "Complexos", "reais", "replicáveis" soam
como qualificação profissional, mas não correspondem a nada que o autor escreveu.
Em currículo isso é o começo de uma afirmação que ele não pode sustentar em
entrevista.

**Reescrita em texto muito curto.** Em uma linha de bio, ele ignora a regra de
tamanho e reescreve tudo. Nesse caso vale pedir versão única em vez de revisão.

**Mexer só para justificar a tarefa.** Quando o texto já está bom, ele altera para
ter o que listar. Se a lista de mudanças vier com itens triviais, é sinal de que o
original estava pronto. Foi o que aconteceu na saída do prompt corrigido: as cinco
alterações são pontuação e concordância, nenhuma de conteúdo, e o texto final tem
102 palavras contra 101 do original.

## Conclusão

Pedido vago não gera texto mais longo. Gera texto mais genérico.

A versão anterior deste arquivo afirmava o contrário, porque eu esperava inflação
de adjetivo. O teste mostrou outro movimento: o texto encolheu de 101 para 78
palavras (22,8% a menos), o concreto virou abstrato e a frase de assinatura foi
apagada. O modelo não exagerou, ele diluiu.

A regra geral que fica: ao pedir revisão, a restrição mais importante não é sobre
o que o modelo não deve acrescentar, e sim sobre o que ele não pode retirar.
Palavra específica, frase curta e construção informal são decisões do autor, não
descuidos de escrita, e é sobre elas que o modelo age primeiro.

Um sinal prático de que a revisão funcionou: a lista de mudanças descreve
pontuação, não conteúdo. Se ela descreve substituição de vocabulário, o modelo
mexeu onde não devia.
