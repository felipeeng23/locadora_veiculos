# Locadora de Veículos

Este é um projeto de **Locadora de Veículos**, onde um sistema de gerenciamento de aluguéis de carros é desenvolvido para facilitar a administração da locadora. O sistema inclui informações sobre os **clientes**, **carros**, **marcas**, **aluguéis** e **detalhes dos carros alugados**.

## Descrição

A **Locadora de Veículos** permite que os **clientes** alugem **carros**, e o sistema registra as informações sobre os **modelos** de carros alugados, as **marcas** dos carros, **valor de aluguel** e **datas** dos aluguéis. O banco de dados foi criado para fornecer funcionalidades de consulta e relatório, como saber quais clientes alugaram os carros, quanto gastaram, e quais modelos e marcas foram mais alugados.

## Estrutura do Banco de Dados

O banco de dados é composto por 4 tabelas principais:

1. **cliente**: Contém informações sobre os clientes da locadora.
2. **marca**: Armazena as marcas dos carros.
3. **carro**: Detalha os carros disponíveis para aluguel, incluindo o modelo e o valor do aluguel.
4. **aluguel**: Registra os aluguéis realizados pelos clientes, com a data do aluguel e o carro alugado.

### Diagrama das Tabelas

O banco de dados possui as seguintes tabelas e relações:

- **cliente**
    - `codcliente` (PK)
    - `nome`
    - `cidade`
    - `sexo`
    - `estado`
    - `estadocivil`

- **marca**
    - `codmarca` (PK)
    - `marca`

- **carro**
    - `codcarro` (PK)
    - `codmarca` (FK)
    - `modelo`
    - `valor` (valor do aluguel)

- **aluguel**
    - `codaluguel` (PK)
    - `codcliente` (FK)
    - `codcarro` (FK)
    - `data_aluguel`

## Funcionalidades

Este sistema permite realizar diversas consultas no banco de dados, tais como:

1. **Listar todos os carros e seus modelos, marcas e valores**.
2. **Consultar clientes que alugaram carros e o total gasto**.
3. **Filtrar carros alugados por um período específico de tempo**.
4. **Agrupar aluguéis por modelo e marca**.
5. **Gerar relatórios sobre os carros mais alugados e os clientes que mais gastaram**.

## Tecnologias Usadas

- **MySQL**: Para gerenciamento e consultas ao banco de dados.
- **SQL**: Linguagem utilizada para realizar consultas e manipulação dos dados.

## Exemplo de Consultas SQL

1. **Listar todos os clientes e os carros que alugaram:**

    ```sql
    SELECT c.nome AS cliente, ca.modelo AS carro, m.marca, a.data_aluguel
    FROM aluguel a
    JOIN cliente c ON a.codcliente = c.codcliente
    JOIN carro ca ON a.codcarro = ca.codcarro
    JOIN marca m ON ca.codmarca = m.codmarca
    ORDER BY c.nome;
    ```

2. **Encontrar os clientes que alugaram mais de um carro:**

    ```sql
    SELECT c.nome AS cliente, COUNT(DISTINCT a.codcarro) AS total_modelos_alugados
    FROM aluguel a
    JOIN cliente c ON a.codcliente = c.codcliente
    GROUP BY c.nome
    HAVING COUNT(DISTINCT a.codcarro) > 1;
    ```

3. **Listar os carros e o número total de aluguéis por marca:**

    ```sql
    SELECT m.marca, COUNT(a.codaluguel) AS total_alugueis
    FROM marca m
    JOIN carro ca ON m.codmarca = ca.codmarca
    LEFT JOIN aluguel a ON ca.codcarro = a.codcarro
    GROUP BY m.marca
    ORDER BY total_alugueis DESC;
    ```

## Como Rodar

Para rodar esse projeto, siga os passos abaixo:

1. Clone o repositório:
   ```bash
   git clone https://github.com/usuario/locadora-de-veiculos.git
