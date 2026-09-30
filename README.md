# ecommerce-database-design

![Database](https://img.shields.io/badge/Database-Relational-blue)
![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow)
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)


Projeto de **modelagem e projeto de banco de dados relacional** para uma plataforma de **E-Commerce**, desenvolvido com foco na aplicação prática de conceitos de modelagem conceitual, modelo lógico, normalização, relacionamentos, cardinalidade e implementação em SQL.

O projeto contempla desde a definição das regras de negócio até a construção do modelo conceitual, modelo lógico, dicionário de dados e a estrutura física do banco de dados.


## Authors

- [@brunoxsys](https://github.com/brunoxsys)


## Índice
- [Objetivo do Projeto](#-objetivo-do-projeto)
- [Regras de Negócio](#-regras-de-negócio)
- [Escopo do Sistema](#-escopo-do-sistema)
- [Fase Atual do Projeto](#-fase-atual-do-projeto)
- [Próximos Passos](#-próximos-passos)
- [Tecnologias e Ferramentas](#-tecnologias-e-ferramentas)
- [Desafios e Aprendizados](#-desafios-e-aprendizados)
- [Estrutura do Repositório](#-estrutura-do-repositório)
- [Contato](#-contato)

---

## Objetivo do Projeto

O objetivo deste projeto é desenvolver uma estrutura de banco de dados **organizada, consistente e normalizada** para suportar as principais operações de uma plataforma de comércio eletrônico. 

A modelagem foi desenvolvida para centralizar e estruturar informações relacionadas a:
* Clientes
* Endereços dos clientes
* Telefones dos clientes
* Produtos
* Categorias
* Pedidos
* Itens dos pedidos
* Pagamentos

O projeto busca aplicar conceitos fundamentais de Modelagem de Dados, Modelo Entidade-Relacionamento (MER), Modelo Relacional, Cardinalidade, Normalização e SQL (DDL/DML).

## Regras de Negócio
* **Clientes:** Cadastro de clientes com dados de contato e endereço. Um cliente não pode ser registrado duas vezes (validação por CPF/E-mail únicos).
* **Pedidos:** Registro de compras feitas por clientes, mantendo o histórico de data e status (ex: Pendente, Pago, Enviado, Cancelado).
* **Itens do Pedido:** Relação N:M (muitos para muitos) entre Pedidos e Produtos, registrando a quantidade comprada de cada item e o preço praticado no momento da venda (para proteger o histórico financeiro contra futuras alterações de preço no catálogo).
* **Pagamentos:** Registro dos pagamentos atrelados aos pedidos (ex: Cartão de Crédito, Pix, Boleto).
* **Produtos & Categorias:** Produtos organizados por categorias, com controle de preço unitário e quantidade em estoque.

## Escopo do Sistema

### Clientes
A entidade `Cliente` representa os consumidores cadastrados na plataforma. Cada cliente possui informações de identificação e contato, incluindo:
* Nome
* E-mail (Unique)
* CPF (Unique)

*Nota de Modelagem:* Inicialmente, no modelo conceitual, o projeto apresentou uma única entidade denominada `Cliente` com os atributos `Endereço_Cliente` e `Telefone_Cliente`. Durante a conversão para o modelo lógico e aplicação das regras de normalização, esses campos foram separados em tabelas próprias. O Endereço, por ser um atributo composto, tornou-se uma entidade fraca relacionada a Cliente. Da mesma forma, o Telefone, por ser um atributo multivalorado, também foi isolado em uma entidade relacionada.

### Endereços dos Clientes
A entidade `Endereco_Cliente` armazena os endereços associados aos clientes. Cada endereço contém:
* Logradouro
* Bairro
* Cidade
* CEP
* Cliente associado (Chave Estrangeira)

### Telefones dos Clientes
A entidade `Telefone_Cliente` armazena os números de telefone associados aos clientes. Cada registro possui:
* Identificador único do Telefone
* Número do telefone
* Cliente associado (Chave Estrangeira)

A utilização de uma entidade própria permite que um cliente possua mais de um telefone cadastrado, respeitando a Primeira Forma Normal (1FN).

### Pedidos
A entidade `Pedido` representa as compras realizadas pelos clientes. Cada pedido possui:
* Identificador único do pedido
* Data do pedido
* Status do pedido (ex: Pendente, Pago, Enviado, Cancelado)
* Cliente responsável pela compra (Chave Estrangeira)

Um cliente pode realizar diversos pedidos, enquanto cada pedido está associado a um único cliente (Relação 1:N).

### Pagamentos
A entidade `Pagamento` representa a transação financeira associada a um pedido. Cada pagamento possui:
* Identificador único do pagamento
* Data do pagamento
* Forma de pagamento (ex: Cartão de Crédito, Pix, Boleto)
* Status do pagamento
* Valor total
* Pedido associado (Chave Estrangeira)

### Itens do Pedido
A entidade `Itens_Pedido` funciona como uma tabela associativa, resolvendo o relacionamento N:M entre Pedido e Produto. Cada item registra:
* Pedido associado (Chave Estrangeira)
* Produto associado (Chave Estrangeira)
* Quantidade
* Preço unitário praticado na venda

*Importante:* O campo `Preço_Unitário` nesta tabela é crucial para preservar o histórico financeiro da compra. Caso o preço atual de um produto seja alterado posteriormente na tabela `Produto`, o valor registrado no pedido histórico permanece inalterado.

### Produtos
A entidade `Produto` representa os itens comercializados. Cada produto possui:
* Identificador único do Produto
* Nome
* Quantidade em estoque
* Preço atual
* Categoria associada (Chave Estrangeira)

### Categorias
A entidade `Categoria` organiza os produtos do catálogo em grupos. Cada categoria possui:
* Identificador único da Categoria
* Nome da categoria

Uma categoria pode possuir diversos produtos, enquanto cada produto pertence a uma única categoria (Relação 1:N).

---

## Fase Atual do Projeto

O projeto acaba de concluir a etapa de **Modelagem de Dados**. O Modelo Conceitual e o Modelo Lógico foram finalizados, garantindo a correta normalização das entidades (como a separação dos atributos de endereço e telefone) e a definição de todos os relacionamentos, chaves primárias e estrangeiras. O Dicionário de Dados também está foi atualizado para documentar essa estrutura.

## Próximos Passos

A partir de agora, o projeto avança para a fase de **Implementação Física e Análise**. As próximas etapas incluem:

- [ ] **Implementação do Banco de Dados (DDL):** Criação do script SQL (`schema.sql`) no MySQL para estruturar as tabelas e restrições com base no modelo lógico validado.
- [ ] **População com Dados de Teste (DML):** Criação de scripts de inserção (`INSERT`) com dados fictícios para simular cenários reais de compras, clientes e produtos.
- [ ] **Consultas e Automação:** Desenvolvimento de Views para relatórios de vendas e Stored Procedures para regras de negócio (como a atualização de estoque no momento da compra).

---

## Tecnologias e Ferramentas

 **Modelagem:** brModelo, Engenharia de Software
 **Banco de Dados:** MySQL (Fase de Implementação)
 **Análise e BI:** Power BI (Fase Futura)
 **Controle de Versão:** Git e GitHub
 **Ambiente de Desenvolvimento:** Visual Studio Code

---

## Desafios e Aprendizados

Durante o desenvolvimento deste projeto, os principais conceitos aplicados e desafios superados foram:
 **Normalização na Prática:** A transição do modelo conceitual para o lógico exigiu a aplicação das Formas Normais (1FN, 2FN e 3FN), resultando na criação de entidades separadas para Endereços (entidade fraca) e Telefones (atributo multivalorado).

**Preservação de Histórico Financeiro:** A decisão de incluir o campo `preco_unitario` na tabela `Itens_Pedido` foi um aprendizado crucial para entender como proteger dados de compras passadas contra atualizações futuras de valores no catálogo de produtos.

---

## Estrutura do Repositório

```text
.
├── docs/
│   ├── Dicionario_de_Dados_Ecommerce.md  # Especificação detalhada de tabelas e campos
│   ├── modelos/                          # Arquivos fontes editáveis do brModelo (.brM3)
│   │   ├── modelo-conceitual.brM3
│   │   └── modelo-logico.brM3
│   └── imagens/                          # Exportações visuais para documentação (.png)
│       ├── modelo-conceitual.png
│       └── modelo-logico.png
├── database/
│   └── schema.sql                        # Script DDL de criação das tabelas (CREATE TABLE)
└── README.md                             # Documentação principal do repositório
```
--- 
## Contato

Desenvolvido por **Bruno de Moura Amaral**.
Sinta-se à vontade para entrar em contato ou contribuir com o projeto!

**LinkedIn:** www.linkedin.com/in/bruno6637127b/

**GitHub:** [github.com/brunoxsys](https://github.com/brunoxsys)


