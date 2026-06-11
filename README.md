# Assistente de WhatsApp do Procon de Jacareí

## Visão geral

Este repositório documenta uma proposta de **assistente de WhatsApp** para o **Procon de Jacareí**, voltado ao **primeiro atendimento** do cidadão: orientação, triagem e encaminhamento.

O foco é automatizar o que for repetitivo, mantendo **clareza**, **rastreabilidade** e **fallback para atendimento humano** quando necessário.

## Escopo (resumo)

- orientar sobre direitos do consumidor e documentação;
- triagem inicial de reclamações/denúncias;
- direcionamento para serviços/fluxos internos;
- consulta de status/protocolo (quando houver integração);
- encaminhamento para humano em baixa confiança.

---

## Fluxo Geral de Atendimento

```text
Usuário -> WhatsApp -> Observador do WhatsApp -> Web Service de Orquestração
			 -> Pipeline de PLN -> Classificador de ML -> Regras de Negócio
			 -> Módulo de Geração de Texto -> Web Service -> WhatsApp -> Usuário
```

Em geral:

1. recebe a mensagem;
2. normaliza/processa (PLN);
3. classifica e aplica regras;
4. gera resposta;
5. envia de volta ao usuário.

---

## Requisitos (resumo)

- Atendimento inicial com linguagem clara e acessível.
- Roteamento por confiança (automático vs. humano).
- Rastreabilidade (histórico, logs e trilha de decisão).
- Segurança e conformidade (LGPD) para dados sensíveis.
- Escalabilidade e baixo acoplamento entre módulos.

---

## Product Backlog (Inicial)

Backlog inicial para orientar a evolucao incremental do assistente de WhatsApp do Procon de Jacareí.

| ID | Item de backlog | Historia de usuario | Prioridade | Criterio de aceite | Status |
|---|---|---|---|---|---|
| PB-01 | Recebimento de mensagens WhatsApp | Como cidadão, quero enviar mensagens e receber confirmação de recebimento para iniciar meu atendimento. | Alta | Mensagens de texto sao recebidas, registradas e respondidas com confirmacao em ate 5 segundos. | Concluido |
| PB-02 | Normalização e preprocessamento de texto | Como sistema, quero normalizar mensagens para reduzir ruido e melhorar a classificacao. | Alta | Pipeline aplica limpeza, tokenizacao e padronização antes da classificação em 100% das mensagens válidas. | Concluido |
| PB-03 | Geração de respostas pré designadas | Como cidadão, quero receber respostas iniciais padronizadas para obter orientação imediata no primeiro contato. | Alta | Sistema responde com templates validados por tipo de solicitação e registra o envio no histórico da conversa. | Concluido |
| PB-04 | Orquestracao de fluxos de atendimento | Como plataforma, quero decidir automaticamente a proxima ação com base em intenção, contexto e regras de negocio. | Alta | Orquestrador chama o servico correto por classe mapeada. | Pendente |
| PB-05 | Classificação de intencao com ML | Como atendente, quero que o sistema identifique a intenção principal da mensagem para rotear corretamente cada caso. | Alta | Classificador retorna intenção e confianca; quando confiança for menor que limiar definido, deve acionar fallback. | Concluido |
| PB-06 | Base de conhecimento institucional | Como sistema, quero consultar conteudo oficial do Procon para responder com informacoes atualizadas. | Media | Respostas de orientacao referenciam base validada e exibem data de atualizacao do conteudo. | Concluido |
| PB-07 | Escalonamento para atendimento humano | Como cidadao, quero ser encaminhado a um atendente quando o bot nao tiver confianca suficiente na resposta. | Media | Casos de baixa confianca ou erro sao encaminhados para fila humana com contexto da conversa. | Pendente |
| PB-08 | Seguranca e conformidade LGPD | Como instituicao, quero proteger dados pessoais e rastrear acessos para atender requisitos legais. | Alta | Dados sensiveis sao mascarados em logs; acessos e operacoes criticas ficam auditaveis. | Pendente |
| PB-09 | Autoaprendizado | Como sistema, quero poder aprender com os feedbacks dos usuários para refinar minhas respostas. | Media | Sistema gera respostas melhores conforme interações com usuários | Pendente |

