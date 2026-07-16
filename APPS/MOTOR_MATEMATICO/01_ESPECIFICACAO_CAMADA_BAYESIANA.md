# ESPECIFICAÇÃO FORMAL — CAMADA BAYESIANA DA MÁSCARA PROBABILÍSTICA

Data: 2026-07-12
Versão: 1.0
Status: ATIVO
Entregável: #1

---

## 1. Objetivo

Incorporar à Máscara Probabilística do Motor Matemático uma camada formal de atualização bayesiana, capaz de revisar continuamente a probabilidade das hipóteses analisadas à medida que novas evidências forem recebidas.

A implementação não substitui os métodos estatísticos, matemáticos ou heurísticos já existentes. Atua como camada adicional de inferência, calibração e revisão probabilística.

---

## 2. Fundamento Matemático

### 2.1 Teorema de Bayes

```
P(H|E) = [P(E|H) × P(H)] / P(E)
```

| Símbolo | Significado |
|---|---|
| H | Hipótese analisada |
| E | Nova evidência observada |
| P(H) | Probabilidade anterior (prior) |
| P(E\|H) | Verossimilhança: probabilidade de observar E se H for verdadeira |
| P(E) | Probabilidade marginal da evidência (normalizador) |
| P(H\|E) | Probabilidade posterior atualizada |

### 2.2 Forma expandida do normalizador

```
P(E) = P(E|H) × P(H) + P(E|¬H) × P(¬H)
```

Onde `¬H` representa a negação da hipótese.

### 2.3 Forma de razão de verossimilhança (Bayes Factor)

```
Razão posterior = Razão prior × Razão de verossimilhança

P(H|E) / P(¬H|E) = [P(H) / P(¬H)] × [P(E|H) / P(E|¬H)]
```

O Bayes Factor `BF = P(E|H) / P(E|¬H)` quantifica o quanto a evidência E favorece H em relação a ¬H.

| Bayes Factor | Interpretação |
|---|---|
| BF > 100 | Evidência decisiva para H |
| 30 < BF ≤ 100 | Evidência muito forte para H |
| 10 < BF ≤ 30 | Evidência forte para H |
| 3 < BF ≤ 10 | Evidência moderada para H |
| 1 < BF ≤ 3 | Evidência fraca para H |
| BF = 1 | Evidência neutra |
| BF < 1 | Evidência contrária a H |

---

## 3. Integração com a Máscara Probabilística

A Máscara Probabilística passa a distinguir explicitamente os seguintes campos:

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `hipotese` | texto | sim | Enunciado claro e falsificável da hipótese |
| `probabilidade_anterior` | intervalo ou categoria | sim | Prior antes desta rodada de evidências |
| `evidencias_favoraveis` | lista | sim | Evidências que aumentam P(H) |
| `evidencias_contrarias` | lista | sim | Evidências que reduzem P(H) |
| `forca_evidencia` | categoria | sim | Peso de cada evidência |
| `qualidade_fonte` | categoria | sim | Confiabilidade da fonte |
| `independencia_evidencias` | categoria | sim | Grau de correlação entre evidências |
| `probabilidade_posterior` | intervalo ou categoria | sim | Resultado após atualização |
| `grau_confianca` | categoria | sim | Confiança na estimativa |
| `nivel_incerteza` | categoria | sim | Grau de incerteza remanescente |
| `condicoes_invalidacao` | lista | sim | O que tornaria a hipótese falsa |
| `proxima_evidencia_necessaria` | texto | sim | Evidência que dispararia nova atualização |
| `horizonte_temporal` | categoria | sim | Horizonte de validade da análise |
| `timestamp_atualizacao` | data/hora | sim | Momento da última atualização |

---

## 4. Classes de Evidência

### 4.1 Evidência Confirmatória
- Aumenta P(H)
- BF > 1
- Deve ser registrada com força e fonte

### 4.2 Evidência Contraditória
- Reduz P(H)
- BF < 1
- Deve receber mesmo rigor que confirmatória

