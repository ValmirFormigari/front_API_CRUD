# API CRUD de Usuários com Node.js, Express e Firebase Firestore

Este projeto implementa uma API RESTful básica para realizar operações **CRUD** (Criar, Ler, Atualizar, Deletar) em uma coleção de usuários armazenada no **Firebase Firestore**. Utiliza Node.js, Express, e o Firebase Admin SDK.

## ✨ Funcionalidades

*   Criação de novos usuários com nome, email e senha (senha é armazenada com hash **bcrypt**).
*   Listagem de todos os usuários cadastrados.
*   Busca de um usuário específico por ID.
*   Atualização dos dados (nome e email) de um usuário existente.
*   Deleção de um usuário por ID.
*   Uso de **HATEOAS** para links de navegação na API.
*   Validação básica de entrada e tratamento de erros.

## 🛠️ Pré-requisitos

*   [**Node.js**](https://nodejs.org/) (versão LTS recomendada)
*   [**npm**](https://www.npmjs.com/) (instalado com Node.js) ou [**Yarn**](https://yarnpkg.com/)
*   [**Git**](https://git-scm.com/)
*   Uma conta **Google** para usar o Firebase.

## 🚀 Configuração e Execução

Siga os passos abaixo para configurar e executar o projeto localmente:

1.  **Clonar o Repositório:**
    ```bash
    git clone <URL_DO_REPOSITORIO_GIT> api-crud-firebase
    cd api-crud-firebase
    ```
    *Substitua `<URL_DO_REPOSITORIO_GIT>` pela URL do repositório. O comando acima clona o projeto para uma pasta chamada `api-crud-firebase`.*

2.  **Configurar o Firebase:**
    *   Acesse o **Console do Firebase**.
    *   Crie um novo projeto ou selecione um existente.
    *   No menu lateral, vá para "**Build**" -> "**Firestore Database**".
    *   Clique em "**Criar banco de dados**".
    *   Escolha o modo de **teste** para desenvolvimento inicial. *Lembre-se que as regras de segurança no modo de teste permitem acesso aberto por um tempo limitado.* Para produção, configure regras de segurança adequadas.
    *   Selecione a localização do servidor Firestore.
    *   Aguarde a criação do banco de dados.
    *   No menu lateral, clique no ícone de engrenagem ⚙️ -> "**Configurações do projeto**".
    *   Vá para a aba "**Contas de serviço**".
    *   Selecione "Node.js" e clique no botão "**Gerar nova chave privada**". Confirme a geração.
    *   Um arquivo JSON será baixado (ex: `<project-id>-firebase-adminsdk-....json`).
    *   **Renomeie** este arquivo para `serviceAccountKey.json`.
    *   **Mova** o arquivo `serviceAccountKey.json` para a **raiz** do diretório do projeto (`api-crud-firebase`).
    *   **Importante:** Este arquivo contém credenciais sensíveis. Ele já está incluído no `.gitignore` para prevenir o envio acidental para o Git. **Nunca** o remova do `.gitignore` ou faça commit dele.

3.  **Configurar Variáveis de Ambiente:**
    *   Na raiz do projeto (`api-crud-firebase`), crie um arquivo chamado `.env`.
    *   Adicione o seguinte conteúdo, ajustando os valores conforme necessário:

    ```dotenv
    # .env

    # Caminho para a chave de serviço do Firebase Admin SDK.
    # O caminho relativo './serviceAccountKey.json' funciona se o arquivo
    # estiver na raiz do projeto e você executar o servidor a partir da raiz.
    # No Windows, pode ser necessário usar barras normais '/' ou barras invertidas duplas '\\'.
    GOOGLE_APPLICATION_CREDENTIALS=./serviceAccountKey.json

    # Porta em que o servidor Node.js será executado.
    PORT=3001

    # URL base da API (usada para links HATEOAS).
    # Certifique-se de que a porta aqui corresponde à variável PORT.
    API_BASE_URL=http://localhost:3001
    ```

4.  **Instalar Dependências:**
    No terminal, dentro do diretório raiz do projeto (`api-crud-firebase`), execute:
    ```bash
    npm install
    ```
    *(Ou `yarn install` se preferir)*

5.  **Executar o Projeto:**
    Ainda no diretório raiz, execute:
    ```bash
    node index.js
    ```
    O servidor deverá iniciar. Você verá mensagens no console como:
    ```
    Firebase Admin SDK inicializado com sucesso.
    Servidor rodando na porta 3001
    ```

## 📡 Endpoints da API

A API estará disponível na URL base configurada (padrão: `http://localhost:3001`).

*   **`POST /usuarios`**: Cria um novo usuário.
    *   **Corpo da Requisição (JSON):**
        ```json
        {
          "nome": "Nome Sobrenome",
          "email": "email@exemplo.com",
          "senha": "senhaSegura123"
        }
        ```
    *   **Resposta (Exemplo - Status 201 Created):**
        ```json
        {
          "id": "userIdGeradoPeloFirestore",
          "nome": "Nome Sobrenome",
          "email": "email@exemplo.com",
          "_links": {
            "self": { "href": "http://localhost:3001/usuarios/userIdGeradoPeloFirestore" },
            "collection": { "href": "http://localhost:3001/usuarios" }
          }
        }
        ```

*   **`GET /usuarios`**: Lista todos os usuários.
    *   **Resposta (Exemplo - Status 200 OK):**
        ```json
        {
          "_links": {
            "self": { "href": "http://localhost:3001/usuarios" }
          },
          "_embedded": {
            "usuarios": [
              {
                "id": "userId1",
                "nome": "Usuário Um",
                "email": "um@exemplo.com",
                "_links": {
                  "self": { "href": "http://localhost:3001/usuarios/userId1" }
                }
              },
              {
                "id": "userId2",
                "nome": "Usuário Dois",
                "email": "dois@exemplo.com",
                "_links": {
                  "self": { "href": "http://localhost:3001/usuarios/userId2" }
                }
              }
              // ... outros usuários
            ]
          }
        }
        ```

*   **`GET /usuarios/:id`**: Busca um usuário pelo seu ID.
    *   **Resposta (Exemplo - Status 200 OK):**
        ```json
        {
          "id": "userIdEspecifico",
          "nome": "Nome do Usuário",
          "email": "usuario@exemplo.com",
          "_links": {
            "self": { "href": "http://localhost:3001/usuarios/userIdEspecifico" },
            "collection": { "href": "http://localhost:3001/usuarios" }
          }
        }
        ```
    *   **Resposta (Exemplo - Status 404 Not Found):**
        ```json
        {
          "message": "Usuário não encontrado"
        }
        ```

*   **`PUT /usuarios/:id`**: Atualiza o nome e/ou email de um usuário.
    *   **Corpo da Requisição (JSON):** (pelo menos um campo é necessário)
        ```json
        {
          "nome": "Novo Nome",
          "email": "novoemail@exemplo.com"
        }
        ```
    *   **Resposta (Exemplo - Status 200 OK):**
        ```json
        {
          "id": "userIdAtualizado",
          "nome": "Novo Nome",
          "email": "novoemail@exemplo.com",
          "_links": {
            "self": { "href": "http://localhost:3001/usuarios/userIdAtualizado" },
            "collection": { "href": "http://localhost:3001/usuarios" }
          }
        }
        ```

*   **`DELETE /usuarios/:id`**: Deleta um usuário pelo seu ID.
    *   **Resposta (Exemplo - Status 204 No Content):** (Sem corpo na resposta)

Use ferramentas como **Postman**, **Insomnia**, ou `curl` para interagir com a API.

## 📁 Estrutura do Projeto (Simplificada)

