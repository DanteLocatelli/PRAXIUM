# TABELA MESTRE DE CONTROLE DE FONTES — NUCLEO O PENSAMENTO

Data: 2026-07-10
Origem: PRAXIUM / Aurora / frente operacional do livro
Status: CONTROLE OPERACIONAL ATIVO — SEM EXTRACAO E SEM CANONIZACAO
Escopo: acompanhamento das fontes previstas para o nucleo `O Pensamento`

## 1. Finalidade

Esta tabela consolida o estado tecnico e documental das fontes identificadas para o nucleo `O Pensamento`.

Ela serve como painel unico de acompanhamento entre identificacao, recebimento, verificacao, cadeia de custodia, extracao e comparacao.

Nenhum campo desta tabela atribui valor editorial, autenticidade definitiva ou prioridade canonica a uma fonte.

## 2. Regras de uso

1. registrar somente dados verificaveis;
2. usar `NAO VERIFICADO` quando a informacao ainda nao tiver sido confirmada;
3. manter um unico estado operacional atual por fonte;
4. vincular cada fonte ao respectivo manifesto de cadeia de custodia;
5. nao alterar texto literario nesta etapa;
6. nao escolher versao definitiva automaticamente;
7. preservar o nome original do arquivo em registro separado do nome tecnico;
8. registrar incidentes sem apagar historico anterior.

## 3. Estados permitidos

- `IDENTIFICADO`
- `RECEBIDO`
- `VERIFICADO`
- `LIBERADO_PARA_EXTRACAO`
- `EM_EXTRACAO`
- `EXTRACAO_CONCLUIDA`
- `EM_COMPARACAO`
- `QUARENTENA`
- `BLOQUEADO`
- `SUBSTITUIDO_POR_NOVA_COPIA`

## 4. Tabela mestre

| ID da fonte | Formato | Nome original | Origem declarada | Local atual | Hash SHA-256 | Manifesto | Integridade | Estado operacional | Extracao | Comparacao | Incidente | Proxima acao |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `OP-PDF-001` | PDF | `NAO VERIFICADO` | `NAO VERIFICADO` | `NAO RECEBIDO` | `NAO CALCULADO` | `NAO CRIADO` | `NAO VERIFICADA` | `IDENTIFICADO` | `NAO INICIADA` | `NAO INICIADA` | `NAO VERIFICADO` | localizar e receber copia preservando o original |
| `OP-DOCX-001` | DOCX | `NAO VERIFICADO` | `NAO VERIFICADO` | `NAO RECEBIDO` | `NAO CALCULADO` | `NAO CRIADO` | `NAO VERIFICADA` | `IDENTIFICADO` | `NAO INICIADA` | `NAO INICIADA` | `NAO VERIFICADO` | localizar e receber copia preservando o original |
| `OP-TXT-001` | TXT | `NAO VERIFICADO` | `NAO VERIFICADO` | `NAO RECEBIDO` | `NAO CALCULADO` | `NAO CRIADO` | `NAO VERIFICADA` | `IDENTIFICADO` | `NAO INICIADA` | `NAO INICIADA` | `NAO VERIFICADO` | localizar e receber copia preservando o original |
| `OP-REF-001` | referencia documental | `NAO VERIFICADO` | `NAO VERIFICADO` | `NAO RECEBIDO` | `NAO SE APLICA` | `NAO CRIADO` | `NAO VERIFICADA` | `IDENTIFICADO` | `NAO SE APLICA` | `NAO INICIADA` | `NAO VERIFICADO` | confirmar natureza, localizacao e funcao da referencia |
| `OP-REF-002` | referencia documental | `NAO VERIFICADO` | `NAO VERIFICADO` | `NAO RECEBIDO` | `NAO SE APLICA` | `NAO CRIADO` | `NAO VERIFICADA` | `IDENTIFICADO` | `NAO SE APLICA` | `NAO INICIADA` | `NAO VERIFICADO` | confirmar natureza, localizacao e funcao da referencia |

## 5. Controle de recebimento

| ID | Data/hora de recebimento | Responsavel | Original preservado | Copia tecnica criada | Hash conferido | Metadados registrados | Resultado |
|---|---|---|---|---|---|---|---|
| `OP-PDF-001` | `PENDENTE` | `PENDENTE` | `NAO` | `NAO` | `NAO` | `NAO` | `AGUARDANDO ARQUIVO` |
| `OP-DOCX-001` | `PENDENTE` | `PENDENTE` | `NAO` | `NAO` | `NAO` | `NAO` | `AGUARDANDO ARQUIVO` |
| `OP-TXT-001` | `PENDENTE` | `PENDENTE` | `NAO` | `NAO` | `NAO` | `NAO` | `AGUARDANDO ARQUIVO` |
| `OP-REF-001` | `PENDENTE` | `PENDENTE` | `NAO SE APLICA` | `NAO SE APLICA` | `NAO SE APLICA` | `NAO` | `AGUARDANDO IDENTIFICACAO` |
| `OP-REF-002` | `PENDENTE` | `PENDENTE` | `NAO SE APLICA` | `NAO SE APLICA` | `NAO SE APLICA` | `NAO` | `AGUARDANDO IDENTIFICACAO` |

