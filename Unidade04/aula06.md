# Atividade — 18/08/2026

# Sistema de Gestão para Clínica Médica

## 1. Stakeholders

Os stakeholders são as pessoas ou grupos que utilizam o sistema, participam do processo ou são afetados diretamente pelas mudanças que ele vai trazer para a clínica.

Neste projeto, foram identificados os seguintes stakeholders:

* **Paciente:** é o principal beneficiado pelo sistema. Deve conseguir realizar e acompanhar agendamentos, receber lembretes e ser informado quando houver alguma alteração em sua consulta.
* **Recepcionista:** utiliza o sistema no dia a dia para cadastrar pacientes, consultar horários, realizar agendamentos, cancelar consultas e controlar a chegada dos pacientes.
* **Médico:** utiliza o sistema para acompanhar sua agenda, consultar os pacientes agendados, organizar sua disponibilidade e registrar informações relacionadas ao atendimento.
* **Gerente da clínica:** acompanha o funcionamento da operação e utiliza os indicadores para identificar problemas e oportunidades de melhoria.
* **Equipe de TI:** é responsável pela manutenção, segurança, disponibilidade e evolução técnica do sistema.
* **Direção da clínica:** possui interesse nos resultados gerais do sistema, principalmente na redução de custos, melhora da organização e qualidade do atendimento.

Cada stakeholder possui necessidades diferentes. Por isso, o sistema deve considerar tanto as necessidades dos usuários que trabalham diretamente com a clínica quanto as necessidades dos gestores responsáveis por acompanhar os resultados.

---

## 2. Problemas de Negócio

Antes de definir as funcionalidades do sistema, foi necessário identificar os principais problemas enfrentados pela clínica.

### 2.1 Conflitos de horários

Um dos principais problemas é a possibilidade de ocorrerem conflitos de horários. Como as informações podem estar distribuídas em planilhas ou sistemas diferentes, um mesmo horário pode aparecer como disponível para mais de uma pessoa.

Isso pode causar:

* Dupla marcação de consultas;
* Sobrecarga do médico;
* Confusão na recepção;
* Necessidade de remarcar consultas;
* Insatisfação dos pacientes.

---

### 2.2 Retrabalho

Outro problema identificado é o retrabalho. Algumas informações precisam ser procuradas ou preenchidas novamente porque não estão centralizadas.

Por exemplo, um paciente que já possui cadastro pode precisar informar novamente seus dados básicos quando realiza uma nova consulta.

Isso aumenta:

* O tempo de atendimento;
* O trabalho da recepção;
* A possibilidade de erro;
* A insatisfação do paciente.

---

### 2.3 Duplicidade de informações

Sem um banco de dados centralizado e sem validações adequadas, existe a possibilidade de o mesmo paciente possuir mais de um cadastro.

Essa duplicidade pode gerar informações diferentes para uma mesma pessoa e dificultar a consulta do histórico correto.

---

### 2.4 Dificuldade para atualizar dados

Quando as informações estão distribuídas entre várias planilhas ou programas, uma alteração feita em um local pode não aparecer nos demais.

Isso faz com que diferentes usuários trabalhem com dados desatualizados.

---

### 2.5 Falhas na comunicação com os pacientes

A clínica também enfrenta dificuldades na comunicação com os pacientes.

Sem lembretes automáticos, o paciente pode esquecer a data ou o horário da consulta. Da mesma forma, quando ocorre uma alteração na agenda médica, pode ser difícil avisar todos os pacientes envolvidos.

---

### 2.6 Dificuldade para controlar cancelamentos

Quando uma consulta é cancelada, o horário pode ficar vazio até o final do dia.

Sem uma fila de espera ou algum processo de reocupação, a clínica perde a oportunidade de utilizar aquele horário para atender outro paciente.

---

## 3. Principais Causas dos Problemas

Os problemas identificados possuem relação principalmente com a forma como as informações são armazenadas e utilizadas.

As principais causas são:

