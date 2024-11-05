Telemetria e updates
Repository templates and scaffolding (stackspot do Itaú)
App compute and memory limits
Métricas/analytics (dashboard)
ABAC
Integração com CI/CD
Webhook GitHub (https://docs.github.com/en/webhooks/webhook-events-and-payloads?actionType=opened#pull_request) (mandar URL com ambiente de preview quando criar um PR)
inventar integrações (slack)
RBAC VS ABAC
Mostrar os logs de auditoria e possibilitar exportar para CSV
Group Mapping/Sync <> Grupos do diretório do usuário aparecem como grupos no CPS1
Autenticação: SAML (parece ser o ideal para o mundo Enterprise), OAuth, azure ad; OpenID Connect?
Audit log: CPS1 gera log de auditoria e armazena internamente para mostrar na dashboard por padrão, e é configurável para enviar o log de auditoria para um serviço externo (datadog, cloudwatch, logstash, etc)
Vai ser servir para reporting & analytics
Vamos embedar o loki ou postgres e deixar configurável os prazos de retenção dos logs
Vamos deixar configurável enviar os logs para um destino e o que seria logado
Exportação para CSV
RBAC: tem que ter, vamos entregar com uma pré-configuração, a princípio Admin, Manager, Developer (TBD)
Group Mapping/Sync <> Grupos do diretório do usuário aparecem como grupos no CPS1
Gerenciar projetos (criar, arquivar, incluir e remover usuários, definir configurações do projeto)
Controle de acesso a uma lista de repositórios que devem pertencer a um projeto específico. Usuários desse workspace podem utilizar um conjunto específico de repositórios
Quem pode criar stacks usando o sistema de templates.
Criar template, publicar template, arquivar, deletar, etc
Integrações
Criar/parar workspace sob demanda de um PR/MR
API que chama as tasks do workspace para usar no CI/CD
Documentar casos de uso de ferramentas de DevOps
Alguma exportação CSV de algo
Ver o rolê de controle de quais projetos git podem ter workspace. Importante pra governança, um dev não pode pegar qualquer repositório git e sair fazendo workspace no freestyle
Documentação de exemplos de ferramentas externas de banco de dados ou de preparação de ambiente, como Neon e aquelas outras que embaralham para LGPD
API do CPS1 ou instrumentação ou sei lá que pra que ele seja monitorado por um time de Ops. /healthz
