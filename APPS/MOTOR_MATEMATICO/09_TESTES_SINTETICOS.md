# TESTES SINTÉTICOS — CENÁRIOS CONTROLADOS

Data: 2026-07-12
Versão: 1.0
Status: ESPECIFICAÇÃO
Entregável: #9

---

## 1. Objetivo

Testar o comportamento do sistema em cenários completos e controlados, com múltiplas rodadas de atualização, cobrindo interações entre módulos que testes unitários não capturam individualmente.

---

## 2. Cenário TS-01 — Atualização Sequencial Simples

**Hipótese:** continuidade de tendência de alta em ativo fictício AXY3

**Rodada 0 — Prior inicial**
```
Prior: 0,50 (não informativo)
Origem: HEURISTICA
Justificativa: sem histórico suficiente comparável
```

**Rodada 1 — Evidência confirmatória forte**
```
EV-01: Rompimento de resistência com volume 3× a média
Classe: confirmatória
P(E|H) = 0,75 | P(E|¬H) = 0,25
P(E) = 0,75 × 0,50 + 0,25 × 0,50 = 0,50
Posterior_1 = (0,75 × 0,50) / 0,50 = 0,75
Estado: HIPOTESE_FORTALECIDA
```

**Rodada 2 — Evidência contraditória moderada**
```
EV-02: Volume decrescente nos 3 dias seguintes
Classe: contraditória
P(E|H) = 0,35 | P(E|¬H) = 0,60
Prior = 0,75 (= Posterior_1)
P(E) = 0,35 × 0,75 + 0,60 × 0,25 = 0,4125
Posterior_2 = (0,35 × 0,75) / 0,4125 = 0,636
Estado: HIPOTESE_ENFRAQUECIDA (em relação a Posterior_1)
```

**Rodada 3 — Evidência neutra**
```
EV-03: IPCA dentro do esperado (dado macro sem relação direta)
Classe: neutra
P(E|H) = 0,50 | P(E|¬H) = 0,50
Prior = 0,636
Posterior_3 = 0,636 (inalterado)
Estado: HIPOTESE_INALTERADA
```

**Verificações obrigatórias:**
- Posterior_1 = 0,75 ✓
- Posterior_2 < Posterior_1 ✓
- Posterior_3 = Posterior_2 ✓ (evidência neutra não altera)
- Histórico de 3 rodadas preservado ✓

---

## 3. Cenário TS-02 — Detecção e Bloqueio de Dupla Contagem

**Hipótese:** valorização de ativo BCD4 no horizonte semanal

**Evidências candidatas:**
```
EV-A: preço acima da MM20 (confirmatória)
EV-B: preço acima da MM50 (confirmatória)
EV-C: preço no maior valor dos últimos 30 dias (confirmatória)
EV-D: resultado trimestral acima do consenso (confirmatória)
EV-E: mesma notícia do resultado, fonte secundária (redundante de EV-D)
```

**Classificação de correlação esperada:**
```
Grupo 1: [EV-A, EV-B, EV-C] → altamente_correlacionadas (mesmo movimento de preço)
  → Manter EV-C (mais informativa); excluir EV-A e EV-B
Grupo 2: [EV-D, EV-E] → EV-E é redundante de EV-D
  → Manter EV-D; excluir EV-E
EV-C e EV-D: independentes (preço vs. fundamentos)
  → Ambas entram com peso integral
```

**Atualização esperada:**
```
Prior = 0,50
Atualizar com EV-C (confirmatória), depois com EV-D (confirmatória)
Posterior deve refletir apenas 2 evidências efetivas, não 5
```

**Verificações obrigatórias:**
- `dupla_contagem_detectada = true`
- `evidencias_excluidas_por_correlacao = [EV-A, EV-B, EV-E]`
- `total_evidencias_independentes_efetivas = 2`
- Posterior condizente com 2 evidências confirmatórias, não 5

---

## 4. Cenário TS-03 — Decaimento e Rejeição de Evidência Inativa

**Análise de horizonte semanal, realizada 20 dias após os dados**

**Evidências:**
```
EV-01: preço rompeu resistência (coletado há 20 dias)
  → Tipo de decaimento: rápido
  → Idade: 20 dias → fator = 0,05 → status = inativa

EV-02: resultado trimestral acima do consenso (coletado há 20 dias)
  → Tipo de decaimento: trimestral
  → Idade: 20 dias → fator = 1,00 → status = ativa
```

