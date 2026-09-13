## 1. Análise do Problema

A Clínica Médica objeto deste estudo atende múltiplas especialidades (clínica geral, pediatria, ortopedia, cardiologia e ginecologia), realizando atendimentos particulares e por convênios/planos de saúde. O crescimento da base de pacientes nos últimos anos não foi acompanhado por uma evolução equivalente dos processos administrativos e assistenciais, que ainda dependem fortemente de controles manuais, planilhas eletrônicas e prontuários em papel.
O agendamento de consultas é realizado majoritariamente por telefone, o que gera filas de espera, erros de digitação e conflitos de horário na agenda dos médicos. O prontuário do paciente é parcialmente físico, dificultando o acesso ao histórico clínico em atendimentos de urgência ou por outros profissionais da clínica.
O faturamento de convênios é feito manualmente, com alto índice de glosas (recusa de pagamento pela operadora) por preenchimento incorreto de guias. Não existem indicadores consolidados de desempenho, o que impede a gestão de tomar decisões baseadas em dados.
O problema central pode ser sintetizado como: **a ausência de um sistema integrado de gestão clínica gera retrabalho administrativo, perda de informações assistenciais, baixa eficiência operacional e perda financeira por falhas no ciclo de faturamento, comprometendo a experiência do paciente e a sustentabilidade do negócio.**
Este documento apresenta a análise de stakeholders, a modelagem do processo atual (AS-IS), as melhorias propostas, a modelagem do processo futuro (TO-BE), as regras de negócio, os requisitos funcionais e não funcionais do sistema a ser desenvolvido, os indicadores de acompanhamento e a priorização dos principais requisitos.

---

## 2. Stakeholders

| Stakeholder | Papel no processo | Interesse / Expectativa |
|---|---|---|
| **Paciente**                                        | Solicita e recebe o atendimento médico                | Agilidade no agendamento, atendimento sem erros, sigilo de dados |
| **Recepcionista / Atendente**                       | Realiza o agendamento, check-in e cadastro            | Ferramenta simples e rápida, redução de retrabalho manual        |
| **Médico(a)**                                       | Realiza a consulta, registra o prontuário e prescreve | Acesso rápido ao histórico do paciente, agenda sem conflitos     |
| **Enfermagem / Técnico**                            | Apoia a triagem e o pré-atendimento                   | Fila organizada, dados clínicos disponíveis                      |
| **Setor Financeiro / Faturamento**                  | Fatura convênios e particulares, controla recebíveis  | Redução de glosas, faturamento automatizado e rastreável         |
| **Coordenação / Gerência da clínica**               | Gerencia a operação e a equipe                        | Indicadores de desempenho e visão consolidada da operação        |
| **Diretoria / Sócios**                              | Define estratégia e investimentos                     | Sustentabilidade financeira e crescimento da clínica             |
| **Operadoras de plano de saúde (convênios)**        | Autoriza e paga procedimentos                         | Guias corretas no padrão TISS, elegibilidade validada            |
| **Setor de TI / Suporte**                           | Mantém e evolui o sistema                             | Sistema estável, documentado e seguro                            |
| **Órgãos reguladores (ANS, CFM, ANPD/LGPD)**        | Regulam o setor de saúde e a proteção de dados        | Conformidade legal e proteção de dados sensíveis de saúde        |

---

## 3. Processo AS-IS (Situação Atual)

O processo atual de atendimento ao paciente, do agendamento ao pagamento, é predominantemente manual e fragmentado entre diferentes ferramentas (telefone, planilhas, papel).

### 3.1 Descrição do fluxo macro (AS-IS)

* Paciente liga para a clínica solicitando agendamento de consulta.
* Recepcionista consulta a agenda física/planilha do médico e verifica disponibilidade manualmente.
* Recepcionista anota os dados do paciente (muitas vezes repetidos, sem verificação de cadastro existente).
* Não há envio de lembrete automático; a confirmação da consulta depende do paciente lembrar a data.
* No dia da consulta, o paciente chega e aguarda em fila física na recepção, sem controle de senha/tempo de espera.
* Recepcionista localiza a ficha/prontuário físico do paciente (quando existente) ou abre uma nova ficha.
* Médico realiza a consulta e registra anotações no prontuário de papel.
* Se necessário, o médico prescreve exames ou medicamentos manualmente (papel).
* Recepção calcula o valor a cobrar (particular) ou monta a guia de convênio manualmente.
* Guias de convênio são enviadas em lote, posteriormente, ao final do mês, para faturamento — com alto risco de erro e glosa.
* Pagamento particular é registrado em planilha; não há conciliação automática com o financeiro.
* Prontuário físico é arquivado; não há histórico digital consolidado nem indicadores de gestão.

