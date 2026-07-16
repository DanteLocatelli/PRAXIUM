# DOCUMENTAÇÃO DE AUDITORIA — CAMADA BAYESIANA

Data: 2026-07-12
Versão: 1.0
Status: ATIVO
Entregável: #14

---

## 1. Objetivo

Garantir rastreabilidade completa de cada análise produzida pela camada bayesiana, permitindo reconstituição integral de qualquer decisão tomada com base nela.

**Princípio:** qualquer análise que não possa ser reconstituída a partir do registro de auditoria não satisfaz os requisitos desta especificação.

---

## 2. O que Deve Ser Rastreado

Para cada análise bayesiana realizada, o registro de auditoria deve conter:

| Item | Obrigatório | Descrição |
|---|---|---|
| ID único da análise | Sim | Formato: AUD-YYYYMMDD-HHMMSS-XXX |
| Ativo ou estratégia | Sim | Identificador |
| Hipótese declarada | Sim | Enunciado completo |
| Prior declarado | Sim | Valor e origem |
| Data/hora da declaração do prior | Sim | Timestamp ISO 8601 |
| Evidências recebidas | Sim | Lista completa com classe, fonte e data |
| Classificação de correlação | Sim | Para cada par de evidências |
| Evidências excluídas ou ajustadas | Sim | Com justificativa |
| P(E\|H) e P(E\|¬H) estimados | Sim | Com método de estimativa |
| Posterior calculado | Sim | Valor e intervalo |
| Estado de saída | Sim | Da lista de estados padronizados |
| Histórico completo de rodadas | Sim | Sequência Prior_0 → Posterior_N |
| VEL calculado | Sim (se decisão de operação) | Com todos os componentes de custo |
| Hash de integridade | Sim | SHA-256 do conteúdo da análise |
| Versão da especificação | Sim | Versão do modelo bayesiano utilizado |
| Reversibilidade | Sim | Confirmação de que a análise pode ser revertida |

---

## 3. Estrutura do Registro de Auditoria

```yaml
auditoria_analise:
  id: "AUD-20260712-220000-001"
  versao_especificacao: "1.0"
  timestamp_inicio: "2026-07-12T22:00:00Z"
  timestamp_conclusao: "2026-07-12T22:05:00Z"
  operador: "MOTOR_MATEMATICO"
  
  objeto:
    ativo: "identificador"
    hipotese: "enunciado completo"
    horizonte: "mensal"
  
  prior_declarado:
    valor: 0.50
    tipo: "nao_informativo"
    origem: "HEURISTICA"
    justificativa: "sem histórico comparável suficiente"
    timestamp_declaracao: "2026-07-12T22:00:00Z"
    declarado_antes_das_evidencias: true
  
  evidencias_recebidas:
    - id: "EV-20260712-001"
      descricao: "rompimento de resistência com volume elevado"
      classe: "confirmatoria"
      forca: "forte"
      fonte: "dado de mercado B3"
      data_evento: "2026-07-10"
      data_recepcao: "2026-07-12"
      p_e_dado_h: 0.75
      p_e_dado_nao_h: 0.25
      bayes_factor: 3.0
      metodo_estimativa_verossimilhanca: "FREQ_HISTORICA"
      independencia: "independente"
      decaimento_tipo: "rapido"
      decaimento_fator: 0.70
      peso_ajustado: 0.70
      status: "ativa"
  
  controle_correlacao:
    dupla_contagem_detectada: false
    evidencias_excluidas: []
    evidencias_com_peso_reduzido: []
  
  historico_rodadas:
    - rodada: 0
      prior: 0.50
      posterior: 0.50
      evidencias: []
      timestamp: "2026-07-12T22:00:00Z"
    - rodada: 1
      prior: 0.50
      posterior: 0.677
      evidencias: ["EV-20260712-001"]
      variacao: "+0.177 pp"
      timestamp: "2026-07-12T22:03:00Z"
  
  resultado_final:
    posterior: 0.677
    grau_confianca: "moderado"
    nivel_incerteza: "moderado"
    estado_saida: "HIPOTESE_FORTALECIDA"
  
  vel:
    calculado: false
    motivo: "análise informativa, sem decisão de operação nesta rodada"
  
  integridade:
    hash_sha256: "a1b2c3d4e5f6..."
    reversivel: true
    snapshot_estado_anterior: "referência ao estado antes desta análise"
  
  condicoes_invalidacao:
    - "rompimento da suporte principal do dia anterior"
    - "resultado trimestral abaixo do consenso"
  
  proxima_evidencia_necessaria: "confirmação de fechamento acima da resistência"
```

---

## 4. Princípio de Imutabilidade Histórica

O histórico de auditoria é **append-only**.

- Rodadas anteriores nunca podem ser modificadas após o registro
- Um novo estado é adicionado ao histórico, nunca sobrescreve o anterior
- O prior de cada rodada deve ser idêntico ao posterior da rodada anterior (verificado por hash)

---

## 5. Protocolo de Reconstituição

Para reconstituir qualquer análise a partir do registro de auditoria:

**Passo 1 — Localizar registro**
- Buscar por ID da análise, ativo, data ou hipótese

**Passo 2 — Verificar integridade**
- Recalcular hash SHA-256 do conteúdo
- Comparar com hash registrado

**Passo 3 — Reproduzir cálculo**
- Com prior declarado e evidências registradas, recalcular posterior
- Verificar se resultado coincide com posterior registrado (tolerância: ±0,001)

**Passo 4 — Confirmar rastreabilidade**
- Verificar se cada evidência tem fonte, data e classe registradas
- Verificar se controle de correlação foi aplicado

**Passo 5 — Emitir laudo de reconstituição**
- `reconstituicao_confirmada: true` se todos os passos passarem
- `reconstituicao_confirmada: false` se houver discrepância — registrar qual

---

## 6. Retenção de Registros

| Tipo de análise | Período de retenção mínimo |
|---|---|
| Análise informativa | 2 anos |
| Análise que gerou decisão de operação | 5 anos |
| Análise que gerou perda relevante (> 5% do capital) | 10 anos |
| Análise em período de investigação | Indefinido até resolução |

---

## 7. Rastreabilidade de Versão

Cada análise deve registrar a versão da especificação bayesiana em vigor no momento da execução.

Se a especificação for atualizada, análises anteriores permanecem válidas sob a versão em que foram produzidas. Não se aplica retroativamente versão nova a análises já registradas.

| Versão | Data de vigência | Changelog |
|---|---|---|
| 1.0 | 2026-07-12 | Versão inicial — especificação completa da camada bayesiana |

---

## 8. Responsabilidade

O Motor Matemático é responsável por:
- Gerar e armazenar o registro de auditoria de cada análise
- Manter integridade do histórico (append-only)
- Permitir reconstituição por Dante ou auditor designado

Dante é responsável por:
- Revisar análises de alta relevância
- Validar decisões de incorporação ou rejeição de evidências excepcionais
- Autorizar mudanças na especificação (atualização de versão)
