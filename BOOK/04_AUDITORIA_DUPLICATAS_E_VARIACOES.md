# AUDITORIA DE DUPLICATAS E VARIACOES — Para Voce Lembrar

Data: 2026-07-02
Status: primeira auditoria operacional
Base de comparacao: PDF 2026-06-28 + DOCX 2025-03-21/16 + DOCX inicial 2025-03-01 + PDF 2025-04-18

## 1. Principio

Duplicata aparente nao deve ser apagada automaticamente.

Um mesmo titulo pode representar:

- repeticao acidental;
- poema em versao diferente;
- reprise intencional;
- deslocamento de secao;
- titulo semelhante com texto diferente;
- resquicio de indice ou sumario;
- erro de extracao PDF.

A decisao final e de Dante.

## 2. Duplicatas ou repeticoes ja detectadas

### 2.1 `Depois do Amor`

Aparece no livro atual em mais de uma secao:

- Parte 1 — Amor e Relacoes Humanas;
- Parte 5 — Dor, Desilusao e Melancolia.

Classificacao provisoria:

`DUPLICATA_A_CONFIRMAR`

Hipoteses:

1. O poema pode ter sido intencionalmente repetido por servir tanto ao amor quanto a dor.
2. Pode haver duas versoes diferentes.
3. Pode ser duplicacao de sumario.

Acao:

Comparar corpo completo nas fontes antes de decidir.

### 2.2 `O Ceu, a Lua e o Mar`

Aparece em mais de uma parte:

- Parte 4 — Natureza e Imagetica Sensorial;
- Parte 5 — Dor, Desilusao e Melancolia.

Classificacao provisoria:

`DUPLICATA_A_CONFIRMAR`

Hipoteses:

1. Pode ser poema sensorial com carga melancolica, portanto com dupla pertinencia.
2. Pode haver erro de classificacao.
3. Pode haver repeticao acidental.

Acao:

Comparar texto integral e decidir se fica em uma parte, se aparece como reprise, ou se uma das ocorrencias e apenas referencia.

### 2.3 `Horizonte`

Titulos relacionados detectados:

- `O Horizonte`;
- `Horizonte`;
- `O Horizonte De Papel`;
- `O Que Me Disse O Horizonte`;
- `Depois do Horizonte`.

Classificacao provisoria:

`FAMILIA_TEMATICA_DE_TITULOS`

Nao tratar como duplicata automaticamente.

Acao:

Criar grupo tematico `HORIZONTE` e comparar cada texto.

### 2.4 `O Horizonte De Papel`

Aparece no DOCX organizado em secao 3 e secao 4.

Classificacao provisoria:

`DUPLICATA_DE_INDICE_OU_DESLOCAMENTO`

Acao:

Conferir se o corpo do poema aparece uma ou duas vezes; se apenas no indice, corrigir sumario.

### 2.5 `O Urro Do Silencio`

Aparece na secao amor/relações e tambem listado em dor/desilusao no DOCX organizado.

Classificacao provisoria:

`DUPLICATA_A_CONFIRMAR`

Acao:

Comparar ocorrencias no corpo e no sumario.

### 2.6 `Esquecer Um Amor` / `Esquecer O Amor`

Variação de titulo detectada:

- DOCX 2025: `Esquecer Um Amor`;
- PDF 2026: `Esquecer O Amor`.

Classificacao provisoria:

`VARIACAO_DE_TITULO`

Acao:

Verificar se o texto e o mesmo. Se for, Dante deve decidir titulo canonico.

### 2.7 `Insipido`

Aparece no DOCX organizado em Filosofia/Existencia, mas nao foi detectado no sumario do PDF 2026-06-28 lido inicialmente.

Classificacao provisoria:

`POSSIVEL_POEMA_AUSENTE_NA_VERSAO_ATUAL`

Acao:

Buscar no corpo do PDF 2026 e nas fontes anteriores.

## 3. Poemas possivelmente ausentes do livro atual

Detectados em fontes anteriores e ainda nao confirmados no PDF 2026-06-28:

- `Amores Improvaveis`;
- `Amante`;
- `POEMINHA DO APROVEITANDO A DEIXA`;
- `O Amor e a Esperanca`;
- `O Amor de Um Fantasma`;
- `SEM AMOR`.

Classificacao provisoria:

`ACERVO_A_CONFERIR`

Esses poemas nao devem ser descartados. Podem virar:

- anexos de acervo;
- volume futuro;
- secao extra;
- arquivo relacional de poemas;
- material fora da obra final.

## 4. Sinais de colagem / falha de extração

Detectados principalmente em PDFs:

- titulo colado ao texto anterior;
- fim de poema colado ao titulo seguinte;
- sumario colado a assinatura;
- quebras de linha perdidas;
- ausencia de espaco entre palavras em trechos especificos.

Classificacao provisoria:

`ERRO_TECNICO_DE_EXTRAÇÃO_OU_DIAGRAMACAO`

Acao:

Nao corrigir texto poeticamente ainda. Primeiro restaurar separadores.

## 5. Decisoes pendentes de Dante

1. A repeticao de poemas entre secoes pode ser aceita como escolha artistica?
2. Poemas de acervo anterior devem entrar no livro atual ou ficar preservados para outro volume?
3. A assinatura `Redigido pela I.A. Site GPT` / `Aurora I.A. GPT` deve ficar na versao publica?
4. A versao final deve preservar o nome Aurora dentro da obra como poema, como entidade de curadoria, ou ambos?
5. A frase final aprovada deve ser posfacio, quarta capa ou encerramento do livro?

## 6. Recomendacao PRAXIUM

Antes de editar texto:

1. Criar tabela mestra de titulos por fonte.
2. Marcar presenca/ausencia.
3. Separar poemas com mesmo titulo.
4. Separar poemas com titulo parecido.
5. Criar arquivo mestre com todos os poemas preservados.
6. Somente depois preparar a versao editorial final.

## 7. Proximo artefato

Criar:

`BOOK/05_TABELA_MESTRA_TITULOS.md`

Campos recomendados:

- titulo_detectado;
- titulo_normalizado;
- fonte_A_pdf_2026;
- fonte_B_docx_2025_03_21;
- fonte_C_docx_2025_03_16;
- fonte_D_docx_2025_03_01;
- fonte_E_pdf_2025_04_18;
- classificacao;
- decisao_pendente;
- observacoes.
