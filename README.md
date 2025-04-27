# Gerenciamento de Usuários (React + Vite)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) <!-- Exemplo de Badge de Licença -->

Um projeto CRUD (Create, Read, Update, Delete) para gerenciamento de usuários, desenvolvido com React e Vite. Ideal para demonstrar conceitos de frontend e integração com API.

*Este projeto foi desenvolvido como parte de um trabalho acadêmico.*

## 📋 Índice

-   [✨ Funcionalidades](#-funcionalidades)
-   [🚀 Tecnologias Utilizadas](#-tecnologias-utilizadas)
-   [🖼️ Screenshots (Opcional)](#️-screenshots-opcional)
-   [✅ Pré-requisitos](#-pré-requisitos)
-   [⚙️ Configuração do Projeto](#️-configuração-do-projeto)
-   [📁 Estrutura do Projeto](#-estrutura-do-projeto)
-   [🛠️ Como Utilizar](#️-como-utilizar)
-   [📜 Scripts Disponíveis](#-scripts-disponíveis)
-   [📝 Observações](#-observações)
-   [📄 Licença](#-licença)
-   [👨‍💻 Autor](#-autor)

## ✨ Funcionalidades

-   **Adicionar Usuário**: Formulário para cadastrar novos usuários (nome, e-mail, senha).
-   **Listar Usuários**: Exibe a lista de usuários cadastrados.
-   **Editar Usuário**: Permite editar o nome e o e-mail de um usuário existente.
-   **Excluir Usuário**: Remove um usuário da lista após confirmação.

## 🚀 Tecnologias Utilizadas

-   **Frontend**:
    -   [React](https://reactjs.org/): Biblioteca JavaScript para construção de interfaces de usuário.
    -   [Vite](https://vitejs.dev/): Ferramenta de build e servidor de desenvolvimento rápido.
    -   [Axios](https://axios-http.com/): Cliente HTTP baseado em Promises para requisições à API.
    -   CSS: Estilização da interface (pode incluir CSS Modules, Styled Components, etc., se aplicável).
-   **Desenvolvimento**:
    -   [ESLint](https://eslint.org/): Ferramenta para análise estática de código, identificando padrões problemáticos e garantindo a consistência do estilo.
    -   [Node.js](https://nodejs.org/): Ambiente de execução JavaScript.
    -   [npm](https://www.npmjs.com/) / [yarn](https://yarnpkg.com/): Gerenciadores de pacotes.

## 🖼️ Screenshots (Opcional)

*(Adicione aqui screenshots ou um GIF demonstrando a aplicação)*

*Exemplo:*
*![Screenshot da Tela Principal](link_para_sua_imagem.png)*
*![GIF Adicionando Usuário](link_para_seu_gif.gif)*

## ✅ Pré-requisitos

Antes de começar, garanta que você tenha instalado:

-   [Node.js](https://nodejs.org/) (versão 16 ou superior recomendada)
-   [npm](https://www.npmjs.com/) (geralmente vem com o Node.js) ou [yarn](https://yarnpkg.com/)

## ⚙️ Configuração do Projeto

Siga os passos abaixo para configurar e rodar o projeto localmente:

1.  **Clone o repositório**:
    *(Substitua `<URL_DO_REPOSITORIO>` pela URL real do seu repositório Git)*
    ```bash
    git clone <URL_DO_REPOSITORIO>
    cd frontend-react-crud-main # Ou o nome da pasta do projeto
    ```

2.  **Instale as dependências**:
    Escolha um gerenciador de pacotes:
    ```bash
    npm install
    ```
    *ou*
    ```bash
    yarn install
    ```

3.  **Configure as Variáveis de Ambiente**:
    Crie um arquivo chamado `.env` na raiz do projeto. Este arquivo **não** deve ser versionado (já está no `.gitignore`). Adicione a URL da sua API backend:
    ```env
    # Exemplo de configuração da URL da API
    VITE_API_URL=http://localhost:3001/usuarios
    ```
    *⚠️ **Importante**: Certifique-se de que o servidor da API backend esteja em execução e acessível na URL configurada.*

4.  **Inicie o servidor de desenvolvimento**:
    ```bash
    npm run dev
    ```
    *ou*
    ```bash
    yarn dev
    ```

A aplicação estará disponível por padrão em `http://localhost:5173`. Se a porta 5173 estiver em uso, o Vite poderá usar outra porta (verifique o output no terminal).

## 📁 Estrutura do Projeto

