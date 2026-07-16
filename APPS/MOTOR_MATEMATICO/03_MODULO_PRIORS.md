# MÓDULO DE PRIORS — PROBABILIDADES INICIAIS

Data: 2026-07-12
Versão: 1.0
Status: ATIVO
Entregável: #3

---

## 1. Definição

O prior é a probabilidade que o Motor Matemático atribui a uma hipótese **antes de receber qualquer nova evidência na rodada atual**.

O prior deve ser explicitamente declarado e documentado. Um prior não declarado invalida a análise bayesiana.

---

## 2. Tipos de Prior

### 2.1 Prior Histórico

**Definição:** baseado na frequência observada em casos comparáveis.

**Quando usar:**
- Há histórico suficiente de situações similares (mínimo: 30 casos comparáveis)
- Os casos históricos são relevantes para o contexto atual
- A frequência é estável ao longo do tempo

**Como calcular:**
```
Prior histórico = (número de casos em que H foi verdadeira) / (total de casos comparáveis)
```

**Exemplo:**
```
Hipótese: continuidade de tendência de alta após rompimento de resistência
Casos históricos analisados: 150
H confirmada: 89
Prior histórico = 89 / 150 = 0,593 (categoria: moderada a alta)
```

**Registro obrigatório:**
- Universo de casos utilizados
- Período histórico
- Critérios de comparabilidade
- Tamanho da amostra
- Estabilidade temporal da frequência

### 2.2 Prior Estrutural

**Definição:** baseado nas propriedades permanentes ou duradouras do fenômeno analisado.

**Quando usar:**
- O fenômeno tem características estruturais bem conhecidas
- As propriedades não mudam com frequência
- Há teoria ou modelo que sustenta a estimativa

**Exemplos de base estrutural:**
- Empresas com histórico longo de dividendos crescentes: prior moderado para manutenção
- Setor com barreiras de entrada elevadas: prior moderado para estabilidade de margens
- Ativo com alta correlação estrutural a commodity específica: prior informado por essa correlação

**Registro obrigatório:**
- Propriedade estrutural identificada
- Justificativa teórica ou empírica
- Horizonte de validade esperado da premissa estrutural

### 2.3 Prior Não Informativo ou Conservador

**Definição:** utilizado quando não há informação suficiente para estimar a probabilidade com base em dados ou teoria.

**Quando usar:**
- Histórico insuficiente (menos de 30 casos comparáveis)
- Fenômeno novo ou sem precedente
- Incerteza genuína sobre a distribuição

**Valores padrão:**
- Prior agnóstico: 0,50 (hipótese e negação igualmente prováveis)
- Prior conservador para hipótese favorável: 0,30 (benefício da dúvida não concedido automaticamente)
- Prior conservador para hipótese desfavorável: 0,50 (precaução assimétrica)

**Registro obrigatório:**
- Justificativa para uso de prior não informativo
- Ausência de dados comprovada
- Análise de sensibilidade ao prior (obrigatória quando prior é não informativo)

---

## 3. Proibições na Escolha do Prior

O Motor Matemático não pode:

1. **Escolher prior para confirmar conclusão desejada.** O prior deve refletir o conhecimento disponível antes da evidência, não o resultado esperado.

2. **Usar prior implícito.** Todo prior deve ser registrado explicitamente antes de receber evidências.

3. **Usar prior excessivamente otimista sem justificativa histórica ou estrutural.** Prior > 70% para hipótese favorável requer justificativa documentada.

4. **Importar o posterior de uma análise como prior de outra sem registrar a transferência.** Quando o posterior de uma análise alimenta o prior de outra, o vínculo deve ser explícito.

5. **Usar prior de horizonte diferente sem ajuste.** Um prior de longo prazo não pode ser aplicado diretamente a uma análise intradiária.

---

## 4. Procedimento Formal de Declaração do Prior

Antes de cada rodada de análise, registrar:

```yaml
prior_declaracao:
  hipotese: "enunciado"
  valor_prior: "0,45 ou categoria: moderada"
  tipo_prior: "historico | estrutural | nao_informativo | conservador"
  origem_prior: "FREQ_HISTORICA | MODELO_ESTATISTICO | SIMULACAO |
                 ESPECIALISTA | HEURISTICA | INDETERMINAVEL"
  justificativa: "texto"
  universo_historico: "N casos / período"
  data_declaracao: "AAAA-MM-DD"
  analista_responsavel: "MOTOR_MATEMATICO"
  analise_sensibilidade_necessaria: true
```

---

## 5. Análise de Sensibilidade ao Prior

Quando o prior for não informativo, conservador ou contestável, o Motor deve executar análise de sensibilidade:

| Prior alternativo | Posterior resultante | Variação |
|---|---|---|
| Prior baixo (0,20) | ? | ? |
| Prior moderado (0,50) | ? | ? |
| Prior alto (0,80) | ? | ? |

Se o posterior variar mais de 20 pontos percentuais entre os priors extremos, registrar:
- `sensibilidade_prior: alta`
- Conclusão marcada como dependente do prior escolhido

---

## 6. Migração de Prior entre Horizontes Temporais

Cada horizonte temporal possui seu próprio prior.

| Horizonte | Prior deve refletir |
|---|---|
| Intradiário | Condições de mercado nas últimas horas |
| Diário | Tendência dos últimos dias |
| Semanal | Dinâmica das últimas semanas |
| Mensal | Ciclo corrente |
| Trimestral | Resultado operacional mais recente |
| Longo prazo | Qualidade estrutural do ativo |

Migração de prior entre horizontes requer ajuste explícito e justificado.

---

## 7. Atualização do Prior entre Ciclos

O posterior de uma rodada torna-se o prior da rodada seguinte.

```
Prior_0 → Evidência_1 → Posterior_1
Posterior_1 = Prior_1 → Evidência_2 → Posterior_2
Posterior_2 = Prior_2 → Evidência_3 → Posterior_3
```

Regras:
- O prior de cada rodada deve ser registrado como igual ao posterior anterior
- O histórico completo de transições deve ser preservado
- Nenhum prior pode ser modificado retroativamente após receber evidências