### 3.2 Modelo do processo AS-IS (raia de atores)

| Etapa | Ator responsável | Descrição |
|---:|---|---|
| 1                              | Paciente      | Liga para a clínica solicitando agendamento                    |
| 2                              | Recepcionista | Verifica disponibilidade manualmente (papel/planilha)          |
| 3                              | Recepcionista | Registra dados do paciente (possível duplicidade de cadastro)  |
| 4                              | Paciente      | Comparece (ou não) na data agendada — sem lembrete automático  |
| 5                              | Recepcionista | Recebe o paciente e organiza fila física de espera             |
| 6                              | Recepcionista | Busca prontuário físico ou abre novo                           |
| 7                              | Médico        | Realiza a consulta e registra em papel                         |
| 8                              | Médico        | Prescreve receita/exames manualmente                           |
| 9                              | Recepcionista | Calcula valor particular ou monta guia de convênio manualmente |
| 10                             | Financeiro    | Envia guias de convênio em lote mensal (risco de glosa)        |
| 11                             | Financeiro    | Registra pagamento particular em planilha isolada              |
| 12                             | Recepcionista | Arquiva prontuário físico — sem histórico digital consolidado  |

---

## 4. Problemas Identificados e Melhorias Propostas

| Problema identificado (AS-IS) | Melhoria proposta (para o TO-BE) |
|---|---|
| Agendamento manual por telefone, sujeito a erro e demora      | Agendamento online (app/portal) e por telefone integrado a uma agenda única e centralizada      |
| Alto índice de faltas (no-show) por falta de lembrete         | Envio automático de lembretes por SMS/WhatsApp/e-mail com confirmação de presença               |
| Prontuário em papel, sem histórico consolidado                | Prontuário Eletrônico do Paciente (PEP) único, acessível a todos os profissionais autorizados   |
| Fila física de espera sem controle de tempo                   | Fila digital com senha eletrônica e painel de chamada                                           |
| Faturamento manual de convênios com alto índice de glosa      | Geração automática de guias no padrão TISS, com validação de elegibilidade antes do atendimento |
| Conciliação financeira manual e sujeita a erro                | Controle financeiro integrado, com status de pagamento por consulta/paciente                    |
| Ausência de indicadores de gestão                             | Painel gerencial (dashboard) com indicadores em tempo real                                      |
| Risco de vazamento/perda de dados sensíveis de saúde          | Controle de acesso por perfil, criptografia e trilha de auditoria (conformidade com a LGPD)     |
| Duplicidade de cadastro de pacientes                          | Cadastro único validado por CPF, com verificação de duplicidade                                 |

---

## 5. Processo TO-BE (Situação Futura)

No processo futuro, o Sistema de Gestão para Clínica Médica passa a integrar agendamento, prontuário eletrônico, fila de atendimento, faturamento e indicadores em uma única plataforma, eliminando etapas manuais redundantes e reduzindo o risco de erro humano.

### 5.1 Descrição do fluxo macro (TO-BE)

* Paciente agenda a consulta pelo aplicativo/portal ou por telefone, com verificação automática de disponibilidade e de conflito de agenda.
* Sistema valida o cadastro do paciente (evitando duplicidade) e, se for consulta por convênio, valida a elegibilidade da carteirinha em tempo real.
* Sistema envia confirmação e lembretes automáticos (SMS/WhatsApp/e-mail) antes da consulta.
* Paciente realiza check-in digital (app, totem ou recepção) e entra automaticamente na fila eletrônica.
* Painel de senhas chama o paciente; recepção acompanha o status da fila em tempo real.
* Médico acessa o Prontuário Eletrônico do Paciente (PEP), com todo o histórico clínico disponível.
* Médico registra a consulta, prescreve receitas/exames e assina digitalmente os documentos.
* Sistema gera automaticamente a fatura particular ou a guia TISS do convênio, já vinculada ao atendimento.
* Setor financeiro acompanha o status de pagamento e o envio/retorno das guias de convênio em tempo real.
* Indicadores de desempenho (agenda, faturamento, satisfação, glosas) são atualizados automaticamente em um painel gerencial.

### 5.2 Modelo do processo TO-BE (raia de atores)

