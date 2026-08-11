Atividade — 11/08/2026
1. Problema
Uma startup enfrenta dificuldades na organização e acompanhamento de seus projetos, principalmente em relação à comunicação interna, controle de tarefas, identificação de atrasos e visibilidade gerencial.

Atualmente, as informações estão distribuídas entre diferentes ferramentas, dificultando a consolidação dos dados e aumentando a necessidade de atualizações manuais por parte dos funcionários e gestores.

2. Solução Proposta
A solução consiste no desenvolvimento de um sistema de gestão ágil integrado a um agente de Inteligência Artificial (LLM).

O agente será responsável por coletar, interpretar e consolidar informações provenientes das ferramentas utilizadas pela empresa, como:

GitHub;

Obsidian;

Trello;

Google Drive;

WhatsApp.

A VPS será responsável por hospedar e intermediar as integrações entre os serviços, utilizando APIs, webhooks e/ou MCPs.

O Obsidian funcionará como o "cérebro" de conhecimento, armazenando e organizando informações relevantes dos projetos para que a LLM possa consultá-las quando necessário.

O sistema permitirá que os funcionários enviem informações por texto ou áudio, principalmente durante as dailies. A LLM poderá interpretar essas informações, consultar os dados existentes nas ferramentas integradas e gerar atualizações para a equipe e para os gestores.

3. Requisitos de Negócio
RN01 — Melhorar a comunicação interna
A solução deve facilitar a comunicação entre os membros da equipe, reduzindo a necessidade de atualizações manuais e repetitivas.

Objetivo
Centralizar e automatizar o compartilhamento de informações relacionadas ao andamento dos projetos.

RN02 — Reduzir atrasos nos projetos
A solução deve permitir identificar antecipadamente:

Tarefas atrasadas;

Impedimentos;

Riscos;

Atividades sem atualização;

Possíveis problemas que possam comprometer os prazos.

Objetivo
Permitir que gestores e equipes atuem de forma preventiva antes que os problemas afetem o cronograma dos projetos.

RN03 — Aumentar a visibilidade da gestão
Os gestores devem possuir uma visão consolidada do andamento dos projetos e das atividades da equipe.

Objetivo
Facilitar a tomada de decisões por meio de informações centralizadas e atualizadas.

RN04 — Otimizar processos internos
A solução deve automatizar atividades relacionadas ao acompanhamento de:

Dailies;

Weeklies;

Sprints;

Tarefas;

Impedimentos;

Progresso dos projetos.

Objetivo
Reduzir o trabalho manual e tornar o acompanhamento dos projetos mais eficiente.

RN05 — Centralizar informações
A solução deve utilizar as informações existentes nas ferramentas utilizadas pela empresa para gerar uma visão integrada dos projetos.

Objetivo
Evitar que informações importantes fiquem isoladas em diferentes sistemas e facilitar o acesso ao conhecimento da organização.

4. Stack Tecnológica
Tecnologia	Função
LLM / API de IA	Interpretação de mensagens, análise das informações e geração de respostas
VPS	Hospedagem do agente e centralização das integrações
GitHub	Repositórios de código e informações relacionadas ao desenvolvimento
Obsidian	Base de conhecimento e "cérebro" do agente
Trello	Organização e acompanhamento dos projetos e tarefas
Google Drive	Armazenamento de arquivos e documentos
WhatsApp	Interface de comunicação com os funcionários
APIs / MCPs	Integração entre o agente e as ferramentas
Webhooks	Comunicação e acionamento automático entre os sistemas
Observação: informações sensíveis, como senhas e credenciais de acesso, devem ser armazenadas de forma segura. O Google Drive não deve ser utilizado como armazenamento direto de senhas em texto puro.