### Criterios de priorizacao

- impacto no cidadao e no atendimento publico;
- risco operacional e juridico;
- dependencia tecnica entre servicos;
- ganho de valor nas primeiras entregas.

### Planejamento em 3 sprints (com pontuacao)

### Sprint 1 - Fundação do atendimento (13 pontos)

| ID | Item | Pontos |
|---|---|---|
| PB-01 | Recebimento de mensagens WhatsApp | 5 |
| PB-02 | Normalizacao e preprocessamento de texto | 3 |
| PB-03 | Geracao de respostas pré designadas | 5 |

### Sprint 2 - Inteligencia e governanca (21 pontos)

| ID | Item | Pontos |
|---|---|---|
| PB-04 | Orquestracao de fluxos de atendimento | 8 |
| PB-05 | Classificacao de intencao com ML | 8 |
| PB-06 | Base de conhecimento institucional | 5 |

### Sprint 3 - Expansao de servicos (18 pontos)

| ID | Item | Pontos |
|---|---|---|
| PB-07 | Escalonamento para atendimento humano | 5 |
| PB-08 | Seguranca e conformidade LGPD | 5 |
| PB-09 | Autoaprendizado | 8 |

### Escala de pontuacao utilizada

- 3 pontos: baixa complexidade;
- 5 pontos: media complexidade;
- 8 pontos: alta complexidade;

### Burndown das entregas

Total planejado do backlog atual: **52 pontos**.

#### Burndown geral por sprint

| Marco | Pontos planejados restantes | Pontos reais restantes | Entregas concluidas | Data da atualização |
|---|---:|---:|---:|---|
| Inicio (Kickoff) | 52 | 52 | 6/9 | 18-05-2026 |
| Fim Sprint 1 | 13 | 0 | 3/3 | 28-04-2026 |
| Fim Sprint 2 | 21 | 0 | 3/3 | 18-05-2026 |
| Fim Sprint 3 | 18 | 18 | 0/3 | A preencher |

#### Grafico burndown 
(Verde: Real, Azul : Esperado)

##### Sprint 1

```mermaid
xychart-beta
	title "Burndown Sprint 1 (Pontos Restantes)"
	x-axis [W0, W1, W2, W3, W4, W5]
	y-axis "Pontos" 0 --> 13
	line "planejado" [13, 13, 10, 5, 3, 0]
	line "real" [13, 13, 13, 10, 3, 0]
```

##### Sprint 2

```mermaid
xychart-beta
	title "Burndown Sprint 2 (Pontos Restantes)"
	x-axis [W0, W1, W2, W3, W4, W5]
	y-axis "Pontos" 0 --> 21
	line "planejado" [21, 13, 13, 8, 8, 0]
	line "real" [21, 16, 16, 16, 8, 0]
```

##### Sprint 3

```mermaid
xychart-beta
	title "Burndown Sprint 3 (Pontos Restantes)"
	x-axis [W0, W1, W2, W3, W4, W5]
	y-axis "Pontos" 0 --> 18
	line "planejado" [18, 14, 11, 7, 4, 0]
	line "real" [18, 18, 18, 18, 18, 18]
```

<!--#### Regra de atualizacao
- ao concluir uma historia, subtraia seus pontos do campo "Real restante";
- atualize o marco de fim da sprint no quadro geral;
- replique os numeros no grafico Mermaid (serie `real`) para manter o visual sincronizado.
-->

---

## Resumo

Proposta de assistente de WhatsApp para o **Procon de Jacareí**, com triagem e orientação no primeiro contato, evoluindo de forma incremental conforme o backlog e as metas de burndown.
