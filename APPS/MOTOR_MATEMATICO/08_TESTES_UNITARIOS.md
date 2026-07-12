# TESTES UNITÁRIOS — CAMADA BAYESIANA

Data: 2026-07-12
Versão: 1.0
Status: ESPECIFICAÇÃO
Entregável: #8

---

## 1. Objetivo

Verificar o comportamento isolado de cada módulo da camada bayesiana com entradas controladas.

---

## 2. Módulo: Cálculo Bayesiano Básico

### TU-01 — Atualização com evidência confirmatória

```
Entrada:
  prior = 0,50
  P(E|H) = 0,80
  P(E|¬H) = 0,30

Cálculo esperado:
  P(E) = 0,80 × 0,50 + 0,30 × 0,50 = 0,55
  Posterior = (0,80 × 0,50) / 0,55 = 0,727

Resultado esperado: posterior ≈ 0,727
Estado esperado: HIPOTESE_FORTALECIDA
```

### TU-02 — Atualização com evidência contraditória

```
Entrada:
  prior = 0,60
  P(E|H) = 0,20
  P(E|¬H) = 0,70

Cálculo esperado:
  P(E) = 0,20 × 0,60 + 0,70 × 0,40 = 0,40
  Posterior = (0,20 × 0,60) / 0,40 = 0,30

Resultado esperado: posterior = 0,30
Estado esperado: HIPOTESE_FORTEMENTE_ENFRAQUECIDA
```

### TU-03 — Evidência neutra não altera prior

```
Entrada:
  prior = 0,45
  P(E|H) = 0,50
  P(E|¬H) = 0,50

Cálculo esperado:
  P(E) = 0,50 × 0,45 + 0,50 × 0,55 = 0,50
  Posterior = (0,50 × 0,45) / 0,50 = 0,45

Resultado esperado: posterior = prior = 0,45
Estado esperado: HIPOTESE_INALTERADA
```

### TU-04 — Prior extremo com evidência oposta

```
Entrada:
  prior = 0,95
  P(E|H) = 0,05
  P(E|¬H) = 0,90

Cálculo esperado:
  P(E) = 0,05 × 0,95 + 0,90 × 0,05 = 0,0925
  Posterior = (0,05 × 0,95) / 0,0925 ≈ 0,513

Resultado esperado: posterior ≈ 0,513
Verificação: evidência forte pode reverter prior alto, mas não colapsa a zero
```

### TU-05 — Posterior nunca ultrapassa [0,1]

```
Entrada: qualquer combinação de prior e verossimilhanças válidas
Resultado esperado: 0 ≤ posterior ≤ 1 sempre
```

---

## 3. Módulo: Priors

### TU-06 — Prior declarado antes de receber evidência

```
Condição: análise iniciada sem prior registrado
Resultado esperado: erro — análise bloqueada até prior ser declarado
```

### TU-07 — Prior histórico com amostra insuficiente

```
Condição: N < 30 casos históricos comparáveis
Resultado esperado: aviso de amostra insuficiente; sugestão de prior conservador
```

### TU-08 — Migração de posterior para prior da rodada seguinte

```
Rodada 1:
  prior_0 = 0,50
  posterior_1 = 0,65

Rodada 2:
  prior_declarado = 0,65 (= posterior_1)
  Resultado esperado: prior da rodada 2 aceito sem conflito

Rodada 2 com inconsistência:
  prior_declarado = 0,70 (diferente do posterior_1)
  Resultado esperado: aviso de inconsistência registrado
```

---

## 4. Módulo: Controle de Correlação

### TU-09 — Dupla contagem bloqueada

```
Entrada:
  EV-A: preço acima da MM20 (classe: confirmatória)
  EV-B: preço acima da MM50 (classe: confirmatória)
  Correlação EV-A + EV-B: altamente_correlacionada

Resultado esperado:
  dupla_contagem_detectada = true
  EV-B excluída (peso = 0)
  Atualização feita apenas com EV-A
```

### TU-10 — Evidência redundante não atualiza posterior

```
Entrada:
  EV-C: resultado acima do consenso (corretora X)
  EV-D: resultado acima do consenso (corretora Y) — mesma fonte primária
  EV-D classificada como: redundante

Resultado esperado:
  posterior após EV-C + EV-D = posterior após EV-C apenas
  EV-D registrada no histórico mas com peso = 0
```

### TU-11 — Ajuste de peso parcial

