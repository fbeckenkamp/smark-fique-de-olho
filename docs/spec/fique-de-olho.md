# Especificação: tela Fique de olho

> Publicada também como issue #21 (https://github.com/fbeckenkamp/smark-fique-de-olho/issues/21). Este arquivo é a cópia versionada.

> Especificação funcional da tela **Fique de olho** (Smark CRM 4.0, protótipo), para analistas, desenvolvedores e testadores. Ela descreve o comportamento que está hoje no `main`, depois dos PRs #11 a #20.

## Problem Statement

O executivo de vendas começa o dia com follow-ups, agendamentos e tarefas espalhados por e-mail, WhatsApp, agenda e CRM. Ele perde tempo decidindo o que fazer primeiro, trocando de ferramenta para executar cada atividade e atualizando o CRM à mão depois de cada contato.

Atividades atrasadas se acumulam sem um jeito rápido de resolvê-las. Negócios de maior valor recebem a mesma atenção que tarefas administrativas. O agente de IA, o Mark, até sugere o que fazer, mas não age, e o vendedor não sabe o que ele pode ou não fazer sozinho.

Quem analisa, desenvolve ou testa a tela também não tem uma descrição única das regras. Elas estão espalhadas em 10 PRs e no código do protótipo.

## Solution

O Fique de olho é a fila de trabalho do dia. Numa única tela, o vendedor:

- vê o que está atrasado, o que é para hoje e o que vem nos próximos 5 dias;
- ordena a fila por data ou por impacto em receita;
- executa cada atividade no próprio painel, ligando, mandando WhatsApp ou e-mail com rascunho do Mark;
- registra o resultado e deixa o Mark propor a atualização do CRM e a próxima atividade;
- adia, pula ou descarta com um clique, sempre com Desfazer;
- trabalha só com o teclado, em lote ou em sessão de ligações;
- define quanto o Mark pode fazer sozinho em cada canal e aprova o que ele preparou.

### Conceitos (glossário)

| Termo | Significado |
|---|---|
| **Atividade** | Item da fila. Tem um **tipo**, um **canal**, empresa, contato, dia (deslocamento em dias em relação a hoje) e horário opcional |
| **Tipo** | Follow-up, Agendamento ou Tarefa |
| **Canal** | E-mail, Ligação, WhatsApp, Reunião, Reunião online, Visita, Demonstração, CRM, Financeiro, Proposta, Contrato, Reunião interna |
| **Faixa** | Grupo de urgência por data: *Mais de 2 semanas* (atraso de 14 dias ou mais), *Menos de 2 semanas* (atraso de 1 a 13 dias), *Hoje* e *Próximos 5 dias* (de 1 a 5 dias à frente) |
| **Prioridade** | Nota de 0 a 100 por atividade: Alta (70 ou mais), Média (40 a 69) e Baixa (abaixo de 40) |
| **Próxima ação** | Recomendação curta do Mark para a atividade, com os sinais que a justificam ("Por quê?") |
| **Oportunidade** | Negócio ligado à atividade, com valor, etapa e sinais |
| **Valor esperado** | valor da oportunidade × probabilidade da etapa × multiplicador de sinais |
| **Mark** | Agente de IA que sugere, rascunha, prepara e executa ações |
| **Central do Mark** | Gaveta com as abas Aprovações, O que o Mark fez e Autonomia |
| **Nível de autonomia** | Sugerir, Rascunhar, Executar com aprovação ou Executar sozinho, definido por canal: E-mail, WhatsApp, Agenda e CRM |
| **Ação preparada** | Ação que o Mark deixou pronta para uma atividade. Por exemplo: enviar convite, atualizar valor, enviar contrato |
| **Proteções** | Regras que limitam a autonomia: horário comercial, limite diário e aprovação obrigatória acima de R$ 50 mil |
| **Resultado** | O que aconteceu na atividade, em texto ou áudio transcrito |
| **Descartada** | Atividade encerrada como "Não é mais necessária". Sai das pendentes, mas não conta como feita |

### Premissas do protótipo
- **Relógio:** o "agora" é fixo em **quarta, 23/09/2026, 10:00**. Todos os cálculos de data e horário partem desse momento.
- **Dados:** são fictícios e ficam embutidos na página. São 28 atividades, das quais 2 já começam concluídas.
- **Tamanho:** a página tem largura fixa de 1440 px e altura mínima de 1500 px.

