# PLANO DE EXTRACAO DO NUCLEO O PENSAMENTO

Data: 2026-07-10
Origem: PRAXIUM / Aurora / frente operacional do livro
Status: FRENTE ATIVA - PRE-CANONICA
Escopo: extracao, identificacao e controle de integridade

## 1. Finalidade

Este plano operacionaliza o protocolo definido em `BOOK/21_PROTOCOLO_COMPARACAO_TEXTUAL_FONTES.md` para o nucleo `O Pensamento`.

Seu objetivo e organizar a extracao rastreavel das fontes PDF, DOCX e TXT, sem alterar os arquivos de origem, sem escolher versao canonica e sem desenvolver conteudo literario novo.

## 2. Principios de execucao

1. preservar todas as fontes originais em modo somente leitura;
2. registrar caminho, nome, formato, tamanho, data aparente e origem de cada arquivo;
3. separar extracao bruta de copia normalizada para comparacao;
4. impedir correcao silenciosa de ortografia, pontuacao ou estilo;
5. registrar paginas, paragrafos e blocos nao extraidos;
6. manter o nucleo `O Pensamento` separado das demais frentes do livro;
7. produzir apenas artefatos tecnicos e pre-canonicos.

## 3. Ordem pratica de extracao

### Etapa 1 - Confirmacao das fontes

Criar uma ficha para cada arquivo candidato contendo:

- identificador da fonte;
- nome exato do arquivo;
- formato;
- localizacao;
- origem documental;
- data de criacao e modificacao, quando disponiveis;
- tamanho;
- quantidade de paginas ou paragrafos;
- presenca de texto pesquisavel;
- observacoes de integridade;
- relacao presumida com `O Pensamento`;
- status de verificacao.

Nenhum arquivo entra na comparacao sem ficha minima de origem.

### Etapa 2 - Extracao do PDF

Ordem:

1. verificar se o PDF possui camada de texto pesquisavel;
2. extrair o texto pagina a pagina;
3. preservar marcadores de pagina no texto bruto;
4. registrar paginas vazias, ilustradas ou parcialmente ilegíveis;
5. separar cabecalhos, rodapes e numeracao em camada tecnica;
6. gerar relatorio de cobertura da extracao;
7. manter o PDF inalterado.

Saidas previstas:

- `BOOK/EXTRACOES/O_PENSAMENTO/PDF/FONTE_PDF_FICHA.md`;
- `BOOK/EXTRACOES/O_PENSAMENTO/PDF/FONTE_PDF_BRUTA.txt`;
- `BOOK/EXTRACOES/O_PENSAMENTO/PDF/FONTE_PDF_NORMALIZADA.txt`;
- `BOOK/EXTRACOES/O_PENSAMENTO/PDF/FONTE_PDF_LACUNAS.md`.

### Etapa 3 - Extracao do DOCX

Ordem:

1. extrair paragrafos na ordem original;
2. registrar estilos de titulo, subtitulo e corpo;
3. identificar notas, comentarios, caixas de texto e trechos ocultos;
4. registrar controle de alteracoes, quando existente;
5. separar texto autoral de metadados editoriais;
6. gerar mapa de estrutura;
7. manter o DOCX inalterado.

Saidas previstas:

- `BOOK/EXTRACOES/O_PENSAMENTO/DOCX/FONTE_DOCX_FICHA.md`;
- `BOOK/EXTRACOES/O_PENSAMENTO/DOCX/FONTE_DOCX_BRUTA.txt`;
- `BOOK/EXTRACOES/O_PENSAMENTO/DOCX/FONTE_DOCX_ESTRUTURA.md`;
- `BOOK/EXTRACOES/O_PENSAMENTO/DOCX/FONTE_DOCX_NORMALIZADA.txt`;
- `BOOK/EXTRACOES/O_PENSAMENTO/DOCX/FONTE_DOCX_LACUNAS.md`.

### Etapa 4 - Extracao do TXT

Ordem:

1. identificar codificacao;
2. preservar quebras de linha e espacamento originais na copia bruta;
3. registrar ausencia de hierarquia formal;
4. marcar titulos apenas como hipoteses estruturais;
5. criar copia normalizada sem substituir a original;
6. registrar caracteres invalidos ou perdas de codificacao.

Saidas previstas:

- `BOOK/EXTRACOES/O_PENSAMENTO/TXT/FONTE_TXT_FICHA.md`;
- `BOOK/EXTRACOES/O_PENSAMENTO/TXT/FONTE_TXT_BRUTA.txt`;
- `BOOK/EXTRACOES/O_PENSAMENTO/TXT/FONTE_TXT_NORMALIZADA.txt`;
- `BOOK/EXTRACOES/O_PENSAMENTO/TXT/FONTE_TXT_LACUNAS.md`.

## 4. Identificadores de fontes

Padrao:

- `OP-PDF-001` para a primeira fonte PDF;
- `OP-DOCX-001` para a primeira fonte DOCX;
- `OP-TXT-001` para a primeira fonte TXT.

Novas variantes devem receber sequencia propria, sem reaproveitar identificadores.

Exemplos:

- `OP-PDF-002`;
- `OP-DOCX-002`;
- `OP-TXT-002`.

## 5. Identificadores de blocos

