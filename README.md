# ponderada_semana_2

Este documento descreve o processo para compilar, executar e testar o aplicativo Backstage em uma instância local usando Docker. Seguindo este guia, você será capaz de reproduzir o ambiente e acessar a funcionalidade de catálogo de serviços.

## Índice

- [ponderada\_semana\_2](#ponderada_semana_2)
  - [Índice](#índice)
    - [1. Pré-requisitos](#1-pré-requisitos)
    - [2. Instalação e Configuração](#2-instalação-e-configuração)
    - [3. Compilação da Imagem Docker](#3-compilação-da-imagem-docker)
    - [4. Execução da Instância Backstage](#4-execução-da-instância-backstage)
    - [5. Acesso e Verificação](#5-acesso-e-verificação)
    - [6. Evidências de Execução](#6-evidências-de-execução)

---

### 1. Pré-requisitos

Para executar esta aplicação, você precisa dos seguintes componentes instalados no sistema:

- **Node.js** versão LTS (recomendado: v18)
- **Yarn** para gerenciar dependências
- **Docker** para containerização

Certifique-se de que essas ferramentas estão acessíveis via linha de comando. Além disso, portas **3000** e **3000** devem estar abertas no firewall.

### 2. Instalação e Configuração

1. **Criação do Aplicativo Backstage:**
   Utilize o comando `npx` para criar o aplicativo Backstage (recomenda-se `npx @backstage/create-app@latest`).

   ```bash
   npx @backstage/create-app@latest
   cd my-backstage-app
   ```

2. **Instalação das Dependências:**
   Navegue até o diretório raiz do projeto e instale as dependências com `yarn`.

   ```bash
   yarn install --immutable
   ```

3. **Compilação do Backend:**
   Antes de construir a imagem Docker, compile o backend:

   ```bash
   yarn build:backend --config app-config.yaml --config app-config.production.yaml
   ```

### 3. Compilação da Imagem Docker

A seguir, construiremos a imagem Docker usando o Dockerfile fornecido em `packages/backend/Dockerfile`.

1. **Build da Imagem:**
   No diretório raiz do projeto, execute o seguinte comando para construir a imagem Docker:

   ```bash
   docker image build . -f packages/backend/Dockerfile --tag backstage
   ```

   **Nota**: Certifique-se de que o Docker está configurado corretamente e que o `daemon.json` (no diretório `/etc/docker/`) contém a configuração DNS apropriada se enfrentar problemas de conectividade com repositórios.

### 4. Execução da Instância Backstage

Após a construção da imagem, execute o contêiner Docker.

1. **Executar o Contêiner:**

   ```bash
   docker run -it -p 3000:3000 backstage
   ```

2. **Logs e Verificação:**
   Após iniciar o contêiner, você verá logs de execução no terminal. Quando o Backstage estiver em execução, ele poderá ser acessado no navegador.

### 5. Acesso e Verificação

Abra o navegador e acesse o Backstage na URL:

```plaintext
http://localhost:3000
```

Acesse a funcionalidade de catálogo de serviços no link [Backstage Demo Catalog](http://localhost:3000/catalog?filters%5Bkind%5D=component&filters%5Buser%5D=all) para verificar se o catálogo está funcionando conforme o esperado.

### 6. Evidências de Execução

Aqui estão alguns prints de tela para demonstrar a aplicação em execução:
<img width="1440" alt="Captura de Tela 2024-11-01 às 11 14 06" src="https://github.com/user-attachments/assets/b80c42dd-8a65-48b2-9183-711fa781626e">

<img width="1440" alt="Captura de Tela 2024-11-01 às 11 14 13" src="https://github.com/user-attachments/assets/5f368831-6918-464b-908a-2e41789306c8">

---

Essa documentação visa ser clara e completa, oferecendo instruções detalhadas e prints para fácil replicação do ambiente de desenvolvimento do Backstage. Em caso de dúvidas ou problemas, consulte a documentação oficial do [Backstage](https://backstage.io/).