## User Stories

### Visão geral e navegação
1. Como executivo de vendas, quero ver no topo quantas atividades tenho em cada faixa (mais de 2 semanas, menos de 2 semanas, hoje e próximos 5 dias), para saber o tamanho do meu dia e do meu atraso.
2. Como executivo de vendas, quero ver em cada faixa a divisão por tipo (follow-ups, agendamentos e tarefas), para entender a natureza do trabalho pendente.
3. Como executivo de vendas, quero clicar numa faixa e ver só as atividades dela, para atacar o atraso por blocos.
4. Como executivo de vendas, quero navegar dia a dia com as setas e voltar para "Hoje" com um clique, para planejar os próximos dias.
5. Como executivo de vendas, quero ver no menu lateral um contador de atividades atrasadas, para saber do atraso de qualquer tela.
6. Como executivo de vendas, quero filtrar a lista por tipo (Todos, Follow-ups, Agendamentos, Tarefas), com a contagem de pendentes em cada filtro, para focar num tipo de trabalho.
7. Como executivo de vendas, quero que o subtítulo da lista mostre quantas atividades estão pendentes e quantas já concluí, para acompanhar meu progresso.
8. Como executivo de vendas, quero que a lista agrupe as atividades por dia, com rótulos como "Hoje", "Ontem", "Há 6 dias" e "Em 2 dias", para entender o tempo de cada uma.
9. Como executivo de vendas, quero que cada atividade mostre título, tipo, canal, empresa e uma tag de horário ou atraso, para identificá-la sem abrir.
10. Como executivo de vendas, quero que as atividades concluídas apareçam riscadas com a tag "Feita" e as descartadas com a tag "Descartada", para distinguir o que fiz do que abandonei.
11. Como executivo de vendas, quero ver "Nada por aqui" quando um filtro ou dia não tem atividades, para saber que a lista não está quebrada.

### Prioridade e próxima ação
12. Como executivo de vendas, quero ver em cada atividade aberta um chip de prioridade (Alta, Média ou Baixa, com a nota), para saber a importância sem abrir.
13. Como executivo de vendas, quero ver em cada atividade aberta a próxima ação sugerida pelo Mark, para agir sem precisar ler o contexto inteiro.
14. Como executivo de vendas, quero ver no painel a faixa "Próxima ação" com a prioridade, para começar pelo que importa.
15. Como executivo de vendas, quero abrir "Por quê?" e ver os sinais usados pelo Mark (valor, etapa, dias sem resposta, intenção), para confiar na recomendação.
16. Como executivo de vendas, quero que o "Por quê?" feche quando troco de atividade, para não carregar contexto errado.
17. Como executivo de vendas, quero que as atividades concluídas não mostrem próxima ação, para a lista não ficar poluída.

### Painel de execução
18. Como executivo de vendas, quero ver no painel o tipo, o canal, o status (atrasada há N dias, hoje às HH:MM, data futura, concluída ou descartada), o título, o contato e a empresa, para ter o contexto completo.
19. Como executivo de vendas, quero ver os campos de contexto da oportunidade (valor, etapa, último contato, sinais), para me preparar.
20. Como executivo de vendas, quero ver a descrição da atividade e a dica do Mark, para saber o que fazer.
21. Como executivo de vendas, quero concluir uma atividade e ir direto para a próxima pendente, para manter o ritmo.
22. Como executivo de vendas, quero reabrir uma atividade concluída, para corrigir um engano.

### Follow-up por e-mail com o Mark (atividade da Kato)
23. Como executivo de vendas, quero receber um rascunho de e-mail escrito pelo Mark com base na demonstração, no histórico e na oportunidade, para não começar do zero.
24. Como executivo de vendas, quero pedir ajustes rápidos ao rascunho (mais curto, mais formal, incluir case de sucesso, mais direto), para adequar o tom sem reescrever.
25. Como executivo de vendas, quero escrever uma instrução livre para o Mark, para pedir um ajuste que não está nos chips.
26. Como executivo de vendas, quero regerar o rascunho, para ver outra versão.
27. Como executivo de vendas, quero editar assunto e corpo antes de enviar, para ter a palavra final.
28. Como executivo de vendas, quero que o envio crie o próximo follow-up em 3 dias úteis se não houver resposta (opção marcada por padrão), para não esquecer.
29. Como executivo de vendas, quero desfazer o envio, para corrigir um erro logo depois de enviar.

