# RELATÓRIO DE CALIBRAÇÃO

Data: 2026-07-12
Versão: 1.0
Status: ESPECIFICAÇÃO — TEMPLATE ATIVO
Entregável: #11

---

## 1. Objetivo

Verificar se as probabilidades produzidas pelo Motor Matemático correspondem à frequência real de ocorrência dos eventos.

**Definição de calibração perfeita:**
Entre todas as previsões classificadas como 70%, o evento deve ocorrer em aproximadamente 70% dos casos.

---

## 2. Métricas de Calibração

### 2.1 Brier Score

```
BS = (1/N) × Σ (probabilidade_prevista_i − resultado_i)²
```

Onde `resultado_i = 1` se o evento ocorreu, `0` se não ocorreu.

| Brier Score | Interpretação |
|---|---|
| 0,00 | Calibração perfeita (impossível na prática) |
| < 0,10 | Excelente |
| 0,10 — 0,15 | Bom |
| 0,15 — 0,20 | Aceitável |
| 0,20 — 0,25 | Fraco |
| > 0,25 | Inadequado |

### 2.2 Log Loss (Cross-Entropy)

```
LL = −(1/N) × Σ [y_i × log(p_i) + (1−y_i) × log(1−p_i)]
```

Penaliza severamente probabilidades extremas incorretas (ex: prever 95% quando o evento não ocorre).

| Log Loss | Interpretação |
|---|---|
| < 0,30 | Excelente |
| 0,30 — 0,45 | Bom |
| 0,45 — 0,60 | Aceitável |
| > 0,60 | Fraco |

### 2.3 Curva de Calibração

Agrupar previsões em faixas e calcular a taxa real de acerto por faixa:

| Faixa de probabilidade prevista | Taxa real de acerto esperada | Taxa real observada |
|---|---|---|
| 0% — 10% | ~5% | A medir |
| 10% — 20% | ~15% | A medir |
| 20% — 30% | ~25% | A medir |
| 30% — 40% | ~35% | A medir |
| 40% — 50% | ~45% | A medir |
| 50% — 60% | ~55% | A medir |
| 60% — 70% | ~65% | A medir |
| 70% — 80% | ~75% | A medir |
| 80% — 90% | ~85% | A medir |
| 90% — 100% | ~95% | A medir |

**Diagnóstico por desvio:**
- Taxa real consistentemente acima da prevista → modelo subestima probabilidade (underconfident)
- Taxa real consistentemente abaixo da prevista → modelo superestima probabilidade (overconfident)

### 2.4 Taxa de Acerto por Faixa de Probabilidade

Calculada para cada faixa de categoria (muito baixa / baixa / moderada / alta / muito alta).

### 2.5 Estabilidade Fora da Amostra

```
Degradação = Brier_Score_fora_amostra − Brier_Score_dentro_amostra
```

- Degradação < 0,03: modelo estável
- 0,03 ≤ Degradação < 0,08: degradação moderada
- Degradação ≥ 0,08: modelo instável (overfitting provável)

### 2.6 Sensibilidade a Mudanças de Prior

Executar o modelo com priors alternativos (±20% em relação ao prior central) e medir variação do Brier Score.

- Variação < 0,02: baixa sensibilidade (robusto ao prior)
- 0,02 ≤ Variação < 0,05: sensibilidade moderada
- Variação ≥ 0,05: alta sensibilidade (conclusões dependentes do prior)

### 2.7 Robustez por Regime de Mercado

| Regime | Definição | Brier Score | Status |
|---|---|---|---|
| Bull market | Índice +20% no período | A medir | A executar |
| Bear market | Índice −20% no período | A medir | A executar |
| Mercado lateral | Variação entre −10% e +10% | A medir | A executar |
| Crise aguda | Queda > 30% em < 3 meses | A medir | A executar |

**Meta:** diferença entre melhor e pior regime < 0,08 no Brier Score.

---

## 3. Desempenho Após Custos

A calibração de probabilidades é condição necessária, mas não suficiente.

O Motor deve também medir se as operações com VEL positivo ex-ante realmente geraram VEL positivo ex-post:

| Métrica | Definição |
|---|---|
| Razão VEL ex-ante / VEL ex-post | Quanto do VEL previsto foi realizado |
| Taxa de operações com VEL positivo que geraram retorno positivo | Consistência da previsão de VEL |
| Distribuição real dos retornos vs. prevista | Verificar se as caudas são maiores que o previsto |

---

## 4. Frequência de Recalibração

| Situação | Ação |
|---|---|
| A cada 6 meses | Recalcular todas as métricas com novos dados |
| Brier Score piora > 0,05 | Recalibração imediata |
| Mudança de regime detectada | Recalibração imediata |
| Novo horizonte ou ativo adicionado | Calibração inicial antes de operar |

---

## 5. Template de Relatório de Calibração

```yaml
relatorio_calibracao:
  id: "CAL-YYYYMMDD-001"
  data_relatorio: "AAAA-MM-DD"
  periodo_avaliado_inicio: "AAAA-MM-DD"
  periodo_avaliado_fim: "AAAA-MM-DD"
  n_previsoes: 0
  horizonte: "mensal"
  
  metricas_gerais:
    brier_score: 0.0
    log_loss: 0.0
    taxa_acerto_global: 0.0
    degradacao_fora_amostra: 0.0
    sensibilidade_prior: "baixa | moderada | alta"
  
  curva_calibracao:
    faixa_0_10:
      n_previsoes: 0
      taxa_real_observada: 0.0
    faixa_10_20:
      n_previsoes: 0
      taxa_real_observada: 0.0
    faixa_20_30:
      n_previsoes: 0
      taxa_real_observada: 0.0
    faixa_30_40:
      n_previsoes: 0
      taxa_real_observada: 0.0
    faixa_40_50:
      n_previsoes: 0
      taxa_real_observada: 0.0
    faixa_50_60:
      n_previsoes: 0
      taxa_real_observada: 0.0
    faixa_60_70:
      n_previsoes: 0
      taxa_real_observada: 0.0
    faixa_70_80:
      n_previsoes: 0
      taxa_real_observada: 0.0
    faixa_80_90:
      n_previsoes: 0
      taxa_real_observada: 0.0
    faixa_90_100:
      n_previsoes: 0
      taxa_real_observada: 0.0
  
  robustez_por_regime:
    bull_market:
      brier_score: 0.0
    bear_market:
      brier_score: 0.0
    lateral:
      brier_score: 0.0
    crise_aguda:
      brier_score: 0.0
    diferenca_max_min: 0.0
    robusto: true
  
  diagnostico:
    viés: "subestima | superestima | sem viés identificado"
    estavel: true
    requer_recalibracao: false
    notas: "observações"
```
