# PROTOCOLO DE COMPARACAO TEXTUAL DAS FONTES DO LIVRO

Data: 2026-07-10
Origem: PRAXIUM / Aurora / frente operacional do livro
Status: FRENTE ATIVA - PROTOCOLO PRE-CANONICO
Escopo: documental, estrutural e editorial

## 1. Finalidade

Este protocolo da continuidade a `BOOK/20_MATRIZ_COMPARACAO_FONTES_LIVRO.md`.

Seu objetivo e permitir a comparacao rastreavel entre as fontes do livro sem escolher automaticamente uma versao canonica, sem reescrever texto autoral e sem misturar frentes literarias distintas.

## 2. Principios obrigatorios

1. preservar integralmente os arquivos de origem;
2. trabalhar inicialmente em modo somente leitura;
3. registrar toda transformacao tecnica aplicada ao texto extraido;
4. distinguir diferenca editorial de diferenca meramente tecnica;
5. impedir que data mais recente, nome `final` ou acabamento visual determinem canonizacao;
6. separar `O Pensamento`, acervo poetico, `Meu Primeiro Livro Livre` e `Stella`;
7. manter evidencia suficiente para auditoria posterior.

## 3. Unidade de comparacao

A comparacao deve ocorrer em quatro niveis:

1. documento completo;
2. estrutura de capitulos, secoes e titulos;
3. blocos de texto ou paragrafos;
4. frases, apenas quando necessario para esclarecer divergencias.

Nao se deve iniciar pela comparacao palavra a palavra quando a estrutura geral ainda nao estiver mapeada.

## 4. Extracao por formato

### 4.1 PDF

- extrair texto preservando numero de pagina quando possivel;
- registrar se o PDF contem texto pesquisavel ou depende de reconhecimento;
- nao corrigir automaticamente palavras durante a extracao;
- separar cabecalhos, rodapes e numeracao do corpo autoral;
- registrar paginas com imagens, diagramas ou texto nao extraido.

### 4.2 DOCX

- preservar ordem dos paragrafos;
- registrar estilos de titulo e subtitulo;
- identificar notas, comentarios, caixas de texto e trechos ocultos;
- separar propriedades editoriais do texto autoral;
- nao aceitar controle de alteracoes sem registrar autor e data quando disponiveis.

### 4.3 TXT

- preservar codificacao e quebras originais;
- registrar ausencia de estilos ou hierarquia formal;
- inferir titulos apenas como hipotese operacional, nunca como decisao editorial;
- manter copia exata antes de qualquer normalizacao.

### 4.4 Google Docs e e-mails

- tratar como fonte documental ou de governanca, salvo evidencia de manuscrito;
- registrar origem, data, remetente ou proprietario e relacao com o livro;
- nao incorporar automaticamente trechos ao corpo da obra.

## 5. Normalizacao minima permitida

A normalizacao serve somente para comparar e nao altera a fonte original.

E permitido:

1. converter finais de linha para um padrao comum;
2. normalizar espacos duplicados;
3. remover cabecalhos, rodapes e numeracao quando claramente nao autorais;
4. padronizar aspas e hifens apenas na copia tecnica;
5. marcar palavras quebradas por mudanca de linha;
6. criar identificadores estaveis para capitulos e blocos.

Nao e permitido:

1. corrigir ortografia silenciosamente;
2. modernizar vocabulario;
3. completar frases;
4. reorganizar paragrafos por criterio estetico;
5. fundir blocos semelhantes;
6. eliminar repeticoes sem classificacao previa;
7. substituir o arquivo de origem pela versao normalizada.

## 6. Sequencia de comparacao

### Fase A - mapa estrutural

Para cada fonte, registrar:

- titulo aparente;
- sequencia de capitulos e secoes;
- quantidade de blocos;
- aberturas e encerramentos;
- anexos, notas e complementos;
- lacunas aparentes.

### Fase B - alinhamento de blocos

Relacionar blocos equivalentes usando:

1. titulo ou subtitulo;
2. frase inicial;
3. palavras-chave raras;
4. posicao relativa;
5. semelhanca textual;
6. continuidade tematica.

Toda correspondencia deve receber grau de confianca: alto, medio ou baixo.

### Fase C - classificacao das divergencias

Cada divergencia deve ser classificada como:

