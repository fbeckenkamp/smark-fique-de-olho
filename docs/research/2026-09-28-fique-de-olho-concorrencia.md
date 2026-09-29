# Fique de olho × concorrência (pesquisa de 28/09/2026)

Esta pesquisa compara a página `smark-home-4.0-vercel_1/fique-de-olho.html` com a concorrência. Ela foi feita com o workflow deep-research: 5 frentes de busca, 22 fontes lidas, 96 afirmações extraídas e 25 verificadas por 3 votos cada. Dessas, 22 foram confirmadas e 3 descartadas.

O resultado bruto, com todas as afirmações e votos, está em `2026-09-28-fique-de-olho-concorrencia.raw.json`.

## Resumo

Os líderes organizam o dia do vendedor como uma fila única, priorizada e executada em sequência: HubSpot Sales Workspace, Dynamics 365 Sales Accelerator, Salesloft Rhythm e Close Power Dialer. A prioridade vem cada vez mais de sinais e da probabilidade de fechar, e não só da data.

A página "Fique de olho" já tem a base certa:
- painel de execução;
- "Concluir e ir para a próxima";
- rascunho do Mark com ajuste de tom;
- desfazer envio;
- follow-up automático.

As lacunas em relação aos concorrentes:
- ordenar por receita e probabilidade;
- pontuação e próxima ação visíveis em cada item;
- adiar e pular com motivo;
- ações em lote;
- atalhos de teclado;
- avanço configurável depois de concluir;
- nível de autonomia do Mark escolhido explicitamente;
- agentes que atualizam o CRM e preparam briefing de reunião;
- WhatsApp sincronizado.

## O que cada concorrente faz

| Concorrente | Padrão | Fonte |
|---|---|---|
| HubSpot, fila de prospecção | Uma fila única com tarefas e ações guiadas. "Auto-open action box" abre o discador ou o e-mail ao selecionar a tarefa | [doc](https://knowledge.hubspot.com/prospecting/use-the-prospecting-queue) |
| HubSpot, Prospecting Agent | Dois modos: "Review before sending" e "Send automatically". O envio respeita remetente, tom e horário comercial, e há um resumo diário às 9h | [doc](https://knowledge.hubspot.com/prospecting/use-the-prospecting-agent?app=wp) |
| Dynamics 365, Sales Accelerator | Cada item mostra a próxima melhor ação e a pontuação. Tem concluir, pular, adiar e pular espera, e-mail em lote e avanço automático | [doc](https://learn.microsoft.com/en-us/dynamics365/sales/prioritize-sales-pipeline-through-work-list) |
| Salesloft, Focus Zones | A Close Focus Zone foca nos deals com maior chance de fechar | [produto](https://www.salesloft.com/platform/rhythm/focus-zones) |
| Pipedrive, AI Sales Assistant | Prevê a probabilidade de ganho e sugere a próxima melhor ação (planos superiores) | [produto](https://www.pipedrive.com/en/features/ai-sales-assistant) |
| Close, Power Dialer | Liga em sequência para uma Smart View, com anotações entre as ligações | [doc](https://help.close.com/feature-guide/power-predictive-dialing/using-the-power-dialer) |
| Outreach | cmd/ctrl+K abre as tarefas de qualquer tela e há atalhos globais | [doc](https://support.outreach.io/support/solutions/articles/159000425949-using-keyboard-shortcuts-in-outreach) |
| Agentforce Sales | Um agente atualiza campos do CRM e sugere próximos passos, e outro gera briefing de reunião | [newsroom](https://www.salesforce.com/news/stories/agentforce-sales-announcement/) |
| Agendor, WhatsApp Sync | Registra as conversas de WhatsApp no histórico sozinho: texto, áudio e arquivos | [site](https://www.agendor.com.br/) |

## Números de mercado (indicam tendência, não provam causa)

- **Gartner (maio/2026, 227 CSOs):** organizações que dão ao vendedor próximas ações sugeridas por IA têm 2,6 vezes mais chance de crescer ([press release](https://www.gartner.com/en/newsroom/press-releases/2026-05-20-gartner-survey-finds-sales-organizations-that-provide-ai-enabled-next-best-actions-are-two-point-six-times-more-likely-to-achieve-commercial-growth)).
- **Salesforce State of Sales, 7ª edição:** vendedores gastam 60% do tempo fora da venda, e 85% dos que usam agentes dizem ter mais tempo para trabalho de maior valor ([stats](https://www.salesforce.com/sales/state-of-sales/sales-statistics/)). A pesquisa é patrocinada por quem vende a solução.
- **Feng, McDonald e Zhang (2025):** propõem níveis de autonomia de agentes como uma decisão de design ([arXiv](https://arxiv.org/pdf/2506.12469)).

## Afirmações descartadas (não usar)

- Que a work list do Dynamics é sempre ordenada pela pontuação preditiva. Isso depende de configuração.
- Que o Agentforce exige aprovação humana de toda ação.
- Que a agente Ava do Agendor executa tarefas no CRM sozinha.

## Recomendações e issues

| # | Recomendação | Impacto e esforço | Issue |
|---|---|---|---|
| 1 | Pontuação e próxima ação do Mark em cada item | Alto impacto, baixo esforço | #1 |
| 2 | Adiar com opções rápidas e Pular com motivo (o Reagendar hoje não tem ação) | Alto impacto, baixo esforço | #2 |
| 3 | Atalhos de teclado | Alto impacto, baixo esforço | #3 |
| 4 | Abrir a ação do canal automaticamente e escolher o que acontece depois de concluir | Alto impacto, baixo esforço | #4 |
| 5 | Modo Foco em receita | Alto impacto, esforço médio | #5 |
| 6 | Seletor de autonomia do Mark, fila de aprovações e registro de ações | Alto impacto, esforço médio | #6 |
| 7 | WhatsApp com o Mark e conversas sincronizadas | Alto impacto, esforço médio | #7 |
| 8 | Agente pós-atividade que propõe mudanças de campo | Alto impacto, esforço alto | #8 |
| 9 | Briefing antes de reuniões e visitas | Alto impacto, esforço alto | #9 |
| 10 | Ações em lote e sessão de ligações | Alto impacto, esforço alto | #10 |

## Pendências da pesquisa

- CRMs brasileiros sem cobertura: RD Station CRM, Ploomes, Piperun, Moskit, Meetime e Exact/Spotter. Falta saber como organizam a fila e usam IA no WhatsApp.
- LGPD para envio automático e para sincronizar conversas de WhatsApp.
- Nível de autonomia padrão para PMEs e métricas para liberar níveis mais altos.
- Dados independentes (não de fornecedores) sobre ganho de produtividade.