### Ação conforme o canal
30. Como executivo de vendas, quero que uma atividade de ligação mostre o botão "Ligar para <contato>" com o número e o roteiro do Mark ao lado, para ligar sem procurar o telefone.
31. Como executivo de vendas, quero ver "Ligação iniciada · registre o resultado abaixo" depois de clicar para ligar, para lembrar de registrar.
32. Como executivo de vendas, quero que uma atividade de WhatsApp mostre a mensagem pronta e editável, para enviar em segundos.
33. Como executivo de vendas, quero copiar a mensagem ou abrir o WhatsApp com o texto já preenchido, para usar o canal que eu preferir.
34. Como executivo de vendas, quero que uma atividade de e-mail com rascunho do Mark abra um composer (Para, Assunto, Corpo), para responder sem sair da tela.
35. Como executivo de vendas, quero escolher se a ação do canal abre automaticamente ao selecionar a atividade, para controlar quanta informação aparece.
36. Como executivo de vendas, quero escolher o que acontece depois de concluir (ir para a próxima, ficar na atividade ou voltar para a lista), para adaptar ao meu jeito de trabalhar.
37. Como executivo de vendas, quero que essas preferências continuem valendo quando eu recarregar a página, para não configurar de novo.

### WhatsApp com o Mark
38. Como executivo de vendas, quero ver a conversa de WhatsApp sincronizada com o contato, para saber o que já foi dito.
39. Como executivo de vendas, quero um sinal de resposta (respondeu recentemente, última resposta há mais de 24 h ou sem resposta desde a minha mensagem), para decidir o tom.
40. Como executivo de vendas, quero pedir ao Mark para reescrever a mensagem (mais curto, mais formal, mais direto) ou regerar, para ajustar sem digitar.
41. Como executivo de vendas, quero ser avisado quando a conversa está fora da janela de 24 h e a mensagem vai sair como template aprovado, para não ter o envio recusado pelo WhatsApp Business.
42. Como executivo de vendas, quero enviar pelo Smark e ver a mensagem entrar na conversa, para registrar tudo num só lugar.

### Adiar, pular e descartar
43. Como executivo de vendas, quero adiar uma atividade para Mais 1 h, Amanhã 9h, Próxima segunda ou uma data e hora que eu escolher, para reorganizar o dia rapidamente.
44. Como executivo de vendas, quero ver primeiro a sugestão do Mark quando ele encontrou um horário livre para mim e para o cliente, para reagendar sem consultar agendas.
45. Como executivo de vendas, quero que o menu de adiar não ofereça horários anteriores ao da própria atividade, para não "adiar para trás".
46. Como executivo de vendas, quero pular uma atividade informando o motivo (Sem tempo agora, Aguardando cliente, Não é mais necessária, Outro), para registrar por que não fiz.
47. Como executivo de vendas, quero ver "Pulada antes: <motivo>" quando volto a uma atividade pulada, para lembrar o contexto.
48. Como executivo de vendas, quero que "Não é mais necessária" descarte a atividade e a tire das pendentes, para limpar a fila.
49. Como executivo de vendas, quero um aviso com Desfazer por 5 segundos depois de adiar, pular, descartar ou enviar, para corrigir enganos sem medo.

### Teclado
50. Como executivo de vendas, quero navegar pela lista com J/K ou com as setas, para não depender do mouse.
51. Como executivo de vendas, quero concluir e avançar com E, para percorrer a fila rapidamente.
52. Como executivo de vendas, quero abrir o menu de adiar com S, para reagendar sem o mouse.
53. Como executivo de vendas, quero enviar o rascunho com ⌘/Ctrl+Enter, inclusive dentro do campo de texto, para enviar sem tirar as mãos do teclado.
54. Como executivo de vendas, quero abrir uma busca com ⌘/Ctrl+K e ir até qualquer atividade pendente pela empresa, pelo contato ou pelo título, para achar algo rapidamente.
55. Como executivo de vendas, quero ver a lista de atalhos com ? e fechar menus e janelas com Esc, para aprender e sair rápido.
56. Como executivo de vendas, quero que os atalhos de uma letra não funcionem enquanto digito num campo ou com uma janela aberta, para não disparar ações por acidente.
57. Como executivo de vendas, quero que os botões principais mostrem a tecla do atalho, para aprender sem consultar ajuda.