5. Arquitetura Proposta
                         ┌─────────────────┐
                         │   Funcionário   │
                         └────────┬────────┘
                                  │
                           Texto ou Áudio
                                  │
                                  ▼
                         ┌─────────────────┐
                         │    WhatsApp     │
                         └────────┬────────┘
                                  │
                               Webhook
                                  │
                                  ▼
                         ┌─────────────────┐
                         │      VPS        │
                         │                 │
                         │  Agente / LLM   │
                         └────────┬────────┘
                                  │
                   ┌──────────────┼──────────────┐
                   │              │              │
                   ▼              ▼              ▼
              ┌─────────┐   ┌──────────┐   ┌─────────┐
              │ GitHub  │   │ Obsidian │   │ Trello  │
              └─────────┘   └──────────┘   └─────────┘
                   │              │              │
                   └──────────────┼──────────────┘
                                  │
                                  ▼
                            ┌───────────┐
                            │ Google    │
                            │ Drive     │
                            └─────┬─────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │      LLM        │
                         │                 │
                         │ Analisa dados   │
                         │ Identifica      │
                         │ riscos e gera   │
                         │ atualizações    │
                         └────────┬────────┘
                                  │
                              Webhook
                                  │
                                  ▼
                         ┌─────────────────┐
                         │ Grupo da        │
                         │ Empresa         │
                         │ (Daily)         │
                         └─────────────────┘
6. Fluxo de Funcionamento
6.1 Entrada da informação
O funcionário envia uma mensagem para o sistema através do WhatsApp.

A mensagem pode ser:

Texto;

Áudio.

6.2 Processamento
Caso a mensagem seja um áudio, o sistema realiza a transcrição do conteúdo.

Após a transcrição, a informação é encaminhada para o agente de IA.

Áudio
  ↓
Transcrição
  ↓
Texto
  ↓
LLM
6.3 Consulta às fontes de informação
A LLM recebe a informação enviada pelo funcionário e consulta as fontes disponíveis através da VPS.

                ┌─────────────┐
                │     LLM     │
                └──────┬──────┘
                       │
                 Consulta dados
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
     GitHub         Obsidian        Trello
        │              │              │
        └──────────────┼──────────────┘
                       │
                    Google Drive
Essas consultas podem ser realizadas utilizando APIs oficiais, APIs não oficiais quando apropriado, ou MCPs, dependendo da disponibilidade e das necessidades de cada integração.

7. Papel do Obsidian
O Obsidian será utilizado como o "cérebro" do sistema.

Ele terá a função de concentrar o conhecimento relacionado aos projetos, permitindo que a LLM consulte informações como:

Contexto dos projetos;

Requisitos;

Decisões tomadas;

Documentação;

Regras de negócio;

Histórico de atividades;

Informações importantes da equipe;

Registros de reuniões;

Informações relacionadas às sprints.

A ideia é que a LLM não dependa apenas das informações presentes na mensagem recebida, mas também possa consultar o conhecimento previamente armazenado.

8. Funcionamento da Daily
Um possível fluxo para a Daily seria:

Funcionário envia áudio/texto
            ↓
       WhatsApp
            ↓
          Webhook
            ↓
           VPS
            ↓
     Transcrição do áudio
            ↓
           LLM
            ↓
    Consulta das informações
            ↓
 GitHub / Obsidian / Trello / Drive
            ↓
      Análise pela LLM
            ↓
 Identificação de progresso,
 atrasos, impedimentos e riscos
            ↓
      Geração do resumo
            ↓
          Webhook
            ↓
     Grupo da empresa
9. Exemplo de Funcionamento
Um desenvolvedor pode enviar pelo WhatsApp:

"Ontem finalizei a API de autenticação, mas estou travado na integração com o banco porque estou esperando as credenciais."

O sistema poderá:

Receber o áudio ou texto;

Transcrever o áudio, caso necessário;

Identificar que a tarefa de autenticação foi concluída;

Identificar o impedimento relacionado às credenciais;

Consultar o Trello para verificar a tarefa correspondente;

Consultar o Obsidian para obter o contexto do projeto;

Registrar ou sugerir a atualização das informações;

Identificar o impedimento;

Gerar um resumo para a Daily;

Enviar a informação para o grupo da empresa.

Exemplo de resultado:

📋 Daily — Projeto X

👨‍💻 Desenvolvedor: João

✅ Concluído:
- API de autenticação.

🚧 Impedimento:
- Integração com o banco aguardando credenciais.