* Utilização de planilhas individuais sem sincronização;
* Ausência de um banco de dados centralizado;
* Utilização de diferentes softwares para processos relacionados;
* Falta de atualização em tempo real da agenda;
* Ausência de lembretes automáticos;
* Falta de uma fila de espera organizada;
* Dependência de processos manuais;
* Falta de integração entre os envolvidos no processo.

A principal proposta do sistema é justamente centralizar essas informações e permitir que todos trabalhem com uma base única e atualizada.

---

# 4. Regras de Negócio

As regras de negócio representam condições que devem ser respeitadas durante o funcionamento do sistema.

Elas ajudam a garantir que os processos ocorram de acordo com as necessidades da clínica.

---

### RN01 — CPF válido e único

O cadastro de um paciente deve possuir um CPF válido.

O mesmo CPF não deve ser utilizado em mais de um cadastro ativo.

**Classificação:** Estudo de Caso — Duplicidade de informações.

---

### RN02 — Um paciente por horário

Um médico não deve possuir mais de um paciente agendado para o mesmo horário.

O sistema deve verificar a disponibilidade antes de concluir o agendamento.

**Classificação:** Estudo de Caso — Conflito de horários.

---

### RN03 — Agendamento dentro da escala

Os agendamentos devem ser realizados apenas nos horários que estiverem cadastrados como disponíveis na escala do médico.

Um paciente não deve ser agendado fora da disponibilidade cadastrada.

**Classificação:** Processo de Negócio.

---

### RN04 — Liberação após cancelamento

Quando uma consulta for cancelada, o horário deve ficar disponível novamente.

O horário não deve continuar aparecendo como ocupado após o cancelamento.

**Classificação:** Estudo de Caso — Cancelamentos.

---

### RN05 — Alteração da agenda médica

Quando uma alteração na escala de um médico afetar pacientes já agendados, esses pacientes devem ser identificados.

O sistema deve gerar uma notificação para informar os pacientes sobre a alteração.

**Classificação:** Estudo de Caso — Mudanças de agenda.

---

### RN06 — Lembretes de consulta

Os pacientes devem receber lembretes automáticos antes de suas consultas.

Os lembretes devem ser enviados com 24 horas e 2 horas de antecedência.

**Classificação:** Estudo de Caso — Faltas.

---

### RN07 — Reutilização de dados

Quando o paciente já possuir um cadastro válido, seus dados básicos devem ser reutilizados nos próximos agendamentos.

O paciente não deve precisar informar novamente informações que já estejam cadastradas e atualizadas.

**Classificação:** Estudo de Caso — Retrabalho.

---

### RN08 — Acesso ao prontuário

As informações do prontuário devem ser acessadas apenas por usuários autorizados.

Usuários sem permissão não devem visualizar ou alterar informações médicas restritas.

**Classificação:** Segurança e privacidade.

---

### RN09 — Prioridade de reocupação

Caso um paciente não confirme sua consulta dentro do prazo definido pela clínica, o horário poderá ser identificado como prioridade para reocupação.

O processo deve respeitar as regras operacionais definidas pela clínica.

**Classificação:** Política operacional.

---

### RN10 — Início do atendimento

O atendimento deve seguir o fluxo definido pela clínica.

A consulta deve ser iniciada quando o paciente estiver identificado e com o status adequado para atendimento.

**Classificação:** Operacional da clínica.

---

# 5. Melhorias Propostas

| Problema                   | Melhoria                                                       |
| -------------------------- | -------------------------------------------------------------- |
| Conflitos de horários      | Implantação de uma agenda unificada e atualizada em tempo real |
| Retrabalho                 | Centralização das informações dos pacientes                    |
| Duplicidade de dados       | Validação de CPF único no cadastro                             |
| Dificuldade de atualização | Utilização de um banco de dados centralizado                   |
| Falhas na comunicação      | Envio automático de lembretes e notificações                   |
| Cancelamentos              | Liberação automática do horário e utilização de fila de espera |
| Falta de acompanhamento    | Criação de dashboards e indicadores                            |

