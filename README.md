# Biblioteca de testes de prompts

Prompts que uso no trabalho, documentados com a decisão por trás e com o modo
de falha conhecido de cada um.

Não é uma lista de comandos prontos. Cada arquivo registra um teste: o prompt
que falhou, o que ele devolveu, o prompt corrigido e o que ele devolveu. Quem
lê vê a relação entre a decisão de escrita e a qualidade da saída.

<br>

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

<br>

## Os dez campos de cada arquivo

Todo arquivo desta biblioteca segue essa mesma estrutura.

1. **Identificação do teste**: modelo e versão, data da última execução, base
   usada e a variável que foi alterada entre as duas versões do prompt.
2. **Problema e quando usar**: o que resolve e em que situação faz sentido.
3. **Entrada e saída esperadas**: o que o prompt recebe e o formato que
   deveria devolver.
4. **O prompt que falhou**: texto literal da versão abandonada.
5. **Saída do prompt que falhou**: transcrição do que ele devolveu.
6. **O prompt corrigido**: texto literal da versão atual, para copiar.
7. **Saída do prompt corrigido**: transcrição do que ele devolveu.
8. **Por que ficou estruturado assim**: a decisão por trás de cada bloco.
9. **Modo de falha conhecido**: onde ainda quebra, como perceber, com trecho.
10. **Conclusão**: a regra geral que vale para outros prompts.

<br>

## Índice

### Prompt de análise de dados

- [Classificar divergência em conciliação](https://github.com/vitorogata/biblioteca-testes-prompts/blob/main/analise/classificar-divergencia.md)

### Prompt de revisão de texto

- [Revisar texto](https://github.com/vitorogata/biblioteca-testes-prompts/blob/main/escrita/revisar-texto.md)

### Prompt de revisão de código

- [Revisar script antes de publicar](https://github.com/vitorogata/biblioteca-testes-prompts/blob/main/codigo/revisar-script.md)

<br>

## Origem dos prompts

Todos foram escritos para resolver tarefas de análise de processos,
documentação e revisão de código em ambiente corporativo. Os exemplos dentro
dos arquivos usam dados fictícios.
