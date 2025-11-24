# Blueprint do Downstream - Análise, Projeto e Desenvolvimento Ágil

## 1. Estratégia de Git e PR (Previsibilidade)
**Modelo de Branch:**
Adotaremos uma estratégia de **Trunk-Based Development (Leve)**.
- **Branches Curtas:** As branches de feature devem ter vida curta (1 a 2 dias no máximo) para evitar conflitos complexos e facilitar a revisão.
- **Convenção de Commits:** Uso do padrão **Conventional Commits** (ex: `feat:`, `fix:`, `refactor:`) para permitir a geração automática de changelogs.

## 2. Qualidade e Estratégia de Testes
**Pirâmide de Testes:**
Seguiremos a proporção ideal para equilibrar custo e confiabilidade:
1.  **Testes Unitários (Base - 70%):** Rápidos e isolados. Foco na lógica de negócio.
2.  **Testes de Integração (Meio - 20%):** Validação de contratos de API e comunicação com banco de dados.
3.  **Testes E2E (Topo - 10%):** Parcimoniosos, focados nos fluxos críticos do usuário.

**Definições de Qualidade:**
- **Meta de Cobertura Mínima:** 80% (Foco em código útil, não apenas métrica de vaidade).
- **Ferramentas:**
    - *Lint:* ESLint (Padronização de código).
    - *SAST:* SonarQube (Segurança estática).
- **Política de Bloqueio:** O pipeline falhará imediatamente se houver erros de Lint ou vulnerabilidades de segurança de nível **Alto** ou **Crítico**.

## 3. Observabilidade, DORA e Melhoria Contínua (PDCA)
**Logs Essenciais:**
1.  **Log de Transação:** Registro estruturado de sucesso/falha em operações críticas (ex: checkout finalizado).
2.  **Log de Erro (Application Error):** Stack traces de exceções não tratadas com contexto do usuário.

**Métricas Chave (SLIs):**
1.  **Taxa de Erros (Error Rate):** Quantidade de respostas 5xx por minuto.
2.  **Latência (Latency):** Percentil 95 (p95) do tempo de resposta das requisições.

**Métricas DORA (DevOps Research and Assessment):**
Monitoraremos estas métricas como bússola de melhoria:
- **Lead Time for Changes:** Tempo entre o commit e o código rodando em produção.
- **Change Failure Rate:** Porcentagem de deploys que resultam em falha/rollback.

**Rotina PDCA (Kaizen):**
- **Quando:** Reunião quinzenal de retrospectiva.
- **Quem:** Todo o time de engenharia.
- **Ação:** Analisar as métricas DORA e incidentes da quinzena para ajustar o processo (ex: melhorar testes se a taxa de falha subiu).