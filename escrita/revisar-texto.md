# Revisar texto

## Problema e quando usar

Peço revisão para IA e recebo um texto melhor escrito que não parece meu:
frases mais longas, vocabulário mais formal, tudo com o mesmo ritmo. Serve
para texto genérico, não para currículo nem para mensagem que eu assino.

Uso este prompt quando o texto precisa melhorar sem perder a característica
que faz ele parecer escrito por uma pessoa.

## Entrada e saída esperada

Entrada: o texto e o contexto de uso, como currículo, mensagem ou
documentação técnica.

Saída: o texto revisado, seguido de uma lista curta do que mudou e por quê,
com o trecho original ao lado.

## O prompt

    Revise o texto abaixo para [contexto de uso].

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
    [colar]

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

## Versão anterior que não funcionou

A primeira versão dizia "melhore este texto". Ela devolvia versão mais formal,
mais longa e com adjetivo que eu não tinha escrito. O que faltou foi a
restrição de não acrescentar informação e o pedido de auditoria das mudanças.
