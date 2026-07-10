# MODELO DE MANIFESTO E CADEIA DE CUSTODIA — NUCLEO O PENSAMENTO

Data: 2026-07-10
Origem: PRAXIUM / Aurora / frente operacional do livro
Status: MODELO OPERACIONAL ATIVO — SEM CANONIZACAO
Escopo: registro individual de cada fonte recebida do nucleo `O Pensamento`

## 1. Finalidade

Este modelo executa a etapa prevista em `BOOK/24_PROTOCOLO_RECEPCAO_ARQUIVOS_O_PENSAMENTO.md`.

Seu objetivo e assegurar que cada arquivo recebido tenha origem, integridade, movimentacoes, verificacoes e estado operacional documentados antes de qualquer extracao textual.

O preenchimento deste manifesto nao transforma a fonte em versao canonica, definitiva ou editorialmente aprovada.

## 2. Identificacao da fonte

| Campo | Preenchimento |
|---|---|
| ID estavel da fonte | `<OP-PDF-001 / OP-DOCX-001 / OP-TXT-001...>` |
| nome original exato | `<preencher>` |
| nome da copia tecnica | `<preencher>` |
| formato/extensao | `<PDF / DOCX / TXT / outro>` |
| tamanho em bytes | `<preencher>` |
| origem declarada | `<Drive / HD local / Gmail / outro>` |
| caminho ou local de origem | `<preencher quando disponivel>` |
| responsavel pela entrega | `<preencher>` |
| responsavel pela recepcao | `<preencher>` |
| data e hora de recebimento | `<AAAA-MM-DD HH:MM>` |
| observacao inicial | `<preencher>` |

## 3. Metadados preservados

| Campo | Valor |
|---|---|
| data de criacao original | `<preencher ou NAO DISPONIVEL>` |
| data de modificacao original | `<preencher ou NAO DISPONIVEL>` |
| autor/proprietario informado | `<preencher ou NAO DISPONIVEL>` |
| aplicacao de origem | `<preencher ou NAO DISPONIVEL>` |
| idioma aparente | `<preencher>` |
| restricao de acesso/senha | `<SIM / NAO / NAO VERIFICADO>` |
| comentarios ou revisoes | `<SIM / NAO / NAO SE APLICA>` |
| midias ou objetos incorporados | `<SIM / NAO / NAO VERIFICADO>` |

## 4. Integridade criptografica

| Verificacao | Valor |
|---|---|
| algoritmo | `SHA-256` |
| hash da copia original recebida | `<preencher>` |
| hash apos armazenamento | `<preencher>` |
| hashes coincidem | `<SIM / NAO>` |
| ferramenta utilizada | `<preencher>` |
| data da verificacao | `<AAAA-MM-DD HH:MM>` |
| responsavel | `<preencher>` |

Se os hashes nao coincidirem, a fonte deve ser movida para `QUARENTENA` e nenhuma extracao deve ser iniciada.

## 5. Verificacao estrutural por formato

### 5.1 PDF

| Item | Resultado |
|---|---|
| abre sem erro | `<SIM / NAO / NAO SE APLICA>` |
| numero de paginas | `<preencher>` |
| camada de texto | `<SIM / NAO / PARCIAL>` |
| paginas vazias ou duplicadas aparentes | `<preencher>` |
| senha ou restricao | `<preencher>` |
| observacoes | `<preencher>` |

### 5.2 DOCX

| Item | Resultado |
|---|---|
| abre sem reparo automatico | `<SIM / NAO / NAO SE APLICA>` |
| numero de paragrafos | `<preencher>` |
| numero de tabelas | `<preencher>` |
| comentarios | `<preencher>` |
| controle de alteracoes | `<preencher>` |
| cabecalhos/rodapes/notas | `<preencher>` |
| midias incorporadas | `<preencher>` |
| observacoes | `<preencher>` |

### 5.3 TXT

| Item | Resultado |
|---|---|
| codificacao | `<UTF-8 / ANSI / outra>` |
| numero de linhas | `<preencher>` |
| numero de caracteres | `<preencher>` |
| tipo de quebra de linha | `<LF / CRLF / outra>` |
| caracteres invalidos ou substituidos | `<preencher>` |
| marcadores estruturais aparentes | `<preencher>` |
| observacoes | `<preencher>` |

## 6. Cadeia de custodia

Registrar toda movimentacao ou transformacao tecnica da fonte.