Cada bloco extraido deve receber identificador estavel no formato:

`OP-<FONTE>-<SECAO>-<BLOCO>`

Exemplos:

- `OP-PDF001-S001-B0001`;
- `OP-DOCX001-S003-B0012`;
- `OP-TXT001-S000-B0047`.

Regras:

1. o identificador nunca muda depois de atribuido;
2. a secao `S000` indica ausencia de secao formal;
3. paragrafos vazios nao recebem identificador autoral, mas podem ser registrados tecnicamente;
4. blocos divididos durante a extracao devem manter relacao com o bloco de origem;
5. nenhuma correspondencia entre fontes altera os identificadores originais.

## 6. Campos minimos por bloco

Cada bloco deve registrar:

| Campo | Conteudo esperado |
|---|---|
| ID do bloco | Identificador estavel |
| ID da fonte | Fonte de origem |
| Localizacao | Pagina, paragrafo ou linha |
| Secao aparente | Titulo ou hipotese estrutural |
| Texto bruto | Transcricao sem correcao |
| Texto normalizado | Copia tecnica para comparacao |
| Tipo | Titulo, corpo, nota, legenda ou indeterminado |
| Integridade | Completo, parcial ou ilegivel |
| Observacoes | Anomalias, quebras ou duvidas |

## 7. Normalizacao permitida

Na copia tecnica, e permitido:

1. padronizar finais de linha;
2. remover espacos duplicados;
3. marcar palavras quebradas por mudanca de linha;
4. separar cabecalhos e rodapes claramente nao autorais;
5. padronizar aspas e hifens para comparacao;
6. manter referencia ao texto bruto correspondente.

Permanece proibido:

1. corrigir ortografia silenciosamente;
2. completar frases;
3. modernizar vocabulario;
4. reorganizar paragrafos;
5. eliminar repeticoes;
6. fundir blocos semelhantes;
7. substituir a fonte por qualquer saida normalizada.

## 8. Controles de integridade

Cada fonte deve passar pelos seguintes controles:

### 8.1 Integridade documental

- arquivo acessivel;
- formato reconhecido;
- ausencia de alteracao no original;
- identificacao de versao e origem;
- registro de falhas de leitura.

### 8.2 Integridade de extracao

- contagem de paginas, paragrafos ou linhas;
- comparacao entre volume original e volume extraido;
- registro de paginas ou blocos ausentes;
- verificacao de caracteres corrompidos;
- marcacao de trechos ilegíveis.

### 8.3 Integridade estrutural

- sequencia preservada;
- titulos e secoes registrados;
- anexos e notas separados;
- lacunas visiveis;
- nenhum bloco deslocado sem registro.

### 8.4 Integridade de rastreabilidade

- todo texto normalizado aponta para o texto bruto;
- todo bloco aponta para sua fonte;
- toda lacuna possui registro;
- toda transformacao tecnica e documentada;
- nenhuma decisao editorial e tomada durante a extracao.

## 9. Manifesto geral de extracao

Ao final das tres extracoes, criar:

`BOOK/EXTRACOES/O_PENSAMENTO/MANIFESTO_EXTRACAO.md`

Campos obrigatorios:

- fontes processadas;
- identificadores atribuidos;
- ferramentas utilizadas;
- data da extracao;
- cobertura por fonte;
- lacunas conhecidas;
- falhas tecnicas;
- quantidade de blocos;
- hash ou identificador tecnico, quando disponivel;
- status de cada fonte;
- impedimentos para comparacao.

## 10. Saidas consolidadas

Depois da extracao individual, produzir:

- `BOOK/EXTRACOES/O_PENSAMENTO/MAPA_ESTRUTURAL_FONTES.md`;
- `BOOK/EXTRACOES/O_PENSAMENTO/INDICE_BLOCOS.csv`;
- `BOOK/EXTRACOES/O_PENSAMENTO/RELATORIO_INTEGRIDADE.md`;
- `BOOK/EXTRACOES/O_PENSAMENTO/LACUNAS_CONSOLIDADAS.md`.

Essas saidas nao substituem as fontes e nao definem texto canonico.

## 11. Criterios para iniciar a comparacao

A comparacao entre PDF, DOCX e TXT so pode comecar quando:

1. todas as fontes tiverem ficha de origem;
2. as extracoes brutas estiverem completas ou com lacunas registradas;
3. os blocos tiverem identificadores estaveis;
4. as copias normalizadas estiverem vinculadas aos textos brutos;
5. o manifesto geral estiver concluido;
6. nao houver risco de sobrescrita das fontes;
7. as limitacoes tecnicas estiverem declaradas.

## 12. Limite atual de execucao

Permanece vedado nesta etapa:

- desenvolver conteudo literario;
- reescrever trechos;
- escolher fonte definitiva;
- fundir variantes;
- corrigir o manuscrito;
- completar lacunas por inferencia;
- publicar ou substituir arquivos autorais.

## 13. Proxima acao operacional

Localizar e registrar os arquivos efetivos do nucleo `O Pensamento` em uma ficha de fontes, antes de executar qualquer extracao textual.

Arquivo previsto:

`BOOK/23_FICHA_FONTES_NUCLEO_O_PENSAMENTO.md`