### Foco em receita
58. Como executivo de vendas, quero alternar entre "Por data" e "Foco em receita", para trabalhar pelo impacto quando o tempo é curto.
59. Como executivo de vendas, quero que o Foco em receita reúna as atividades pendentes de todas as faixas e as ordene por valor esperado, para atacar primeiro o que mais pesa no resultado.
60. Como executivo de vendas, quero ver o valor esperado em cada atividade e o total em jogo no subtítulo, contando cada oportunidade uma vez só, para dimensionar o dia.
61. Como executivo de vendas, quero ver no "Por quê?" a conta do valor esperado de qualquer atividade com oportunidade, para entender a ordem do Foco em receita.
62. Como executivo de vendas, quero que as atividades sem oportunidade fiquem numa faixa própria no fim, para não perdê-las de vista.

### Central do Mark (autonomia)
63. Como executivo de vendas, quero ver ao lado do título quantas ações o Mark preparou e aguardam minha aprovação, para não deixar nada parado.
64. Como executivo de vendas, quero aprovar, rejeitar ou abrir e editar cada ação preparada, para manter o controle.
65. Como executivo de vendas, quero aprovar uma ação preparada direto no painel da atividade, para não precisar abrir a Central.
66. Como executivo de vendas, quero definir para cada canal (E-mail, WhatsApp, Agenda, CRM) se o Mark só sugere, rascunha, executa com minha aprovação ou executa sozinho, para delegar na medida da minha confiança.
67. Como executivo de vendas, quero que, ao passar um canal para "Executar sozinho", o Mark execute na hora o que já tinha pronto naquele canal, para ver o efeito da delegação.
68. Como executivo de vendas, quero que oportunidades acima de R$ 50 mil sempre peçam aprovação, para não arriscar negócios grandes.
69. Como executivo de vendas, quero ver quantas ações automáticas o Mark já usou do limite diário, para acompanhar o volume.
70. Como executivo de vendas, quero ver tudo o que o Mark fez hoje, se foi automático ou aprovado por mim, e desfazer as ações recentes, para auditar o agente.
71. Como gestor comercial, quero que cada ação do agente fique registrada com horário e autoria, para ter rastreabilidade.

### Resultado e atualização do CRM
72. Como executivo de vendas, quero registrar o resultado digitando ou gravando um áudio que o Mark transcreve, para não perder o que aconteceu.
73. Como executivo de vendas, quero que, ao concluir com resultado registrado, o Mark proponha as mudanças no CRM (antes → depois) e a próxima atividade, para não atualizar campo por campo.
74. Como executivo de vendas, quero desmarcar mudanças específicas antes de aplicar, ou concluir sem alterar, para corrigir o Mark.
75. Como executivo de vendas, quero que, com o CRM em "Executar sozinho", o Mark aplique a proposta sem perguntar e registre a ação, para ganhar tempo.
76. Como executivo de vendas, quero desfazer a atualização e ver os campos, a atividade criada e o registro voltarem ao estado anterior, para errar sem medo.

### Reuniões e visitas
77. Como executivo de vendas, quero um briefing do Mark em toda reunião ou visita aberta, com participantes, histórico, objetivo, objeções, perguntas, materiais, notícias da empresa e logística, para chegar preparado.
78. Como executivo de vendas, quero recolher o briefing, para liberar espaço no painel.
79. Como executivo de vendas, quero um aviso no topo quando faltar até 60 minutos para a próxima reunião, com o botão "Ver briefing", para não ser pego de surpresa.
80. Como executivo de vendas, quero dispensar esse aviso, para ele não me distrair.

### Lote, atrasadas e ligações
81. Como executivo de vendas, quero selecionar várias atividades e, de uma vez, pedir rascunhos ao Mark, adiar para amanhã ou concluir, para ganhar escala.
82. Como executivo de vendas, quero revisar os rascunhos um a um e tirar os que não devem sair, antes de enviar em lote, para manter a qualidade.
83. Como executivo de vendas, quero que o Mark monte um plano para todas as atrasadas (executar o que está pronto, trazer para hoje, reagendar para amanhã ou descartar) e eu ajuste cada item antes de aplicar, para zerar o atraso em minutos.
84. Como executivo de vendas, quero fazer uma sessão de ligações em sequência, com progresso, roteiro, anotações e resultado (Atendeu, Não atendeu · tentar amanhã, Pular), para fazer todas as ligações sem trocar de tela.
85. Como executivo de vendas, quero ver um resumo no fim da sessão de ligações, para saber o que ficou pendente.
86. Como executivo de vendas, quero desfazer de uma vez uma ação em lote ou um plano aplicado, para corrigir sem refazer item por item.

