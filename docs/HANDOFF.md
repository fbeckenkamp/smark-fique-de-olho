# Estado do trabalho (atualizado em 01/10/2026)

Use este arquivo para retomar o trabalho numa nova sessão.

## O que foi feito

1. **Pesquisa competitiva:** `docs/research/2026-09-28-fique-de-olho-concorrencia.md`.
2. **Configuração das agent skills:** `AGENTS.md` e `docs/agents/`. As issues ficam no GitHub em https://github.com/fbeckenkamp/smark-fique-de-olho, repositório público.
3. **As 10 recomendações foram implementadas** na `smark-home-4.0-vercel_1/fique-de-olho.html`, um PR por issue.

## PRs: todos com merge no `main` (01/10/2026)

As issues #1 a #10 estão fechadas, e os branches das issues foram apagados. O zip para a Vercel (`smark-home-4.1-vercel.zip`, fora do git) tem a mesma versão do `main`.

| PR | Issue | Branch |
|---|---|---|
| #11 | #1 Prioridade e próxima ação | issue-1-score-nba |
| #12 | #2 Adiar, pular com motivo, desfazer | issue-2-snooze-skip |
| #13 | #3 Atalhos de teclado e busca ⌘K | issue-3-shortcuts |
| #14 | #4 Ação do canal e preferência de avanço | issue-4-channel-action |
| #15 | #5 Foco em receita | issue-5-revenue-focus |
| #16 | #6 Central do Mark: autonomia, aprovações, registro | issue-6-mark-autonomy |
| #17 | #7 WhatsApp com o Mark e conversa sincronizada | issue-7-whatsapp |
| #18 | #8 Agente pós-atividade (atualiza o CRM) | issue-8-post-activity |
| #19 | #9 Briefing antes de reuniões | issue-9-briefing |
| #20 | #10 Lote, plano para atrasadas, sessão de ligações | issue-10-bulk-calls |

As issues #5 a #10 estavam como `needs-triage`. As decisões de produto tomadas para o protótipo estão na tabela "Decisões tomadas" de cada PR.

## Pendências antes de produção

- **LGPD:** base legal, prazo de retenção e opt-out para envio automático (#6) e para sincronizar conversas de WhatsApp (#7). No protótipo isso aparece só como texto na interface.
- **Pontuação e valor esperado:** hoje são manuais (mapas `PRIO` e `DEAL`) e precisam de um modelo real.
- **Integrações ainda simuladas:** WhatsApp Business API, telefonia e envio de e-mail.

## Notas técnicas

- **Estrutura da página:** usa o `support.js` (Preact) com um componente `DCLogic`. O estado fica em `this.state`, os dados mock em `this.items` e nos mapas do constructor (`PRIO`, `DEAL`, `prep`, `postPlan`, `briefs`, `convs`, `waDrafts`, `mailDrafts`), e `renderVals()` devolve os valores do template `{{...}}`.
- **Relógio do mock:** fixo em qua, 23/09/2026, 10:00. O campo `off` é o deslocamento em dias.
- **Preferências salvas no navegador:** `localStorage` com as chaves `fdo.prefs` e `fdo.autonomy`.
- **Rodar localmente:** `.claude/launch.json` sobe `python3 -m http.server 5173`. O navegador do painel guarda cache, então recarregue com `?v=N`.
- **Ambiente:** iMac Intel com macOS 13.7, sem Homebrew. O `gh` foi instalado por `.pkg` e está logado como `fbeckenkamp`.
