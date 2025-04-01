# Guia para Inicializar um Projeto com Node.js, Next.js, Prisma, React e Expo no Windows

Este guia descreve como configurar projetos utilizando Node.js, Next.js, Prisma, React e Expo, executando os comandos no terminal do VS Code.

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

## 3. Inicializando um Projeto React

### Passos:
1. **Crie um novo projeto React**:
    ```bash
    npx create-react-app meu-app
    cd meu-app
    ```

2. **Inicie o servidor de desenvolvimento**:
    ```bash
    npm start
    ```

3. **Estrutura básica do React**:
    O arquivo `src/App.js` já contém um exemplo inicial. Você pode editar para:
    ```javascript
    function App() {
      return <h1>Olá, React!</h1>;
    }

    export default App;
    ```

---

## 4. Inicializando um Projeto Expo

### Passos:
1. **Instale o Expo CLI**:
    ```bash
    npm install -g expo-cli
    ```

2. **Crie um novo projeto Expo**:
    ```bash
    expo init meu-app-expo
    cd meu-app-expo
    ```

3. **Escolha o template**:
    Durante a criação, escolha o template `blank`.

4. **Inicie o servidor de desenvolvimento**:
    ```bash
    npm start
    ```

5. **Estrutura básica do Expo**:
    O arquivo `App.js` já contém um exemplo inicial. Você pode editar para:
    ```javascript
    import { Text, View } from 'react-native';

    export default function App() {
      return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
          <Text>Olá, Expo!</Text>
        </View>
      );
    }
    ```

---

## 5. Next.js - Passo a Passo

### Criando o Projeto:
1. **Execute o comando**:
    ```bash
    npx create-next-app@latest nome_do_projeto
    ```

2. **Responda às perguntas**:
    - `Ok to proceed? (y)` -> Yes
    - `Would you like to use TypeScript?` -> No
    - `Would you like to use ESLint?` -> Yes
    - `Would you like to use Tailwind CSS?` -> No
    - `Would you like your code inside a src/ directory?` -> Yes
    - `Would you like to use App Router? (recommended)` -> Yes
    - `Would you like to use Turbopack for next dev?` -> Yes
    - `Would you like to customize the import alias (@/* by default)?` -> No

3. **Configuração do Projeto**:
    - Renomeie os arquivos:
        ```bash
        mv src/app/layout.js src/app/layout.jsx
        mv src/app/page.js src/app/page.jsx
        ```

4. **Execute o projeto**:
    ```bash
    npm run dev
    ```

### Possível Erro:
- **Erro no PowerShell**:
    - Abra o PowerShell como administrador e execute:
        ```bash
        Set-ExecutionPolicy Unrestricted -Scope CurrentUser -Force
        Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
        ```

---

## 6. Possíveis Erros e Soluções

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