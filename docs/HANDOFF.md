# Estado do trabalho (atualizado em 28/09/2026)

Use este arquivo para retomar o trabalho numa nova sessão.

## O que foi feito

1. Revisão da página `smark-home-4.0-vercel_1/fique-de-olho.html`, que é um protótipo com dados mock. Ela tem o agente Mark, as faixas de atraso e o painel de execução.
2. Pesquisa competitiva, em `docs/research/2026-09-28-fique-de-olho-concorrencia.md`.
3. Configuração das agent skills: `AGENTS.md` e `docs/agents/`. As issues ficam no GitHub e as etiquetas de triagem são as padrão.
4. Repositório público criado em https://github.com/fbeckenkamp/smark-fique-de-olho.
5. 10 issues criadas a partir das recomendações:
   - #1 a #4 com `ready-for-agent`;
   - #5 a #10 com `needs-triage`.

## Próximo passo sugerido

Implementar a issue #1 (pontuação e próxima ação em cada item) na `fique-de-olho.html`. Depois seguir com #2, #3 e #4. A #3 depende da #2, por causa da tecla `S` de adiar.

## Notas técnicas

- A página usa `support.js` com um componente `DCLogic`. O estado fica em `this.state`, os dados mock em `this.items`, e `renderVals()` devolve os valores do template `{{...}}`.
- A data fixa do mock é quarta, 23/09/2026. O campo `off` é o deslocamento em dias.
- O composer de e-mail só existe para a atividade `f1` (Kato Alimentos).
- Ambiente: iMac Intel com macOS 13.7. Não há Homebrew. O `gh` foi instalado por `.pkg` e está logado como `fbeckenkamp`.