### Para quem constrói e valida
87. Como testador, quero que os dados e o relógio sejam fixos, para que os testes sejam determinísticos.
88. Como testador, quero que as áreas, janelas e grupos da tela tenham rótulos acessíveis estáveis, para localizar os elementos nos testes sem depender de estilo.
89. Como desenvolvedor, quero que as preferências e a autonomia sejam salvas em chaves conhecidas do armazenamento local, para limpar o estado entre testes.
90. Como analista, quero que cada decisão de produto do protótipo esteja documentada, para revisar com o negócio antes de produção.

## Implementation Decisions

### Arquitetura
- **Estrutura:** a tela é uma página estática (HTML com um template declarativo e um componente de lógica em Preact), servida por qualquer servidor estático, inclusive a Vercel. Não há backend: todo o estado vive no componente durante a sessão.
- **Template:** usa valores `{{...}}`, condicionais (`sc-if`) e repetições (`sc-for`). O componente expõe um único método que devolve todos os valores e handlers que o template usa.
- **Template oculto:** o template original continua no DOM, escondido. Por isso, todo seletor (em código ou teste) precisa considerar só os elementos visíveis.
- **Atividades:** são mantidas pelo componente. Adiar e criar a próxima atividade alteram a própria atividade ou a lista; os demais estados (concluída, descartada, motivo de pulo, rascunhos, notas, resultado da sessão) ficam no estado do componente.
- **Armazenamento local:** só duas chaves sobrevivem ao recarregar: `fdo.prefs` (abrir ação automaticamente; depois de concluir) e `fdo.autonomy` (nível por canal; proteções). Leitura e escrita ficam protegidas contra falha do navegador.

### Regras de negócio

**Faixas e datas**
- Mais de 2 semanas: atraso de 14 dias ou mais. Menos de 2 semanas: de 1 a 13 dias. Hoje: dia 0. Próximos 5 dias: de 1 a 5 dias à frente.
- O contador do menu lateral soma as atividades abertas das duas faixas de atraso.

**Ordenação**
- *Por data*: dia, depois horário. Atividades sem horário vêm depois das com horário.
- *Foco em receita*: primeiro a faixa de valor (mais de R$ 15 mil esperados; até R$ 15 mil; sem oportunidade), depois o valor esperado, em que as atividades futuras pesam 60%. As sem oportunidade são ordenadas pela prioridade.
- J/K e "concluir e ir para a próxima" seguem a ordem da visão atual.

**Prioridade e valor esperado**
- **Prioridade:** Alta se a nota for 70 ou mais, Média de 40 a 69, Baixa abaixo de 40.
- **Probabilidade por etapa:** Qualificação 10%, Diagnóstico 20%, Demonstração 30%, Proposta 50%, Negociação 60%, Negociação pausada 40%, Contrato 90%.
- **Multiplicador de sinais:** de 1,2 a 1,5, aplicado quando há sinal (proposta aberta 3x, e-mail aberto 2x, reunião hoje, lead inbound esperando).
- **Total em jogo:** soma cada empresa uma vez só.

**Adiar**
- **Opções**, nesta ordem:
  - *Sugestão do Mark*, quando a atividade tem horário livre sugerido;
  - *Mais 1 h*, contada a partir do mais tarde entre 10:00 e o horário da atividade;
  - *Amanhã 9h*;
  - *Próxima segunda 9h*;
  - *Escolher data…*.
- **Filtro:** opções iguais ou anteriores ao dia e horário atuais da atividade não aparecem.
- **Depois de adiar:** a seleção vai para a próxima pendente.

**Pular**
- Os motivos, exceto "Não é mais necessária", ficam guardados e a atividade continua pendente.
- "Não é mais necessária" marca a atividade como concluída e descartada.

**Desfazer**
- O aviso dura 5 s.
- Restaura dia, horário, estados de concluída e descartada, motivo, seleção, campos alterados, atividade criada, entradas do registro do Mark e mensagens enviadas.
- Nas ações em lote, restaura todas as atividades envolvidas.