A ideia principal é que as melhorias estejam diretamente relacionadas aos problemas encontrados.

Por exemplo, a fila de espera foi proposta para resolver a dificuldade de reaproveitar horários cancelados. Da mesma forma, os lembretes automáticos foram incluídos para ajudar a reduzir faltas.

---

# 6. Requisitos Funcionais

Os requisitos funcionais descrevem as ações que o sistema deve realizar.

Para manter os requisitos claros, foram utilizadas principalmente duas formas de escrita:

* **O sistema deve...** para definir o que é obrigatório;
* **O sistema não deve...** para definir o que não pode acontecer.

---

## RF01 — Gerenciamento de Pacientes

**Prioridade: Alta**

O sistema deve permitir cadastrar pacientes.

O sistema deve permitir consultar os dados cadastrados.

O sistema deve permitir atualizar informações do paciente.

O sistema deve permitir inativar um cadastro sem apagar o histórico já registrado.

O cadastro deve possuir, no mínimo, informações básicas para identificar e entrar em contato com o paciente.

O sistema deve validar o CPF informado.

O sistema não deve permitir dois pacientes ativos cadastrados com o mesmo CPF.

O sistema não deve apagar automaticamente o histórico do paciente quando seu cadastro for inativado.

---

## RF02 — Gerenciamento de Médicos e Escalas

**Prioridade: Alta**

O sistema deve permitir cadastrar médicos.

O sistema deve permitir registrar as especialidades dos médicos.

O sistema deve permitir cadastrar a escala e os horários de atendimento.

O sistema deve permitir atualizar a disponibilidade do médico.

O sistema deve permitir consultar os horários cadastrados.

O sistema não deve disponibilizar para agendamento um horário que esteja fora da escala ou bloqueado.

---

## RF03 — Consulta de Horários Disponíveis

**Prioridade: Alta**

O sistema deve permitir consultar os horários disponíveis para agendamento.

A consulta deve considerar o médico selecionado.

A consulta deve considerar a data escolhida.

O sistema deve considerar a escala cadastrada para o profissional.

O sistema deve atualizar os horários disponíveis sempre que ocorrer um novo agendamento, cancelamento ou bloqueio.

O sistema não deve apresentar como disponível um horário que já esteja ocupado ou bloqueado.

---

## RF04 — Agendamento de Consultas

**Prioridade: Muito Alta**

O sistema deve permitir realizar o agendamento de consultas.

Cada agendamento deve estar relacionado a um paciente, um médico, uma data e um horário.

O sistema deve verificar se o horário continua disponível antes de confirmar o agendamento.

O sistema deve impedir conflitos de horários.

O sistema não deve permitir dois agendamentos para o mesmo médico no mesmo horário.

Ao criar um novo agendamento, o sistema deve registrar inicialmente o status **"Agendado"**.

O sistema deve registrar a data e o horário em que o agendamento foi criado.

---

## RF05 — Cancelamento e Reagendamento

**Prioridade: Muito Alta**

O sistema deve permitir cancelar uma consulta.

O sistema deve registrar o cancelamento no histórico do agendamento.

O sistema deve alterar o status da consulta para **"Cancelado"**.

O sistema deve permitir reagendar uma consulta para outro horário disponível.

Antes de confirmar o reagendamento, o sistema deve verificar a disponibilidade do novo horário.

O sistema não deve manter dois horários ativos para a mesma consulta depois que o reagendamento for concluído.

---

## RF06 — Liberação Automática de Horários

**Prioridade: Muito Alta**

Quando uma consulta for cancelada, o sistema deve liberar o horário automaticamente.

O sistema deve atualizar a agenda após o cancelamento.

O horário liberado deve ficar disponível para novos agendamentos.

O horário também pode ser utilizado no processo de fila de espera.

O sistema não deve manter como ocupado um horário pertencente a uma consulta cancelada.

---

## RF07 — Lembretes Automáticos

**Prioridade: Muito Alta**

O sistema deve enviar lembretes automáticos para os pacientes que possuem consultas futuras.

