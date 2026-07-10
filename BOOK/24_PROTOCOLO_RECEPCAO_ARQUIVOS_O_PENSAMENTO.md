# PROTOCOLO DE RECEPCAO DE ARQUIVOS — NUCLEO O PENSAMENTO

Data: 2026-07-10
Origem: PRAXIUM / Aurora / frente operacional do livro
Status: FRENTE ATIVA — RECEPCAO CONTROLADA DEFINIDA
Escopo: entrada tecnica das fontes sem perda de origem, metadados ou integridade

## 1. Finalidade

Este protocolo executa a proxima etapa prevista em `BOOK/23_FICHA_FONTES_NUCLEO_O_PENSAMENTO.md`.

Seu objetivo e definir como os arquivos do nucleo `O Pensamento` devem ser recebidos, preservados, identificados e liberados para extracao tecnica.

A recepcao nao transforma nenhuma fonte em versao canonica e nao autoriza alteracao editorial.

## 2. Condicao operacional

O repositorio `DanteLocatelli/PRAXIUM` esta acessivel para leitura e escrita por conector GitHub, permitindo continuidade estrutural da frente do livro.

Nao foi confirmada nesta execucao a abertura de aplicativo local Codex ou Copilot nem o acesso direto ao caminho `C:\PRAXIUM`.

A recepcao de conteudo integral somente podera ocorrer quando os arquivos estiverem disponiveis em ambiente diretamente acessivel e verificavel.

## 3. Fontes previstas

| ID | Arquivo esperado | Formato | Trilha inicial |
|---|---|---|---|
| `OP-PDF-001` | `O Pensamento_ O Livro Definitivo.pdf` | PDF | consolidado anterior candidato |
| `OP-DOCX-001` | `O pensamento anotações e raciocínio primário.docx` | DOCX | raciocinio primario editavel |
| `OP-TXT-001` | `O Pensamento o livro definitivo 1 organizado.txt` | TXT | organizacao intermediaria |
| `OP-TXT-002` | `o_pensamento_complementar.txt` | TXT | complemento conceitual |
| `OP-TXT-003` | `tema de 23 11 2025 o livro como porograma.txt` | TXT | apresentacao ou abertura |

## 4. Regra de entrada

Cada arquivo deve entrar como copia tecnica imutavel da fonte recebida.

Na recepcao, e proibido:

- renomear silenciosamente o arquivo original;
- converter formato antes da preservacao da copia original;
- corrigir texto, estilos, acentos ou quebras;
- fundir arquivos;
- substituir uma fonte anterior por outra;
- remover comentarios, revisoes, propriedades ou metadados;
- declarar qualquer arquivo como definitivo.

## 5. Estrutura recomendada de armazenamento

```text
BOOK/
  SOURCES/
    O_PENSAMENTO/
      00_RECEBIDOS_ORIGINAIS/
      01_COPIAS_TECNICAS/
      02_EXTRACOES_BRUTAS/
      03_METADADOS/
      04_COMPARACOES/
      05_QUARENTENA/
```

Regras:

1. `00_RECEBIDOS_ORIGINAIS` guarda a copia exata recebida.
2. `01_COPIAS_TECNICAS` guarda duplicatas destinadas a processamento.
3. `02_EXTRACOES_BRUTAS` recebe apenas saidas de extracao, nunca texto corrigido.
4. `03_METADADOS` guarda manifestos, hashes, contagens e registros de origem.
5. `04_COMPARACOES` recebe tabelas de correspondencia e divergencia.
6. `05_QUARENTENA` recebe arquivos corrompidos, duvidosos, incompletos ou sem origem verificavel.

## 6. Manifesto obrigatorio por arquivo

Cada fonte recebida deve ter um manifesto com os seguintes campos:

| Campo | Obrigatorio |
|---|---|
| ID estavel | sim |
| nome original exato | sim |
| nome da copia tecnica | sim |
| formato e extensao | sim |
| tamanho em bytes | sim |
| data de recebimento | sim |
| origem declarada | sim |
| caminho ou local de origem | quando disponivel |
| data de criacao original | quando disponivel |
| data de modificacao original | quando disponivel |
| hash SHA-256 | sim |
| numero de paginas, paragrafos ou linhas | conforme formato |
| observacoes de integridade | sim |
| responsavel pela recepcao | sim |
| status de liberacao | sim |

## 7. Nomenclatura das copias tecnicas

Formato:

