# Dicionário de Dados — E-Commerce

Este arquivo possui a especificação detalhada das entidades, relacionamentos e atributos do modelo lógico. 

## Entidades

| Nome da Entidade     | Descrição                                        |
| :------------------- | :----------------------------------------------- |
| **Cliente**          | Tabela para cadastro e registro de clientes      |
| **Endereço_Cliente** | Tabela para registros de endereços de clientes   |
| **Telefone_Cliente** | Tabela para cadastro de telefones dos clientes   |
| **Pedido**           | Tabela para registro dos pedidos                 |
| **Pagamento**        | Tabela para registro dos pagamentos              |
| **Itens_Pedido**     | Tabela Associativa contendo detalhes dos pedidos |
| **Produto**          | Tabela contendo a descrição dos produtos         |
| **Categoria**        | Tabela contendo as categorias dos produtos       |

---

## Relacionamentos

| Nome do Relacionamento | Entidades Relacionadas     | Tipo de Relacionamento | Descrição do Relacionamento                                                                                                                                                               | Representação / Cardinalidades                       |
| :--------------------- | :------------------------- | :--------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------- |
| **Reside em**          | Cliente — Endereço_Cliente |         `0:1`          | Um cliente pode possuir no máximo um endereço cadastrado. Um endereço cadastrado pertence obrigatoriamente a exatamente um cliente. Um cliente pode existir temporariamente sem endereço. | `Cliente (0:1) — Reside em — (1:1) Endereço_Cliente` |
| **Possui**             | Cliente — Telefone_Cliente |         `1:N`          | Um cliente pode possuir mais de um telefone de contato. Um telefone pertence apenas a um cliente                                                                                          | `Cliente (1,N) — Possui — (1,1)Telefone_Cliente`     |
| **Realiza**            | Cliente — Pedido           |         `1:N`          | Um cliente pode realizar zero ou vários pedidos. Cada pedido é realizado por um, e somente um, cliente.                                                                                   | `Clientes (0,n) — Realiza — (1,1) Pedidos`           |
| **Gera**               | Pedido — Pagamento         |         `1:1`          | Um pedido pode gerar um ou nenhum pagamento. Um pagamento é gerado por um e apenas um pedido.                                                                                             | `Pedido (0,1) — Gera — (1,1) Pagamento`              |
| **Contém**             | Pedido — Produto           |         `N:N`          | Um pedido contém um ou mais produtos. Um produto pode ou não estar contido em vários pedidos.                                                                                             | `Pedido (1,N) — Contém — (0,N) Produto`              |
| **Pertence**           | Produto — Categoria        |         `1:N`          | Um produto pertence a uma categoria. Uma categoria pode ou não conter N produtos.                                                                                                         | `Produto (1,1) — Pertence — (0,N) Categoria`         |

---

## Atributos

### Tabela: `Cliente`

| Atributo        | Tipo Sugerido  | Restrição                                 | Descrição                                                   |
| :-------------- | :------------- | :---------------------------------------- | :---------------------------------------------------------- |
| `Cliente_ID`    | `INT`          | `PK`, `NOT NULL`, `AUTO_INCREMENT`        | Identificador único do cliente                              |
| `Nome_Cliente`  | `VARCHAR(75)`  | `NOT NULL`                                | Nome completo do cliente                                    |
| `Email_Cliente` | `VARCHAR(100)` | `UNIQUE`                                  | Endereço de e-mail do cliente                               |
| `CPF_Cliente`   | `CHAR(11)`     | `NOT NULL`, `UNIQUE`, `CHECK ([0-9]{11})` | CPF do cliente, armazenado somente com 11 dígitos numéricos |

---

### Tabela: Endereço_Cliente

| Atributo              | Tipo Sugerido  | Restrição                          | Descrição                                                      |
| :-------------------- | :------------- | :--------------------------------- | :------------------------------------------------------------- |
| `Endereço_Cliente_ID` | `INT`          | `PK`, `NOT NULL`, `AUTO_INCREMENT` | Identificador único de endereço                                |
| `Cliente_ID`          | `INT`          | `FK`, `NOT NULL`                   | Chave estrangeira de ID do cliente                             |
| `Logradouro`          | `VARCHAR(150)` | `NOT NULL`                         | Nome e número do logradouro (incluindo complemento, se houver) |
| `Bairro`              | `VARCHAR(100)` | `NOT NULL`                         | Nome do bairro                                                 |
| `Cidade`              | `VARCHAR(100)` | `NOT NULL`                         | Nome da cidade                                                 |
| `CEP`                 | `CHAR(8)`      | `NOT NULL`                         | N° do CEP, armazenado com 8 dígitos numéricos                  |

