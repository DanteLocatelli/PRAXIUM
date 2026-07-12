# MECANISMO DE DECAIMENTO TEMPORAL

Data: 2026-07-12
Versão: 1.0
Status: ATIVO
Entregável: #6

---

## 1. Princípio

Evidências antigas perdem peso quando deixam de representar o estado atual.

O decaimento temporal é o mecanismo pelo qual o Motor Matemático reduz progressivamente o peso de uma evidência à medida que ela envelhece, conforme sua natureza e o horizonte da análise.

---

## 2. Tipos de Decaimento

### 2.1 Decaimento Rápido

**Aplicável a:** preço, volume, fluxo de ordem, spread, volatilidade realizada de curto prazo.

**Lógica:** dados de mercado de curto prazo tornam-se obsoletos rapidamente.

| Idade da evidência | Fator de decaimento |
|---|---|
| 0 — 1 dia | 1,00 |
| 2 — 3 dias | 0,70 |
| 4 — 7 dias | 0,40 |
| 8 — 14 dias | 0,20 |
| > 14 dias | 0,05 |

### 2.2 Decaimento Intermediário

**Aplicável a:** tendência técnica, momentum, força relativa, padrões gráficos.

| Idade da evidência | Fator de decaimento |
|---|---|
| 0 — 7 dias | 1,00 |
| 8 — 21 dias | 0,75 |
| 22 — 45 dias | 0,50 |
| 46 — 90 dias | 0,25 |
| > 90 dias | 0,10 |

### 2.3 Decaimento Trimestral

**Aplicável a:** resultados financeiros, lucro, margem, dívida, dividendos declarados.

| Idade da evidência | Fator de decaimento |
|---|---|
| 0 — 45 dias (dentro do trimestre) | 1,00 |
| 46 — 90 dias | 0,85 |
| 91 — 135 dias (próximo resultado esperado) | 0,60 |
| 136 — 180 dias | 0,40 |
| > 180 dias (dois trimestres atrás) | 0,20 |

### 2.4 Decaimento Lento

**Aplicável a:** qualidade empresarial, valuation estrutural, vantagem competitiva, histórico de alocação de capital.

| Idade da evidência | Fator de decaimento |
|---|---|
| 0 — 180 dias | 1,00 |
| 181 — 365 dias | 0,85 |
| 1 — 2 anos | 0,70 |
| 2 — 3 anos | 0,55 |
| > 3 anos | 0,40 |

### 2.5 Persistência Elevada

**Aplicável a:** fraude confirmada, quebra estrutural grave, irregularidade contábil, evento de governança crítico.

| Condição | Fator de decaimento |
|---|---|
| Evento não resolvido | 1,00 (sem decaimento) |
| Resolução parcial documentada | 0,70 |
| Resolução completa com auditoria independente | 0,30 |
| Tempo decorrido > 5 anos + resolução completa | 0,10 |

---

## 3. Tabela Resumo por Natureza de Evidência

| Natureza da Evidência | Tipo de Decaimento |
|---|---|
| Preço e variação intradiária | Rápido |
| Volume intradiário e diário | Rápido |
| Fluxo de ordens | Rápido |
| Spread e liquidez | Rápido |
| Tendência técnica | Intermediário |
| Momentum e força relativa | Intermediário |
| Padrões gráficos | Intermediário |
| Resultado trimestral (lucro, margem) | Trimestral |
| Fluxo de caixa reportado | Trimestral |
| Dívida líquida reportada | Trimestral |
| Dividendos declarados | Trimestral |
| Valuation (P/L, EV/EBITDA etc.) | Lento |
| Qualidade da gestão | Lento |
| Vantagem competitiva | Lento |
| Histórico de governança | Lento |
| Fraude ou irregularidade grave | Persistência elevada |
| Quebra estrutural comprovada | Persistência elevada |
| Mudança regulatória estrutural | Persistência elevada |

---

## 4. Fórmula de Peso com Decaimento

```
peso_ajustado(t) = peso_bruto × fator_decaimento(t, tipo)
```

Onde:
- `t` = idade da evidência em dias
- `tipo` = tipo de decaimento (rápido, intermediário, trimestral, lento, persistente)

---

## 5. Interação com Horizontes Temporais

Uma evidência com decaimento rápido pode ser completamente irrelevante para análise de longo prazo, mesmo que ainda esteja "fresca".

| Horizonte da análise | Evidências com decaimento rápido | Evidências com decaimento lento |
|---|---|---|
| Intradiário | Peso integral (1,00) | Peso reduzido (0,30) |
| Diário | Peso integral | Peso reduzido (0,50) |
| Semanal | Peso parcial (0,70) | Peso moderado (0,70) |
| Mensal | Peso baixo (0,30) | Peso alto (0,90) |
| Trimestral | Peso muito baixo (0,10) | Peso integral (1,00) |
| Longo prazo | Peso mínimo (0,05) | Peso integral (1,00) |

---

## 6. Invalidação por Decaimento Total

Quando `fator_decaimento ≤ 0,05`, a evidência é considerada **inativa**.

Evidência inativa:
- Não pode ser usada para calcular posterior
- Permanece no histórico como registrada
- Pode ser "reativada" apenas se nova ocorrência do mesmo tipo for observada

---

## 7. Evento de Reversão de Decaimento

Algumas situações revertem o decaimento de uma evidência antiga:

1. **Reaparição do padrão:** o mesmo padrão de preço ou técnico se repete — reclassificar como nova evidência
2. **Novo resultado confirma tendência anterior:** resultado trimestral subsequente confirma tendência — atualizar data de início do decaimento
3. **Investigação ativa de evento passado:** fraude sob investigação ativa — manter fator de decaimento = 1,00

---

## 8. Registro no Esquema de Dados

```yaml
decaimento:
  tipo: "rapido | intermediario | trimestral | lento | persistente"
  data_evento_evidencia: "AAAA-MM-DD"
  data_aplicacao_decaimento: "AAAA-MM-DD"
  idade_em_dias: 15
  fator_decaimento: 0.20
  status: "ativa | inativa"
  horizonte_analise: "semanal"
  peso_bruto: 1.0
  peso_ajustado: 0.20
  notas: "evidência de preço com 15 dias — decaimento rápido aplicado"
```