```text
<ID>__<NOME_NORMALIZADO_MINIMO>__RECEBIDO_<AAAA-MM-DD>.<ext>
```

Exemplos:

```text
OP-PDF-001__O_PENSAMENTO_LIVRO_DEFINITIVO__RECEBIDO_2026-07-10.pdf
OP-DOCX-001__O_PENSAMENTO_RACIOCINIO_PRIMARIO__RECEBIDO_2026-07-10.docx
```

A normalizacao do nome da copia tecnica nao altera nem substitui o nome original, que deve permanecer registrado no manifesto.

## 8. Verificacao de integridade por formato

### 8.1 PDF

Verificar:

- abertura sem erro;
- numero total de paginas;
- presenca de senha ou restricao;
- existencia de camada de texto;
- paginas vazias, duplicadas ou aparentemente ausentes;
- fontes incorporadas, quando identificaveis;
- hash antes e depois da copia.

### 8.2 DOCX

Verificar:

- abertura sem reparo automatico;
- quantidade de paragrafos, tabelas, notas e comentarios;
- controle de alteracoes;
- cabecalhos, rodapes, notas de rodape e notas finais;
- estilos e quebras de secao;
- arquivos internos e midias incorporadas;
- hash antes e depois da copia.

### 8.3 TXT

Verificar:

- codificacao;
- quantidade de linhas e caracteres;
- tipo de quebra de linha;
- caracteres invalidos ou substituidos;
- presenca de marcadores estruturais;
- hash antes e depois da copia.

## 9. Estados de recepcao

Cada arquivo deve receber um unico estado:

- `IDENTIFICADO` — existe referencia ao arquivo, mas sem acesso direto;
- `RECEBIDO` — copia original armazenada, verificacao ainda pendente;
- `VERIFICADO` — integridade e metadados basicos confirmados;
- `LIBERADO_PARA_EXTRACAO` — copia tecnica autorizada para processamento;
- `QUARENTENA` — arquivo incompleto, corrompido, divergente ou sem origem suficiente;
- `SUBSTITUIDO_POR_NOVA_COPIA` — nova copia recebida, mantendo-se a anterior preservada;
- `BLOQUEADO` — acesso ou uso impedido por restricao tecnica.

Nenhum desses estados significa `CANONICO`.

## 10. Controle de duplicidade

Arquivos com nomes iguais nao devem ser considerados identicos.

A verificacao deve comparar:

1. hash;
2. tamanho;
3. data e origem;
4. contagem estrutural;
5. conteudo extraido, somente depois da liberacao.

Se os hashes forem diferentes, ambas as copias devem ser preservadas e identificadas como variantes.

## 11. Liberacao para extracao

Uma fonte somente pode receber o estado `LIBERADO_PARA_EXTRACAO` quando:

- a copia original estiver preservada;
- o hash estiver registrado;
- o formato abrir sem perda aparente;
- o manifesto estiver preenchido;
- a copia tecnica estiver separada da original;
- nao houver conversao destrutiva;
- a origem estiver suficientemente documentada.

## 12. Saidas permitidas apos a liberacao

A extracao pode produzir:

- texto bruto por pagina ou bloco;
- inventario de titulos e subtitulos aparentes;
- contagem de paragrafos, linhas e secoes;
- registro de comentarios, notas e revisoes;
- mapa de correspondencia entre fontes;
- lista de divergencias sem julgamento editorial.

Nao pode produzir nesta fase:

- reescrita;
- correcao automatica;
- fusao editorial;
- novo capitulo;
- texto de ligacao;
- escolha de versao definitiva.

## 13. Registro de incidente

Qualquer problema deve ser registrado com:

- ID da fonte;
- data;
- descricao objetiva;
- etapa em que ocorreu;
- impacto potencial;
- acao tomada;
- necessidade de nova copia;
- estado final do arquivo.

Problemas de integridade nunca devem ser corrigidos diretamente na copia original.

## 14. Criterio de conclusao desta etapa

A recepcao sera considerada pronta quando existir, para cada fonte disponivel:

1. copia original preservada;
2. copia tecnica separada;
3. hash registrado;
4. manifesto completo;
5. verificacao basica de integridade;
6. estado operacional atribuido.

## 15. Proxima acao operacional

Preparar o modelo padrao de manifesto e cadeia de custodia para preenchimento por fonte recebida.

Arquivo previsto:

`BOOK/25_MODELO_MANIFESTO_CADEIA_CUSTODIA_O_PENSAMENTO.md`
