# Guia para Configuração de `.env` com Prisma

Este guia descreve como configurar o arquivo `.env` para dois tipos de banco de dados diferentes utilizando Prisma. Cada configuração será tratada de forma independente.

---

## 1. Configuração com SQLite

### Passos:
1. **Crie um novo projeto Node.js**:
    ```bash
    mkdir projeto-sqlite
    cd projeto-sqlite
    npm init -y
    ```

2. **Instale o Prisma**:
    ```bash
    npm install prisma --save-dev
    ```

3. **Inicialize o Prisma**:
    ```bash
    npx prisma init
    ```

4. **Configure o arquivo `.env`**:
    No arquivo `.env`, defina a variável `DATABASE_URL` para utilizar o SQLite:
    ```env
    DATABASE_URL="file:./dev.db"
    ```

5. **Atualize o arquivo `schema.prisma`**:
    No arquivo `prisma/schema.prisma`, configure o modelo desejado. Exemplo:
    ```prisma
    datasource db {
      provider = "sqlite"
      url      = env("DATABASE_URL")
    }

    generator client {
      provider = "prisma-client-js"
    }

    model User {
      id    Int    @id @default(autoincrement())
      name  String
      email String @unique
    }
    ```

6. **Crie o banco de dados e gere o cliente Prisma**:
    ```bash
    npx prisma migrate dev --name init
    npx prisma generate
    ```

7. **Teste a conexão**:
    Crie um arquivo `test.js` para verificar a conexão:
    ```javascript
    const { PrismaClient } = require('@prisma/client');
    const prisma = new PrismaClient();

    async function main() {
      const users = await prisma.user.findMany();
      console.log(users);
    }

    main()
      .catch(e => console.error(e))
      .finally(async () => await prisma.$disconnect());
    ```

---

## 2. Configuração com PostgreSQL

### Passos:
1. **Crie um novo projeto Node.js**:
    ```bash
    mkdir projeto-postgresql
    cd projeto-postgresql
    npm init -y
    ```

2. **Instale o Prisma**:
    ```bash
    npm install prisma --save-dev
    ```

3. **Inicialize o Prisma**:
    ```bash
    npx prisma init
    ```

4. **Configure o arquivo `.env`**:
    No arquivo `.env`, defina a variável `DATABASE_URL` para utilizar o PostgreSQL:
    ```env
    DATABASE_URL="postgresql://username:password@localhost:5432/database_name"
    ```

5. **Atualize o arquivo `schema.prisma`**:
    No arquivo `prisma/schema.prisma`, configure o modelo desejado. Exemplo:
    ```prisma
    datasource db {
      provider = "postgresql"
      url      = env("DATABASE_URL")
    }

    generator client {
      provider = "prisma-client-js"
    }

    model User {
      id    Int    @id @default(autoincrement())
      name  String
      email String @unique
    }
    ```

6. **Crie o banco de dados e gere o cliente Prisma**:
    ```bash
    npx prisma migrate dev --name init
    npx prisma generate
    ```

7. **Teste a conexão**:
    Crie um arquivo `test.js` para verificar a conexão:
    ```javascript
    const { PrismaClient } = require('@prisma/client');
    const prisma = new PrismaClient();

    async function main() {
      const users = await prisma.user.findMany();
      console.log(users);
    }

    main()
      .catch(e => console.error(e))
      .finally(async () => await prisma.$disconnect());
    ```

---

Pronto! Agora você sabe como configurar o arquivo `.env` para SQLite e PostgreSQL utilizando Prisma.