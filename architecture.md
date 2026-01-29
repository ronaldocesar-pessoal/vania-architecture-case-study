# Arquitetura da tecnologia Vânia

Este documento descreve a arquitetura base da tecnologia Vânia, independentemente da identidade visual, nome da assistente ou domínio de cada cliente.

Visão geral
A solução é composta por três camadas principais, com fronteiras claras de responsabilidade.

Componentes
Chat UI
- Responsável pela experiência do usuário e controle do fluxo conversacional.
- Não possui segredos nem integração direta com o provedor de IA.

Chat API
- Camada de mediação confiável.
- Aplica regras de comportamento, empacota contexto e integra com o provedor.

Provedor de IA
- Dependência externa baseada em LLM.

Fronteiras de confiança
- A UI é considerada não confiável para lógica crítica.
- A API concentra regras e governança.
- O provedor é tratado como serviço externo substituível.

Evolução prevista
- Estratégias mais sofisticadas de seleção de contexto.
- Fortalecimento progressivo de segurança.
- Observabilidade proporcional ao uso real.
