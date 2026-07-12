# ESQUEMA DE DADOS — MÁSCARA PROBABILÍSTICA BAYESIANA

Data: 2026-07-12
Versão: 1.0
Status: ATIVO
Entregável: #2

---

## 1. Estrutura Principal da Máscara

```yaml
mascara_probabilistica:
  versao: "1.0"
  timestamp_criacao: "AAAA-MM-DDTHH:MM:SSZ"
  timestamp_ultima_atualizacao: "AAAA-MM-DDTHH:MM:SSZ"
  ativo_ou_estrategia: "identificador único"
  horizonte_temporal: "intradiario | diario | semanal | mensal | trimestral | longo_prazo"

  hipotese:
    enunciado: "texto claro e falsificável"
    tipo: "valorizacao | continuidade_tendencia | reversao | manutencao_dividendos |
           deterioracao_financeira | retorno_valor_justo | perda_permanente_capital |
           desempenho_superior_benchmark | outro"
    condicoes_invalidacao:
      - "condição 1 que tornaria a hipótese falsa"
      - "condição 2"
    proxima_evidencia_necessaria: "descrição da evidência que dispararia nova atualização"

  estado_atual:
    probabilidade_anterior: "valor numérico ou categoria"
    probabilidade_posterior: "valor numérico ou categoria"
    grau_confianca: "muito_baixo | baixo | moderado | alto | muito_alto"
    nivel_incerteza: "muito_baixo | baixo | moderado | alto | muito_alto"
    origem_probabilidade: "FREQ_HISTORICA | MODELO_ESTATISTICO | SIMULACAO |
                           ESPECIALISTA | HEURISTICA | INDETERMINAVEL"
    estado_saida: "HIPOTESE_FORTALECIDA | HIPOTESE_MODERADAMENTE_FORTALECIDA |
                   HIPOTESE_INALTERADA | HIPOTESE_ENFRAQUECIDA |
                   HIPOTESE_FORTEMENTE_ENFRAQUECIDA | EVIDENCIA_INSUFICIENTE |
                   CONFLITO_ENTRE_EVIDENCIAS | PROBABILIDADE_NAO_CALIBRADA |
                   DECISAO_ECONOMICAMENTE_DESFAVORAVEL | AGUARDAR_NOVA_EVIDENCIA"

  historico_atualizacoes:
    - rodada: 0
      prior: "valor"
      evidencias: []
      posterior: "valor"
      timestamp: "AAAA-MM-DDTHH:MM:SSZ"
    - rodada: 1
      prior: "posterior da rodada 0"
      evidencias: []
      posterior: "valor"
      timestamp: "AAAA-MM-DDTHH:MM:SSZ"

  evidencias:
    - id: "EV-001"
      descricao: "descrição da evidência"
      classe: "confirmatoria | contraditorica | neutra | redundante |
               baixa_confiabilidade | estrutural | conjuntural"
      forca: "muito_fraca | fraca | moderada | forte | muito_forte"
      bayes_factor: "valor numérico estimado ou intervalo"
      qualidade_fonte: "alta | media | baixa | desconhecida"
      independencia: "independente | parcialmente_correlacionada |
                      altamente_correlacionada | redundante | relacao_desconhecida"
      evidencias_correlacionadas: ["EV-002", "EV-003"]
      fonte: "nome da fonte"
      data_evidencia: "AAAA-MM-DD"
      data_recepcao: "AAAA-MM-DD"
      horizonte_relevante: "intradiario | diario | semanal | mensal | trimestral | longo_prazo"
      peso_ajustado: "valor entre 0 e 1"
      decaimento_aplicado: true
      fator_decaimento: "valor entre 0 e 1"
      notas: "observações adicionais"

  valor_esperado_liquido:
    probabilidade_ganho: "valor"
    ganho_liquido_esperado: "valor"
    probabilidade_perda: "valor"
    perda_liquida_esperada: "valor"
    custos:
      corretagem: "valor"
      emolumentos: "valor"
      spread: "valor"
      slippage: "valor"
      impostos: "valor"
      custo_aluguel: "valor"
      custo_oportunidade: "valor"
      risco_execucao: "valor"
    resultado: "valor numérico"
    favoravel: true

  calibracao:
    brier_score: "valor"
    log_loss: "valor"
    taxa_acerto_por_faixa:
      muito_baixa: "valor"
      baixa: "valor"
      moderada: "valor"
      alta: "valor"
      muito_alta: "valor"
    estabilidade_fora_amostra: "valor"
    sensibilidade_prior: "baixa | moderada | alta"
    robustez_por_regime: "estavel | instavel | nao_testado"
    ultima_avaliacao: "AAAA-MM-DD"
```

---

## 2. Esquema de Evidência Individual

