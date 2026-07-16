# BACKTEST FORA DA AMOSTRA — PROTOCOLO

Data: 2026-07-12
Versão: 1.0
Status: ESPECIFICAÇÃO
Entregável: #10

---

## 1. Objetivo

Verificar se a camada bayesiana produz resultados superiores aos modelos de referência em dados que não foram utilizados para calibrar o modelo.

O desempenho dentro da amostra não valida um modelo. O único teste relevante é o desempenho fora da amostra.

---

## 2. Separação de Dados

### 2.1 Divisão temporal obrigatória

```
Amostra de treino/calibração: período histórico anterior ao corte
Amostra de teste (out-of-sample): período após o corte, nunca visto durante calibração
```

| Horizonte da análise | Período mínimo de treino | Período mínimo de teste |
|---|---|---|
| Intradiário | 6 meses | 3 meses |
| Diário | 2 anos | 1 ano |
| Semanal | 3 anos | 1 ano |
| Mensal | 5 anos | 2 anos |
| Trimestral | 7 anos | 3 anos |
| Longo prazo | 10 anos | 5 anos |

### 2.2 Proibições absolutas

- **Proibido**: usar dados do período de teste para ajustar priors ou verossimilhanças
- **Proibido**: rever parâmetros após ver os resultados do teste e declarar sucesso com os novos parâmetros
- **Proibido**: selecionar o período de teste com base em onde o modelo performa melhor
- **Proibido**: tratar o período de teste como amostra adicional de treino e repetir o processo

---

## 3. Modelos de Referência Obrigatórios

A camada bayesiana deve ser comparada contra no mínimo cinco modelos de referência:

| Modelo | Descrição |
|---|---|
| M0 — Sem atualização | Prior fixo durante todo o período, sem atualização |
| M1 — Regra simples | Decisão baseada em único indicador (ex: preço vs. MM200) |
| M2 — Benchmark de mercado | Buy and hold no índice de referência (Ibovespa / S&P 500) |
| M3 — Modelo aleatório | Previsão aleatória calibrada com a frequência base histórica |
| M4 — Modelo anterior | Máscara Probabilística sem a camada bayesiana |

---

## 4. Métricas de Comparação

### 4.1 Métricas de calibração

| Métrica | Definição | Meta |
|---|---|---|
| Brier Score | Erro quadrático médio das probabilidades | Menor que M4 e M1 |
| Log Loss | Penalidade por probabilidades extremas incorretas | Menor que M4 e M1 |
| Curva de calibração | % de acertos por faixa de probabilidade | Mais próxima da diagonal |

### 4.2 Métricas de desempenho financeiro

| Métrica | Definição |
|---|---|
| Retorno total após custos | Soma dos retornos líquidos gerados |
| Sharpe ratio | Retorno / Desvio padrão (benchmark: CDI ou índice) |
| Máximo drawdown | Maior queda de pico a vale |
| Taxa de acerto | Proporção de operações corretas |
| Payoff ratio | Ganho médio / Perda média |
| VEL médio por operação | Valor esperado líquido médio realizado |

### 4.3 Métricas de robustez

| Métrica | Definição |
|---|---|
| Desempenho por regime | Resultado separado por mercado bull, bear, lateral |
| Sensibilidade ao prior | Variação do resultado ao mudar prior em ±20% |
| Estabilidade temporal | Desempenho consistente ao longo do período de teste |
| Resultado em mercados extremos | Desempenho em crises (quedas > 30% do índice) |

---

## 5. Procedimento de Execução do Backtest

**Passo 1 — Congelar parâmetros**
- Registrar todos os parâmetros do modelo (priors, verossimilhanças, fatores de decaimento, limites de correlação) antes de iniciar o teste
- Calcular hash dos parâmetros para rastreabilidade

**Passo 2 — Aplicar modelo ao período de teste**
- Processar evidências na ordem cronológica exata em que ocorreram
- Nunca usar informação de t+1 em t
- Registrar cada decisão e seu fundamento

**Passo 3 — Registrar resultados**
- Registrar resultado de cada operação simulada
- Calcular todas as métricas da seção 4

**Passo 4 — Comparar com modelos de referência**
- Calcular as mesmas métricas para M0, M1, M2, M3 e M4 no mesmo período
- Preencher tabela de comparação

**Passo 5 — Avaliar critério de adoção**

---

## 6. Critério de Adoção

A camada bayesiana é considerada útil se demonstrar melhora robusta em pelo menos 4 das 6 dimensões abaixo:

| Dimensão | Condição de melhora |
|---|---|
| Calibração | Brier Score menor que M4 e M1 |
| Valor esperado | VEL médio por operação maior que M4 e M2 |
| Controle de risco | Drawdown menor que M4 e M2 |
| Estabilidade | Desempenho consistente em pelo menos 2 dos 3 regimes testados |
| Interpretabilidade | Decisões com rastreabilidade completa (não comparável a M3) |
| Fora da amostra | Degradação de desempenho fora da amostra menor que M4 |

Se a camada bayesiana não superar esses critérios, o resultado deve ser documentado e reportado. **A camada não deve ser incorporada formalmente se não demonstrar valor adicional.**

---

## 7. Template de Relatório de Backtest

```yaml
backtest:
  id: "BT-YYYYMMDD-001"
  modelo_testado: "camada_bayesiana_v1.0"
  data_execucao: "AAAA-MM-DD"
  
  dados:
    ativo_ou_universo: "descrição"
    periodo_treino_inicio: "AAAA-MM-DD"
    periodo_treino_fim: "AAAA-MM-DD"
    periodo_teste_inicio: "AAAA-MM-DD"
    periodo_teste_fim: "AAAA-MM-DD"
    n_operacoes_teste: 0
    hash_parametros: "sha256 dos parâmetros congelados"
  
  resultados_modelo_bayesiano:
    brier_score: 0.0
    log_loss: 0.0
    taxa_acerto: 0.0
    sharpe_ratio: 0.0
    maximo_drawdown: 0.0
    vel_medio_operacao: 0.0
  
  resultados_modelos_referencia:
    M0_sem_atualizacao:
      brier_score: 0.0
      sharpe_ratio: 0.0
    M1_regra_simples:
      brier_score: 0.0
      sharpe_ratio: 0.0
    M2_benchmark:
      sharpe_ratio: 0.0
    M3_aleatorio:
      brier_score: 0.0
    M4_mascara_anterior:
      brier_score: 0.0
      sharpe_ratio: 0.0
  
  criterio_adocao:
    dimensoes_superadas: 0
    dimensoes_necessarias: 4
    recomendacao: "adotar | nao_adotar | investigar"
    justificativa: "texto"
  
  limitacoes_identificadas:
    - "limitação 1"
    - "limitação 2"
```