O sistema deve enviar um lembrete com 24 horas de antecedência.

O sistema deve enviar outro lembrete com 2 horas de antecedência.

Os lembretes devem utilizar os canais de comunicação disponíveis e cadastrados pela clínica, como WhatsApp ou SMS.

O sistema deve registrar o envio das mensagens.

Quando o paciente responder à mensagem, o sistema deve registrar essa interação quando houver integração disponível.

O sistema não deve enviar lembretes para consultas canceladas.

---

## RF08 — Gerenciamento da Agenda pelo Médico

**Prioridade: Alta**

O sistema deve permitir que o médico consulte sua própria agenda.

O sistema deve permitir que o médico visualize seus horários e pacientes agendados.

O sistema deve permitir bloquear horários.

O sistema deve considerar os horários bloqueados durante novos agendamentos.

O sistema não deve permitir novos agendamentos em horários que estejam bloqueados.

Quando uma alteração na agenda afetar pacientes já agendados, o sistema deve identificar os pacientes envolvidos.

---

## RF09 — Prontuário Eletrônico

**Prioridade: Alta**

O sistema deve permitir registrar informações relacionadas às consultas no prontuário eletrônico.

Cada registro deve estar associado ao paciente correspondente.

O sistema deve permitir consultar o histórico autorizado do paciente.

O sistema deve controlar o acesso às informações conforme as permissões de cada usuário.

O sistema não deve permitir que usuários sem autorização visualizem ou alterem informações médicas restritas.

---

## RF10 — Fila de Espera

**Prioridade: Alta**

O sistema deve permitir cadastrar pacientes em uma fila de espera.

O sistema deve identificar horários que foram liberados após cancelamentos.

O sistema deve permitir relacionar pacientes da fila aos horários compatíveis com sua disponibilidade.

O sistema deve registrar o processo de contato e ocupação do horário.

O sistema não deve confirmar o mesmo horário para mais de um paciente.

---

## RF11 — Avisos sobre Alterações na Agenda

**Prioridade: Alta**

Quando ocorrer uma alteração na escala médica, o sistema deve identificar os pacientes afetados.

O sistema deve gerar avisos para os pacientes que possuem consultas impactadas.

O sistema deve registrar que a comunicação foi enviada.

O sistema não deve enviar notificações de alteração para pacientes que não foram afetados pela mudança.

---

## RF12 — Dashboard de Indicadores

**Prioridade: Média**

O sistema deve disponibilizar dashboards para acompanhamento do funcionamento da clínica.

O sistema deve apresentar indicadores relacionados a:

* Faltas dos pacientes;
* Ocupação da agenda;
* Cancelamentos;
* Reocupação de horários;
* Tempo de espera;
* Tempo de atendimento na recepção;
* Resposta aos lembretes;
* Satisfação dos pacientes;
* Disponibilidade do sistema;
* Tempo de resposta das consultas.

O sistema deve permitir visualizar os indicadores em períodos definidos.

---

## RF13 — Autoatendimento

**Prioridade: Alta**

O sistema deve disponibilizar um canal de autoatendimento para os pacientes.

O autoatendimento pode ser realizado por meio de um portal web ou chatbot integrado.

O sistema deve permitir consultar horários disponíveis.

O sistema deve validar o horário antes da confirmação do agendamento.

O sistema não deve confirmar um horário que já esteja ocupado.

As mesmas regras de disponibilidade utilizadas pela recepção devem ser respeitadas pelo autoatendimento.

---

## RF14 — Controle do Status do Atendimento

**Prioridade: Muito Alta**

O sistema deve controlar os seguintes status:

* **Agendado**;
* **Confirmado**;
* **Em Espera**;
* **Atendido**;
* **Cancelado**.

O sistema deve permitir atualizar o status conforme o andamento do atendimento.

Quando o paciente chegar à clínica, a recepção deve poder alterar seu status para **"Em Espera"**.

O sistema deve registrar as alterações importantes de status.

O sistema não deve permitir que uma consulta cancelada seja iniciada como atendimento.

