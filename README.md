# onboard-project

Olá, seja bem-vindo!

O intuito deste guia é lhe auxiliar a configurar seu ambiente de desenvolvimento e criar um projeto para que você se familierize com uma arquitetura bastante utilizada em nossos projetos.

## Configurando seu ambiente

Acesse o site da [Oracle](https://www.oracle.com/technetwork/java/javase/overview/index.html) e faça a instalação do Java JDK 8, você deve encontrar uma versão de 64 bits na aba de downloads. Provavelmente vai precisar criar uma conta da Oracle para realizar o download.

Em seguida acesse o site do [Spring Tool Suite](https://spring.io/tools), faça download da versão de 64 bits e descompacte o arquivo em C:/

Agora faça a instalação do [Git](https://git-scm.com/), abra o terminal em alguma pasta de sua preferência e execute o comando `git clone https://github.com/matheus-pereira/onboard-project.git`

Em seguida entre na pasta `onboard-project` e crie uma nova branch para você com o comando `git checkout -b SEU_NOME`

Abra o Spring Tool Suite e importe o projeto para a IDE.

Instale o [Docker](https://www.docker.com/products/docker-desktop), será necessário configurar o Hyper-V e reiniciar a máquina.

Crie um container de Redis com o comando `docker pull redis` seguido de `docker run -it -p 6379:6379 --name redis redis`

Agora crie um container de MongoDB com o comando `docker pull mongo` seguido de `docker run -it -p 27017:27017 --name mongo mongo`

Se quiser utilizar uma interface gráfica também, você pode instalar o [Compass](https://www.mongodb.com/download-center/compass)

Instale o [Postman](https://www.getpostman.com/downloads/)

E para finalizar, também instale o [Visual Studio Code](https://code.visualstudio.com/). Além de ser um ótimo editor de textos, possui uma interface ótima para visualizar alterações de código com Git.

## O Projeto

Sua tarefa é criar uma API RESTful que realize um CRUD de usuário com side cache.

O usuário deve possuir os seguintes dados: CÓDIGO, NOME, EMAIL e TELEFONE

Você deve implementar cinco endpoints:
* `POST /user` - cadastrar um usuário
* `GET /user` - listar todos os usuários
* `GET /user/:id` - buscar um usuário através de seu ID
* `PUT /user/:id` - atualizar um usuário
* `DELETE /user/:id` - excluir um usuário

Crie um modelo de usuário na camada `Model`, uma `Controller` para receber as requisições HTTP, execute as regras de negócio em uma camada de `Service` e acesse o banco de dados na camada `Repository`

Em seguida crie uma camada de `Cache` e implemente o seguinte comportamento na camada de `Service`:
* Quando um usuário for buscado pelo ID, primeiro realize a busca na camada de `Cache`
* Se ele for encontrado retorne para a `Controller`
* Caso contrátio efetue uma busca na camada `Repository`
* Se ele for encontrado, salve na camada `Cache` antes de retornar para a `Controller`
* Caso o usuário não exista retorne nulo para a `Controller`

Escreva testes unitários para cobrir ao menos 80% do código e utilize anotações em sua classes e métodos para criar a `javadoc`

Ao final solicite acesso ao projeto para algum `maintainer`, faça `commit` e `push` da sua `branch` e abra um `merge request` para a `branch master`