**Concluir**
- O comportamento depois de concluir segue a preferência: próxima pendente, ficar ou voltar para a lista (foco na linha).
- A atividade da Kato só é concluída pelo envio do e-mail.
- Com E sobre uma atividade já concluída, a seleção só avança.

**Resultado e atualização do CRM**
- Se há resultado registrado (exceto na atividade da Kato), concluir abre a proposta do Mark.
- Atividades sem plano próprio recebem apenas um follow-up padrão em 5 dias.
- Se o CRM está em "Executar sozinho", a proposta completa é aplicada direto.

**Autonomia**
- **Padrões:** E-mail e WhatsApp em Rascunhar; Agenda e CRM em Executar com aprovação.
- **Fila de aprovações:** ações preparadas de atividades atuais ou atrasadas, cujo canal está em "Executar com aprovação", ou em "Executar sozinho" com oportunidade acima de R$ 50 mil (com a proteção ligada). Itens rejeitados saem da fila.
- **Ao passar um canal para "Executar sozinho":** o Mark executa na hora as ações preparadas daquele canal que não exigem aprovação, até o limite de 20 por dia.

**WhatsApp**
- **Sinal verde:** o cliente foi o último a escrever, há no máximo 24 h.
- **Sinal âmbar:** o cliente foi o último a escrever, há mais de 24 h.
- **Sinal vermelho:** o vendedor foi o último a escrever.
- **Template:** é exigido (com aviso) quando a última mensagem do cliente tem mais de 24 h.

**Briefing**
- Aparece em atividades do tipo Agendamento que estão abertas.
- O aviso do topo considera a próxima reunião de hoje depois das 10:00 que comece em até 60 min.

**Plano das atrasadas**
- Executar, se há ação preparada.
- Trazer para hoje às 14:30, se a prioridade for 60 ou mais.
- Descartar, se a prioridade for menor que 35 e o atraso for de 14 dias ou mais.
- Nos demais casos, Amanhã 9h.

**Sessão de ligações**
- Percorre as atividades pendentes da visão atual cujo canal é ligação.
- Atendeu: conclui a atividade e guarda as anotações como resultado.
- Não atendeu: move a atividade para amanhã às 9h.
- Pular: não altera a atividade.

### Contratos de interface (rótulos acessíveis usados por testes)
- **Regiões:** "Atividades", com a lista, e "Executar atividade", com o painel.
- **Grupos e barras:** "Filtrar por tipo", "Ordenar atividades", "Ações da lista", "Ações em lote".
- **Janelas e regiões:** "Central do Mark", "Buscar atividade", "Atalhos de teclado", "Preferências", "Rascunhos do Mark", "Plano do Mark para as atrasadas", "Sessão de ligações", "Briefing do Mark", "Mark sugere atualizar o CRM", "Conversa sincronizada", "Próxima reunião".
- **Linha da lista:** a atividade selecionada tem `aria-current="true"`. As faixas, os filtros e os modos usam `aria-pressed`. Os níveis de autonomia e o plano usam `role="radio"` e `aria-checked`.
- **Avisos:** o aviso com Desfazer usa `role="status"`.

## Testing Decisions

- **Ponto de teste único:** a página no navegador. Os testes servem a pasta da página com um servidor estático, abrem a tela e interagem como o vendedor (clique, teclado, digitação), conferindo só o que aparece na tela. Não testam o estado interno do componente nem a estrutura do template.
- **Ferramenta sugerida:** Playwright, ou equivalente com navegador real. Teclas devem ser enviadas como eventos reais, já que a ajuda usa "?".
- **O que é um bom teste:**
  - descreve um comportamento do glossário (por exemplo: "adiar pela sugestão do Mark move a atividade para os Próximos 5 dias e o Desfazer restaura");
  - localiza elementos por papel e rótulo acessível;
  - ignora elementos invisíveis (por causa do template oculto);
  - verifica contagens, textos e estados visíveis.