---

## RF15 — Pesquisa de Satisfação

**Prioridade: Média**

Após a conclusão do atendimento, o sistema deve permitir o envio de uma pesquisa de satisfação.

A pesquisa deve estar relacionada ao atendimento realizado.

O sistema deve registrar as respostas recebidas.

As informações obtidas devem poder ser utilizadas nos indicadores de satisfação.

O sistema não deve enviar pesquisas para consultas canceladas.

---

# 7. Resumo dos Requisitos Funcionais

| Código | Requisito                           | Prioridade |
| ------ | ----------------------------------- | ---------- |
| RF01   | Gerenciamento de Pacientes          | Alta       |
| RF02   | Gerenciamento de Médicos e Escalas  | Alta       |
| RF03   | Consulta de Horários Disponíveis    | Alta       |
| RF04   | Agendamento de Consultas            | Muito Alta |
| RF05   | Cancelamento e Reagendamento        | Muito Alta |
| RF06   | Liberação Automática de Horários    | Muito Alta |
| RF07   | Lembretes Automáticos               | Muito Alta |
| RF08   | Gerenciamento da Agenda pelo Médico | Alta       |
| RF09   | Prontuário Eletrônico               | Alta       |
| RF10   | Fila de Espera                      | Alta       |
| RF11   | Avisos sobre Alterações na Agenda   | Alta       |
| RF12   | Dashboard de Indicadores            | Média      |
| RF13   | Autoatendimento                     | Alta       |
| RF14   | Controle do Status do Atendimento   | Muito Alta |
| RF15   | Pesquisa de Satisfação              | Média      |

---

# 8. Requisitos Não Funcionais

Os requisitos não funcionais definem características relacionadas à qualidade do sistema.

Eles ajudam a estabelecer como o sistema deve se comportar em relação a desempenho, segurança, disponibilidade e facilidade de uso.

---

## RNF01 — Desempenho da Busca

**Categoria: Desempenho**

O sistema deve apresentar os resultados da busca por horários disponíveis em até 2 segundos em condições normais de utilização.

---

## RNF02 — Segurança da Comunicação

**Categoria: Segurança**

Os dados transmitidos entre o usuário e o sistema devem utilizar uma conexão segura.

O sistema deve utilizar HTTPS/TLS para a comunicação entre a aplicação e seus usuários.

O sistema não deve transmitir informações sensíveis por conexões não seguras.

---

## RNF03 — Facilidade de Agendamento

**Categoria: Usabilidade**

A interface da recepção deve ser simples e objetiva.

O processo de agendamento deve exigir o menor número possível de etapas.

Depois que as informações principais estiverem definidas, a confirmação do agendamento deve ocorrer de forma rápida.

A meta do projeto é permitir a conclusão da operação principal de agendamento em até três ações principais.

---

## RNF04 — Disponibilidade

**Categoria: Disponibilidade**

O sistema deve manter uma disponibilidade mínima de 99,5% ao mês.

A disponibilidade deve ser monitorada para permitir o acompanhamento do indicador de uptime.

---

## RNF05 — Backup

**Categoria: Confiabilidade**

O sistema deve realizar backups automatizados do banco de dados diariamente.

Deve existir um processo que permita recuperar os dados quando necessário.

---

## RNF06 — Privacidade

**Categoria: Privacidade**

O tratamento dos dados pessoais deve respeitar as regras aplicáveis de proteção de dados.

O acesso às informações deve ser controlado de acordo com as permissões de cada usuário.

---

## RNF07 — Acessos Simultâneos

**Categoria: Desempenho**

O sistema deve suportar pelo menos 50 acessos simultâneos.

Durante esse período, as funcionalidades principais não devem apresentar perda significativa de desempenho.

---

## RNF08 — Autenticação em Duas Etapas

**Categoria: Segurança**

Médicos e gerentes devem utilizar autenticação em duas etapas quando acessarem o sistema.

O sistema não deve permitir que esses perfis acessem funcionalidades sensíveis apenas com senha quando a autenticação em duas etapas estiver ativa.

