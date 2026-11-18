# Revisar texto

## Identificação do teste
## Problema e quando usar

Peço revisão para IA e recebo um texto melhor escrito que não parece meu:
frases mais longas, vocabulário mais formal, tudo com o mesmo ritmo. Serve
para texto genérico, não para currículo nem para mensagem que eu assino.

Uso este prompt quando o texto precisa melhorar sem perder a característica
que faz ele parecer escrito por uma pessoa.

## Entrada e saída esperadas

Entrada: o texto e o contexto de uso, como currículo, mensagem ou
documentação técnica.

Saída: o texto revisado, seguido de uma lista curta do que mudou e por quê,
com o trecho original ao lado.

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

    Minha trajetória na UFABC começou com interesse em projetos mecânicos, mas, ao longo 
    do curso de Engenharia de Gestão, descobri que me identificava mais com processos e dados.
    Hoje, trabalho com análise de processos, documentação e conciliação de dados com Python.
    Gosto de organizar processos complexos e transformá-los em rotinas claras, documentadas e 
    replicáveis, para que outras pessoas consigam executá-las com autonomia. Aprendi Python 
    de forma autodidata, resolvendo demandas reais do trabalho e desenvolvendo scripts 
    para problemas concretos.

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

    Entrei na UFABC pensando em projeto mecânico e saí interessado em processo. No meio do curso de Engenharia de Gestão, comecei a gostar mais de organizar fluxo e dado do que de desenhar peça. Hoje, é isso que faço: análise de processos, documentação e, mais recentemente, conciliação de dados com Python. Gosto de pegar processo bagunçado e deixar ele com regra escrita, de um jeito que a próxima pessoa consiga repetir sem me chamar. Aprendi Python sozinho, na maior parte das vezes resolvendo problemas que apareceram no trabalho. Não tenho certificação nenhuma de programação. O que eu tenho é script que roda.

    • Original: “No meio do curso de Engenharia de Gestão comecei...”
     Mudou: Acrescentei uma vírgula após “Gestão”.
     Motivo: Separar a expressão inicial e facilitar a leitura.
    • Original: “..., e hoje é isso que eu faço:”
     Mudou: Separei em duas frases: “... de desenhar peça. Hoje, é isso que faço:”
     Motivo: Deixar a frase mais direta e curta.
    • Original: “do jeito que a próxima pessoa consegue repetir”
     Mudou: “de um jeito que a próxima pessoa consiga repetir”
     Motivo: Ajustar a construção sem mudar a ideia.
    • Original: “na maior parte resolvendo problema que apareceu no trabalho”
     Mudou: “na maior parte das vezes resolvendo problemas que apareceram no trabalho”
     Motivo: Ajustar a expressão e a concordância.
    • Original: “Não tenho certificação nenhuma de programação, o que eu tenho é script que roda.”
     Mudou: Dividi em duas frases.
     Motivo: Evitar a junção de duas orações independentes e preservar o fechamento enfático.

## Por que está estruturado assim

A regra de não acrescentar informação é a que evita o problema mais comum, que
é o modelo inventar qualificação ou resultado para deixar a frase mais forte.
Em currículo isso é grave, porque vira afirmação falsa em documento que você
assina.

Pedir a lista de mudanças com o original ao lado transforma a revisão em algo
auditável. Eu leio a lista antes do texto e descarto a alteração que não
concordo. Sem essa lista, aceito o texto inteiro sem saber o que mudou.

A instrução de manter o tamanho aproximado existe porque sem ela o modelo
sempre expande. Texto revisado maior não é texto melhor.

## Modo de falha conhecido

Em texto muito curto, como uma linha de bio, ele ignora a regra de tamanho e
reescreve tudo. Nesse caso vale pedir versão única em vez de revisão.

Quando o texto já está bom, ele mexe só para justificar a tarefa. Se a lista
de mudanças vier com itens triviais do tipo "troquei por um sinônimo", é sinal
de que o original estava pronto.

## Conclusão

A primeira versão dizia "melhore este texto". Ela devolvia versão mais formal,
mais longa e com adjetivo que eu não tinha escrito. O que faltou foi a
restrição de não acrescentar informação e o pedido de auditoria das mudanças.
