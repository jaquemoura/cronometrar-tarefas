## alura-tracker

<img width="1341" height="637" alt="image" src="https://github.com/user-attachments/assets/32807a78-7c0c-4ce0-a74b-6e8e74613193" />

<img width="942" height="469" alt="image" src="https://github.com/user-attachments/assets/54d49d9d-a111-45c1-91f5-f531f195029a" 

<img width="1225" height="627" alt="image" src="https://github.com/user-attachments/assets/bb0d6f79-7c1a-4413-a256-78bb8c6dc95c" />

Esse projeto se trata de um gerenciador do tempo das tarefas executadas no dia a dia.

Funcionalidades:

- Controlar o tempo gasto em cada tarefa;
- Vincular uma tarefa a um projeto;
- Listar tarefas;
- Buscar tarefa com o filtro de pesquisa;
- Navegar entre as tarefas através dos controles de paginação (implementei pois não existia no projeto inicial);

Ferramentas:

Foi desenvolvido utilizando o vue 3 e o TypeScript. Também foi utilizado o json-server para simular uma API REST

Minha contribuição:

Um problema que identifiquei ocorria ao cadastrar muitas tarefas, observe a coluna do header que está com 100vh Exemplo 1. Ao mudar para 100% resolvia o problema da página da home Exemplo 2, mas aí é surge outro problema na página de projetos que precisava do height: 100vh; para cobrir tudo baseado na altura da tela, quando houver poucos projetos Exemplo 3, Exemplo 4

Para isso resolvi fazer uma paginação para melhorar a visualização e organização e aproveitar para colocar em prática todo o entendimento de como uma paginação funciona

# Como executar o projeto

# Requisitos

Node.js

# Clonar este repositório
```
git clone https://github.com/jaquemoura/cronometrar-tarefas.git
```

## Project setup

Execute npm install na pasta do projeto para instalar as dependências do projeto


### Compiles and hot-reloads for development

Dentro da pasta do projeto execute o comando npm run serve


## Back-end
Vamos utilizar uma fake API para prover os dados, para isso abre outro Prompt de Comando, entre na pasta do projeto e execute

json-server --watch db.json ou npx json-server --watch db.json


### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
