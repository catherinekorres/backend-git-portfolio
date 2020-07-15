<img alt="GoStack" src="https://storage.googleapis.com/golden-wind/bootcamp-gostack/header-desafios.png" />
#Git Portfolio
![npm](https://img.shields.io/badge/npm-v6.14.4-%23CB3837) ![express](https://img.shields.io/badge/express-v4.17.1-%2338A6FF)  ![uuidv4](https://img.shields.io/badge/uuidv4-v6.0.7-%23DB7093) ![jest](https://img.shields.io/badge/jest-v25.2.6-%2399425B) ![supertest](https://img.shields.io/badge/supertest-v4.0.2-%23F1DA50) ![nodemon](https://img.shields.io/badge/nodemon-v2.0.2-%2376D04B)

Esta é uma aplicação backend em Node.js com **`Express`** que permite armazenar repositórios do GitHub como um portfólio, servindo como uma API REST. 

A idéia é que além de listar os repositórios, pode-se interagir com eles através de likes. Estes serão armazenados juntamente com os dados do repositório.

Como esta é uma aplicação do primeiro módulo do bootcamp, os dados estão sendo salvos em um atributo na memória da aplicação, sem nenhum tipo de banco de dados. O intuito deste desafio é focar na implementação das rotas e lógicas pertinentes para cada recurso.

**OBS: Para interagir com a aplicação, recomendo a utilização de um REST Client, como o [Insomnia](https://insomnia.rest/) ou [Postman](https://www.postman.com/).**

## Sumário
- [Instalar](#instalar)
- [Executar](#executar)
- [Entidades](#entidades)
- [Rotas](#Rotas)
- [Testes](#testes)


## Instalar
Antes de instalar o projeto, é necessário que tenha instalado anteriormente o [Node.js](https://nodejs.org/pt-br/), e consequentemente o npm, que é um gerenciador de pacotes distribuido juntamente com o Node.js.
Para checar se possui ambos, basta executar os comandos:

```
node -v
npm -v
```

O resultado deverá ser a versão atual instalada em sua máquina. Se desejar, pode utilizar outro gerenciador de pacotes além do npm, como o yarn.
Para checar se possui o yarn, basta executar o comando :

```
yarn -v
```

Caso não possua e deseja instalá-lo, basta instalar via npm:

```
npm install -g yarn
```

Com pelo menos um dos gerenciadores de pacotes em sua máquina, já tem o necessário para instalar e rodar o projeto.
Finalmente, clone este projeto utilizando o comando:

```
git clone https://github.com/catherinekorres/backend-git-portfolio
```

## Executar
Após finalizar a clonagem do projeto, poderá executá-lo usando uma sequência de comandos com o npm ou yarn, de acordo com sua preferência.

### npm
```
cd backend-git-portfolio
npm install
npm run dev
```

### yarn
```
cd backend-git-portfolio
yarn
yarn dev
```
O projeto estará rodando localmente em `http://localhost:3333`.

No seu REST Client de preferência, cadastre as [rotas](#Rotas) fornecidas pela a aplicação para interagir.

Para interromper sua execução, basta encerrar o terminal.


## Entidades
No contexto desse projeto, existem duas entidades:
- **Repositório**
  A entidade repositório é um objeto que deve ter um **`id único`**, **`link para o repositório`**, **`título`**, **`tecnologias associadas`** e **`likes`**
  
  Abaixo um exemplo:

    ```
      {
        id: "7255be00-bac1-43f9-944b-f82ec18ad29d"
        url: "https://github.com/Rocketseat/umbriel",
        title: "Umbriel",
        techs: ["Node", "Express", "TypeScript"],
        likes: 2
      }
    ```

  Cada **`id único`** é criado como um **UUID** (universally unique identifiers) com o auxílio da dependência **`uuidv4`**

- **Like**
  Um like é uma curtida não só associada com um repositório, mas também com o próprio usuário que deu um like. Neste sentido, um usuário **`cria`** um like ao curtir um repositório. 
  Visto que a entidade Usuário não existe neste escopo, o like neste momento é apenas um valor numérico. Porém, como estudo, já foi implementado com o ponto de vista de ser uma entidade.
  Os likes, sendo um valor numérico, iniciam em `0` e são incrementados.

## Rotas

- **`GET /repositories`**: Rota que lista todos os repositórios;

- **`POST /repositories`**: Rota que permite que um repositório novo seja criado. Dentro do corpo da requisição devem ser passados `title`, `url` e `techs`. Ao cadastrar um novo projeto, ele é armazenado dentro de um objeto conforme detalhado na entidade;

- **`PUT /repositories/:id`**: Rota que permite alterar os dados de um repositório. Nesta rota, o `id` é passado nos parâmetros da rota, sendo possível então buscar o repositório que possua um `id` idêntico. Caso enontrado o repositório, seus dados alteráveis são apenas `title`, `url` e `techs`. Se não for encontrado, retorna um erro.

- **`DELETE /repositories/:id`**: Rota que permite deletar um repositório. Busca o repositório com o `id` idêntico ao passado nos parâmetros da rota, e caso encontre, o deleta. Se não for encontrado, retorna um erro. 

- **`POST /repositories/:id/like`**: Rota que incrementa um like em um repositório. Busca um repositório que possua o `id` presente nos parâmetros da rota, e caso encontre, aumenta o número de likes em 1. Caso não encontre, retorna um erro.

## Testes
Os testes são feitos utilizando as dependências **`jest`** e **`supertest`** se encontram na pasta `__tests__`, e são referentes as duas [entidades](#Entidades).

Para rodar os estes, basta executar: 

### npm
```
npm run test
```

### yarn
```
yarn test
```