- **Isolamento:** limpar o armazenamento local (`fdo.prefs`, `fdo.autonomy`) e recarregar antes de cada teste. Com relógio e dados fixos, os resultados são determinísticos.
- **Cenários mínimos**, um por grupo de histórias. Os números esperados vêm das validações dos PRs:
  - **Estado inicial:** faixas 3 / 5 / 11 / 7; subtítulo "11 pendentes · 2 concluídas"; selecionada a Kato, "Follow-up pós-demonstração".
  - **Prioridade:** 11 itens abertos hoje com chip e próxima ação; o "Por quê?" da Vértice lista 3 sinais e a conta do valor esperado (R$ 84 mil × 60% × 1,2 = R$ 60,5 mil).
  - **Adiar e desfazer:** em "Alinhamento de onboarding", a sugestão do Mark leva as faixas para 3 / 4 / 11 / 8; Desfazer volta para 3 / 5 / 11 / 7.
  - **Descartar:** a atividade sai das pendentes e recebe a tag "Descartada".
  - **Teclado:** esvaziar a fila de hoje só com ⌘/Ctrl+Enter (Kato) e E repetido, até a faixa Hoje mostrar "0 atividades"; J no campo de resultado não muda a seleção.
  - **Busca ⌘K:** "serra" leva a "Retomar contato após pausa no projeto".
  - **Foco em receita:** 26 pendentes, "R$ 169,2 mil esperados", com a Vértice no topo (R$ 60,5 mil).
  - **Preferências:** desligar "Abrir ação automaticamente" e escolher "Ficar na atividade" continuam valendo depois de recarregar.
  - **Autonomia:** começa com 3 aprovações; com o E-mail em "Executar sozinho", o Mark executa 2 ações (2 de 20) e a resposta ao Paulo (R$ 84 mil) fica nas Aprovações.
  - **WhatsApp:** `Confirmar recebimento da proposta` mostra a conversa, o sinal âmbar e o aviso de 24 h; enviar pelo Smark conclui; Desfazer devolve a conversa a 2 mensagens.
  - **Pós-atividade:** em "Registrar notas do diagnóstico", Gravar áudio, concluir e aplicar com uma mudança desmarcada dá "CRM atualizado: 3 mudanças", valor R$ 31.000 e a próxima atividade em sex, 25/09.
  - **Briefing:** o aviso "Em 30 min: Apresentação de proposta · Grupo Vértice (10:30)" leva ao briefing completo.
  - **Plano das atrasadas:** com "Conferir NF" trocada para Descartar, o resultado é "5 executadas, 2 para hoje, 0 para amanhã, 1 descartada", com faixas 0 / 0 / 13 / 7.
  - **Sessão de ligações:** 3 ligações (Atendeu, Não atendeu, Pular) terminam no resumo "1 atendida e concluída · 1 para tentar amanhã · 1 pulada".
- **Referência:** o repositório ainda não tem testes automatizados. A referência são as validações registradas na seção "Testes" de cada PR (#11 a #20), feitas por interação no navegador. Elas devem virar a primeira suíte.

## Out of Scope

- Integrações reais: envio de e-mail, WhatsApp Business API, telefonia ou discador, agenda, sincronização de CRM e transcrição de áudio. No protótipo tudo isso é simulado.
- Modelo real de pontuação, de probabilidade de ganho e de sinais. Hoje os valores são definidos à mão.
- Verificação de LGPD: base legal por contato, retenção e opt-out. Aparece só como texto na Central do Mark.
- Persistência das atividades em servidor, múltiplos usuários, permissões e visão do gestor.
- Layout responsivo ou móvel (a tela tem 1440 px fixos), modo escuro e internacionalização.
- A página inicial e as demais telas do Smark.

## Further Notes

- **Origem:** a especificação consolida a pesquisa competitiva (`docs/research/2026-09-28-fique-de-olho-concorrencia.md`) e as issues #1 a #10. As decisões de produto das issues #5 a #10 eram suposições do protótipo e estão nas tabelas "Decisões tomadas" dos PRs #15 a #20. **Precisam de validação com o negócio**, principalmente:
  - as probabilidades por etapa;
  - os níveis padrão de autonomia;
  - o limite de R$ 50 mil;
  - o limite de 20 ações automáticas por dia.
- **Antes de produção:** revisão jurídica de LGPD para envio automático e sincronização de conversas.
- **Para rodar localmente:** servir a pasta da página na porta 5173. Quando o navegador embutido guarda cache, recarregar com um parâmetro de versão na URL.
- **Telefones e conversas:** os números de telefone e as conversas de WhatsApp são fictícios.