- `INCLUSAO`: bloco presente em uma fonte e ausente em outra;
- `EXCLUSAO`: bloco removido em versao posterior aparente;
- `DESLOCAMENTO`: mesmo bloco em posicao diferente;
- `REVISAO`: texto equivalente com alteracoes autorais aparentes;
- `DUPLICACAO`: bloco repetido integral ou parcialmente;
- `FRAGMENTACAO`: um bloco dividido em varios;
- `FUSAO`: varios blocos reunidos em um;
- `VARIACAO_TECNICA`: diferenca de formatacao, codificacao ou extracao;
- `INDETERMINADA`: origem ou sentido da diferenca ainda nao demonstrado.

## 7. Tabela minima de evidencias

Cada comparacao deve produzir registro com os seguintes campos:

| Campo | Conteudo esperado |
|---|---|
| ID da divergencia | Identificador unico |
| Fonte A | Nome e localizacao |
| Fonte B | Nome e localizacao |
| Unidade comparada | Capitulo, secao, bloco ou frase |
| Tipo | Classe da divergencia |
| Evidencia A | Pagina, paragrafo ou trecho de referencia |
| Evidencia B | Pagina, paragrafo ou trecho de referencia |
| Confianca | Alta, media ou baixa |
| Hipotese | Explicacao provisoria |
| Acao futura | Preservar, investigar, validar ou decidir |
| Status | Aberta, validada ou encerrada |

## 8. Regra de autoria e revisao

Uma alteracao so pode ser tratada como revisao autoral confirmada quando houver pelo menos uma destas evidencias:

1. documento posterior com origem confiavel;
2. controle de alteracoes identificavel;
3. mensagem ou nota do autor confirmando a mudanca;
4. continuidade editorial coerente demonstrada por varias fontes;
5. validacao expressa de Dante.

Sem evidencia, a diferenca permanece como variante e nao substitui a redacao anterior.

## 9. Regra contra canonizacao automatica

Nenhuma ferramenta, agente ou rotina pode declarar uma fonte como definitiva apenas por:

- data mais recente;
- nome do arquivo;
- extensao do arquivo;
- maior numero de paginas;
- melhor formatacao;
- maior semelhanca com uma versao publicada;
- resultado de comparacao automatica.

A canonizacao depende de relatorio comparativo, preservacao das variantes e validacao humana expressa.

## 10. Tratamento das frentes paralelas

1. `O Pensamento`: comparar apenas com suas variantes e complementos identificados;
2. `Meu Primeiro Livro Livre`: manter como obra historica e frente editorial propria;
3. acervo poetico: inventariar e comparar poemas individualmente;
4. `Stella`: manter como romance ou frente filosofico-literaria separada;
5. documentos PRAXIUM/Aurora: usar para governanca e rastreabilidade, nao como manuscrito automatico.

Uma aproximacao tematica entre obras nao autoriza fusao textual.

## 11. Controle de saidas

As saidas da comparacao devem ser gravadas em arquivos novos, sem alterar as fontes.

Padrao recomendado:

- `BOOK/COMPARACOES/<fonte_a>__<fonte_b>__MAPA.md`;
- `BOOK/COMPARACOES/<fonte_a>__<fonte_b>__DIVERGENCIAS.csv`;
- `BOOK/COMPARACOES/<fonte_a>__<fonte_b>__RELATORIO.md`.

Cada saida deve informar data, ferramenta utilizada, origem das fontes e limitacoes da extracao.

## 12. Criterio de encerramento da etapa comparativa

A etapa sera considerada concluida quando:

1. todas as fontes criticas da matriz tiverem sido extraidas;
2. a estrutura de cada fonte estiver mapeada;
3. os blocos equivalentes estiverem alinhados;
4. as divergencias relevantes estiverem classificadas;
5. as lacunas de extracao estiverem registradas;
6. as frentes paralelas estiverem separadas;
7. houver relatorio suficiente para indicar candidatas a fonte-base;
8. nenhuma variante tiver sido perdida ou sobrescrita.

## 13. Limite atual de execucao

Permanece vedado nesta etapa:

- desenvolver conteudo literario novo;
- reescrever capitulos;
- completar lacunas por inferencia;
- selecionar versao definitiva;
- fundir obras;
- publicar ou substituir manuscritos.

## 14. Proxima acao operacional

Criar `BOOK/22_PLANO_EXTRACAO_NUCLEO_O_PENSAMENTO.md`, definindo a ordem pratica de extracao do PDF, DOCX e TXT, os identificadores de blocos, as saidas esperadas e os controles de integridade.