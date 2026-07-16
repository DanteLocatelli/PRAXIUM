# COMPARAÇÃO COM O MODELO ATUAL

Data: 2026-07-12
Versão: 1.0
Status: ESPECIFICAÇÃO — A EXECUTAR
Entregável: #12

---

## 1. Objetivo

Demonstrar que a camada bayesiana acrescenta valor mensurável em relação ao modelo anterior da Máscara Probabilística, antes de declará-la incorporada formalmente.

---

## 2. Definição dos Modelos

| ID | Modelo | Descrição |
|---|---|---|
| M4 | Máscara Probabilística anterior | Modelo antes da incorporação da camada bayesiana |
| MB | Máscara Probabilística com camada bayesiana | Modelo com todos os módulos desta especificação |

---

## 3. Eixos de Comparação

A camada bayesiana deve ser superior em pelo menos 4 dos 6 eixos para ser considerada útil.

### Eixo 1 — Calibração

| Métrica | M4 (anterior) | MB (bayesiano) | MB melhor? |
|---|---|---|---|
| Brier Score | A medir | A medir | A verificar |
| Log Loss | A medir | A medir | A verificar |
| Desvio na curva de calibração | A medir | A medir | A verificar |

**Critério:** MB deve ter Brier Score inferior ao M4.

### Eixo 2 — Valor Esperado

| Métrica | M4 | MB | MB melhor? |
|---|---|---|---|
| VEL médio por operação | A medir | A medir | A verificar |
| % de operações com VEL positivo | A medir | A medir | A verificar |
| Retorno total após custos | A medir | A medir | A verificar |

**Critério:** MB deve ter VEL médio superior ao M4.

### Eixo 3 — Controle de Risco

| Métrica | M4 | MB | MB melhor? |
|---|---|---|---|
| Máximo drawdown | A medir | A medir | A verificar |
| Sharpe ratio | A medir | A medir | A verificar |
| Frequência de alertas de risco gerados | A medir | A medir | A verificar |

**Critério:** MB deve ter drawdown menor ou Sharpe superior ao M4.

### Eixo 4 — Estabilidade

| Métrica | M4 | MB | MB melhor? |
|---|---|---|---|
| Degradação fora da amostra | A medir | A medir | A verificar |
| Consistência entre regimes | A medir | A medir | A verificar |
| Sensibilidade a prior | A medir | A medir | A verificar |

**Critério:** MB deve ter degradação fora da amostra menor ou igual a M4.

### Eixo 5 — Interpretabilidade

| Dimensão | M4 | MB |
|---|---|---|
| Prior explicitamente declarado | Não | Sim |
| Evidências classificadas | Parcial | Sim |
| Sequência de atualização rastreável | Não | Sim |
| Dupla contagem controlada | Não | Sim |
| Origem da probabilidade documentada | Não | Sim |
| Condições de invalidação definidas | Parcial | Sim |

**Critério:** MB é estruturalmente superior em interpretabilidade.

### Eixo 6 — Desempenho Fora da Amostra

| Métrica | M4 | MB | MB melhor? |
|---|---|---|---|
| Brier Score (fora da amostra) | A medir | A medir | A verificar |
| Retorno (fora da amostra) | A medir | A medir | A verificar |

**Critério:** MB deve demonstrar desempenho fora da amostra melhor ou equivalente ao M4.

---

## 4. Resultado da Comparação

```yaml
comparacao_modelos:
  data: "AAAA-MM-DD"
  periodo_avaliado: "AAAA-MM-DD a AAAA-MM-DD"
  
  eixo_1_calibracao:
    m4_brier_score: 0.0
    mb_brier_score: 0.0
    mb_superior: false
  
  eixo_2_valor_esperado:
    m4_vel_medio: 0.0
    mb_vel_medio: 0.0
    mb_superior: false
  
  eixo_3_risco:
    m4_drawdown: 0.0
    mb_drawdown: 0.0
    m4_sharpe: 0.0
    mb_sharpe: 0.0
    mb_superior: false
  
  eixo_4_estabilidade:
    m4_degradacao: 0.0
    mb_degradacao: 0.0
    mb_superior: false
  
  eixo_5_interpretabilidade:
    mb_superior: true
    justificativa: "rastreabilidade e transparência estruturalmente melhores"
  
  eixo_6_fora_amostra:
    m4_brier_fora: 0.0
    mb_brier_fora: 0.0
    mb_superior: false
  
  resultado:
    eixos_com_melhora_mb: 0
    eixos_necessarios: 4
    incorporar: false
    status: "A EXECUTAR"
    notas: "comparação pendente de dados reais"
```

---

## 5. Decisão de Incorporação

| Resultado | Decisão |
|---|---|
| MB superior em ≥ 4 eixos | Incorporar formalmente |
| MB superior em 3 eixos | Investigar causas; incorporar com ressalvas documentadas |
| MB superior em ≤ 2 eixos | Não incorporar; registrar limitações; revisar especificação |

**A decisão final de incorporação cabe a Dante.**

O Motor Matemático deve apresentar os resultados da comparação e aguardar confirmação humana antes de declarar a camada bayesiana como componente oficial da Máscara Probabilística.
