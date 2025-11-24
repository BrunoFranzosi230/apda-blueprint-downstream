# Política de Promoção de Ambientes

O fluxo de promoção segue a ordem: **DEV $\rightarrow$ STG $\rightarrow$ PROD**. O artefato gerado no build deve ser **imutável** (o mesmo binário/imagem navega entre os ambientes).

## 1. Ambiente de Desenvolvimento (DEV)
- **Objetivo:** Criação, integração diária e testes rápidos pelos desenvolvedores.
- **Dados:** Fictícios (Mocks/Seeds).
- **Configuração:** Logs verbosos (Debug ativado), Feature Flags livres para teste.
- **Critério de Deploy:** Automático a cada merge na branch `main` (após passar no CI).

## 2. Ambiente de Staging (STG)
- **Objetivo:** Espelho de produção para validação fim a fim (funcional, performance e migrações).
- **Dados:** Anonimizados ou sintéticos próximos do real.
- **Critério de Promoção (Dev -> Stg):**
    1. DoD da tarefa cumprido.
    2. Pipeline de CI (Testes/Lint/SAST) 100% verde.
    3. Aprovação de Quality Gate automático.

## 3. Ambiente de Produção (PROD)
- **Objetivo:** Uso real pelo cliente final. Estabilidade máxima.
- **Dados:** Reais.
- **Configuração:** Configurações e Segredos (Secrets) injetados especificamente para este ambiente. Logs em nível INFO/ERROR.
- **Critério de Promoção (Stg -> Prod):**
    1. Validação completa em Stg realizada com sucesso.
    2. Aprovação manual (Gate humano) no pipeline de release.
    3. Janela de release respeitada (se aplicável).