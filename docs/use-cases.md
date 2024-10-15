

Use cases
Reduce Cloud Costs
Coder reduces cloud costs by automatically shutting down unused resources and starting them back up right before developers begin their day. Augment or replace expensive, always-on VMs or VDI solutions that your developers hated anyway.

Build and Test Faster
Cloud computers can build and test large codebases at breakneck speeds, saving hours of developer time per week. Coder workspaces can run on existing VM, Kubernetes, and other computing infrastructure, putting unused resources to work.

Ver casos de uso do Crafting: https://docs.sandboxes.cloud/docs/use-case-preview

https://www.gitpod.io/docs/introduction/use-cases

## Challenges / Pain points

Who is CPS1 for?

### Equipes paradas aguardando por ambiente bloqueado
É comum um projeto de software ter um ambiente de desenvolvimento/homologação/QA/Staging estático, que é compartilhado por múltiplos desenvolvedores e precisa de um revezamento para testar alguma entrega.

Muitas vezes a existência desses ambientes estáticos acabam engargalando entregas e exigindo um grande esforço de coordenação entre pessoas para o seu uso, evitando conflitos

É comum que uma demanda mais prioritária acabe se sobrepondo a outra, causando um grande impacto de trabalho para a troca de contexto do ambiente, retirando uma versão que estaria sendo validada, por outra que se tornou mais prioritária.
Isso gera uma enorme retrabalho para nova troca de contexto do ambiente

Uma CDE tem a capacidade de subir ambientes isolados sob demanda para cada desenvolvedor. Eliminando o tempo de espera e otimizando recursos através do desligamento automático de ambientes inativos.

### Excesso de tempo na configuração de um ambiente
Todo ambiente de desenvolvimento precisa de um conjunto de ferramentas para que o desenvolvedor consiga realizar as atividades do “ciclo interno”. Ex: interpretador/compilador de linguagem de programação, motor de containers, git, bibliotecas do SO para instalar dependências/pacotes, editor de texto e seus plugins (IDE).

Instruções para configurar ambiente geralmente são incompletas e/ou estão desatualizadas em alguma documentação, às vezes distante do código do projeto.

Dependendo do tamanho e complexidade da aplicação, são necessárias muitas horas para instalação e configuração das ferramentas e podem depender diretamente da capacidade de processamento e memória do laptop

Uma CDE usa como fundação containers e a definição de ambiente como código. Isso faz com que a definição do ambiente sempre esteja atualizada. A imagem de container que descreve o ambiente de desenvolvimento já está com tudo pré-instalado, portanto o tempo para subir um novo ambiente de desenvolvimento é de alguns segundos.

### Onboarding de novos desenvolvedores é longo e custoso
A rotatividade de desenvolvedores na equipe de desenvolvimento pode causar uma constante perda de conhecimento sobre como configurar e lidar com ambiente local (CONHECIMENTO TRIBAL)

Manter a documentação atualizada é sempre desafiador e requer uma forte cultura, pois geralmente mudanças no processo de desenvolvimento não são formalizadas de maneira reproduzível

Outro conjunto de atividades que fazem parte de um processo de onbarding é treinar o desenvolvedor sobre como ele deve executar tarefas rotineiras no projeto, por exemplo: execução de testes unitários, execução de formatadores de código, etc. Geralmente esses pequenos comandos não são bem documentados pelos desenvolvedores.
Solução: Utilizar uma CDE faz com que não um desenvolvedor tenha um ambiente pronto para trabalhar de maneira instantânea e mudanças na configuração do ambiente sempre vão refletir para todo o time, dispensando a necessidade de cada membro realizar mudanças localmente em seu laptop, assim acelerando o onboarding. Tarefas rotineiras no desenvolvimento passam a ser sempre padronizadas, fazendo com que cada desenvolvedor execute exatamente os mesmos comandos.


### Alta incidência de deployments com falha
Uma das grandes causas de falhas no deployment (implantação) de software são por problemas de divergências de configuração de ambientes, onde a aplicação encontra configurações em ambiente de produção diferentes do ambiente onde ela foi desenvolvida

Esse tipo de falha é comum pela dificuldade que um time pode ter em desenvolver a aplicação de maneira mais fiel em relação às dependências de recursos/componentes que existem em produção mas não existem no ambiente desenvolvimento local

Solução: Uma CDE sempre entregará para cada desenvolvedor um ambiente fortemente alinhado com a produção, sem necessidade de configuração pelos desenvolvedores e com recursos computacionais mais adequados do que laptop local, reduzindo a chance de falhas de deployment por divergências de configurações de ambientes

### É difícil reproduzir erros encontrados em produção no ambiente de desenvolvimento
O testador que sabe reproduzir o erro, portanto é importante de alguma forma entregar para ele uma maneira segura de repetir as ações e monitorar

Dificuldade de supervisionar o que o usuário faz que acarreta no erro, uma vez que em muitas empresas desenvolvedores não têm acesso ao ambiente de produção

Os mesmos passos que causam o erro em produção não causam o erro em ambiente de desenvolvimento, gerando uma enorme dificuldade de reproduzir o problema e ter que lidar com a síndrome do “na minha máquina funciona”.

Solução: Uma CDE entrega um ambiente mais próximo ao de produção, facilitando a reprodução desses problemas. Além disso, a CDE entrega URLs acessíveis por terceiros e permite mudanças no código da aplicação pulando a etapa de implantação no ambiente de desenvolvimento/QA/staging/etc. Portanto é muito fácil o desenvolvedor subir o nível dos logs, adicionar mais logs/prints no código e pedir para que o testador reexecute os passos.