# Revisar script antes de publicar

## Problema e quando usar

Script que roda na minha máquina funciona. Antes de publicar no GitHub, quero
saber o que quebra quando outra pessoa roda, o que expõe dado sensível e o que
está escrito de um jeito que eu vou me arrepender em três meses.

Uso antes de cada commit em repositório público.

## Entrada e saída esperada

Entrada: o arquivo, com a informação de que ele vai para repositório público.

Saída: lista de problemas ordenada por gravidade, cada um com a linha e a
correção mínima. Sem reescrita completa do arquivo.

## O prompt

    Revise o código abaixo sabendo que ele vai para um repositório público no
    GitHub.

    Verifique, nesta ordem:
    1. Dado sensível: caminho absoluto da máquina do autor, credencial, nome
       de sistema interno, dado de cliente real.
    2. Erro que impede outra pessoa de rodar: dependência não declarada,
       caminho que não existe, comando que só funciona em um sistema
       operacional.
    3. Erro silencioso: exceção engolida, retorno None não tratado, divisão
       com denominador que pode ser zero.
    4. Legibilidade: nome de variável de uma letra, bloco longo sem função,
       número mágico.

    Para cada problema, informe: linha, o que acontece e a correção mínima.

    Não reescreva o arquivo inteiro. Não comente estilo que não afeta nada
    dos quatro itens acima.

## Por que está estruturado assim

A ordem importa mais que o conteúdo. Problema de dado sensível em repositório
público não tem desfazer, então entra primeiro e sai da discussão estética.

A instrução de não reescrever o arquivo inteiro existe porque o modelo tende a
devolver uma versão completa, que eu não aplico e que esconde o que mudou.
Lista de problemas com linha é aplicável.

O item sobre erro que impede outra pessoa de rodar é o que separa revisão de
estilo de revisão útil. Código que não roda na máquina do outro não é código
publicado, é rascunho.

## Modo de falha conhecido

Ele aponta problema de legibilidade em script que veio de notebook e está
funcionando, o que gera ruído. Se o arquivo for longo, ele ignora o fim. Vale
dividir em partes de até 200 linhas.

Ele também inventa número de linha quando o texto colado não tem numeração.
Conferir a linha antes de aplicar.

## Versão anterior que não funcionou

Pedia "revise este código e sugira melhorias". Recebia reescrita completa com
orientação a objetos, teste, logging e tratamento de erro, tudo em um arquivo
de dez linhas que resolvia o problema. Não era o que eu precisava e não tinha
como aplicar sem reescrever tudo.