---

## RNF09 — Compatibilidade

**Categoria: Compatibilidade**

A aplicação web deve funcionar nos principais navegadores utilizados atualmente:

* Google Chrome;
* Mozilla Firefox;
* Microsoft Edge;
* Safari.

As funcionalidades principais devem continuar disponíveis nos navegadores suportados.

---

## RNF10 — Responsividade

**Categoria: Usabilidade**

A interface deve se adaptar a diferentes tamanhos de tela.

O sistema deve permitir a utilização das funcionalidades principais em:

* Computadores;
* Smartphones;
* Tablets.

---

# 9. Indicadores para Acompanhar o Processo

Os indicadores permitem acompanhar se o sistema está realmente ajudando a resolver os problemas identificados no início do projeto.

---

## 9.1 Taxa de No-Show

Representa o percentual de pacientes que não comparecem à consulta sem realizar o cancelamento.

Esse indicador ajuda a avaliar a quantidade de faltas e a eficiência dos lembretes automáticos.

**Fórmula:**

> Taxa de No-Show = (Quantidade de faltas / Total de consultas agendadas) × 100

---

## 9.2 Taxa de Ocupação da Agenda

Mostra a quantidade de horários preenchidos em relação ao total de horários disponíveis.

Esse indicador permite avaliar se a capacidade de atendimento da clínica está sendo bem aproveitada.

**Fórmula:**

> Taxa de Ocupação = (Horários ocupados / Total de horários disponíveis) × 100

---

## 9.3 Tempo Médio de Reocupação de Vaga

Mede quanto tempo um horário cancelado demora para ser ocupado novamente.

Quanto menor for esse tempo, mais eficiente tende a ser o processo de fila de espera e reaproveitamento da agenda.

---

## 9.4 Taxa de Conversão da Lista de Prioridade

Mostra o percentual de horários que foram recuperados e preenchidos utilizando a lista de prioridade ou fila de espera.

Esse indicador ajuda a verificar se o processo de reocupação está funcionando.

---

## 9.5 Tempo Médio de Atendimento na Recepção

Mede o tempo necessário para realizar o processo inicial do paciente na recepção.

Pode envolver a identificação do paciente, consulta do agendamento e alteração do status para **"Em Espera"**.

---

## 9.6 Tempo Médio de Espera do Paciente

Mede o tempo que o paciente permanece aguardando depois de ser registrado como **"Em Espera"** até o início do atendimento.

Esse indicador está diretamente relacionado à experiência do paciente.

---

## 9.7 Índice de Retrabalho no Cadastro

Acompanha situações em que os dados precisam ser cadastrados novamente ou corrigidos.

O objetivo é verificar se a centralização das informações está reduzindo o trabalho repetitivo.

---

## 9.8 Taxa de Resposta aos Lembretes

Mostra o percentual de pacientes que respondem aos lembretes enviados.

Esse indicador pode ajudar a avaliar o nível de interação dos pacientes com os canais de comunicação utilizados.

**Fórmula:**

> Taxa de Resposta = (Pacientes que responderam / Pacientes que receberam o lembrete) × 100

---

## 9.9 Índice de Satisfação do Paciente

Representa os resultados obtidos nas pesquisas de satisfação.

Os dados podem ser utilizados para identificar pontos positivos e problemas percebidos pelos pacientes.

---

## 9.10 Índice de Disponibilidade

Mostra o percentual de tempo em que o sistema permaneceu disponível.

Esse indicador permite acompanhar a meta de disponibilidade definida nos requisitos não funcionais.

---

## 9.11 Tempo de Resposta de Busca

Mede o tempo necessário para o sistema retornar os horários disponíveis.

O objetivo é verificar se o sistema está cumprindo a meta de resposta definida no RNF01.

---

# 10. Principais Requisitos e Priorização

A priorização foi feita considerando principalmente o impacto de cada requisito nos problemas identificados.

---

## 1º — Agendamento e Controle da Agenda

**RF03, RF04, RF05, RF06 e RF08**

