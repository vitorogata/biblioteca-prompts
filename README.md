# Biblioteca de testes de prompts

Prompts que uso no trabalho, documentados com a decisão por trás e
com o modo de falha conhecido de cada um.

Não é uma lista de comandos prontos. Cada entrada existe porque resolveu um
problema real, e registra também o que não funcionou.

## O que considero um prompt bem estruturado

Cinco coisas, nesta ordem de importância:

- **Contexto explícito**: o modelo sabe quem é o leitor, qual é o material de
  entrada e qual é o limite de atuação.
- **Tarefa única**: um prompt resolve um problema. Quando preciso de duas
  coisas, faço duas chamadas.
- **Formato de saída definido**: quantidade, estrutura e extensão são
  declaradas, não deixadas a critério do modelo.
- **Critério de julgamento**: digo o que torna uma resposta boa e o que a
  torna inaceitável, em vez de pedir "a melhor resposta".
- **Restrição negativa**: incluo o que o modelo não deve fazer, porque é ali
  que a maioria dos erros aparece.

## Os cinco campos de cada entrada

Toda entrada da biblioteca segue o mesmo formato:

1. **Problema e quando usar**: o que a entrada resolve e em que situação ela
   faz sentido.
2. **Entrada e saída esperada**: o que o prompt recebe e qual formato devolve.
3. **Por que está estruturado assim**: a decisão por trás de cada bloco do
   prompt.
4. **Modo de falha conhecido**: o que faz essa entrada produzir resultado ruim,
   e como perceber isso rápido.
5. **Versão anterior que não funcionou**: quando existe, o que tentei antes e
   por que abandonei.

O quarto e o quinto campos são o motivo desta biblioteca existir. Prompt que
funcionou uma vez qualquer pessoa publica. O que quebrou ele é registro de quem
testou.

## Índice

### Análise
- [Classificar divergência em conciliação](analise/classificar-divergencia.md)

### Escrita
- [Revisar texto](escrita/revisar-texto.md)

### Código
- [Revisar script antes de publicar](codigo/revisar-script.md)

## O que entra e o que não entra

Entra: prompt que usei em trabalho real, com o raciocínio documentado.

Não entra: prompt que só funciona citando nome de sistema interno, trecho de
base real ou dado de cliente. Se depende desse contexto, ele não é publicável
aqui, mesmo que seja o melhor prompt que eu tenho.

## Convenção de nomes

Pastas por área de uso (`analise`, `escrita`, `codigo`), um arquivo por prompt,
nome em minúsculas com hífen. Sem acento no nome do arquivo, porque ele vira
parte da URL.

## Origem dos prompts

Todos foram escritos para resolver tarefas de análise de processos,
documentação e revisão de código em ambiente corporativo. Os exemplos dentro
das entradas usam dados fictícios.
