# Modelagem e Projeto de Banco de Dados — E-Commerce

![Database](https://img.shields.io/badge/Database-Relational-blue)
![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow)

Projeto de **modelagem e projeto de banco de dados relacional** para uma plataforma de **E-Commerce**, desenvolvido com foco na aplicação prática de conceitos de modelagem conceitual, modelo lógico, normalização, relacionamentos, cardinalidade e implementação SQL.

O projeto contempla desde a definição das regras de negócio até a construção do modelo conceitual, modelo lógico, dicionário de dados e estrutura do banco de dados.

---

## Objetivo do Projeto

O objetivo deste projeto é desenvolver uma estrutura de banco de dados **organizada, consistente e normalizada** para suportar as principais operações de uma plataforma de comércio eletrônico.

A modelagem foi desenvolvida para centralizar e estruturar informações relacionadas a:

- Clientes;
- Endereços dos clientes;
- Telefones dos clientes;
- Produtos;
- Categorias;
- Pedidos;
- Itens dos pedidos;
- Pagamentos.

O projeto busca aplicar conceitos fundamentais de **Modelagem de Dados**, **Modelo Entidade-Relacionamento (MER)**, **Modelo Relacional**, **Cardinalidade**, **Normalização** e **SQL/DDL**.

---

## Escopo do Sistema

### Clientes

A entidade `Cliente` representa os consumidores cadastrados na plataforma.

Cada cliente possui informações de identificação e contato, incluindo:

- Nome;
- E-mail;
- CPF.

O CPF e o e-mail são definidos como campos únicos, evitando o cadastro duplicado de informações de identificação.

---

### Endereços dos Clientes

A entidade `Endereco_Cliente` armazena os endereços associados aos clientes.

Cada endereço contém informações como:

- Logradouro;
- Bairro;
- Cidade;
- CEP;
- Cliente associado.

A separação dos endereços em uma entidade própria permite que um cliente possa possuir múltiplos endereços cadastrados.

---

### Telefones dos Clientes

A entidade `Telefone_Cliente` armazena os números de telefone associados aos clientes.

Cada registro possui:

- Número do telefone;
- Cliente associado.

A utilização de uma entidade própria permite que um cliente possua mais de um telefone cadastrado.

---

### Produtos

A entidade `Produto` representa os itens comercializados pela plataforma.

Cada produto possui informações como:

- Nome;
- Quantidade em estoque;
- Preço atual;
- Categoria.

O preço atual representa o valor vigente do produto no catálogo.

O histórico do preço praticado em uma venda é preservado na entidade `Itens_Pedido`.

---

### Categorias

A entidade `Categoria` organiza os produtos do catálogo em grupos.

Cada categoria possui:

- Identificador;
- Nome da categoria.

Uma categoria pode possuir diversos produtos, enquanto cada produto pertence a uma categoria.

---

### Pedidos

A entidade `Pedido` representa as compras realizadas pelos clientes.

Cada pedido possui:

- Data do pedido;
- Status do pedido;
- Cliente responsável pela compra.

Exemplos de status:

- Pendente;
- Pago;
- Enviado;
- Cancelado.

Um cliente pode realizar diversos pedidos, enquanto cada pedido está associado a um único cliente.

---

### Itens do Pedido

A entidade `Itens_Pedido` representa os produtos incluídos em cada pedido.

Ela funciona como uma **entidade associativa** entre `Pedido` e `Produto`, permitindo representar o relacionamento N:N entre essas entidades.

Cada item registra:

- Pedido;
- Produto;
- Quantidade;
- Preço unitário praticado na venda.

O campo `Preço_Unitário` é importante para preservar o histórico financeiro da compra. Caso o preço atual de um produto seja alterado posteriormente, o valor registrado no pedido permanece inalterado.

---

### Pagamentos

A entidade `Pagamento` representa o pagamento associado a um pedido.

Cada pagamento possui informações como:

- Data do pagamento;
- Forma de pagamento;
- Valor;
- Status do pagamento;
- Pedido associado.

Exemplos de formas de pagamento:

- Cartão de Crédito;
- Pix;
- Boleto.

---
## Estrutura do Repositório

```text
.
├── docs/
│   ├── Dicionario_de_Dados_Ecommerce.md  # Especificação detalhada de tabelas, tipos e constraints
│   ├── modelos/                          # Arquivos fontes editáveis do brModelo (.brM3)
│   │   ├── modelo-conceitual.brM3
│   │   └── modelo-logico.brM3
│   └── imagens/                          # Exportações visuais do diagrama (.png)
│       ├── modelo-conceitual.png
│       └── modelo-logico.png
├── database/
│   └── schema.sql                        # Script DDL de criação do banco e constraints (CREATE TABLE)
└── README.md                             # Documentação principal do repositório
