# QUADRO OPERACIONAL — SEDIMENTACAO DAS DEFINICOES DE O PENSAMENTO

Data: 2026-07-15
Frente: PRAXIUM / Aurora / BOOK
Estado: ATIVO PARA ESTRUTURA E VALIDACAO; CONTEUDO AUTORAL BLOQUEADO ATE FONTE PRIMARIA LIBERADA

## 1. Finalidade

Este quadro converte a metodologia ja aprovada em uma fila operacional controlada. Cada definicao do livro devera percorrer as mesmas etapas, sem mistura entre texto autoral, explicacao conceitual, formalizacao matematica e decisao editorial.

## 2. Unidade minima de trabalho

Cada item da fila corresponde a uma unica definicao ou relacao conceitual identificada em fonte primaria liberada.

Identificador padrao:

`OP-DEF-###`

Nenhum identificador deve ser criado para conteudo reconstruido por memoria ou inferencia.

## 3. Etapas obrigatorias

1. **Recepcao da fonte**
   - arquivo preservado;
   - versao identificada;
   - localizacao exata registrada.

2. **Extracao literal**
   - transcricao fiel;
   - contexto anterior e posterior;
   - nenhuma reescrita nesta etapa.

3. **Confirmacao autoral por Dante**
   - nucleo indispensavel;
   - termos que nao podem ser substituidos;
   - alcance pretendido.

4. **Analise da Aurora**
   - explicacao em linguagem direta;
   - dependencias com outras definicoes;
   - ambiguidades, pressupostos e riscos de leitura.

5. **Analise do Motor Matematico**
   - objetos, variaveis e parametros;
   - relacoes candidatas;
   - hipoteses, dominio, limites e forma de teste;
   - classificacao entre matematizacao valida, parcial, heuristica, simulavel ou metaforica.

6. **Crivo de Socrates**
   - circularidade;
   - contradicoes;
   - contraexemplos;
   - casos-limite;
   - diferenca entre descrever, explicar, prever e orientar.

7. **Consolidacao PRAXIUM**
   - rastreabilidade completa;
   - nivel de confianca;
   - registro de divergencias;
   - estado final da definicao.

8. **Decisao de Dante**
   - preservar, ajustar, restringir, ampliar, manter em teste ou rejeitar;
   - autorizar ou nao a incorporacao no livro.

## 4. Estados da fila

- `AGUARDANDO_FONTE`
- `FONTE_RECEBIDA`
- `EXTRACAO_LITERAL`
- `AGUARDANDO_DANTE`
- `ANALISE_AURORA`
- `ANALISE_MATEMATICA`
- `CRIVO_SOCRATES`
- `CONSOLIDACAO_PRAXIUM`
- `EM_REVISAO_AUTORAL`
- `SEDIMENTADA`
- `SEDIMENTADA_COM_FORMALIZACAO_PARCIAL`
- `HEURISTICA`
- `EM_TESTE`
- `BLOQUEADA`
- `REJEITADA`

## 5. Campos do quadro mestre

| Campo | Descricao |
|---|---|
| ID | Identificador `OP-DEF-###` |
| Titulo provisório | Nome operacional, sem canonizacao prematura |
| Fonte | Arquivo e versao |
| Localizacao | Pagina, secao ou trecho |
| Estado | Um dos estados da fila |
| Responsavel atual | Dante, Aurora, Motor Matematico, Socrates ou PRAXIUM |
| Dependencias | Definicoes anteriores necessarias |
| Formula vinculada | ID da formula ou `NAO DEFINIDA` |
| Nivel de confianca | Baixo, moderado ou alto |
| Pendencia critica | Obstaculo que impede avancar |
| Proxima acao | Acao unica, objetiva e verificavel |
| Registro de decisao | Referencia ao parecer ou aprovacao |

## 6. Regra de passagem entre etapas

Uma definicao somente avanca quando a etapa anterior produz evidencia registravel. Opiniao verbal, intuicao ou simbolismo isolado nao substituem fonte, hipotese, justificativa ou teste.

A formula nao valida automaticamente a definicao. Ela deve especificar relacoes, revelar limites ou permitir teste. Quando apenas traduzir o texto em simbolos, sera classificada como representacao ou metafora matematica.

## 7. Gate atual

Enquanto nao houver fonte primaria liberada:

- manter o quadro e os instrumentos prontos;
- nao criar IDs de definicoes reais;
- nao preencher texto autoral;
- nao propor formulas para conceitos ausentes;
- nao redigir capitulos como versoes consolidadas.

## 8. Proxima acao autorizada

Localizar, receber, preservar e liberar a primeira fonte primaria de `O Pensamento`. Apos essa liberacao, abrir o primeiro item `OP-DEF-001` usando a ficha operacional vigente.
