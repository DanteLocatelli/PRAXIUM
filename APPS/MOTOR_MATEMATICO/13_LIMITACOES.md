# LIMITAÇÕES FORMAIS — CAMADA BAYESIANA

Data: 2026-07-12
Versão: 1.0
Status: ATIVO — DOCUMENTO VIVO
Entregável: #13

---

## 1. Propósito

Este documento registra formalmente as limitações conhecidas da camada bayesiana. Reconhecer limitações não é fraqueza: é condição de rigor científico e disciplina epistêmica.

**Nenhuma análise produzida pelo Motor Matemático pode ser apresentada sem referência a este documento.**

---

## 2. Limitações Estruturais do Método Bayesiano

### L-01 — Dependência do Prior

**Descrição:** o resultado do posterior é sempre influenciado pelo prior escolhido. Com poucos dados, o prior domina o resultado.

**Implicação:** em mercados novos, ativos sem histórico ou situações sem precedente, o posterior reflete principalmente o prior, não as evidências.

**Mitigação:** usar prior não informativo; executar análise de sensibilidade; comunicar explicitamente quando o prior domina.

### L-02 — Estimativa de Verossimilhança

**Descrição:** P(E|H) e P(E|¬H) raramente são conhecidas com precisão. Em muitos casos, são estimativas baseadas em julgamento ou analogia.

**Implicação:** a precisão numérica do posterior pode ser ilusória se as verossimilhanças forem mal estimadas.

**Mitigação:** documentar método de estimativa; usar intervalos; classificar verossimilhanças por grau de confiança.

### L-03 — Hipótese de Independência

**Descrição:** o método assume evidências condicionalmente independentes. Em mercados financeiros, a maioria das evidências tem alguma correlação.

**Implicação:** mesmo com o controle de correlação (módulo 05), correlações parciais residuais podem inflar artificialmente o posterior.

**Mitigação:** aplicar descontos conservadores; classificar correlações com cautela; preferir subestimar a superestimar independência.

### L-04 — Estacionariedade

**Descrição:** os parâmetros calibrados (verossimilhanças, taxas de decaimento) assumem que o mercado se comporta de forma relativamente estável ao longo do tempo.

**Implicação:** em regimes de mercado novos (ex: taxa de juros em 0%, pandemia, guerra), os parâmetros históricos podem não ser válidos.

**Mitigação:** monitorar Brier Score por regime; recalibrar após mudança de regime detectada; manter prior conservador em regimes novos.

### L-05 — Causalidade vs. Correlação

**Descrição:** a estrutura bayesiana é agnóstica sobre causalidade. Ela quantifica associações, não mecanismos causais.

**Implicação:** o Motor pode atualizar fortemente um posterior com base em correlação histórica que não representa relação causal real.

**Mitigação:** exigir justificativa causal mínima para evidências estruturais; registrar quando evidência é apenas correlacional.

---

## 3. Limitações Operacionais

### L-06 — Quantidade Insuficiente de Dados

**Descrição:** para ativos com histórico curto, setores novos ou situações atípicas, pode não haver casos históricos suficientes para estimar priors históricos.

**Implicação:** análise recai no prior conservador, com baixa informação.

**Mitigação:** sinalizar explicitamente quando N < 30; nunca simular precisão que não existe.

### L-07 — Qualidade das Fontes de Evidência

**Descrição:** o Motor depende da qualidade das informações recebidas. Evidências baseadas em fontes ruins produzem posteriors ruins.

**Implicação:** "garbage in, garbage out" se aplica ao método bayesiano como a qualquer outro.

**Mitigação:** classificar confiabilidade da fonte; reduzir peso de fontes de baixa confiabilidade; nunca usar evidência de fonte desconhecida sem desconto.

### L-08 — Horizonte de Previsão

**Descrição:** a precisão preditiva cai rapidamente à medida que o horizonte se alonga.

**Implicação:** posteriors de longo prazo são menos confiáveis que de curto prazo, mesmo com evidências de alta qualidade.

**Mitigação:** aumentar intervalos de incerteza conforme o horizonte; nunca apresentar probabilidades pontuais para horizontes longos.

### L-09 — Decaimento Temporal como Aproximação

**Descrição:** as taxas de decaimento definidas no módulo 06 são aproximações baseadas em julgamento, não em dados calibrados individualmente.

**Implicação:** o peso ajustado de uma evidência pode não refletir com precisão sua relevância real naquele momento específico.

**Mitigação:** revisar periodicamente as taxas de decaimento; ajustar após backtest; tratar decaimento como parâmetro sujeito a calibração.

---

## 4. Limitações de Escopo

### L-10 — Hipóteses Compostas

**Descrição:** o modelo foi especificado para hipóteses binárias (H ou ¬H). Hipóteses com múltiplos resultados possíveis requerem extensão não coberta nesta versão.

**Implicação:** situações como "qual dentre três cenários ocorrerá" não são diretamente tratadas pelo modelo atual.

**Mitigação:** decompor em hipóteses binárias quando possível; registrar quando a hipótese não é adequadamente representada de forma binária.

### L-11 — Custos de Oportunidade Dinâmicos

**Descrição:** o custo de oportunidade é tratado como fixo no cálculo de VEL. Em mercados dinâmicos, o custo de oportunidade muda ao longo do período de análise.

**Implicação:** o VEL calculado pode estar desatualizado se o custo de oportunidade mudar materialmente após a análise.

**Mitigação:** atualizar custo de oportunidade ao rever análises; registrar data do custo de oportunidade utilizado.

---

## 5. O que o Método Não Faz

A camada bayesiana **não**:

- Prevê o futuro com certeza
- Elimina risco de mercado
- Substitui julgamento humano em situações sem precedente
- Detecta fraude ou manipulação de mercado automaticamente
- Funciona adequadamente em dados manipulados ou incorretos
- Produz resultados superiores em todos os regimes e horizontes
- Elimina a necessidade de revisão periódica por Dante

---

## 6. Registro de Novas Limitações

Este documento deve ser atualizado sempre que:

1. Um teste revelar comportamento não previsto
2. O backtest identificar falha sistemática
3. Uma mudança de regime expuser vulnerabilidade
4. Dante ou especialista identificar lacuna não documentada

```yaml
limitacao_nova:
  id: "L-XX"
  data_identificacao: "AAAA-MM-DD"
  origem: "teste | backtest | uso_em_producao | revisao_especialista"
  descricao: "descrição da limitação"
  implicacao: "impacto"
  mitigacao: "ação corretiva"
  status: "documentada | em_mitigacao | mitigada"
```