| N. | Data/hora | Responsavel | Acao | Origem | Destino | Hash antes | Hash depois | Resultado |
|---:|---|---|---|---|---|---|---|---|
| 1 | `<preencher>` | `<preencher>` | recebimento | `<preencher>` | `00_RECEBIDOS_ORIGINAIS` | `<preencher>` | `<preencher>` | `<preencher>` |
| 2 | `<preencher>` | `<preencher>` | criacao de copia tecnica | `00_RECEBIDOS_ORIGINAIS` | `01_COPIAS_TECNICAS` | `<preencher>` | `<preencher>` | `<preencher>` |
| 3 | `<preencher>` | `<preencher>` | verificacao estrutural | `01_COPIAS_TECNICAS` | `01_COPIAS_TECNICAS` | `<preencher>` | `<preencher>` | `<preencher>` |

Nenhuma linha anterior deve ser apagada. Correcoes devem ser feitas por novo registro, com justificativa.

## 7. Incidentes e divergencias

| Campo | Preenchimento |
|---|---|
| incidente identificado | `<SIM / NAO>` |
| descricao objetiva | `<preencher>` |
| etapa em que ocorreu | `<preencher>` |
| impacto potencial | `<preencher>` |
| acao tomada | `<preencher>` |
| nova copia solicitada | `<SIM / NAO>` |
| vinculo com registro de incidente | `<preencher ou NAO SE APLICA>` |

## 8. Estado operacional da fonte

Selecionar um unico estado atual:

- [ ] `IDENTIFICADO`
- [ ] `RECEBIDO`
- [ ] `VERIFICADO`
- [ ] `LIBERADO_PARA_EXTRACAO`
- [ ] `QUARENTENA`
- [ ] `SUBSTITUIDO_POR_NOVA_COPIA`
- [ ] `BLOQUEADO`

Justificativa do estado:

`<preencher>`

Data da atribuicao:

`<AAAA-MM-DD HH:MM>`

Responsavel:

`<preencher>`

## 9. Autorizacao tecnica para extracao

A fonte somente pode ser liberada quando todos os itens abaixo estiverem confirmados:

- [ ] original preservado sem alteracao;
- [ ] copia tecnica separada;
- [ ] hash SHA-256 registrado e conferido;
- [ ] metadados essenciais preenchidos;
- [ ] verificacao estrutural concluida;
- [ ] origem suficientemente documentada;
- [ ] nenhum incidente impeditivo em aberto;
- [ ] estado `LIBERADO_PARA_EXTRACAO` atribuido.

Autorizacao tecnica:

| Campo | Valor |
|---|---|
| autorizado por | `<preencher>` |
| data/hora | `<preencher>` |
| escopo permitido | `extracao bruta e inventario estrutural` |
| restricoes adicionais | `<preencher>` |

## 10. Bloqueios permanentes desta fase

Mesmo apos a liberacao para extracao, permanecem proibidos:

- corrigir o texto original;
- reescrever trechos;
- fundir fontes;
- escolher versao definitiva;
- criar capitulos novos;
- alterar ordem editorial;
- canonizar automaticamente qualquer arquivo;
- substituir o original por copia processada.

## 11. Nome recomendado do manifesto preenchido

```text
<ID_DA_FONTE>__MANIFESTO_CADEIA_CUSTODIA__<AAAA-MM-DD>.md
```

Exemplo:

```text
OP-PDF-001__MANIFESTO_CADEIA_CUSTODIA__2026-07-10.md
```

Local recomendado:

```text
BOOK/SOURCES/O_PENSAMENTO/03_METADADOS/
```

## 12. Criterio de conclusao

O manifesto de uma fonte sera considerado completo quando:

1. todos os campos obrigatorios estiverem preenchidos;
2. a cadeia de custodia registrar recebimento e copia tecnica;
3. os hashes forem conferidos;
4. a verificacao estrutural estiver documentada;
5. houver estado operacional unico e justificado;
6. a autorizacao ou bloqueio para extracao estiver formalmente registrado.

## 13. Proxima acao operacional

Preparar a tabela mestre de controle das cinco fontes previstas do nucleo `O Pensamento`, usando este modelo como referencia e sem preencher dados ainda nao verificados.

Arquivo previsto:

`BOOK/26_TABELA_MESTRE_CONTROLE_FONTES_O_PENSAMENTO.md`
