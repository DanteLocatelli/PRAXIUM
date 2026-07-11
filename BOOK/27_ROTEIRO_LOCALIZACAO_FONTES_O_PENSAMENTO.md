# ROTEIRO DE LOCALIZACAO E VINCULACAO DAS FONTES — O PENSAMENTO

Data: 2026-07-11
Origem: PRAXIUM / Aurora / frente operacional do livro
Status: EXECUCAO OPERACIONAL ATIVA — SEM INTERVENCAO NO TEXTO LITERARIO

## 1. Objetivo

Localizar, identificar e vincular as fontes do livro `O Pensamento` antes de qualquer extracao, comparacao, reorganizacao ou desenvolvimento de capitulos.

Este roteiro continua a tabela mestre de controle de fontes e preserva a regra de nao alterar o conteudo do livro enquanto a fonte de 23 capitulos e as demais versoes nao estiverem verificadas.

## 2. Fontes prioritarias

1. versao em PDF de `O Pensamento — O Livro Definitivo`;
2. versao DOCX de anotacoes, raciocinio primario ou manuscrito editavel;
3. versao TXT organizada do livro;
4. versao especifica com 23 capitulos;
5. comentarios, diagnosticos e listas de conceitos usados para comparar desenvolvimento e repeticoes.

## 3. Criterios de identificacao

Para cada arquivo localizado, registrar:

- nome original completo;
- extensao;
- tamanho;
- data de criacao e modificacao, quando disponiveis;
- local de origem;
- responsavel pela localizacao;
- numero aparente de capitulos;
- primeiro e ultimo titulo de capitulo;
- presenca de capitulos finais repetitivos;
- existencia de marcas de revisao, comentarios ou intervencao posterior;
- relacao provavel com as demais versoes.

Nenhuma conclusao editorial deve ser tomada apenas pelo nome do arquivo ou pela data do sistema.

## 4. Procedimento de recebimento

1. preservar o arquivo original sem renomear;
2. criar copia tecnica de trabalho;
3. calcular hash SHA-256 do original e da copia;
4. registrar metadados no manifesto individual;
5. atribuir o identificador tecnico da tabela mestre;
6. atualizar o estado para `RECEBIDO`;
7. realizar verificacao de integridade;
8. liberar para extracao somente apos registro completo.

## 5. Localizacao da versao de 23 capitulos

A versao de 23 capitulos deve ser tratada como fonte prioritaria, mas nao automaticamente como versao canonica.

Ao localiza-la, registrar:

- lista integral dos 23 titulos;
- extensao aproximada de cada capitulo;
- ponto em que o desenvolvimento perde densidade;
- repeticoes de conceitos, estruturas e estilo;
- trechos que apenas reformulam capitulos anteriores;
- diferenca entre ideia original, expansao valida e preenchimento por LLM;
- capitulos que exigem reconstrucao integral.

## 6. Estados de classificacao futura dos capitulos

Depois da extracao e comparacao, cada capitulo podera receber um dos seguintes estados:

- `CONSOLIDADO` — estrutura e desenvolvimento autoral suficientes;
- `APROVEITAVEL_COM_REVISAO` — base valida, mas exige depuracao;
- `REPETITIVO` — repete conceitos ou forma de capitulos anteriores sem avancar;
- `DERIVA_DE_LLM` — apresenta expansao automatica, imitacao de estilo ou preenchimento;
- `RECONSTRUCAO_NECESSARIA` — intencao aproveitavel, texto inadequado;
- `NAO VERIFICADO` — ainda sem evidencia suficiente.

Esses estados nao autorizam exclusao automatica nem substituem decisao editorial de Dante / Aurora / PRAXIUM.

## 7. Sequencia operacional

1. localizar as cinco fontes prioritarias;
2. preencher manifestos e hashes;
3. atualizar a tabela mestre;
4. extrair sumarios e titulos sem alterar conteudo;
5. identificar a versao de 23 capitulos;
6. produzir mapa de correspondencia entre capitulos;
7. marcar duplicacoes, lacunas e deriva de LLM;
8. montar diagnostico capitulo por capitulo;
9. submeter a validacao PRAXIUM;
10. somente depois iniciar estruturacao e desenvolvimento editorial.

## 8. Regra de continuidade

A frente deve ser tratada como continuidade do trabalho existente, nunca como reinicio do livro.

O desenvolvimento futuro deve:

- preservar o nucleo autoral;
- evitar imitar mecanicamente o estilo dos capitulos anteriores;
- eliminar repeticoes sem apagar conceitos validos;
- desenvolver apenas onde houver lacuna real;
- diferenciar claramente texto original, revisao e reconstrucao;
- manter historico rastreavel de cada intervencao.

## 9. Bloqueio atual

O conteudo literario permanece bloqueado enquanto a versao de 23 capitulos e as demais fontes nao estiverem acessiveis, verificadas e liberadas para comparacao.

A frente operacional, entretanto, permanece ativa para organizacao, rastreabilidade, localizacao, recebimento e preparacao tecnica.

## 10. Proxima entrega prevista

Apos o recebimento das fontes, criar:

`BOOK/28_INVENTARIO_ESTRUTURAL_23_CAPITULOS_O_PENSAMENTO.md`

Esse inventario devera conter apenas dados extraidos e verificaveis, sem reescrita dos capitulos.