## 6. Controle de extracao

| ID | Metodo previsto | Ferramenta | Inicio | Conclusao | Saida bruta | Inventario estrutural | Revisao tecnica | Situacao |
|---|---|---|---|---|---|---|---|---|
| `OP-PDF-001` | extracao da camada textual; OCR apenas se indispensavel | `A DEFINIR` | `PENDENTE` | `PENDENTE` | `NAO GERADA` | `NAO GERADO` | `NAO REALIZADA` | `BLOQUEADA ATE RECEPCAO` |
| `OP-DOCX-001` | extracao de paragrafos, estilos, notas, comentarios e revisoes | `A DEFINIR` | `PENDENTE` | `PENDENTE` | `NAO GERADA` | `NAO GERADO` | `NAO REALIZADA` | `BLOQUEADA ATE RECEPCAO` |
| `OP-TXT-001` | leitura preservando codificacao e quebras | `A DEFINIR` | `PENDENTE` | `PENDENTE` | `NAO GERADA` | `NAO GERADO` | `NAO REALIZADA` | `BLOQUEADA ATE RECEPCAO` |

## 7. Controle de comparacao

| Par de fontes | Tipo de comparacao | Pre-condicao | Estado | Saida prevista |
|---|---|---|---|---|
| `OP-PDF-001 x OP-DOCX-001` | estrutura, ordem, presenca e divergencia textual | duas extracoes concluidas | `NAO INICIADA` | matriz de correspondencia e divergencias |
| `OP-PDF-001 x OP-TXT-001` | estrutura, ordem e divergencia textual | duas extracoes concluidas | `NAO INICIADA` | matriz de correspondencia e divergencias |
| `OP-DOCX-001 x OP-TXT-001` | estrutura, revisoes e divergencia textual | duas extracoes concluidas | `NAO INICIADA` | matriz de correspondencia e divergencias |
| `fontes primarias x OP-REF-001` | coerencia documental e proveniencia | referencia identificada | `NAO INICIADA` | ficha de evidencia |
| `fontes primarias x OP-REF-002` | coerencia documental e proveniencia | referencia identificada | `NAO INICIADA` | ficha de evidencia |

## 8. Indicadores do painel

| Indicador | Valor atual |
|---|---:|
| fontes previstas | 5 |
| fontes recebidas | 0 |
| fontes verificadas | 0 |
| fontes liberadas para extracao | 0 |
| extracoes concluidas | 0 |
| comparacoes concluidas | 0 |
| fontes em quarentena | 0 |
| incidentes impeditivos confirmados | 0 |
| dados ainda nao verificados | SIM |

## 9. Bloqueios atuais

A operacao permanece bloqueada para extracao e desenvolvimento de conteudo enquanto:

- os arquivos nao estiverem acessiveis;
- a origem nao estiver registrada;
- o original nao estiver preservado;
- a copia tecnica nao estiver criada;
- o hash nao estiver conferido;
- o manifesto individual nao estiver preenchido;
- a fonte nao estiver formalmente liberada para extracao.

## 10. Limites editoriais

Esta tabela nao autoriza:

- corrigir ou modernizar textos;
- fundir versoes;
- completar lacunas por inferencia;
- criar capitulos;
- reorganizar o livro;
- declarar uma fonte como canonica;
- substituir decisao de Dante, Aurora ou PRAXIUM.

## 11. Criterio de atualizacao

A tabela deve ser atualizada sempre que ocorrer:

1. localizacao de uma fonte;
2. recebimento de arquivo;
3. calculo ou verificacao de hash;
4. mudanca de estado operacional;
5. criacao de manifesto;
6. inicio ou conclusao de extracao;
7. identificacao de incidente;
8. conclusao de comparacao;
9. decisao formal de validacao.

Cada mudanca deve preservar o historico no Git.

## 12. Proxima acao operacional

Preparar o roteiro de localizacao e vinculacao das cinco fontes, sem presumir caminhos ou nomes ainda nao confirmados.

Arquivo previsto:

`BOOK/27_ROTEIRO_LOCALIZACAO_FONTES_O_PENSAMENTO.md`