| Etapa | Ator responsável | Descrição (apoiada pelo sistema) |
|---:|---|---|
| 1                                                     | Paciente / Sistema    | Agendamento online com verificação automática de disponibilidade         |
| 2                                                     | Sistema               | Validação de cadastro único e de elegibilidade de convênio               |
| 3                                                     | Sistema               | Envio automático de confirmação e lembretes                              |
| 4                                                     | Paciente              | Check-in digital (app/totem/recepção)                                    |
| 5                                                     | Sistema               | Inclusão automática na fila eletrônica e chamada por painel              |
| 6                                                     | Médico                | Acesso ao Prontuário Eletrônico do Paciente (PEP) com histórico completo |
| 7                                                     | Médico                | Registro da consulta e assinatura digital de receitas/exames             |
| 8                                                     | Sistema               | Geração automática de fatura particular ou guia TISS                     |
| 9                                                     | Financeiro / Sistema  | Acompanhamento do status de pagamento e de glosas                        |
| 10                                                    | Coordenação / Sistema | Atualização automática de indicadores no painel gerencial                |

Em síntese, o ganho do TO-BE em relação ao AS-IS está na automação das etapas de verificação, comunicação e faturamento, na centralização da informação clínica em um único prontuário eletrônico e na disponibilização de indicadores em tempo real para a gestão.

---

## 6. Regras de Negócio

| Código | Regra de negócio |
|---|---|
| **RN01**               | Toda consulta deve estar vinculada a um paciente cadastrado, identificado por CPF válido e único.                                                                      |
| **RN02**               | Um mesmo médico não pode possuir dois agendamentos confirmados no mesmo intervalo de horário (conflito de agenda).                                                     |
| **RN03**               | Consultas por convênio exigem validação da elegibilidade e da carteirinha antes da confirmação do agendamento.                                                         |
| **RN04**               | Cancelamentos com menos de 4 horas de antecedência, sem justificativa, geram registro de falta (no-show) e, para atendimento particular, podem gerar cobrança de taxa. |
| **RN05**               | O prontuário eletrônico só pode ser acessado por profissionais de saúde autorizados e vinculados ao atendimento do respectivo paciente.                                |
| **RN06**               | Toda alteração no prontuário deve ser registrada em histórico, sendo proibida a exclusão ou sobrescrita de registros anteriores.                                       |
| **RN07**               | O faturamento de convênios deve seguir o padrão eletrônico TISS vigente definido pela ANS.                                                                             |
| **RN08**               | Receitas, atestados e laudos emitidos pelo médico devem ser assinados digitalmente pelo profissional responsável.                                                      |
| **RN09**               | Dados sensíveis de saúde devem ser armazenados de forma criptografada, mediante consentimento do paciente, em conformidade com a LGPD.                                 |
| **RN10**               | O reagendamento de uma mesma consulta é permitido no máximo 2 (duas) vezes sem necessidade de aprovação da coordenação da clínica.                                     |
| **RN11**               | Somente a coordenação/gerência pode conceder descontos ou isenções de taxa de cancelamento.                                                                            |

---

## 7. Requisitos Funcionais

| Código | Requisito Funcional |
|---|---|
| **RF01**                  | O sistema deve permitir cadastrar pacientes com dados pessoais, contato, convênio e histórico clínico.               |
| **RF02**                  | O sistema deve permitir agendar consultas online e presencialmente, validando conflitos de horário na agenda médica. |
| **RF03**                  | O sistema deve enviar lembretes automáticos de consulta por SMS, WhatsApp e/ou e-mail.                               |
| **RF04**                  | O sistema deve permitir check-in digital do paciente (aplicativo, totem ou recepção).                                |
| **RF05**                  | O sistema deve gerenciar a fila eletrônica de atendimento, com chamada por painel.                                   |
| **RF06**                  | O sistema deve permitir o registro do prontuário eletrônico (anamnese, diagnóstico, evolução e prescrição).          |
| **RF07**                  | O sistema deve permitir a emissão de receitas e atestados com assinatura digital.                                    |
| **RF08**                  | O sistema deve permitir solicitar exames e anexar os respectivos resultados ao prontuário do paciente.               |
| **RF09**                  | O sistema deve gerar automaticamente a fatura particular ou a guia TISS para atendimentos por convênio.              |
| **RF10**                  | O sistema deve controlar e exibir o status de pagamento de cada atendimento (pendente, pago, glosado).               |
| **RF11**                  | O sistema deve gerar relatórios gerenciais e indicadores de desempenho da clínica.                                   |
| **RF12**                  | O sistema deve controlar o acesso às informações por perfil de usuário (recepção, médico, financeiro, gestor).       |
| **RF13**                  | O sistema deve registrar cancelamentos e faltas, aplicando as regras de negócio associadas (RN04).                   |
| **RF14**                  | O sistema deve permitir o reagendamento de consultas, respeitando o limite definido em RN10.                         |
| **RF15**                  | O sistema deve validar a elegibilidade do convênio do paciente antes da confirmação do agendamento.                  |

