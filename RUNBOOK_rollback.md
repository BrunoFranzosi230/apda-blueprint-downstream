# Runbook de Rollback de Release

**Estratégia de Release:** Blue-Green Deployment (ou Canary).
**Objetivo:** Reverter a produção para um estado estável imediatamente após a detecção de falha crítica.

## 1. Gatilhos de Rollback (Quando acionar?)
O rollback deve ser iniciado imediatamente se, nos primeiros 15 minutos pós-deploy, ocorrer:
- **Taxa de Erros (5xx):** Superior a 1% das requisições.
- **Latência:** Aumento súbito (ex: p95 > 500ms) comparado à versão anterior.
- **Testes Sintéticos (E2E):** Falha crítica no fluxo de login ou pagamento.

## 2. Procedimento de Rollback (Passo a Passo)
Este processo deve ser curto, reversível e testado.

**Passo 1: Identificar e Confirmar**
- Verificar dashboard de monitoramento (Grafana/Datadog).
- Confirmar que a anomalia começou após o último deploy.

**Passo 2: Executar Rollback (Reversão de Tráfego)**
- *Ação:* No painel de Deploy/Pipeline, selecionar a opção **"Revert to Previous Version"** ou mudar a chave do Load Balancer para o ambiente "Blue" (versão antiga estável).
- *Tempo estimado:* < 2 minutos.

**Passo 3: Verificação**
- Validar se a taxa de erros retornou a zero.
- Validar se a latência normalizou.

**Passo 4: Comunicação e Post-Mortem**
- Notificar o canal de incidentes (`#ops-alert`).
- Não tentar corrigir o código em produção ("Hotfix") sob pressão.
- Analisar logs para criar a correção em Dev posteriormente.