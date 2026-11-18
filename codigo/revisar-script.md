# Revisar script antes de publicar

## Identificação do teste

**Modelo:** ChatGPT-6 Luna
<br>
<br>
**Data da execução:** 03/11/2026
<br>
<br>
**Base:** script Python de 36 linhas que calcula parcelas com taxa, mais três contratos de exemplo. Idêntico nos dois prompts.
<br>
<br>
**Variável alterada:** estrutura do prompt. O que falhou tem apenas o pedido; o corrigido declara o sintoma, a ordem de verificação, o formato da resposta e três restrições. Modelo, código e dados constantes.
<br>
<br>
## Problema e quando usar

Script que roda na minha máquina e não roda na de outra pessoa. Caminho absoluto, codificação fixa, dependência que não existe no ambiente do outro. E script que roda mas entrega resultado errado sem avisar.

Uso este prompt antes de publicar qualquer script em repositório público, quando preciso de diagnóstico localizado em linha e não de reescrita.

<br>

## Entrada e saída esperadas

Entrada: o código com numeração de linha, o sintoma observado e os dados de exemplo que reproduzem o problema.

Saída: para cada problema, número da linha, o que acontece e a correção mínima. Para o erro de cálculo, um trecho de até cinco linhas. Ao final, a contagem de quantos casos de exemplo fecham e quantos não fecham.

<br>

## O prompt que falhou

    Dá uma olhada nesse código Python e me diz se tem algo errado. Se tiver, corrige.

     1  import csv
     2
     3  TAXA = 0.0299
     4  CAMINHO = r"C:\Users\hidek\Documentos\conciliacao-estornos\entrada\contratos.csv"
     5
     6
     7  def calcular_parcelas(valor, meses):
     8      valor_com_taxa = valor * (1 + TAXA)
     9      parcela = round(valor_com_taxa / meses, 2)
    10      return [parcela] * meses
    11
    12
    13  def gerar_relatorio(caminho):
    14      linhas = []
    15      with open(caminho, encoding="latin-1") as arquivo:
    16          leitor = csv.DictReader(arquivo, delimiter=";")
    17          for row in leitor:
    18              valor = float(row["valor"])
    19              meses = int(row["meses"])
    20              parcelas = calcular_parcelas(valor, meses)
    21              linhas.append({
    22                  "contrato": row["contrato"],
    23                  "parcela": parcelas[0],
    24                  "total_calculado": sum(parcelas),
    25                  "total_esperado": round(valor * (1 + TAXA), 2),
    26              })
    27      return linhas
    28
    29
    30  def main():
    31      for linha in gerar_relatorio(CAMINHO):
    32          print(linha)
    33
    34
    35  if __name__ == "__main__":
    36      main()

    Dados de exemplo (contratos.csv, separador ponto e vírgula):

    contrato;valor;meses
    C-001;1000.00;7
    C-002;500.00;3
    C-003;1500.00;7

<br>

## Saída do prompt que falhou

    O principal problema é que round() arredonda cada parcela separadamente. Assim, a soma das parcelas pode não bater com o total esperado. Além disso, float não é adequado para cálculos monetários, e meses = 0 causa divisão por zero.

    A versão abaixo usa Decimal e ajusta a última parcela para que a soma feche exatamente:

    import csv
    from decimal import Decimal, ROUND_HALF_UP

    TAXA = Decimal("0.0299")
    CENTAVO = Decimal("0.01")
    CAMINHO = r"C:\Users\hidek\Documentos\conciliacao-estornos\entrada\contratos.csv"


    def calcular_total(valor):
        return (valor * (1 + TAXA)).quantize(
            CENTAVO,
            rounding=ROUND_HALF_UP,
        )


    def calcular_parcelas(valor, meses):
        if meses <= 0:
            raise ValueError("'meses' deve ser maior que zero.")

        total = calcular_total(valor)
        parcela_base = (total / meses).quantize(
            CENTAVO,
            rounding=ROUND_HALF_UP,
        )

        parcelas = [parcela_base] * (meses - 1)
        ultima_parcela = total - sum(parcelas, Decimal("0.00"))
        parcelas.append(ultima_parcela)

        return parcelas


    def gerar_relatorio(caminho):
        linhas = []

        with open(caminho, encoding="latin-1", newline="") as arquivo:
            leitor = csv.DictReader(arquivo, delimiter=";")

            for numero_linha, row in enumerate(leitor, start=2):
                try:
                    valor = Decimal(row["valor"].strip())
                    meses = int(row["meses"].strip())
                except (KeyError, AttributeError, ValueError) as erro:
                    raise ValueError(
                        f"Dados inválidos na linha {numero_linha} do CSV."
                    ) from erro

                parcelas = calcular_parcelas(valor, meses)
                total_esperado = calcular_total(valor)

                linhas.append({
                    "contrato": row["contrato"],
                    "parcela": parcelas[0],
                    "parcelas": parcelas,
                    "total_calculado": sum(parcelas, Decimal("0.00")),
                    "total_esperado": total_esperado,
                })

        return linhas


    def main():
        for linha in gerar_relatorio(CAMINHO):
            print(linha)


    if __name__ == "__main__":
        main()

    Com os dados de exemplo, os totais fecham em 1029,90, 514,95 e 1544,85. A última parcela pode diferir alguns centavos das anteriores para compensar o arredondamento.

