# AGENTS.md — Padrão de trabalho do projeto Site-Fabi

> Este arquivo define como qualquer agente de IA (Claude, GPT, Copilot, etc.) ou pessoa deve trabalhar neste repositório. Leia antes de fazer qualquer alteração.

Repositório: github.com/oDevNova/Site-Fabi
Projeto: site vitrine institucional (fabi-florminhas-site) — HTML/CSS/JS estático, sem framework, sem etapa de build.

## 1. Regra de ouro: tudo passa por Issue e PR

Nenhuma alteração é feita direto na branch principal (main). O fluxo é sempre:

1. Abrir uma Issue descrevendo a tarefa, antes de escrever qualquer código.
2. Criar uma branch a partir da main para trabalhar nessa Issue.
3. Abrir um Pull Request (PR) quando o trabalho estiver pronto para revisão.
4. Mencionar a Issue na descrição do PR (ver seção 4).
5. Só depois de aprovado o PR é mesclado (merge) — é esse merge que representa o deploy.

## 2. Tipos de Issue

| Tipo | Quando usar | Prefixo no título |
|---|---|---|
| Correção (bug) | Algo que já existe e está quebrado | fix: |
| Melhoria (enhancement) | Algo que existe e pode ficar melhor | improve: |
| Nova função (feature) | Algo que ainda não existe | feat: |

Use os templates em .github/ISSUE_TEMPLATE/.

## 3. Nomenclatura de branches

Formato: <tipo>/<numero-da-issue>-<descricao-curta>
Exemplos: fix/12-modal-nao-fecha-no-esc, feat/20-filtro-por-categoria

## 4. Regras do Pull Request

- Título no mesmo padrão da Issue (fix:, improve:, feat: + descrição curta).
- A descrição DEVE conter a menção à Issue: `Closes #12` (ou Fixes/Resolves).
- Deve conter: o que foi feito, por quê, como testar (passo a passo manual), checklist (seção 6).
- PRs pequenos e focados em uma única Issue.
- Merge para main só após aprovação e checklist completo.

## 5. Commits (Conventional Commits, validado por Commitlint)

`<tipo>(<escopo opcional>): <descrição curta no imperativo>`
Tipos: feat, fix, docs, style, refactor, perf, test, chore, ci.

## 6. Checklist antes de abrir o PR

- [ ] Issue referenciada (Closes #...)
- [ ] Site continua funcionando abrindo index.html direto (sem servidor/build)
- [ ] Testado em modo claro e escuro
- [ ] Testado em PT e EN
- [ ] Testado no celular e no desktop
- [ ] Navegação por teclado e foco visível funcionam
- [ ] prefers-reduced-motion respeitado
- [ ] Lint (Biome) sem erros
- [ ] Testes relevantes passando
- [ ] Nenhuma chave/token/dado sensível commitado

## 7. Qualidade, testes e observabilidade

- Lint/qualidade: Biome, Commitlint, Knip, regras de arquitetura (arch-contract).
- Testes: unitários e integração, E2E com Playwright, cobertura via Codecov.
- Observabilidade: erros de front-end no Sentry; telemetria via OpenTelemetry, com Datadog e/ou New Relic como backend.
- Credenciais nunca hardcoded em script.js — sempre em GitHub Secrets/variáveis de ambiente.

## 8. Animação e interface (Motion Principles)

Toda interface deve ter, quando fizer sentido:
- Skeleton/estado de carregamento antes do conteúdo real
- Lazy loading de imagens e blocos fora da tela inicial
- Animação de entrada suave (scroll reveal / fade+slide leve)
- Animação de saída suave (modal, painel mobile)
- Indicador de progresso em ações perceptíveis
- Sempre respeitando prefers-reduced-motion: reduce

## 9. Resumo para o agente

1. Sem Issue? Abra uma primeiro.
2. Branch nomeada conforme seção 3.
3. PR referenciando a Issue com Closes #<numero>.
4. Checklist da seção 6 preenchido.
5. Não quebrar "site estático sem build" nem expor segredos.
6. Respeitar commits, lint, testes e animação acima.
