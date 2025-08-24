# sample-flask-auth

Repositório criado para armazenar o código de uma API de autenticação com banco de dados utilizando Flask.

## Arquitetura e Tecnologias

*   **Linguagem:** Python
*   **Framework:** Flask
*   **Banco de Dados:** MySQL
*   **ORM:** Flask-SQLAlchemy
*   **Autenticação:** Flask-Login
*   **Containerização:** Docker (para o banco de dados)

## Pré-requisitos

*   Python 3.x
*   Pip
*   Docker
*   Docker Compose
*   Postman

## Configuração e Execução

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/cadugr/sample-flask-auth.git
    cd sample-flask-auth
    ```

2.  **Inicie o container do banco de dados com o Docker Compose:**
    ```bash
    docker-compose up -d
    ```

3.  **Crie e ative um ambiente virtual (virtualenv):**
    ```bash
    python3 -m venv .venv
    source .venv/bin/activate  # No Windows, use: .venv\Scripts\activate
    ```

4.  **Instale as dependências do Python:**
    ```bash
    pip3 install -r requirements.txt
    ```

5.  **Crie as tabelas no banco de dados:**

    Abra o terminal interativo do Flask:
    ```bash
    flask shell
    ```

    Dentro do shell, importe o objeto `db` e crie as tabelas:
    ```python
    db.create_all()
    d.session.commit()
    exit()
    ```

6.  **Execute a aplicação Flask:**
    ```bash
    python3 app.py
    ```

A API estará em execução no endereço `http://127.0.0.1:5000`.

## Testando com o Postman

Para testar os endpoints da API, você pode utilizar o Postman. Siga os passos abaixo:

1.  **Instale o Postman:**
    Faça o download e instale o Postman a partir do [site oficial](https://www.postman.com/downloads/).

2.  **Importe a coleção:**
    *   Abra o Postman e clique em "Import".
    *   Selecione o arquivo `api/tests/API de autenticação.postman_collection.json`.

3.  **Configure o ambiente:**
    A coleção utiliza uma variável `{{baseUrl}}`. Para configurá-la, crie um ambiente (environment) no Postman:
    *   Clique no ícone de environments no menu lateral esquerdo.
    *   Clique em "+".
    *   Dê um nome ao ambiente (por exemplo, "Development").
    *   Adicione uma variável com o nome `baseUrl` e no campo "INITIAL VALUE" e "CURRENT VALUE" insira `http://127.0.0.1:5000`.
    *   Clique em "Add" para salvar o ambiente.
    *   Selecione o ambiente que você acabou de criar no menu dropdown no canto superior direito.

4.  **Fluxo de Teste:**

    *   **Crie um usuário:** Utilize a requisição "Create User" da coleção para criar um novo usuário. 
    *   **Torne o usuário um administrador (Opcional):** Para testar os endpoints que exigem permissão de administrador, você precisará atualizar manualmente a role do usuário no banco de dados. Conecte-se ao seu banco de dados MySQL e execute o seguinte comando SQL (substitua `1` pelo ID do usuário que você criou):
        ```sql
        UPDATE user SET role = 'admin' WHERE id = 1;
        ```
    *   **Faça o login:** Utilize a requisição "Login" para autenticar e obter um cookie de sessão.
    *   **Teste os outros endpoints:** Agora você pode testar os outros endpoints da coleção, como "Get user", "Update user" e "Delete user".