**Resultado esperado:**
```
EV-01: excluída do cálculo (inativa)
EV-02: incluída com peso integral
Posterior calculado somente com EV-02
Aviso gerado: "EV-01 inativa por decaimento"
```

**Verificações obrigatórias:**
- EV-01 não participa do cálculo do posterior
- EV-01 permanece no histórico como registrada
- EV-02 recebe peso integral

---

## 5. Cenário TS-04 — Decisão Economicamente Desfavorável com VEL Negativo

**Hipótese:** valorização de XYZ3 em 10% no horizonte mensal

**Dados:**
```
Posterior bayesiano: 0,58 (P_ganho = 0,58)
P_perda = 0,42
Ganho bruto esperado: R$ 200
Perda bruta esperada: R$ 600
Custos totais: R$ 40
Ganho líquido = 200 − 40 = 160
Perda líquida = 600 + 40 = 640
Custo de oportunidade (CDI 3 meses): R$ 80
```

**Cálculo:**
```
VEL bruto = (0,58 × 160) − (0,42 × 640) = 92,80 − 268,80 = −176,00
VEL ajustado = −176,00 − 80,00 = −256,00
```

**Resultado esperado:**
```
favoravel = false
estado_saida = DECISAO_ECONOMICAMENTE_DESFAVORAVEL
VEL_final = −256,00
Nota: posterior de 58% é insuficiente dado o desequilíbrio de tamanhos
```

**Verificações obrigatórias:**
- Sistema bloqueia operação mesmo com P_ganho > 50%
- Custos explicitamente registrados
- Custo de oportunidade incorporado

---

## 6. Cenário TS-05 — Conflito Entre Evidências

**Hipótese:** continuidade de tendência de alta em EFG5

**Evidências:**
```
EV-BULL: Rompimento com volume forte
  BF = 4,0 (evidência forte a favor)

EV-BEAR: Resultado trimestral muito abaixo do consenso
  BF = 0,20 (evidência forte contra)
```

**Condição de conflito:**
```
BF(EV-BULL) > 3 E BF(EV-BEAR) < 0,33 → conflito ativado
```

**Resultado esperado:**
```
estado_saida = CONFLITO_ENTRE_EVIDENCIAS
posterior = calculado, mas marcado como de baixa confiança
nivel_incerteza = alto
Recomendação: aguardar resolução do conflito
```

**Verificações obrigatórias:**
- Estado = CONFLITO_ENTRE_EVIDENCIAS
- Sistema não promove decisão de operação neste estado
- Histórico preserva ambas as evidências

---

## 7. Cenário TS-06 — Análise Multi-Horizonte

**Ativo:** HIJ6

**Horizonte intradiário:**
```
Prior: 0,55 (baseado na abertura do dia)
Evidências: fluxo de ordens, spread, momentum 5 minutos
Posterior: 0,62
Decaimento: rápido (evidências expiram em < 1 dia)
```

**Horizonte trimestral:**
```
Prior: 0,60 (baseado em qualidade dos fundamentos)
Evidências: lucro, margem, fluxo de caixa (resultado recente)
Posterior: 0,70
Decaimento: trimestral
```

**Verificações obrigatórias:**
- Priors distintos para cada horizonte
- Evidências distintas por horizonte
- Posterior intradiário não contamina posterior trimestral
- Evidências de preço intradiário recebem peso próximo de zero na análise trimestral

---

## 8. Resultado Esperado dos Cenários

| Cenário | Foco | Criticidade | Status |
|---|---|---|---|
| TS-01 | Sequência bayesiana correta | Alta | A executar |
| TS-02 | Controle de dupla contagem | Alta | A executar |
| TS-03 | Decaimento e exclusão de evidência inativa | Alta | A executar |
| TS-04 | VEL negativo bloqueia operação | Alta | A executar |
| TS-05 | Detecção de conflito entre evidências | Média | A executar |
| TS-06 | Separação de horizontes temporais | Média | A executar |

**Critério de aprovação:** todos os cenários de criticidade Alta devem produzir os resultados esperados. Desvio em cenário de criticidade Alta é bloqueante.
