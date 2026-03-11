# Como o CPS1 se encaixa no seu workflow

Para entender nossa visão para o CPS1, primeiro você precisa conhecer os conceitos de inner e outer development loops. Esses termos descrevem duas fases do workflow de desenvolvimento de software.

O CPS1 pertence ao estágio de desenvolvimento de código do workflow, capacitando os desenvolvedores sem interromper as pipelines de CI/CD existentes. Ele aprimora o trabalho que os desenvolvedores fazem até que o código seja enviado para o source control, um processo conhecido como **inner development loop**.

O **inner development loop** refere-se ao ciclo de um desenvolvedor de codar, buildar e testar mudanças. Esse processo deve fornecer feedback rápido até que o código esteja pronto para revisão, normalmente como um pull request (PR). Esse processo ocorre no CPS1 em vez do computador do desenvolvedor dentro de um ambiente local.

No CPS1, os desenvolvedores acessam um **Workspace**, que serve como ponto de entrada para seu **Environment**. Um **Workspace** é um ambiente de desenvolvimento baseado em nuvem onde os desenvolvedores codam, buildam e testam o código da aplicação. Uma vez concluído, os desenvolvedores fazem o commit e o push do código para o source control, normalmente acionando as pipelines de CI/CD.

![CPS1 no seu workflow](assets/cps1-overview.png)

O **outer development loop** começa depois que um desenvolvedor faz o push do código para o repositório. Nesta fase, as mudanças são integradas ao main branch, normalmente acionando uma pipeline de CI/CD para testar e buildar o novo código. Esse processo produz um artefato pronto para produção para deployment.

Quais vantagens o CPS1 traz:

- Fornece um ambiente semelhante à produção com toda a infraestrutura, IDE e ferramentas necessárias para os desenvolvedores.
- Lançar aplicações complexas com uma versão específica do código para testes end-to-end, incluindo todos os serviços e dependências de resources.
- Desenvolver qualquer parte da aplicação diretamente na nuvem e ver as mudanças em tempo real, reduzindo o tempo de iteração.
- Libera os desenvolvedores e as equipes de plataforma do gerenciamento de provisioning de ambientes e dependências de resources.
- Elimina a complexidade de configurar ambientes locais e resolve discrepâncias entre desenvolvimento e produção.