<br>

## O prompt corrigido

    Você vai revisar um script Python que roda na máquina do autor mas vai para um
    repositório público, e que apresenta um erro de cálculo.

    Sintoma observado: em alguns contratos, a soma das parcelas não fecha com o
    valor total com taxa. Em outros, fecha.

    Verifique, nesta ordem:

    1. Causa do erro de cálculo: aponte a linha exata e explique por que o total
       não fecha.
    2. Erro que impede outra pessoa de rodar: caminho absoluto da máquina do autor,
       dependência não declarada, codificação fixa, comando que só funciona em um
       sistema operacional.
    3. Erro silencioso: ponto em que o script continua sem avisar que o resultado
       está inconsistente.

    Formato da resposta:

    - Para cada problema: número da linha, o que acontece, correção mínima.
    - Para o item 1, escreva a correção como trecho de até cinco linhas. Não
      entregue o arquivo completo.
    - Ao final, uma linha informando quantos dos três contratos de exemplo fecham
      e quantos não fecham.

    Regras:

    - Não reescreva o arquivo inteiro.
    - Não introduza biblioteca nova nem altere a estrutura de pastas.
    - Não comente estilo que não afete os três itens acima.
    - Os números à esquerda são só referência de linha. Não os inclua no código
      corrigido.

    Arquivo:

     1  import csv
     2
     3  TAXA = 0.0299
     4  CAMINHO = r"C:\Users\hidek\Documentos\conciliacao-estornos\entrada\contratos.csv"
     5
     6
     7  def calcular_parcelas(valor, meses):
     8      valor_com_taxa = valor * (1 + TAXA)
     9      parcela = round(valor_com_taxa / meses, 2)
    10      return [parcela] * meses
    11
    12
    13  def gerar_relatorio(caminho):
    14      linhas = []
    15      with open(caminho, encoding="latin-1") as arquivo:
    16          leitor = csv.DictReader(arquivo, delimiter=";")
    17          for row in leitor:
    18              valor = float(row["valor"])
    19              meses = int(row["meses"])
    20              parcelas = calcular_parcelas(valor, meses)
    21              linhas.append({
    22                  "contrato": row["contrato"],
    23                  "parcela": parcelas[0],
    24                  "total_calculado": sum(parcelas),
    25                  "total_esperado": round(valor * (1 + TAXA), 2),
    26              })
    27      return linhas
    28
    29
    30  def main():
    31      for linha in gerar_relatorio(CAMINHO):
    32          print(linha)
    33
    34
    35  if __name__ == "__main__":
    36      main()

    Dados de exemplo (contratos.csv, separador ponto e vírgula):

    contrato;valor;meses
    C-001;1000.00;7
    C-002;500.00;3
    C-003;1500.00;7

<br>

## Saída do prompt corrigido

    1. Causa do erro de cálculo

    • Linha 9: arredonda cada parcela para duas casas e a linha 10 repete esse
      valor. Os centavos que sobram ou faltam não são distribuídos; por isso, a
      soma pode diferir do total esperado.
    • Correção mínima, substituindo as linhas 8–10:

        total_centavos = int(round(round(valor * (1 + TAXA), 2) * 100))
        base, resto = divmod(total_centavos, meses)
        return [(base + (i < resto)) / 100 for i in range(meses)]

    2. Problemas que podem impedir outra pessoa de rodar

    • Linha 4: o caminho aponta para uma pasta específica no computador do autor.
      Em outra máquina, esse arquivo provavelmente não existe. Correção mínima:
      usar um caminho relativo, como "entrada/contratos.csv", executando o script
      a partir da raiz do repositório.
    • Linha 15: fixa a codificação como latin-1. Se o CSV estiver em UTF-8 e tiver
      caracteres fora de ASCII, a leitura pode falhar ou interpretar o texto
      incorretamente. Correção mínima: configurar a codificação de acordo com a
      codificação real do arquivo e documentá-la.
    • Dependências e sistema operacional: não há dependência externa não
      declarada, pois csv faz parte da biblioteca padrão do Python. O trecho
      também não contém comando específico de um sistema operacional.

    3. Erro silencioso

    • Linha 32: imprime os totais, mas não compara os valores nem avisa quando
      divergem. Assim, a inconsistência aparece apenas se alguém notar a
      diferença. Correção mínima: antes de imprimir, comparar os totais
      arredondados a duas casas e emitir um aviso quando forem diferentes.

    Dos três contratos de exemplo, 1 fecha e 2 não fecham.

