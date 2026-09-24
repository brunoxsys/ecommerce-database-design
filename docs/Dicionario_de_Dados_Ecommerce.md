# Dicionário de Dados — E-Commerce

Este arquivo possui a especificação detalhada das entidades, relacionamentos e atributos do modelo conceitual. 

## Entidades

| Nome da Entidade | Descrição                                           |
| :--------------- | :-------------------------------------------------- |
| **Cliente**      | Tabela para cadastro e registro de clientes         |
| **Pedido**       | Tabela para registro dos pedidos                    |
| **Pagamento**    | Tabela para registro dos pagamentos                 |
| **Itens_Pedido** | Tabela Associativa contendo a descrição dos pedidos |
| **Produto**      | Tabela contendo a descrição dos produtos            |
| **Categoria**    | Tabela contendo as categorias dos produtos          |

---

## Relacionamentos

| Nome do Relacionamento | Entidades Relacionadas | Tipo de Relacionamento | Descrição do Relacionamento                                                                   | Representação / Cardinalidades                 |
| :--------------------- | :--------------------- | :--------------------: | :-------------------------------------------------------------------------------------------- | :--------------------------------------------- |
| **Realiza**            | Clientes — Pedidos     |         `1:N`          | Um cliente pode ou não realizar N pedidos. Um pedido é realizado por 1 e apenas 1 cliente.    | `Clientes (0,n) — Realiza — (1,1) Pedidos`     |
| **Gera**               | Pedidos — Pagamento    |         `1:1`          | Um pedido pode ou não gerar um pagamento. Um pagamento é gerado por um e apenas um pedido.    | `Pedidos (0,1) — Gera — (1,1) Pagamentos`      |
| **Contém**             | Pedidos — Produtos     |         `N:N`          | Um pedido contém um ou mais produtos. Um produto pode ou não estar contido em vários pedidos. | `Pedidos (1,N) — Contém — (0,N) Produtos`      |
| **Pertence**           | Produtos — Categoria   |         `1:N`          | Um produto pertence a uma categoria. Uma categoria pode ou não conter N produtos.             | `Produtos (1,1) — Pertence — (0,N) Categorias` |

---

## Atributos

### Tabela: `Cliente`

| Atributo           | Tipo Sugerido  | Restrição                                 | Descrição                                                   |
| :----------------- | :------------- | :---------------------------------------- | :---------------------------------------------------------- |
| `Cliente_ID`       | `INT`          | `PK`, `NOT NULL`, `AUTO_INCREMENT`        | Identificador único do cliente                              |
| `Nome_Cliente`     | `VARCHAR(100)` | `NOT NULL`                                | Nome completo do cliente                                    |
| `CPF_Cliente`      | `CHAR(11)`     | `NOT NULL`, `UNIQUE`, `CHECK ([0-9]{11})` | CPF do cliente, armazenado somente com 11 dígitos numéricos |
| `Logradouro`       | `VARCHAR(150)` | `NOT NULL`                                | Rua, avenida ou outro logradouro do endereço                |
| `Bairro`           | `VARCHAR(100)` | `NOT NULL`                                | Bairro onde o cliente reside                                |
| `Cidade`           | `VARCHAR(100)` | `NOT NULL`                                | Cidade do endereço do cliente                               |
| `CEP`              | `CHAR(8)`      | `NOT NULL`                                | CEP do endereço, armazenado somente com números             |
| `Telefone_Cliente` | `VARCHAR(20)`  |                                           | Telefone de contato do cliente                              |
| `Email_Cliente`    | `VARCHAR(150)` | `UNIQUE`                                  | Endereço de e-mail do cliente                               |

---

### Tabela: `Pedido`

| Atributo        | Tipo Sugerido | Restrição                          | Descrição                              |
| :-------------- | :------------ | :--------------------------------- | :------------------------------------- |
| `Pedido_ID`     | `INT`         | `PK`, `NOT NULL`, `AUTO_INCREMENT` | Identificador único do pedido          |
| `Cliente_ID`    | `INT`         | `FK`, `NOT NULL`                   | Cliente que realizou o pedido          |
| `Data_Pedido`   | `DATETIME`    | `NOT NULL`                         | Data e horário da realização do pedido |
| `Status_Pedido` | `VARCHAR(30)` | `NOT NULL`                         | Situação atual do pedido               |

---

### Tabela: `Pagamento`

| Atributo           | Tipo Sugerido   | Restrição                          | Descrição                                 |
| :----------------- | :-------------- | :--------------------------------- | :---------------------------------------- |
| `Pagamento_ID`     | `INT`           | `PK`, `NOT NULL`, `AUTO_INCREMENT` | Identificador único do pagamento          |
| `Pedido_ID`        | `INT`           | `FK`, `NOT NULL`, `UNIQUE`         | Pedido relacionado ao pagamento           |
| `Data_Pagamento`   | `DATETIME`      | `NULL`                             | Data e horário do pagamento               |
| `Forma_Pagamento`  | `VARCHAR(30)`   | `NOT NULL`                         | Forma utilizada para realizar o pagamento |
| `Valor_Pagamento`  | `DECIMAL(10,2)` | `NOT NULL`                         | Valor total pago                          |
| `Status_Pagamento` | `VARCHAR(30)`   | `NOT NULL`                         | Situação atual do pagamento               |

---

### Tabela: `Produto`

| Atributo             | Tipo Sugerido   | Restrição                          | Descrição                                   |
| :------------------- | :-------------- | :--------------------------------- | :------------------------------------------ |
| `Produto_ID`         | `INT`           | `PK`, `NOT NULL`, `AUTO_INCREMENT` | Identificador único do produto              |
| `Categoria_ID`       | `INT`           | `FK`, `NOT NULL`                   | Categoria à qual o produto pertence         |
| `Nome_Produto`       | `VARCHAR(150)`  | `NOT NULL`                         | Nome do produto                             |
| `Quantidade_Estoque` | `INT`           | `NOT NULL`                         | Quantidade atualmente disponível em estoque |
| `Preço_Atual`        | `DECIMAL(10,2)` | `NOT NULL`                         | Preço atual de venda do produto             |

---

### Tabela: `Categoria`

| Atributo         | Tipo Sugerido  | Restrição                          | Descrição                        |
| :--------------- | :------------- | :--------------------------------- | :------------------------------- |
| `Categoria_ID`   | `INT`          | `PK`, `NOT NULL`, `AUTO_INCREMENT` | Identificador único da categoria |
| `Nome_Categoria` | `VARCHAR(100)` | `NOT NULL`, `UNIQUE`               | Nome da categoria de produtos    |

---

### Tabela: `Itens_Pedido`

| Atributo         | Tipo Sugerido   | Restrição              | Descrição                             |
| :--------------- | :-------------- | :--------------------- | :------------------------------------ |
| `Pedido_ID`      | `INT`           | `PK`, `FK`, `NOT NULL` | Pedido ao qual o item pertence        |
| `Produto_ID`     | `INT`           | `PK`, `FK`, `NOT NULL` | Produto incluído no pedido            |
| `Quantidade`     | `INT`           | `NOT NULL`             | Quantidade comprada daquele produto   |
| `Preço_Unitário` | `DECIMAL(10,2)` | `NOT NULL`             | Preço do produto no momento da compra |