```yaml
evidencia:
  id: "EV-YYYYMMDD-001"
  ativo: "identificador do ativo ou estratégia"
  hipotese_vinculada: "identificador da hipótese"

  descricao:
    texto: "descrição objetiva da evidência"
    categoria_dado: "preco | volume | volatilidade | forca_tendencia | lucro |
                     margem | fluxo_caixa | divida | dividendo | valuation |
                     revisao_estimativas | cenario_juros | cambio | setor |
                     governanca | evento_corporativo | comportamento_vs_indice | outro"

  classificacao:
    classe: "confirmatoria | contraditorica | neutra | redundante |
             baixa_confiabilidade | estrutural | conjuntural"
    natureza_temporal: "estrutural | conjuntural"
    forca: "muito_fraca | fraca | moderada | forte | muito_forte"
    bayes_factor_estimado: "valor ou intervalo"
    justificativa_bayes_factor: "texto explicativo"

  fonte:
    nome: "identificação da fonte"
    tipo: "dado_mercado | relatorio_empresa | analise_externa | dado_macro |
           dado_setorial | evento_noticiado | model_output | especialista | outro"
    confiabilidade: "alta | media | baixa | desconhecida"
    verificavel: true
    url_ou_referencia: "link ou citação"

  temporalidade:
    data_evento: "AAAA-MM-DD"
    data_recepcao: "AAAA-MM-DD"
    horizonte_relevante: "intradiario | diario | semanal | mensal | trimestral | longo_prazo"
    vida_util_estimada: "duração estimada da relevância"
    taxa_decaimento: "rapida | moderada | lenta | muito_lenta | persistente"

  correlacao:
    independencia: "independente | parcialmente_correlacionada |
                    altamente_correlacionada | redundante | relacao_desconhecida"
    evidencias_da_mesma_origem: []
    justificativa_correlacao: "texto"

  peso:
    peso_bruto: "valor entre 0 e 1"
    ajuste_confiabilidade: "fator multiplicador"
    ajuste_decaimento: "fator multiplicador"
    peso_final: "valor entre 0 e 1"

  auditoria:
    registrado_por: "MOTOR_MATEMATICO"
    timestamp_registro: "AAAA-MM-DDTHH:MM:SSZ"
    rodada_atualizacao: "número da rodada"
    hash_evidencia: "hash SHA-256 do conteúdo"
```

---

## 3. Esquema de Rodada de Atualização

```yaml
rodada_atualizacao:
  id: "ROD-YYYYMMDD-001"
  ativo: "identificador"
  hipotese: "identificador"
  numero_rodada: 1

  estado_inicial:
    prior: "valor"
    origem_prior: "FREQ_HISTORICA | MODELO_ESTATISTICO | SIMULACAO |
                   ESPECIALISTA | HEURISTICA | INDETERMINAVEL"
    grau_confianca_prior: "muito_baixo | baixo | moderado | alto | muito_alto"

  evidencias_desta_rodada:
    - id_evidencia: "EV-001"
      papel: "confirmatoria"
      peso_aplicado: "valor"
    - id_evidencia: "EV-002"
      papel: "contraditorica"
      peso_aplicado: "valor"

  calculo:
    p_e_dado_h: "valor calculado"
    p_e_dado_nao_h: "valor calculado"
    p_e_marginal: "valor calculado"
    bayes_factor_composto: "valor"
    metodo_calculo: "analitico | numerico | categoria_qualitativa"
    dupla_contagem_detectada: false
    evidencias_excluidas_por_correlacao: []

  estado_final:
    posterior: "valor"
    grau_confianca_posterior: "muito_baixo | baixo | moderado | alto | muito_alto"
    nivel_incerteza: "muito_baixo | baixo | moderado | alto | muito_alto"
    estado_saida: "HIPOTESE_FORTALECIDA"
    variacao_probabilidade: "+X pp ou categoria"

  auditoria:
    timestamp: "AAAA-MM-DDTHH:MM:SSZ"
    hash_rodada: "hash SHA-256"
    reversivel: true
    snapshot_estado_anterior: "referência ao estado anterior completo"
```

---

## 4. Campos Obrigatórios vs. Opcionais

| Campo | Obrigatório | Motivo |
|---|---|---|
| `hipotese.enunciado` | SIM | Sem enunciado, não há hipótese |
| `hipotese.condicoes_invalidacao` | SIM | Princípio de falsificabilidade |
| `estado_atual.probabilidade_anterior` | SIM | Bayes requer prior explícito |
| `estado_atual.origem_probabilidade` | SIM | Evitar falsa precisão |
| `evidencias[].classe` | SIM | Classificação obrigatória |
| `evidencias[].independencia` | SIM | Controle de dupla contagem |
| `evidencias[].fonte.confiabilidade` | SIM | Ajuste de peso |
| `rodada_atualizacao.dupla_contagem_detectada` | SIM | Gate de segurança |
| `valor_esperado_liquido` | SIM (se decisão) | Custos não podem ser ignorados |
| `calibracao` | Recomendado | Verificação periódica |
| `evidencias[].bayes_factor_estimado` | Recomendado | Quantificação da força |

---

## 5. Regras de Validação do Esquema

1. `probabilidade_posterior` deve ser diferente de `probabilidade_anterior` apenas se houver ao menos uma evidência não redundante desta rodada.
2. Se `dupla_contagem_detectada = true`, registrar `evidencias_excluidas_por_correlacao` obrigatoriamente.
3. `estado_saida = DECISAO_ECONOMICAMENTE_DESFAVORAVEL` somente se `valor_esperado_liquido.resultado < 0`.
4. `historico_atualizacoes` deve ser append-only (nunca sobrescrever rodadas anteriores).
5. O `prior` da rodada N deve ser igual ao `posterior` da rodada N-1.