⚠️ Atenção:
- A ausência das credenciais pode impactar o prazo da tarefa.

📌 Próxima ação:
- Disponibilizar as credenciais necessárias para continuidade da integração.
10. Stakeholders
10.1 Gestores
Responsáveis por acompanhar o progresso dos projetos, identificar atrasos, analisar riscos e tomar decisões.

Necessidades
Visão consolidada dos projetos;

Identificação de atrasos;

Identificação de riscos;

Acompanhamento da equipe;

Indicadores de progresso.

10.2 Desenvolvedores
Responsáveis pela execução das atividades e pelo registro de progresso, dificuldades e impedimentos.

Necessidades
Registrar atividades rapidamente;

Comunicar impedimentos;

Atualizar tarefas;

Reduzir atividades manuais;

Interagir com o sistema por texto ou áudio.

10.3 Analistas de Negócio
Responsáveis por levantar, analisar e organizar as necessidades da empresa.

Necessidades
Organizar requisitos;

Acompanhar necessidades dos projetos;

Garantir alinhamento entre negócio e equipe técnica.

10.4 Engenheiros de Requisitos
Responsáveis pela documentação, análise e organização dos requisitos.

Necessidades
Centralizar requisitos;

Manter documentação atualizada;

Relacionar requisitos às atividades dos projetos;

Facilitar o rastreamento das mudanças.

10.5 Usuários / Funcionários
Interagem diretamente com o sistema, principalmente por meio de mensagens de texto ou áudio.

Necessidades
Facilidade de uso;

Comunicação rápida;

Pouca necessidade de preenchimento manual;

Possibilidade de enviar informações por áudio.

10.6 Equipe de Infraestrutura
Responsável pela manutenção da VPS, APIs, integrações e demais componentes técnicos.

Necessidades
Monitoramento dos serviços;

Segurança;

Disponibilidade;

Gerenciamento das integrações;

Controle de acessos;

Manutenção da infraestrutura.

10.7 LLM / Agente de IA
Componente responsável por interpretar informações, consultar as fontes de dados e gerar respostas e atualizações.

Responsabilidades
Interpretar mensagens;

Processar transcrições;

Consultar informações;

Correlacionar dados de diferentes ferramentas;

Identificar atrasos e impedimentos;

Gerar resumos;

Auxiliar na comunicação da equipe;

Automatizar atividades relacionadas às Dailies, Weeklies e Sprints.

11. Visão Geral da Solução
A solução proposta busca transformar diversas ferramentas isoladas em um ecossistema integrado de gestão ágil, no qual a LLM atua como uma camada inteligente entre os funcionários, gestores e as fontes de informação da empresa.

                    FUNCIONÁRIOS
                         │
                         ▼
                    ┌──────────┐
                    │ WhatsApp │
                    └────┬─────┘
                         │
                    Texto / Áudio
                         │
                         ▼
                    ┌──────────┐
                    │   VPS    │
                    └────┬─────┘
                         │
                         ▼
                    ┌──────────┐
                    │   LLM    │
                    │  AGENTE   │
                    └────┬─────┘
                         │
          ┌──────────────┼──────────────┐
          │              │              │
          ▼              ▼              ▼
       GitHub         Obsidian        Trello
          │              │              │
          └──────────────┼──────────────┘
                         │
                         ▼
                    Google Drive
                         │
                         ▼
                  ┌─────────────┐
                  │   Análise   │
                  │ Inteligente │
                  └──────┬──────┘
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
         Gestão / Alertas       Daily / Weekly
              │                     │
              └──────────┬──────────┘
                         ▼
                    Equipe / Gestores
12. Resultado Esperado
Com a implementação da solução, espera-se:

Melhorar a comunicação interna;

Reduzir atrasos nos projetos;

Identificar impedimentos antecipadamente;

Aumentar a visibilidade dos gestores;

Reduzir atualizações manuais;

Automatizar o acompanhamento de Dailies, Weeklies e Sprints;

Centralizar informações de diferentes ferramentas;

Facilitar o acesso ao conhecimento dos projetos;

Aumentar a eficiência dos processos internos.

## Fontes:
gpt para formatar
livro babok
