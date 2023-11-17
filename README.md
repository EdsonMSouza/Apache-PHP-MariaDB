# Guia de Instalação: Apache + PHP + MySQL

Bem-vindo ao repositório dedicado à instalação e configuração do ambiente Apache, PHP e MySQL no sistema operacional __LINUX__. Este guia abrangente e detalhado foi criado para simplificar o processo de configuração dessas poderosas ferramentas, permitindo que você crie um ambiente de desenvolvimento robusto e eficiente em pouco tempo.

## Objetivo do Repositório

O objetivo principal deste repositório é fornecer um conjunto claro de instruções e scripts para instalar e configurar o Apache como servidor web, o PHP como linguagem de script do lado do servidor e o MySQL como sistema de gerenciamento de banco de dados. Ao seguir este guia passo a passo, você estará pronto para começar a desenvolver e testar suas aplicações web em um ambiente local.

## Conteúdo

1. Instruções Detalhadas: Fornece instruções passo a passo para a instalação do Apache, PHP e MySQL em diferentes sistemas operacionais, incluindo Windows, Linux e macOS.

2. Scripts Automatizados: Disponibilizamos scripts prontos para automatizar o processo de instalação sempre que possível. Isso economizará seu tempo e garantirá uma configuração consistente.

3. Configuração Otimizada: Incluímos dicas e truques para otimizar o desempenho e a segurança do seu ambiente de desenvolvimento, garantindo uma experiência de desenvolvimento eficiente.

## Como Usar Este Guia

* __Iniciantes__: Se você está começando agora, siga as instruções passo a passo para configurar seu ambiente de desenvolvimento local.

* __Desenvolvedores Experientes__: Utilize os scripts fornecidos para uma instalação rápida e personalizável. Adapte as configurações conforme necessário para atender aos requisitos específicos do seu projeto.

* __Contribuição__: Sua contribuição é bem-vinda! Se você encontrar melhorias possíveis, problemas ou tiver sugestões, sinta-se à vontade para abrir uma issue ou enviar um pull request. Juntos, podemos tornar este guia uma referência valiosa para a comunidade de desenvolvedores.

Prepare-se para criar aplicações web poderosas e eficientes com a combinação confiável do Apache, PHP e MySQL!

## Pré-Requisitos

Para facilitar a instalação e configuração em servidores remotos, este guia inclui um tópico adicional sobre como realizar todas as etapas utilizando __SSH__. Isso é especialmente útil para ambientes de produção ou servidores de hospedagem em nuvem.

### Conexão SSH

Certifique-se de ter acesso SSH ao servidor onde deseja configurar o ambiente. Use o seguinte comando para se conectar ao seu servidor a partir da sua máquina:

```bash
ssh seu_usuario@seu_servidor
```

Este método via SSH oferece flexibilidade e segurança, permitindo que você gerencie e configure seu ambiente de desenvolvimento ou produção de qualquer lugar do mundo. Isso permite que você execute comandos no servidor remoto como se estivesse na sua máquina.

## Atualização do Linux

O comando abaixo irá atualizar os __índices__ do sistema.

```bash
sudo apt update
```

O comando abaixo irá atualizar os __pacotes__ atualizáveis.

```bash
sudo apt upgrade
```

## Instalação de Ferraments Essenciais

Vamos instlar um pacote de ferramentas para podermos lidar com questões como IP, DNS, etc. Nesse pacote está disponível o `ifconfig` que permite verificar os IPs da máquina.

```bash
sudo apt install net-tools
```


Uma vez efetuada a conexão remota, vamos executar alguns comandos para atualizar o sistema e instalar algumas ferramentas importantes:

1. Atualizar índices: 

Primeiro, precisaremos atualizar o índice do repositório do sistema para instalar a versão mais recente do Apache2 (Servidor Web)