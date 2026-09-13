# Modelagem e Projeto de Banco de Dados — E-Commerce

[![Database](https://img.shields.io/badge/Database-Relational-blue.svg)](#)
[![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow.svg)](#)

Este repositório contém o projeto completo de modelagem de dados para uma plataforma de **E-Commerce**, cobrindo desde a análise conceitual de requisitos de negócio até a estruturação do dicionário de dados, arquivos fontes de modelagem e implementação do modelo relacional.

---

## Objetivo do Projeto

O objetivo principal deste projeto é projetar uma arquitetura de banco de dados relacional **robusta, escalável e normalizada** para suportar as operações essenciais de uma loja virtual. Realizar controle e registro centralizado de clientes, produtos, pedidos e pagamentos do negócio. 

A modelagem engloba o gerenciamento de:
* **Clientes:** Cadastro de dados pessoais, contatos e endereços de entrega.
* **Catálogo de Produtos:** Agrupamento por categorias e controle dinâmico de estoque.
* **Fluxo de Pedidos:** Registro do histórico de compras e associação dos itens adquiridos.
* **Processamento de Pagamentos:** Controle de métodos, status financeiros e transações.

Clientes: Cadastro de clientes com dados de contato e endereço. Um cliente não pode ser registrado duas vezes.

Produtos & Categorias: Produtos organizados por categorias, com controle de preço unitário e quantidade em estoque.

Pedidos: Registro de compras feitas por clientes, mantendo o histórico de data e status (Ex: Pendente, Pago, Enviado, Cancelado).

Itens do Pedido: Relação N:M entre Pedidos e Produtos, registrando a quantidade comprada de cada item e o preço praticado no momento da venda (para proteger o histórico contra futuras alterações de preço no cadastro de produtos).

Pagamentos: Registro dos pagamentos atrelados aos pedidos (Ex: Cartão de Crédito, Pix, Boleto).

---

## Estrutura do Repositório

```text
.
├── docs/
│   ├── Dicionario_de_Dados_Ecommerce.md  # Especificação detalhada de tabelas e campos
│   ├── modelos/                          # Arquivos fontes editáveis do brModelo (.brM3)
│   │   ├── modelo-conceitual.brM3
│   │   └── Logico_Ecommerce.brM3
│   └── imagens/                          # Exportações visuais para documentação (.png)
│       ├── modelo-conceitual.png
│       └── modelo-logico.png
├── database/
│   └── schema.sql                        # Script DDL de criação das tabelas (CREATE TABLE)
└── README.md                             # Documentação principal do repositório
