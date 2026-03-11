# Fundamentos CPS1

O CPS1 utiliza uma terminologia específica para modelar diversos workloads e estruturas de equipes.

Nosso framework é construído sobre quatro conceitos centrais: **Workspaces**, **Resources**, **Templates** e **Environments**.

## Workspaces

Um **Workspace** serve como um ambiente reproduzível projetado especificamente para o desenvolvimento de aplicações.

Ele contém o código-fonte, portas, linguagens de programação e várias ferramentas necessárias para construir e executar seu software.

Considere cada Workspace como uma unidade funcional que corresponde a um componente técnico específico da sua aplicação, como o frontend ou o backend.

O Workspace é acessível via SSH e a maioria das IDEs modernas suporta desenvolvimento remoto através deste protocolo.

IDEs comuns para desenvolvimento remoto incluem:

* [VS Code Remote Development](https://code.visualstudio.com/docs/remote/remote-overview)
* [IntelliJ IDEA Remote development overview](https://www.jetbrains.com/help/idea/remote-development-overview.html)
* [Zed Remote Development](https://zed.dev/docs/remote-development)

Um Workspace possui atributos que determinam como ele funciona. Esses atributos são: **Code Repositories**, **Packages**, **Network Ports** e **Environment Variables**.

### Packages

Cada Workspace utiliza uma container **Base Image** e um conjunto de **Packages**.

Esses Packages são integrados durante o processo de build do Workspace. Eles funcionam como unidades autônomas de instalação que normalmente incluem linguagens de programação, frameworks, libraries e ferramentas relevantes necessárias para construir, executar e testar o código da sua aplicação.

### Code Repositories

Para aprimorar ainda mais a Developer Experience, um Workspace pode ser configurado com um conjunto específico de repositórios Git. Esses repositórios são automaticamente clonados durante o processo de provisioning do Workspace, garantindo que o código esteja pronto para o desenvolvimento imediatamente após a inicialização.

### Network Ports

O CPS1 permite configurar e expor portas das aplicações que rodam dentro de um Workspace.

Cada porta configurada é mapeada automaticamente para uma URL única e segura.

Essas URLs de preview permitem que os membros da equipe compartilhem seu progresso e obtenham feedback instantaneamente, ignorando a necessidade de pipelines de CI/CD lentos.

#### Environment Variables

Um Workspace pode ser pré-configurado com um conjunto específico de Environment Variables que ficam imediatamente acessíveis após a inicialização.

Ao automatizar essa configuração, o CPS1 elimina a necessidade de os desenvolvedores realizarem configurações manuais, permitindo que permaneçam focados na escrita do código.

### Resources

Um **Resource** refere-se a uma dependência externa que uma aplicação requer para funcionar, como um banco de dados, cache ou message broker.

Um Resource pode ser provisionado internamente no cluster Kubernetes onde o CPS1 reside, ou pode gerenciar infraestrutura externa de provedores de nuvem pública em tempo de execução.

## Templates

Um **Template** é a configuração que dita como o CPS1 provisiona um **Environment**.

Ele atua como um manifesto que declara quais Workspaces (o código e as ferramentas) e quais Resources (a infraestrutura e dependências) são necessários.

Essa abordagem permite que Platform Engineers criem ambientes de desenvolvimento padronizados, garantindo que cada desenvolvedor comece com um setup idêntico e otimizado.

### Environments

No CPS1, um **Environment** é uma instância efêmera criada a partir de um Template específico.

Múltiplos Environments podem ser criados simultaneamente a partir de um único Template.

Ao utilizar ambientes independentes, os membros da equipe podem desenvolver, testar e experimentar sem o risco de interferir no progresso ou na estabilidade uns dos outros.

## Catalog

O CPS1 fornece uma ampla variedade de Packages e Resources testados e prontos para uso. Você pode explorar essas opções no CPS1 Catalog.

Para detalhes sobre linguagens, ferramentas e configurações suportadas, visite o repositório do CPS1 Catalog: [https://github.com/cps-1/helm-charts/tree/main/charts/cps1-catalog](https://github.com/cps-1/helm-charts/tree/main/charts/cps1-catalog).

## Resumo

- **Workspace**
    - A menor unidade de uma aplicação, representando partes relacionadas à tecnologia, como backend ou frontend.
    - Executa código, frequentemente expondo uma network port.
    - Atributos principais: **Code Repository**, **Packages**, **Network Ports** e **Environment Variables**.
    - Suporta repositórios **monorepos** (múltiplas linguagens de programação) e de **linguagem única**.
    - **Packages**: Instalam o runtime e as ferramentas na imagem de container final do Workspace.
    - **Network Ports**: Permitem a comunicação com o código em execução dentro do Workspace.
    - **Code Repository**: Faz o checkout automático do código no lançamento do Workspace.
    - **Environment Variables**: Definem a configuração e o comportamento da aplicação.

- **Resource**
    - Dependências externas como bancos de dados, caches ou message brokers.
    - Contém definições que ditam como um componente de infraestrutura específico deve ser criado e gerenciado.

- **Template**
    - Definição de como um ambiente de desenvolvimento deve ser provisionado.
    - Consiste em **Workspaces** e **Resources**.

- **Environment**
    - Um ambiente de desenvolvimento baseado em nuvem gerenciado em seu cluster Kubernetes.
    - Oferece capacidades aprimoradas em comparação com ambientes de desenvolvimento locais.
    - Workspaces e Resources provisionados.
