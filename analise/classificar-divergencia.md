# Classificar divergência em conciliação

## Problema e quando usar

A conciliação aponta que um estorno não foi aplicado, mas o motivo só aparece
quando alguém abre o caso e compara o extrato linha por linha. Em lote de 300
registros isso não cabe na rotina.

Uso este prompt quando já tenho o status de cada registro e preciso de uma
classificação preliminar de motivo antes da análise manual.

## Entrada e saída esperada

Entrada: uma linha por registro, com CPF mascarado, valor da parcela, status
da conciliação e valor encontrado no extrato.

Saída: para cada registro, uma categoria entre quatro e uma justificativa de
uma linha citando o dado que sustenta a escolha.

## O prompt

    Você vai classificar divergências de conciliação de estornos.

    Categorias permitidas, sem criar outras:
    - VALOR_DIVERGENTE: existe estorno registrado, com valor diferente do devido
    - SEM_CREDITO: o cliente não tem nenhum crédito no período
    - DEBITO_NO_LUGAR: existe lançamento de mesmo valor, mas é débito
    - FORA_DO_PERIODO: o crédito existe, mas em data fora da janela analisada

    Para cada registro, responda em uma linha:
    CPF | categoria | justificativa de até 20 palavras

    Regras:
    - Escolha exatamente uma categoria da lista.
    - A justificativa deve citar o dado concreto do registro.
    - Se nenhuma categoria servir, escreva REVISAR_MANUAL e diga qual
      informação está faltando.
    - Não escreva introdução, conclusão nem comentário geral.

## Por que está estruturado assim

A lista fechada de categorias é o que impede o modelo de inventar motivo
plausível mas inútil para a operação. Categoria inventada não entra em
relatório.

A justificativa obrigatória força o modelo a citar o dado, e isso torna o erro
visível na leitura. Quando ele escreve "valor diferente" sem citar os dois
valores, sei que não olhou o registro.

A saída em uma linha por registro com separador fixo permite colar direto em
planilha, sem reformatação.

A saída de escape REVISAR_MANUAL é o campo mais importante do prompt. Sem ela,
o modelo força o encaixe e produz classificação errada com aparência de certa.

## Modo de falha conhecido

Acima de cerca de 40 registros em uma única chamada, a classificação fica
inconsistente: os últimos registros recebem categoria parecida com a dos
primeiros. Dividir em lotes de 25 resolve.

Quando o campo de valor encontrado vem vazio, o modelo tende a inventar
SEM_CREDITO mesmo existindo crédito na base. A instrução de nomear o campo
ausente reduz, mas não elimina. Vale conferir a contagem final.

## Versão anterior que não funcionou

A primeira versão pedia "analise cada caso e diga o que aconteceu". O modelo
devolvia parágrafos explicativos, com motivo diferente para registros
idênticos, e não dava para agregar. O que faltava era a lista fechada de
categorias e o limite de uma linha por registro.