<br>

## Por que ficou estruturado assim

A ordem importa mais que o conteúdo. Dado sensível em repositório público não tem desfazer, e o caminho absoluto da linha 4 é o caso que não dava para consertar depois de commitado. Ele aparece no item 2, não no fim.

Declarar o sintoma antes do código é o que separa diagnóstico de revisão genérica. "Em alguns contratos a soma não fecha, em outros fecha" aponta para arredondamento, não para estrutura. O prompt vago, sem sintoma, reescreveu o arquivo inteiro e não disse qual linha causava a inconsistência.

A instrução de não reescrever o arquivo inteiro existe porque o modelo tende a devolver a versão completa. Isso esconde o que mudou e não é aplicável quando o arquivo já está em produção. Limitar a correção a cinco linhas força a localização do defeito.

A restrição "não comente estilo que não afete os três itens" tem um custo, e ele apareceu no resultado: o prompt corrigido deixou de apontar a divisão por zero em `meses = 0` e a inadequação de `float` para dinheiro, que o prompt vago havia pego. A restrição compra aplicabilidade e paga em completude.

A exigência da contagem final transforma a revisão em algo conferível. Sem ela, "a soma não fecha" é afirmação. Com ela, é resultado que se verifica na mão.

<br>

## Modo de falha conhecido

**Restrição de escopo omite defeito real.** O item 3 limita a revisão a três categorias. Problema fora delas não aparece: neste teste, divisão por zero em `meses = 0` e uso de `float` para dinheiro ficaram de fora, embora o prompt vago os tenha encontrado. Se o script for para produção, vale uma segunda passada sem restrição de escopo.

**A correção não é única.** As duas versões jogam o resíduo em parcelas diferentes. Em C-001 os dois chegam ao mesmo resultado: seis parcelas de 147,13 e uma de 147,12. Em C-003 divergem. O prompt vago faz seis de 220,69 e uma de 220,71; o corrigido faz duas de 220,70 e cinco de 220,69. As duas somas fecham 1544,85, mas o cliente paga valores diferentes mês a mês. Nenhum dos dois declarou que a distribuição do resíduo é uma escolha.

**Soma ainda em float.** A correção devolve `(base + (i < resto)) / 100`, que é float. Dependendo da máquina, o campo `total_calculado` pode voltar a exibir resíduo de 1e-13. Não afeta o negócio, mas mantém a origem do problema para quem precisa de exatidão contábil.

**Degradação em arquivo longo.** Não testado aqui: o arquivo tem 36 linhas. A hipótese é que acima de 200 linhas o modelo ignore o fim do arquivo. É a mesma lógica do lote de 25 no arquivo de classificação, e está sem evidência.

**Número de linha inventado.** Se o código for colado sem numeração, o modelo tende a estimar a linha. Neste teste a numeração estava presente e as cinco referências foram corretas. O risco permanece para código sem números.

<br>

## Conclusão

Estrutura de prompt não melhorou o diagnóstico. Melhorou o que dava para aplicar.

As duas versões encontraram o bug. O prompt vago achou até mais: divisão por zero e `float` para dinheiro. Mas entregou o arquivo reescrito inteiro, sem citar linha, e manteve o caminho absoluto da máquina do autor, que é o único item sem desfazer depois do commit. O corrigido apontou cinco linhas, entregou três linhas de correção, e a correção soma exatamente 1029,90, 514,95 e 1544,85.

Este é o quarto teste seguido em que o prompt vago é tecnicamente competente. A diferença entre os dois nunca está na capacidade de analisar. Está no que sai do outro lado: prompt vago entrega análise, prompt estruturado entrega patch.

A regra geral que fica: ao restringir escopo num prompt de revisão, declare o que fica de fora. A restrição que comprou aplicabilidade aqui custou dois defeitos reais. Um segundo prompt sem restrição, rodado depois, cobre o que o primeiro deixou passar.

E um sinal prático de que a revisão está pronta para uso: cada problema tem número de linha, cada correção cabe em menos linhas que o problema original, e existe uma frase no fim que você consegue conferir na mão.