Essa é a principal parte do sistema.

Os maiores problemas encontrados estão relacionados a:

* Conflitos de horários;
* Agendamentos incorretos;
* Cancelamentos;
* Horários bloqueados;
* Falta de atualização da agenda.

Por esse motivo, os requisitos relacionados ao agendamento possuem a maior prioridade.

---

## 2º — Cadastro e Organização das Informações

**RF01 e RF02**

Esses requisitos são importantes porque permitem centralizar as informações da clínica.

Eles ajudam a reduzir:

* Retrabalho;
* Duplicidade;
* Dados desatualizados;
* Erros durante o atendimento.

---

## 3º — Comunicação com os Pacientes

**RF07 e RF11**

A comunicação automática pode ajudar a reduzir faltas e evitar problemas quando ocorrerem mudanças na agenda.

Os lembretes e avisos tornam o processo mais rápido e reduzem a dependência de contatos realizados manualmente pela recepção.

---

## 4º — Fluxo de Atendimento

**RF09 e RF14**

Esses requisitos ajudam a acompanhar o paciente durante o processo de atendimento.

O controle de status permite saber em qual etapa o paciente está.

O prontuário permite registrar informações relacionadas às consultas, respeitando as permissões de acesso.

---

## 5º — Fila de Espera

**RF10**

A fila de espera é importante para evitar que horários cancelados permaneçam vazios.

Ela pode ajudar a melhorar a ocupação da agenda e aproveitar melhor os horários disponíveis.

---

## 6º — Autoatendimento

**RF13**

O autoatendimento permite que algumas atividades sejam realizadas sem depender exclusivamente da recepção.

O paciente pode consultar horários e realizar agendamentos pelos canais disponibilizados pela clínica.

---

## 7º — Gestão

**RF12**

O dashboard não é responsável diretamente pelo agendamento ou atendimento, mas é importante para acompanhar os resultados.

Os gestores podem utilizar os indicadores para identificar problemas e tomar decisões.

---

## 8º — Pesquisa de Satisfação

**RF15**

A pesquisa de satisfação permite acompanhar a opinião dos pacientes depois do atendimento.

Os resultados podem ser utilizados para identificar melhorias futuras.

---

# 11. Melhorias Futuras

Depois da implantação das funcionalidades principais, o sistema poderá receber novos recursos.

Algumas possibilidades são:

* Melhorias na fila de espera;
* Novos canais de comunicação;
* Integração com outros sistemas da clínica;
* Aplicativo móvel próprio;
* Sugestões automáticas de horários;
* Análise de padrões de faltas;
* Automação de processos administrativos;
* Integração com processos financeiros;
* Ampliação dos dashboards;
* Novos recursos de autoatendimento.

Essas melhorias não precisam fazer parte da primeira versão do sistema, mas podem ser consideradas conforme a necessidade da clínica.

---

# 12. Conclusão

O principal objetivo deste projeto é melhorar a organização dos processos da clínica por meio de um sistema integrado.

Os problemas identificados estão relacionados principalmente à falta de centralização das informações, à utilização de processos manuais e à dificuldade de comunicação entre os envolvidos.

Com a implantação do sistema, espera-se:

* Reduzir conflitos de horários;
* Evitar cadastros duplicados;
* Diminuir o retrabalho;
* Facilitar a atualização dos dados;
* Melhorar a comunicação com os pacientes;
* Reduzir faltas;
* Melhorar o controle de cancelamentos;
* Reaproveitar horários disponíveis;
* Organizar o fluxo de atendimento;
* Proteger informações sensíveis;
* Acompanhar os resultados por meio de indicadores.

O sistema não deve apenas substituir planilhas ou automatizar tarefas isoladas. A proposta é integrar os principais processos da clínica e permitir que as informações estejam organizadas, atualizadas e disponíveis para quem realmente precisa utilizá-las.

Dessa forma, a clínica poderá ter um processo de agendamento e atendimento mais organizado, com menos erros e maior facilidade para acompanhar os resultados.