### 4.3 Evidência Neutra
- Não altera materialmente P(H)
- BF ≈ 1 (faixa: 0,8 a 1,2)
- Deve ser registrada para completude do histórico

### 4.4 Evidência Redundante
- Repete informação já considerada
- Não deve ser contabilizada como independente
- Aumentar contador de redundância, não de força

### 4.5 Evidência de Baixa Confiabilidade
- Fonte não verificável, anônima ou conflitada
- Peso reduzido: no máximo 30% do peso padrão
- Registrar motivo da redução de peso

### 4.6 Evidência Estrutural
- Afeta a hipótese de forma duradoura
- Exemplos: mudança regulatória, fraude confirmada, quebra de tendência secular
- Decaimento lento (ver módulo de decaimento)

### 4.7 Evidência Conjuntural
- Afeta temporariamente a hipótese
- Exemplos: dado pontual de inflação, resultado trimestral único
- Decaimento rápido (ver módulo de decaimento)

---

## 5. Regras Contra Falsa Precisão

### 5.1 Categorias calibradas (quando não há base estatística suficiente)

| Categoria | Faixa indicativa |
|---|---|
| Muito baixa | < 10% |
| Baixa | 10% — 30% |
| Moderada | 30% — 60% |
| Alta | 60% — 80% |
| Muito alta | > 80% |

### 5.2 Registro obrigatório da origem da probabilidade

Toda probabilidade deve ser acompanhada de um dos seguintes rótulos:

- `FREQ_HISTORICA` — estimada por frequência observada em casos comparáveis
- `MODELO_ESTATISTICO` — inferida por modelo formal
- `SIMULACAO` — derivada de simulação computacional
- `ESPECIALISTA` — atribuída por especialista
- `HEURISTICA` — aproximada por regra heurística
- `INDETERMINAVEL` — não estimável com base disponível

### 5.3 Proibição de números arbitrários

O Motor não pode produzir probabilidades como "73,4%" sem base documentada.

Quando a precisão não for justificável, usar intervalo: "entre 60% e 75%".

---

## 6. Horizontes Temporais

| Horizonte | Janela | Taxa de Decaimento |
|---|---|---|
| Intradiário | < 1 dia | Muito rápida |
| Diário | 1 — 5 dias | Rápida |
| Semanal | 5 — 21 dias | Moderada |
| Mensal | 21 — 90 dias | Moderada |
| Trimestral | 90 — 365 dias | Lenta |
| Longo prazo | > 365 dias | Muito lenta |

Cada horizonte possui:
- prior próprio
- conjunto próprio de evidências relevantes
- janela de atualização
- taxa de decaimento específica
- critérios de invalidação
- custos operacionais correspondentes

---

## 7. Consistência Matemática

### 7.1 Restrições obrigatórias

- `0 ≤ P(H) ≤ 1` para qualquer hipótese H
- `P(H) + P(¬H) = 1`
- `P(H|E) ∈ [0, 1]`
- Posterior nunca pode ser exatamente 0 ou 1 (exceto após invalidação formal)

### 7.2 Verificações de sanidade

Antes de registrar um posterior, o Motor deve verificar:

1. O prior estava registrado antes de receber a evidência?
2. A verossimilhança P(E|H) é distinta de P(E|¬H)?
3. As evidências foram classificadas quanto à correlação?
4. O normalizador P(E) foi calculado corretamente?
5. O posterior está dentro do intervalo [0,1]?

---

## 8. Princípio de Disciplina Epistêmica

Bayes não deve ser usado como decoração matemática.

O Motor deve ser obrigado a declarar:

1. **O que acreditava antes** — prior explícito, com origem documentada
2. **Qual evidência recebeu** — descrição, fonte, data, classe
3. **Quanto essa evidência realmente vale** — Bayes Factor estimado, com justificativa
4. **Como ela alterou a conclusão** — posterior calculado, com rastreabilidade completa

Qualquer análise que não cumpra esses quatro requisitos não está usando a camada bayesiana — está apenas citando Bayes.
