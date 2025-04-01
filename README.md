# Guia para Inicializar um Projeto com Node.js, Next.js e Prisma no Windows

Este guia descreve como configurar um projeto utilizando Node.js, Next.js e Prisma, executando os comandos no terminal do VS Code.

---

## 1. Inicializando o Projeto Node.js

### Passos:
1. **Crie uma pasta para o projeto**:
    ```bash
    mkdir meu-projeto
    cd meu-projeto
    ```

2. **Inicialize o projeto Node.js**:
    ```bash
    npm init -y
    ```

3. **Instale o Next.js e React**:
    ```bash
    npm install next react react-dom
    ```

4. **Adicione um script para rodar o Next.js** no `package.json`:
    ```json
    "scripts": {
      "dev": "next dev",
      "build": "next build",
      "start": "next start"
    }
    ```

5. **Crie a estrutura básica do Next.js**:
    ```bash
    mkdir pages
    echo "export default function Home() { return <h1>Olá, Next.js!</h1>; }" > pages/index.js
    ```

6. **Inicie o servidor de desenvolvimento**:
    ```bash
    npm run dev
    ```

---

## 2. Configurando o Prisma

### Passos:
1. **Instale o Prisma**:
    ```bash
    npm install prisma --save-dev
    ```

2. **Inicialize o Prisma**:
    ```bash
    npx prisma init
    ```

    Isso criará um arquivo `prisma/schema.prisma` e uma pasta `.env`.

3. **Configure o banco de dados no arquivo `.env`**:
    Exemplo para SQLite:
    ```env
    DATABASE_URL="file:./dev.db"
    ```

4. **Crie o banco de dados e gere o cliente Prisma**:
    ```bash
    npx prisma migrate dev --name init
    npx prisma generate
    ```

---

## 3. Possíveis Erros e Soluções

### Erro: `npm: command not found`
- **Causa**: Node.js não está instalado ou não está no PATH.
- **Solução**: Instale o [Node.js](https://nodejs.org/) e reinicie o terminal.

### Erro: `npx: command not found`
- **Causa**: Node.js está desatualizado.
- **Solução**: Atualize o Node.js para a versão mais recente.

### Erro: `DATABASE_URL is not set`
- **Causa**: Variável de ambiente não configurada.
- **Solução**: Verifique o arquivo `.env` e reinicie o terminal.

### Erro: `Prisma Client is not generated`
- **Causa**: O cliente Prisma não foi gerado.
- **Solução**: Execute `npx prisma generate`.

---

## 4. Rodando o Projeto

1. **Inicie o servidor Next.js**:
    ```bash
    npm run dev
    ```

2. **Teste a conexão com o banco de dados**:
    Crie um arquivo `pages/api/test.js`:
    ```javascript
    import { PrismaClient } from '@prisma/client';
    const prisma = new PrismaClient();

    export default async function handler(req, res) {
      const data = await prisma.user.findMany(); // Exemplo para tabela 'user'
      res.json(data);
    }
    ```

3. **Acesse no navegador**:
    - Abra `http://localhost:3000`.

---

Pronto! Seu projeto com Node.js, Next.js e Prisma está configurado.