```
Entrada:
  EV-E e EV-F: parcialmente_correlacionadas
  fator_ajuste = 0,65

Resultado esperado:
  peso_aplicado(EV-E) = peso_bruto × 0,65
  peso_aplicado(EV-F) = peso_bruto × 0,65
```

---

## 5. Módulo: Decaimento Temporal

### TU-12 — Evidência com decaimento rápido após 10 dias

```
Tipo evidência: preço
Idade: 10 dias
Fator esperado: 0,20
Resultado esperado: peso_ajustado = peso_bruto × 0,20
```

### TU-13 — Evidência inativa não entra no posterior

```
Tipo evidência: preço
Idade: 20 dias
Fator esperado: 0,05 → status = inativa
Resultado esperado: evidência excluída do cálculo do posterior
```

### TU-14 — Evento de fraude sem resolução: sem decaimento

```
Tipo: fraude confirmada, sem resolução
Idade: 400 dias
Fator esperado: 1,00 (persistência elevada)
Resultado esperado: peso_ajustado = peso_bruto × 1,00
```

---

## 6. Módulo: Valor Esperado Líquido

### TU-15 — VEL negativo bloqueia operação

```
Entrada:
  P_ganho = 0,55
  Ganho_líquido = 200
  P_perda = 0,45
  Perda_líquida = 500

VEL = (0,55 × 200) − (0,45 × 500) = 110 − 225 = −115

Resultado esperado:
  favoravel = false
  estado_saida = DECISAO_ECONOMICAMENTE_DESFAVORAVEL
```

### TU-16 — VEL positivo mas inferior ao custo de oportunidade

```
VEL bruto = +30
Custo de oportunidade = +50
VEL ajustado = 30 − 50 = −20

Resultado esperado:
  favoravel = false
  observacao = "positivo antes do custo de oportunidade; negativo após"
```

### TU-17 — Probabilidade > 50% não garante VEL positivo

```
P_ganho = 0,60
Ganho_líquido = 50
P_perda = 0,40
Perda_líquida = 200

VEL = (0,60 × 50) − (0,40 × 200) = 30 − 80 = −50

Resultado esperado: favoravel = false
Nota: P_ganho > 50% não é condição suficiente
```

---

## 7. Módulo: Estados de Saída

### TU-18 — Mapeamento de variação para estado

| Variação do posterior | Estado esperado |
|---|---|
| Δ > +15 pp | HIPOTESE_FORTALECIDA |
| +5 pp < Δ ≤ +15 pp | HIPOTESE_MODERADAMENTE_FORTALECIDA |
| −5 pp ≤ Δ ≤ +5 pp | HIPOTESE_INALTERADA |
| −15 pp ≤ Δ < −5 pp | HIPOTESE_ENFRAQUECIDA |
| Δ < −15 pp | HIPOTESE_FORTEMENTE_ENFRAQUECIDA |

### TU-19 — Conflito entre evidências

```
Condição: BF de evidência confirmatória > 3 E BF de evidência contraditória < 0,33
  (evidências fortes em direções opostas)

Resultado esperado: estado_saida = CONFLITO_ENTRE_EVIDENCIAS
```

---

## 8. Resultado Esperado dos Testes

| Teste | Módulo | Criticidade | Status |
|---|---|---|---|
| TU-01 | Cálculo bayesiano | Alta | A executar |
| TU-02 | Cálculo bayesiano | Alta | A executar |
| TU-03 | Cálculo bayesiano | Alta | A executar |
| TU-04 | Cálculo bayesiano | Média | A executar |
| TU-05 | Cálculo bayesiano | Alta | A executar |
| TU-06 | Priors | Alta | A executar |
| TU-07 | Priors | Média | A executar |
| TU-08 | Priors | Alta | A executar |
| TU-09 | Correlação | Alta | A executar |
| TU-10 | Correlação | Alta | A executar |
| TU-11 | Correlação | Média | A executar |
| TU-12 | Decaimento | Alta | A executar |
| TU-13 | Decaimento | Alta | A executar |
| TU-14 | Decaimento | Alta | A executar |
| TU-15 | VEL | Alta | A executar |
| TU-16 | VEL | Alta | A executar |
| TU-17 | VEL | Alta | A executar |
| TU-18 | Estados | Média | A executar |
| TU-19 | Estados | Média | A executar |

**Critério de aprovação:** todos os testes de criticidade Alta devem passar. Falha em qualquer teste de criticidade Alta bloqueia a declaração de conclusão da camada.
