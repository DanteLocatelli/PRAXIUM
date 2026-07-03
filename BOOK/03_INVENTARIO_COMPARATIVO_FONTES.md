# INVENTARIO COMPARATIVO DE FONTES — Para Voce Lembrar

Data: 2026-07-02
Status: auditoria inicial de fontes
Metodo: comparacao por metadados, abertura, sumario, estrutura e sinais de integridade textual
Regra: corrigir sem domesticar; editar sem empobrecer; organizar sem matar a voz

## 1. Conclusao operacional inicial

A obra nao deve ser tratada como um unico arquivo isolado.

Foram detectadas pelo menos tres camadas:

1. **Livro atual estruturado** — PDF de 28/06/2026.
2. **Mestre editavel limpo / versao DOCX organizada** — DOCX de marco/2025, especialmente `Para Você Lembrar 2.docx` e copia `(1)`.
3. **Acervo/compilacao anterior ampliada** — versao inicial DOCX de 01/03/2025 e PDF de 18/04/2025, com poemas e material que podem nao estar no livro atual.

Nenhuma camada deve ser apagada. A fase correta agora e classificar, comparar e preservar.

## 2. Fonte A — PDF recente / candidata a versao-base atual

Arquivo: `Para Você Lembrar_Dante_Locatelli.pdf`
Drive ID: `1BbhZ6DZ9hHmhZ7H_jb5YMa1p0qgtyPMh`
Criado/modificado: 2026-06-28

### Caracteristicas

- Contem titulo `Para Você Lembrar`.
- Autor: Dante Locatelli.
- Contem Nota do Autor, Introducao, Apresentacao e Sumario.
- Organiza o livro em seis partes tematicas.
- Parece ser a versao mais recente e diagramada.

### Problemas detectados

- Extração indica colagens: `Dante LocatelliNota do Autor`, `reencontro.Introdução`, `encontrado.Apresentação`, `Aurora I.A. GPTSumário`.
- Pode haver problema de diagramação ou apenas de extração do PDF.
- Nao deve ser usado como mestre editavel sem reconstrução/limpeza.

### Status PRAXIUM

**Candidata principal a versao-base de conteudo recente**, mas nao candidata ideal a arquivo mestre editavel.

## 3. Fonte B — DOCX organizado / copia 1

Arquivo: `Para Você Lembrar 2 (1).docx`
Drive ID: `1djJitGUcC9rrAYXV2r9wdq-mw421GtJO`
Criado: 2025-03-21
Modificado: 2025-03-14

### Caracteristicas

- Abertura limpa: titulo, autor, Nota do Autor, Introducao, Apresentacao.
- Mantem a apresentacao com assinatura: `Redigido pela I.A. Site GPT`.
- Contem Organizacao e Indice.
- Contem seis secoes.
- Estrutura textual parece muito proxima ao PDF recente, mas em formato editavel.

### Problemas detectados

- Indice duplicado: aparece `Índice` duas vezes.
- Ha itens de organizacao como `Contra capa`, `Posfácio` e secoes que precisam de normalizacao editorial.
- Aparecem duplicatas aparentes em varias secoes.

### Status PRAXIUM

**Forte candidata a mestre editavel comparativo**, especialmente para reconstruir uma versao limpa do PDF recente.

## 4. Fonte C — DOCX organizado / copia 2

Arquivo: `Para Você Lembrar 2.docx`
Drive ID: `1u9yuZT5xa0hf3omP5dux9k_-gFENC0rx`
Criado: 2025-03-16
Modificado: 2025-03-14

### Caracteristicas

- Conteudo inicial coincide com `Para Você Lembrar 2 (1).docx`.
- Parece ser a mesma versao base, com copia posterior criada em 21/03/2025.

### Status PRAXIUM

**Provavel duplicata funcional da Fonte B.** Manter ambas ate verificacao binaria/linha a linha, mas usar a Fonte B como copia mais recente por data de criacao.

## 5. Fonte D — DOCX inicial / acervo anterior

Arquivo: `Para Você Lembrar.docx`
Drive ID: `1R3nvilUi4MRCdrU-MMfvSnphtDYrVuDq`
Criado/modificado: 2025-03-01

### Caracteristicas

- Abertura mais antiga e diferente.
- Nao contem a citacao inicial da rainha na Introducao encontrada nas versoes posteriores.
- Entra rapidamente no acervo de poemas.
- Contem poemas/titulos que podem nao estar na versao atual, por exemplo:
  - `Amores Improváveis`;
  - `AMANTE`;
  - `POEMINHA DO APROVEITANDO A DEIXA`;
  - `O Amor e a Esperança`;
  - `O Amor de Um Fantasma`.

### Risco

Essa fonte pode conter material excluido, deslocado ou nao aproveitado na versao atual.

### Status PRAXIUM

**Fonte de acervo e recuperacao.** Nao deve ser tomada como versao-base atual, mas deve ser preservada e comparada para evitar perda de poemas.

## 6. Fonte E — PDF completo / compilacao anterior

Arquivo: `Para Você Lembrar - livro completo.pdf`
Drive ID: `1MSp_D5YmR1g1AwT0HRoss24S6VMOcipz`
Criado/modificado: 2025-04-18

### Caracteristicas

- Indica data textual `março 07, 2025`.
- Contem material de blog/site: `DANTE LOCATELLI - POEMAS E TEXTOS`.
- Tem colagens de extração e diagramação.
- Inclui poemas como `Amores Improváveis`, `Amante`, `Por Que Eu Te Beijaria`, `SEM AMOR`.

### Status PRAXIUM

**Compilacao anterior ampla / fonte de preservacao.** Pode conter poemas ausentes do livro atual e deve alimentar um apendice de acervo ou banco relacional de poemas.

## 7. Primeira classificacao das fontes

| Fonte | Arquivo | Papel inicial | Risco | Acao recomendada |
|---|---|---|---|---|
| A | PDF 2026-06-28 | Versao-base recente | colagens / nao editavel | comparar e reconstruir mestre |
| B | DOCX 2025-03-21 | Mestre editavel candidato | indice duplicado / assinatura IA | usar como base editavel comparativa |
| C | DOCX 2025-03-16 | Duplicata provavel | redundancia | manter ate comparar |
| D | DOCX 2025-03-01 | Acervo anterior | poemas ausentes podem ser perdidos | preservar e inventariar |
| E | PDF 2025-04-18 | Compilacao/blog anterior | colagens e material externo | preservar e extrair acervo |

## 8. Decisao operacional

Nao fechar o livro ainda.

Proxima etapa correta:

1. Criar lista mestra de titulos por fonte.
2. Marcar cada poema como:
   - presente no livro atual;
   - ausente do livro atual;
   - duplicado;
   - variacao;
   - titulo semelhante;
   - material externo/acervo.
3. Criar arquivo `04_AUDITORIA_DUPLICATAS_E_VARIACOES.md`.
4. Depois, criar `MANUSCRITO_EDITAVEL_BASE.md` ou DOCX editavel somente com base validada.

## 9. Observacao de governanca

A assinatura de IA deve ser tratada como decisao editorial, nao como erro automatico.

Formas possiveis de tratar:

- manter como nota historica;
- converter em nota de organizacao;
- remover da versao publica e manter no log;
- mover para creditos internos.

A decisao final cabe a Dante.