- - -

### Tabela: Telefone_Cliente

| Atributo              | Tipo Sugerido | Restrição                          | Descrição                          |
| :-------------------- | :------------ | :--------------------------------- | :--------------------------------- |
| `Telefone_Cliente_ID` | `INT`         | `PK`, `NOT NULL`, `AUTO_INCREMENT` | Identificador único de telefone    |
| `Cliente_ID`          | `INT`         | `FK`, `NOT NULL`                   | Chave estrangeira de ID do cliente |
| `Telefone`            | `VARCHAR(20)` | `NOT NULL`                         | Número de telefone                 |

- - -

### Tabela: `Pedido`

| Atributo        | Tipo Sugerido | Restrição                          | Descrição                                          |
| :-------------- | :------------ | :--------------------------------- | :------------------------------------------------- |
| `Pedido_ID`     | `INT`         | `PK`, `NOT NULL`, `AUTO_INCREMENT` | Identificador único do pedido                      |
| `Cliente_ID`    | `INT`         | `FK`, `NOT NULL`                   | Chave estrangeira do Cliente que realizou o pedido |
| `Data_Pedido`   | `DATETIME`    | `NOT NULL`                         | Data e horário da realização do pedido             |
| `Status_Pedido` | `VARCHAR(30)` | `NOT NULL`                         | Situação atual do pedido                           |

---

### Tabela: `Pagamento`

| Atributo           | Tipo Sugerido   | Restrição                          | Descrição                                            |
| :----------------- | :-------------- | :--------------------------------- | :--------------------------------------------------- |
| `Pagamento_ID`     | `INT`           | `PK`, `NOT NULL`, `AUTO_INCREMENT` | Identificador único do pagamento                     |
| `Pedido_ID`        | `INT`           | `FK`, `NOT NULL`, `UNIQUE`         | Chave estrangeira do Pedido relacionado ao pagamento |
| `Data_Pagamento`   | `DATETIME`      | `NULL`                             | Data e horário do pagamento                          |
| `Forma_Pagamento`  | `VARCHAR(30)`   | `NOT NULL`                         | Forma utilizada para realizar o pagamento            |
| `Status_Pagamento` | `VARCHAR(30)`   | `NOT NULL`                         | Situação atual do pagamento                          |
| `Valor_Pagamento`  | `DECIMAL(10,2)` | `NOT NULL`                         | Valor total pago                                     |

---
### Tabela: `Itens_Pedido`

| Atributo         | Tipo Sugerido   | Restrição              | Descrição                                       |
| :--------------- | :-------------- | :--------------------- | :---------------------------------------------- |
| `Pedido_ID`      | `INT`           | `PK`, `FK`, `NOT NULL` | Pedido ao qual o item pertence                  |
| `Produto_ID`     | `INT`           | `PK`, `FK`, `NOT NULL` | Chave estrangeira do Produto incluído no pedido |
| `Quantidade`     | `INT`           | `NOT NULL`             | Quantidade comprada daquele produto             |
| `Preço_Unitário` | `DECIMAL(10,2)` | `NOT NULL`             | Preço do produto no momento da compra           |

- - - 

### Tabela: `Produto`

| Atributo             | Tipo Sugerido   | Restrição                          | Descrição                                                |
| :------------------- | :-------------- | :--------------------------------- | :------------------------------------------------------- |
| `Produto_ID`         | `INT`           | `PK`, `NOT NULL`, `AUTO_INCREMENT` | Identificador único do produto                           |
| `Categoria_ID`       | `INT`           | `FK`, `NOT NULL`                   | Chave estrangeira da Categoria à qual o produto pertence |
| `Nome_Produto`       | `VARCHAR(150)`  | `NOT NULL`                         | Nome do produto                                          |
| `Quantidade_Estoque` | `INT`           | `NOT NULL`                         | Quantidade atualmente disponível em estoque              |
| `Preço_Atual`        | `DECIMAL(10,2)` | `NOT NULL`                         | Preço atual de venda do produto                          |

---

### Tabela: `Categoria`

| Atributo         | Tipo Sugerido  | Restrição                          | Descrição                        |
| :--------------- | :------------- | :--------------------------------- | :------------------------------- |
| `Categoria_ID`   | `INT`          | `PK`, `NOT NULL`, `AUTO_INCREMENT` | Identificador único da categoria |
| `Nome_Categoria` | `VARCHAR(100)` | `NOT NULL`, `UNIQUE`               | Nome da categoria de produtos    |

---