---

## 8. Requisitos Não Funcionais

| Código | Requisito Não Funcional |
|---|---|
| **RNF01**                     | Disponibilidade mínima do sistema de 99% em horário de funcionamento da clínica (SLA).                                                 |
| **RNF02**                     | O sistema deve estar em conformidade com a LGPD e com o sigilo médico, incluindo consentimento e controle de acesso a dados sensíveis. |
| **RNF03**                     | O tempo de resposta das operações principais (agendamento, check-in, consulta ao prontuário) deve ser inferior a 3 segundos.           |
| **RNF04**                     | A interface do sistema deve ser responsiva, funcionando em desktop, tablet e smartphone.                                               |
| **RNF05**                     | O sistema deve realizar backup automatizado diário dos dados, com possibilidade de restauração.                                        |
| **RNF06**                     | O sistema deve manter trilha de auditoria (log) de todo acesso e alteração em prontuários.                                             |
| **RNF07**                     | A arquitetura do sistema deve ser escalável, permitindo a inclusão de novas unidades/filiais da clínica.                               |
| **RNF08**                     | O sistema deve ter usabilidade que permita o treinamento da equipe de recepção em no máximo 4 horas.                                   |
| **RNF09**                     | O sistema deve se integrar, via API, com operadoras de saúde no padrão TISS.                                                           |
| **RNF10**                     | Os dados devem ser criptografados em trânsito e em repouso.                                                                            |

---

## 9. Indicadores de Acompanhamento do Processo

| Indicador | Fórmula / Descrição | Meta sugerida |
|---|---|---|
| **Taxa de absenteísmo (no-show)**               | (Nº de faltas / Nº total de consultas agendadas) × 100                    | < 8% ao mês  |
| **Tempo médio de espera na recepção**           | Soma do tempo de espera de todos os pacientes / Nº de pacientes atendidos | < 15 minutos |
| **Taxa de ocupação da agenda médica**           | (Horários ocupados / Horários disponíveis) × 100                          | > 85%        |
| **Taxa de glosa de convênios**                  | (Valor glosado / Valor total faturado em convênios) × 100                 | < 5%         |
| **Tempo médio de recebimento (convênio)**       | Média de dias entre o envio da guia e o efetivo pagamento                 | < 30 dias    |
| **Satisfação do paciente (NPS)**                | Pesquisa de satisfação pós-atendimento                                    | NPS > 70     |
| **% de prontuários completos**                  | (Prontuários preenchidos corretamente / total de atendimentos) × 100      | > 98%        |
| **Número médio de reagendamentos por paciente** | Total de reagendamentos / Nº de pacientes que reagendaram                 | < 1,5        |

---

## 10. Priorização dos Requisitos

A priorização foi realizada utilizando a técnica **MoSCoW** (*Must have, Should have, Could have, Won't have now*), considerando o impacto no problema central, a viabilidade técnica e o valor entregue ao paciente e à gestão da clínica.

| Prioridade | Requisitos | Justificativa |
|---|---|---|
| **Must have (essencial)**                 | RF01, RF02, RF06, RF09, RF12, RN01, RN02, RN05, RNF02, RNF06, RNF10 | Sem cadastro único, agendamento sem conflito, prontuário eletrônico, faturamento e controle de acesso, o sistema não resolve o problema central nem atende à LGPD. |
| **Should have (importante)**              | RF03, RF04, RF08, RF10, RF15, RN03, RN04, RNF01, RNF03              | Reduzem diretamente o no-show, a glosa e o tempo de espera — impacto financeiro e operacional relevante, mas o sistema funciona sem eles no curto prazo.           |
| **Could have (desejável)**                | RF05, RF11, RF13, RF14, RN10, RN11, RNF04, RNF08                    | Agregam valor à experiência e à gestão, porém podem ser entregues em uma segunda fase sem comprometer a operação básica.                                           |
| **Won't have now (fora do escopo atual)** | RNF07 (multiunidade), RNF09 (integração ampla multioperadora TISS)  | Dependem de maturidade do sistema na primeira unidade e de negociação técnica com cada operadora; ficam previstas para fases futuras do projeto.                   |

---

## Conclusão

Este documento foi produzido pela equipe de Engenharia de Requisitos como resultado das **Etapas 1 a 9 da atividade da Unidade 3 — Processos de Negócio**, cobrindo a análise do problema, a identificação de stakeholders, a modelagem AS-IS, a proposta de melhorias, a modelagem TO-BE, as regras de negócio, os requisitos funcionais e não funcionais, os indicadores e a priorização dos requisitos.

---
