# MOTOR MATEMÁTICO — CAMADA BAYESIANA DA MÁSCARA PROBABILÍSTICA

Data de criação: 2026-07-12
Origem: Dante Locatelli / Diretriz Executável
Status: ESPECIFICAÇÃO FORMAL — IMPLEMENTAÇÃO ATIVA
Versão: 1.0

---

## Propósito

Este diretório contém a especificação formal, os módulos operacionais e a documentação de auditoria da Camada Bayesiana incorporada à Máscara Probabilística do Motor Matemático PRAXIUM.

A camada bayesiana **não substitui** os métodos estatísticos, matemáticos ou heurísticos já existentes. Ela atua como **camada adicional de inferência, calibração e revisão probabilística**, obrigando o Motor a declarar:

- o que acreditava antes (prior);
- qual evidência recebeu;
- quanto essa evidência realmente vale;
- como ela alterou a conclusão (posterior).

---

## Princípio Central

> Toda conclusão do sistema deve ser tratada como uma hipótese probabilística provisória, nunca como uma certeza definitiva.

A cada nova evidência, o sistema atualiza a probabilidade anterior por:

```
P(H|E) = [P(E|H) × P(H)] / P(E)
```

Onde:
- **H** = hipótese analisada
- **E** = nova evidência observada
- **P(H)** = probabilidade anterior (prior)
- **P(E|H)** = verossimilhança da evidência dado H
- **P(H|E)** = probabilidade posterior atualizada

---

## Índice de Arquivos

| Arquivo | Conteúdo | Entregável |
|---|---|---|
| `01_ESPECIFICACAO_CAMADA_BAYESIANA.md` | Especificação formal completa | #1 |
| `02_ESQUEMA_DADOS_MASCARA_PROBABILISTICA.md` | Esquema de dados e campos obrigatórios | #2 |
| `03_MODULO_PRIORS.md` | Módulo de probabilidades iniciais | #3 |
| `04_MODULO_ATUALIZACAO_POSTERIOR.md` | Módulo de atualização sequencial | #4 |
| `05_CONTROLE_CORRELACAO_EVIDENCIAS.md` | Controle de correlação e dupla contagem | #5 |
| `06_DECAIMENTO_TEMPORAL.md` | Mecanismo de decaimento temporal | #6 |
| `07_VALOR_ESPERADO_LIQUIDO.md` | Cálculo de valor esperado líquido | #7 |
| `08_TESTES_UNITARIOS.md` | Testes unitários por módulo | #8 |
| `09_TESTES_SINTETICOS.md` | Testes sintéticos controlados | #9 |
| `10_BACKTEST_FORA_AMOSTRA.md` | Protocolo de backtest fora da amostra | #10 |
| `11_RELATORIO_CALIBRACAO.md` | Métricas e relatório de calibração | #11 |
| `12_COMPARACAO_MODELO_ATUAL.md` | Comparação com modelo anterior | #12 |
| `13_LIMITACOES.md` | Registro formal de limitações | #13 |
| `14_DOCUMENTACAO_AUDITORIA.md` | Rastreabilidade e auditoria | #14 |

---

## Gate de Segurança — Proibições Absolutas

O Motor Matemático **não pode**:

1. Transformar probabilidade em certeza
2. Utilizar evidência futura (data snooping)
3. Contaminar teste com dados posteriores (look-ahead bias)
4. Contar evidências correlacionadas como independentes
5. Ajustar priors para confirmar resultado desejado
6. Ignorar custos operacionais
7. Confundir correlação com causalidade
8. Promover modelo apenas por bom desempenho dentro da amostra

---

## Estados de Saída da Máscara Probabilística

| Estado | Descrição |
|---|---|
| `HIPOTESE_FORTALECIDA` | Evidências aumentam materialmente a probabilidade |
| `HIPOTESE_MODERADAMENTE_FORTALECIDA` | Evidências aumentam levemente a probabilidade |
| `HIPOTESE_INALTERADA` | Evidências neutras ou redundantes |
| `HIPOTESE_ENFRAQUECIDA` | Evidências reduzem a probabilidade |
| `HIPOTESE_FORTEMENTE_ENFRAQUECIDA` | Evidências contradizem fortemente |
| `EVIDENCIA_INSUFICIENTE` | Não há base para atualização confiável |
| `CONFLITO_ENTRE_EVIDENCIAS` | Evidências apontam direções opostas |
| `PROBABILIDADE_NAO_CALIBRADA` | Probabilidade não pode ser estimada com rigor |
| `DECISAO_ECONOMICAMENTE_DESFAVORAVEL` | Valor esperado líquido negativo |
| `AGUARDAR_NOVA_EVIDENCIA` | Próxima atualização necessária identificada |

---

## Critério de Conclusão

A integração somente é declarada concluída quando:

- [ ] Formulação matematicamente consistente
- [ ] Priors documentados
- [ ] Evidências rastreáveis
- [ ] Dupla contagem controlada
- [ ] Atualização sequencial testada
- [ ] Resultados calibrados
- [ ] Custos incorporados
- [ ] Desempenho fora da amostra medido
- [ ] Limitações explicitadas
- [ ] Camada bayesiana demonstra valor adicional sobre modelo anterior
