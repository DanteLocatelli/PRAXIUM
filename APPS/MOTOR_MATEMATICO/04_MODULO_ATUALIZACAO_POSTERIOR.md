# MÓDULO DE ATUALIZAÇÃO POSTERIOR — SEQUÊNCIA BAYESIANA

Data: 2026-07-12
Versão: 1.0
Status: ATIVO
Entregável: #4

---

## 1. Definição

O módulo de atualização posterior é responsável por calcular a probabilidade revisada da hipótese após incorporar novas evidências ao prior declarado.

O cálculo deve ser rastreável, documentado e reversível.

---

## 2. Algoritmo de Atualização

### 2.1 Forma analítica (evidência binária)

Dado:
- `P(H)` = prior
- `P(E|H)` = probabilidade da evidência ser observada se H for verdadeira
- `P(E|¬H)` = probabilidade da evidência ser observada se H for falsa

Calcular:
```
P(E) = P(E|H) × P(H) + P(E|¬H) × P(¬H)
P(H|E) = [P(E|H) × P(H)] / P(E)
```

### 2.2 Forma sequencial com múltiplas evidências

Quando há N evidências independentes E₁, E₂, ..., Eₙ:

```
Posterior_1 = atualização com E₁ usando Prior_0
Posterior_2 = atualização com E₂ usando Posterior_1 como prior
Posterior_k = atualização com Eₖ usando Posterior_(k-1) como prior
```

**Condição:** as evidências E₁, ..., Eₙ devem ser independentes entre si.

Se não forem independentes, aplicar controle de correlação (ver módulo 05) antes de combinar.

### 2.3 Forma qualitativa (quando probabilidades numéricas não são justificáveis)

Quando não há base para estimar P(E|H) numericamente, usar escala ordinal:

| Classe da Evidência | Ajuste qualitativo |
|---|---|
| Confirmatória muito forte | Subir 2 categorias na escala |
| Confirmatória forte | Subir 1 categoria |
| Confirmatória moderada | Subir ½ categoria |
| Neutra | Sem alteração |
| Contraditória moderada | Descer ½ categoria |
| Contraditória forte | Descer 1 categoria |
| Contraditória muito forte | Descer 2 categorias |

**Escala de categorias:**
```
Muito baixa → Baixa → Moderada → Alta → Muito alta
```

O Motor deve registrar quando utilizou forma qualitativa e por quê.

---

## 3. Procedimento Formal de Atualização

Para cada rodada de atualização:

**Passo 1 — Declarar o prior**
- Registrar `prior` e `origem_prior` antes de qualquer evidência

**Passo 2 — Listar evidências da rodada**
- Registrar cada evidência com classe, força e fonte
- Separar confirmatórias das contraditórias

**Passo 3 — Verificar correlação**
- Para cada par de evidências, verificar independência
- Excluir ou ajustar evidências correlacionadas (módulo 05)

**Passo 4 — Calcular P(E|H) e P(E|¬H) para cada evidência independente**
- Documentar o método de estimativa
- Registrar nível de incerteza desta estimativa

**Passo 5 — Calcular posterior**
- Aplicar fórmula de Bayes
- Registrar resultado como intervalo quando incerteza for alta

**Passo 6 — Verificações de sanidade**
- `posterior ∈ [0,1]`
- `posterior ≠ 0` e `posterior ≠ 1` (exceto invalidação formal)
- Posterior com evidências apenas neutras = prior (sem variação)
- Posterior com evidências apenas redundantes = prior (sem variação)

**Passo 7 — Registrar estado**
- Gravar rodada completa no histórico
- Calcular variação: `Δ = posterior − prior`
- Determinar estado de saída

---

## 4. Estimativa de P(E|H) e P(E|¬H)

A qualidade da atualização depende diretamente da qualidade dessas estimativas.

### 4.1 Métodos de estimativa

| Método | Quando usar | Confiabilidade |
|---|---|---|
| Frequência histórica | Há histórico suficiente do dado em contextos similares | Alta |
| Modelo estatístico | Há modelo calibrado para o fenômeno | Alta |
| Consenso de especialistas | Domínio com especialistas identificáveis | Média |
| Analogia com proxy | Dado similar com histórico disponível | Média |
| Estimativa conservadora | Sem base suficiente | Baixa |

### 4.2 Valores de referência para evidências comuns

| Tipo de evidência | P(E\|H) típico | P(E\|¬H) típico | BF típico |
|---|---|---|---|
| Rompimento de resistência com volume alto | 0,70 | 0,35 | 2,0 |
| Resultado trimestral acima do consenso | 0,65 | 0,40 | 1,6 |
| Rebaixamento de rating de crédito | 0,15 | 0,55 | 0,27 |
| Insider buying significativo | 0,60 | 0,30 | 2,0 |
| Reversão de tendência em dado único | 0,40 | 0,35 | 1,1 |

**Atenção:** esses valores são referências aproximadas. Cada análise deve estimar P(E|H) com base no contexto específico.

---

## 5. Controle de Mudança de Regime

Quando houver mudança de regime de mercado (ex: transição de mercado bull para bear, crise, mudança de política monetária), o Motor deve:

1. Registrar a quebra estrutural como evidência de classe `estrutural`
2. Avaliar se os priors históricos ainda são válidos no novo regime
3. Considerar reinicialização do prior com valor conservador
4. Não propagar posteriors de regime anterior automaticamente para novo regime

---

## 6. Limites de Atualização

O posterior não pode ultrapassar determinados limites sem evidência extraordinária:

| Variação em uma rodada | Requer |
|---|---|
| Δ > 30 pontos percentuais | Revisão e justificativa explícita |
| Δ > 50 pontos percentuais | Revisão obrigatória por Dante ou especialista designado |
| Posterior > 90% | Documentação explícita das evidências que justificam tal certeza |
| Posterior < 10% | Documentação explícita das evidências que justificam tal rejeição |

---

## 7. Registro Completo de Rodada

```yaml
rodada:
  numero: 3
  prior: 0.52
  origem_prior: "POSTERIOR_RODADA_2"
  
  evidencias_processadas:
    - id: "EV-003"
      classe: "confirmatoria"
      p_e_dado_h: 0.68
      p_e_dado_nao_h: 0.32
      bayes_factor: 2.125
      peso_aplicado: 1.0
    - id: "EV-004"
      classe: "contraditorica"
      p_e_dado_h: 0.25
      p_e_dado_nao_h: 0.60
      bayes_factor: 0.417
      peso_aplicado: 0.7
  
  evidencias_excluidas:
    - id: "EV-005"
      motivo: "correlacionada com EV-003"
  
  calculo:
    p_e_composto_dado_h: "produto ajustado das verossimilhanças"
    p_e_composto_dado_nao_h: "produto ajustado"
    p_e_marginal: "normalizador calculado"
    posterior_calculado: 0.58
    metodo: "analitico"
  
  estado_final:
    posterior: 0.58
    variacao: "+0.06 pp"
    grau_confianca: "moderado"
    nivel_incerteza: "moderado"
    estado_saida: "HIPOTESE_MODERADAMENTE_FORTALECIDA"
  
  auditoria:
    timestamp: "2026-07-12T22:00:00Z"
    reversivel: true
```
