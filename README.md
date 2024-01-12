# PDV API (Ponto de Venda)

![Logo](https://th.bing.com/th/id/OIG.3M9QtpntT_umttdFtkiu?pid=ImgGn)

## Introdução

Bem-vindo ao repositório da PDV API! Este projeto faz parte do Desafio Backend e consiste em uma API para um Ponto de Venda (PDV). Além das funcionalidades básicas, este projeto inclui recursos avançados, como cadastro de produtos com imagem e envio de e-mails para confirmação de pedidos.

# 🚀 Funcionalidades

### Banco de Dados

- Criação das tabelas: `usuarios` e `categorias`.
- Listagem de categorias: `GET /categoria`.
- Cadastro de usuário: `POST /usuario`.
- Cadastro de Clientes: `POST /cliente`.
- Cadastro de Produto: `POST /produto`.
- Login do usuário: `POST /login`.
- Editar cliente: `PUT /cliente/id`.
- Editar produto: `PUT /produto/id`.
- Listar cliente: `GET /cliente`.
- Detalhar cliente: `GET /cliente/id`.
- Detalhar produto: `GET /produto/id`.
- Listar produtos: `GET /produto`.
- Detalhes do perfil do usuário logado: `GET /usuario`.
- Edição do perfil do usuário logado: `PUT /usuario`.
- Deletar produto: `DEL /produto/id`.
- Deploy da aplicação.

### Banco de Dados

<details>
<summary><b>Criando banco de dados</b></summary>
<br>

#### CREATE TABLE IF NOT EXISTS public.usuarios
(
-  id serial,
-  nome text NOT NULL,
-  email text NOT NULL,
-  senha text NOT NULL,
-  PRIMARY KEY (id),
-  CONSTRAINT email UNIQUE (email)
-  INCLUDE(email)
);

#### CREATE TABLE IF NOT EXISTS public.categorias
(
-  id serial,
-  descricao text NOT NULL,
-  PRIMARY KEY (id)
);

- INSERT INTO categorias (descricao) VALUES ('Informática'); 
-  INSERT INTO categorias (descricao) VALUES ('Celulares');
-  INSERT INTO categorias (descricao) VALUES ('Beleza e Perfumaria');
-  INSERT INTO categorias (descricao) VALUES ('Mercado'); 
-  INSERT INTO categorias (descricao) VALUES ('Livros e Papelaria'); 
-  INSERT INTO categorias (descricao) VALUES ('Brinquedos'); 
-  INSERT INTO categorias (descricao) VALUES ('Moda'); 
-  INSERT INTO categorias (descricao) VALUES ('Bebê'); 
-  INSERT INTO categorias (descricao) VALUES ('Games');

#### create table produtos (
-  id serial primary key,
-  descricao varchar(200),
-  quantidade_estoque integer,
-  valor integer,
-  categoria_id integer,
-  foreign key (categoria_id) references categorias(id)
);

#### create table clientes(
-  id serial primary key,
-  nome text not null,
-  email  varchar(200) not null unique,
-  cpf varchar(11) not null unique,
-  cep varchar(8),
-  rua varchar(100),
-  numero varchar(10),
-  bairro varchar(100),
-  cidade varchar(100),
-  estado varchar(50)
);

#### create table pedidos(
-	id serial primary key,
-  cliente_id integer not null references clientes(id),
-  observacao text,
-  valor_total integer
);

#### create table pedido_produtos(
-	id serial primary key,
-  pedido_id integer not null references pedidos(id),
-  produto_id integer not null references produtos(id),
-  quantidade_produto integer,
-  valor_produto integer
);

alter table produtos add produto_imagem VARCHAR(500)
</details>

### ⚡ Recursos Avançados

- Cadastro de produto com imagem.
- Envio de e-mail de confirmação de pedido em caso de sucesso.
- Tratamento de estoque insuficiente ao fazer um pedido.

## 🛠️ Requisitos

- Banco de dados PostgreSQL chamado `pdv`.
- Representação de valores monetários em centavos.
- Utilização de tokens de autenticação.
- Configuração de serviço de e-mail para envio de confirmações.

## 🌐 Status Codes

- 200 (OK)
- 201 (Created)
- 204 (No Content)
- 400 (Bad Request)
- 401 (Unauthorized)
- 403 (Forbidden)
- 404 (Not Found)
- 500 (Internal Server Error)

## ⚙️ Configuração do Banco de Dados

1. Crie um banco de dados PostgreSQL chamado `pdv`.
2. Execute os scripts SQL para criar as tabelas e inserir categorias.

## 🚀 Como Rodar o Projeto

1. Clone o repositório: `git clone https://github.com/LeooAndrade/Sistema-Pdv`
2. Instale as dependências: `npm install`
3. Configure as variáveis de ambiente no arquivo `.env`.
4. Execute o projeto: `npm start`
5. Acesse a API em [http://localhost:3000](http://localhost:3000).

## 📖 Documentação da API

Consulte a [documentação da API](#) para obter detalhes sobre os endpoints e suas funcionalidades.

## 🌟 Recursos Adicionais

### Cadastro de Produto com Imagem

O endpoint `POST /produto` permite o cadastro de produtos, incluindo a opção de enviar uma imagem do produto.

### Envio de E-mail de Confirmação de Pedido

Ao realizar um pedido com sucesso, a API envia automaticamente um e-mail de confirmação para o usuário.

### Tratamento de Estoque Insuficiente

Ao fazer um pedido, a API verifica se há estoque suficiente para cada produto. Se o estoque for insuficiente, o pedido não é concluído, e uma mensagem apropriada é enviada ao usuário.

## 🙏 Agradecimentos

Agradecemos por contribuir para o desenvolvimento da PDV API. Se tiver sugestões ou encontrar problemas, sinta-se à vontade para abrir uma [issue](#) ou enviar um [pull request](#).

## 📄 Licença

Este projeto está licenciado sob a licença MIT. Consulte o arquivo [LICENSE](LICENSE) para obter mais detalhes.