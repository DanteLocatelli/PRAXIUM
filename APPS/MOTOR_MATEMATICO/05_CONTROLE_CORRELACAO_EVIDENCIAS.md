# CONTROLE DE CORRELAÇÃO ENTRE EVIDÊNCIAS

Data: 2026-07-12
Versão: 1.0
Status: ATIVO
Entregável: #5

---

## 1. Problema da Dupla Contagem

O teorema de Bayes, em sua forma sequencial simples, assume que as evidências são independentes entre si.

Quando duas evidências têm a mesma origem causal, derivam da mesma base de dados ou representam o mesmo fenômeno, tratá-las como independentes infla artificialmente a probabilidade posterior.

**Exemplo de erro:**
- EV-1: preço subiu 5% hoje
- EV-2: preço está acima da média de 20 dias
- EV-3: preço rompeu resistência do topo anterior

As três evidências são manifestações do mesmo movimento de preço. Contá-las como três evidências independentes confirmatórias é dupla (ou tripla) contagem.

---

## 2. Classes de Dependência

| Classe | Definição | Tratamento |
|---|---|---|
| `independente` | Origens causais distintas, fenômenos distintos | Usar peso integral em cada evidência |
| `parcialmente_correlacionada` | Compartilham parte da mesma informação | Reduzir peso de ambas (ex: cada uma vale 70%) |
| `altamente_correlacionada` | Manifestações do mesmo fenômeno subjacente | Manter apenas a mais informativa; descartar as demais |
| `redundante` | Mesma informação, fonte diferente | Registrar como redundante; não atualizar posterior novamente |
| `relacao_desconhecida` | Correlação não pode ser determinada | Aplicar desconto conservador de 40% no peso |

---

## 3. Protocolo de Verificação de Correlação

Para cada par de evidências (EV-i, EV-j) na mesma rodada:

**Passo 1 — Verificar origem causal**
- As evidências têm a mesma causa raiz?
- Derivam da mesma base de dados ou fonte primária?
- Representam o mesmo fenômeno medido de forma diferente?

**Passo 2 — Verificar dependência temporal**
- Uma evidência é consequência direta e mecânica da outra?
- O período de observação é o mesmo?

**Passo 3 — Classificar correlação**
- Registrar `independencia` para cada evidência
- Registrar `evidencias_da_mesma_origem` com os IDs relacionados

**Passo 4 — Ajustar pesos**
- Aplicar fatores de ajuste conforme tabela na seção 4

**Passo 5 — Documentar**
- Registrar `dupla_contagem_detectada: true` se houver correlação
- Listar evidências excluídas ou ajustadas

---

## 4. Fatores de Ajuste por Grau de Correlação

| Grau de Correlação | Fator de Ajuste para Cada Evidência |
|---|---|
| Independente | 1,00 (peso integral) |
| Parcialmente correlacionada | 0,65 por evidência do par |
| Altamente correlacionada | Manter a mais forte (1,00); descartar demais (0,00) |
| Redundante | 0,00 (não atualiza posterior) |
| Relação desconhecida | 0,60 por evidência |

**Nota:** quando mais de dois itens formam um grupo correlacionado, aplicar o ajuste ao grupo inteiro, não apenas par a par.

---

## 5. Exemplos Práticos

### 5.1 Grupo de evidências de preço (altamente correlacionadas)

Evidências candidatas:
- EV-A: preço acima da MM20
- EV-B: preço acima da MM50
- EV-C: preço rompeu máxima do mês anterior

Diagnóstico: as três refletem o mesmo movimento de preço subjacente.

Tratamento correto:
- Manter EV-C (mais informativa, pois representa evento de rompimento)
- Classificar EV-A e EV-B como `altamente_correlacionada` com EV-C
- Peso de EV-A e EV-B: 0,00 nesta rodada
- Registrar: `evidencias_excluidas_por_correlacao: [EV-A, EV-B]`

### 5.2 Volume e preço (parcialmente correlacionados)

- EV-D: rompimento de resistência (preço)
- EV-E: volume 2× a média no dia do rompimento (volume)

Diagnóstico: volume confirma o rompimento, mas é dado distinto. Parcialmente correlacionado.

Tratamento correto:
- Aplicar peso 0,65 para EV-D e 0,65 para EV-E
- Registrar como `parcialmente_correlacionada`

### 5.3 Resultado e fluxo de caixa (independentes)

- EV-F: lucro líquido acima do consenso
- EV-G: geração de caixa livre positiva

Diagnóstico: lucro e fluxo de caixa podem divergir. São indicadores distintos.

Tratamento correto:
- Verificar se números são da mesma demonstração
- Se derivados de premissas distintas: `independente`, peso 1,00 cada

### 5.4 Mesmo dado, duas fontes (redundante)

- EV-H: relatório da corretora X indica manutenção de dividendos
- EV-I: relatório da corretora Y indica manutenção de dividendos

Diagnóstico: ambas reportam o mesmo fato com base no mesmo comunicado da empresa.

Tratamento correto:
- EV-H: `independente`, peso 1,00
- EV-I: `redundante`, peso 0,00
- Registrar: EV-I é redundante de EV-H

---

## 6. Casos Especiais

### 6.1 Evidências de diferentes horizontes temporais

Evidências de horizontes diferentes não são diretamente correlacionadas por isso, mas devem ser tratadas em suas respectivas análises de horizonte.

### 6.2 Evidências de diferentes mercados sobre o mesmo ativo

Ex: comportamento do ADR na bolsa americana e da ação na bolsa brasileira.

Classificar como `parcialmente_correlacionada` (mesma empresa, mercados com dinâmicas distintas).

### 6.3 Evidências macro e micro

Ex: cenário de juros (macro) + resultado da empresa (micro).

Geralmente independentes, mas verificar se a hipótese é sensível a ambas.

---

## 7. Campo de Registro no Esquema de Dados

```yaml
correlacao_evidencias:
  dupla_contagem_detectada: true
  pares_analisados:
    - par: ["EV-A", "EV-B", "EV-C"]
      grau: "altamente_correlacionada"
      origem_comum: "mesmo movimento de preço"
      evidencia_mantida: "EV-C"
      evidencias_excluidas: ["EV-A", "EV-B"]
      justificativa: "EV-C contém a informação mais relevante (evento de rompimento)"
    - par: ["EV-D", "EV-E"]
      grau: "parcialmente_correlacionada"
      origem_comum: "mesmo evento de mercado"
      fator_ajuste_aplicado: 0.65
      justificativa: "volume confirma preço, mas são dados distintos"
  total_evidencias_brutas: 5
  total_evidencias_independentes_efetivas: 2.3
```

---

## 8. Impacto na Estimativa Final

Após aplicar controle de correlação, registrar:

| Métrica | Valor |
|---|---|
| Evidências brutas recebidas | N |
| Evidências redundantes descartadas | X |
| Evidências altamente correlacionadas (mantida 1 por grupo) | Y |
| Evidências com peso reduzido | Z |
| Evidências independentes efetivas | N − X − Y + (pares com 0,65) |

O Motor deve usar o número de **evidências efetivas** na avaliação da confiança do posterior, não o número bruto.
