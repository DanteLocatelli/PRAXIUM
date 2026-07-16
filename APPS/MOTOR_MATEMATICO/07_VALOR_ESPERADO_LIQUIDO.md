# CÁLCULO DE VALOR ESPERADO LÍQUIDO

Data: 2026-07-12
Versão: 1.0
Status: ATIVO
Entregável: #7

---

## 1. Princípio

Probabilidade de acerto não é suficiente para determinar se uma operação é favorável.

Uma operação com 60% de probabilidade de ganho e ganho esperado de R$ 100, mas com perda esperada de R$ 400, tem valor esperado negativo e **não deve ser realizada**.

O Motor Matemático combina obrigatoriamente a probabilidade posterior com os custos e dimensões do resultado para produzir o **Valor Esperado Líquido (VEL)**.

---

## 2. Fórmula Central

```
VEL = (P_ganho × Ganho_líquido) − (P_perda × Perda_líquida)
```

Onde:
- `P_ganho` = probabilidade posterior de resultado favorável
- `Ganho_líquido` = ganho bruto esperado menos todos os custos
- `P_perda` = `1 − P_ganho`
- `Perda_líquida` = perda bruta esperada mais todos os custos adicionais

**Condição de favorabilidade:** `VEL > 0`

**Condição de favorabilidade ajustada ao risco:** `VEL > custo_oportunidade`

---

## 3. Componentes de Custo

### 3.1 Custos Operacionais Diretos

| Componente | Definição | Estimativa típica |
|---|---|---|
| Corretagem | Taxa fixa ou percentual por ordem | Variável por corretora |
| Emolumentos | Taxa da bolsa (B3) | 0,02% a 0,035% do financeiro |
| Spread | Diferença entre preço de compra e venda | Variável por ativo e liquidez |
| Slippage | Diferença entre preço esperado e executado | Maior em ativos ilíquidos ou ordens grandes |
| Imposto sobre ganho de capital | IRRF e DARF sobre lucro realizado | 15% a 20% conforme operação |
| Custo de aluguel | Para posições vendidas | Variável por taxa de aluguel |

### 3.2 Custos de Oportunidade

**Definição:** retorno que seria obtido com a melhor alternativa disponível ao mesmo capital e horizonte.

**Referências comuns:**
- CDI para posições de renda variável de curto prazo
- Selic/IPCA para horizonte de médio prazo
- Índice do setor ou Ibovespa para posições em ações

### 3.3 Risco de Execução

**Definição:** risco de a operação não ser executada nas condições previstas.

Inclui:
- Não execução por falta de liquidez
- Execução parcial
- Atraso de execução em eventos de mercado
- Gap de preço em abertura após evento

---

## 4. Estrutura de Cálculo

```yaml
vel_calculo:
  ativo: "PETR4"
  hipotese: "valorização de 15% no horizonte de 3 meses"
  horizonte: "trimestral"
  
  cenario_favoravel:
    probabilidade: 0.55  # posterior bayesiano
    preco_entrada: 38.00
    preco_alvo: 43.70  # +15%
    ganho_bruto_percentual: 0.15
    ganho_bruto_financeiro: 570.00  # sobre R$ 3.800 (100 ações)
    custos_saida:
      corretagem: 10.00
      emolumentos: 0.87  # 0,02% × 4.370
      spread_estimado: 5.00
      slippage: 3.00
      imposto: 84.00  # 15% sobre lucro de R$ 560
    ganho_liquido_financeiro: 467.13
  
  cenario_desfavoravel:
    probabilidade: 0.45  # 1 − 0.55
    preco_alvo_perda: 34.20  # −10%
    perda_bruta_percentual: 0.10
    perda_bruta_financeiro: 380.00
    custos_entrada_saida:
      corretagem: 20.00  # entrada + saída
      emolumentos: 1.44
      spread_estimado: 8.00
      slippage: 5.00
    perda_liquida_financeiro: 414.44
  
  custo_oportunidade:
    taxa_referencia: "CDI"
    taxa_periodo: 0.025  # CDI estimado para 3 meses
    valor_custo_oportunidade: 95.00  # R$ 3.800 × 2,5%
  
  resultado:
    vel_bruto: "(0.55 × 467.13) − (0.45 × 414.44)"
    vel_calculado: 256.92 − 186.50
    vel_final: 70.42
    vel_ajustado_oportunidade: 70.42 − 95.00
    vel_ajustado_final: -24.58
    favoravel: false
    estado_saida: "DECISAO_ECONOMICAMENTE_DESFAVORAVEL"
    observacao: "Positivo antes do custo de oportunidade; negativo após ajuste"
```

---

## 5. Razão Risco-Retorno

Além do VEL, registrar:

```
Razão R/R = Ganho_líquido_esperado / Perda_líquida_esperada
```

| Razão R/R | Interpretação |
|---|---|
| < 1,0 | Desfavorável (mais se perde do que se ganha) |
| 1,0 — 1,5 | Marginal |
| 1,5 — 2,0 | Adequado |
| 2,0 — 3,0 | Favorável |
| > 3,0 | Muito favorável |

**Atenção:** razão R/R alta com probabilidade muito baixa pode resultar em VEL negativo.

---

## 6. Kelly Criterion (Dimensionamento de Posição)

Para operações com VEL positivo, o Motor pode calcular o tamanho ótimo de posição pelo critério de Kelly:

```
f* = (P_ganho × Razão_R/R − P_perda) / Razão_R/R
```

Onde `f*` é a fração do capital a alocar.

**Regra de segurança:** nunca usar Kelly integral. Aplicar fração de 25% a 50% do Kelly calculado para controle de drawdown.

---

## 7. Condições de Não Execução

O Motor deve marcar `favoravel: false` quando qualquer das seguintes condições ocorrer:

1. `VEL < 0`
2. `VEL_ajustado_oportunidade < 0`
3. `Razão R/R < 1,0` com `P_ganho < 0,60`
4. `P_ganho < 0,40` independentemente da razão R/R
5. Custos superam 30% do ganho bruto esperado
6. Risco de execução classificado como alto em ativo ilíquido

---

## 8. Regra sobre Probabilidade de 50%

Nenhuma operação deve ser considerada favorável apenas porque possui probabilidade superior a 50%.

Exemplo de falsa lógica:
```
"P_ganho = 51% > 50%, portanto executar"
```

Isso ignora custos, dimensão do resultado e custo de oportunidade.

O critério correto é `VEL_ajustado_oportunidade > 0`.
