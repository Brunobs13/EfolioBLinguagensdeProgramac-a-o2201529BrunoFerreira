# Product Sales Management System

## Overview

This application integrates Java with SWI-Prolog to manage product sales. The main functionality includes registering sales, viewing sales data, and calculating various metrics related to sales. The system involves Prolog queries to handle data operations and Java methods to interact with the user and the Prolog system.

## Main Functionality

### Initialization and User Interaction

The `main` function initializes the Prolog environment, sets up a `Scanner` for user interaction, displays the main menu, navigates to submenus based on user choices, and ensures valid inputs until the exit option is selected.

### Key Methods and Prolog Connections

#### `registerSale`

**Connections and Calls:**
- **Java Method:** `store.lerClientes()`
  - **Store:** Sends a Prolog query to retrieve all client records (`cliente/4`).
  - **Prolog:** Retrieves client records from the Prolog database.
- **Java Method:** `store.lerItens()`
  - **Store:** Sends a Prolog query to retrieve all item records (`item/5`).
  - **Prolog:** Retrieves item records from the Prolog inventory.
- **Java Method:** `realizarVenda(store, carrinho)`
  - **Store:** Uses several Store class methods to calculate sales totals, apply discounts, calculate shipping costs, and register the sale.
  - **Prolog:** Involves multiple Prolog queries:
    - Calculate the total of items in the cart (`getItemTotalFromProlog`).
    - Calculate applicable discounts (`getDiscountsFromProlog`).
    - Calculate shipping cost (`getShippingCostFromProlog`).
    - Register the final sale (`registrarVenda`), recording a new `purchase/7` fact in the Prolog system.

#### `realizarVenda`

**Connections and Calls:**
- **Java Method:** `store.getItemTotalFromProlog(carrinho.getItems())`
  - **Store:** Queries Prolog to calculate the total of items in the cart.
  - **Prolog:** Calculates the total based on `item/5` records.
- **Java Method:** `store.getDiscountsFromProlog(carrinho.getItems(), carrinho.getCliente().getAnosLealdade())`
  - **Store:** Queries Prolog to calculate applicable discounts.
  - **Prolog:** Calculates discounts based on `discount/2` and `loyalty_discount/2` records.
- **Java Method:** `store.getShippingCostFromProlog(carrinho.getCliente().getDistrito())`
  - **Store:** Queries Prolog to calculate shipping cost.
  - **Prolog:** Calculates shipping cost based on `shipping_cost/2` records.
- **Java Method:** `store.registrarVenda(carrinho.getCliente().getId(), data, carrinho.getItems())`
  - **Store:** Sends a Prolog query to register the sale.
  - **Prolog:** Records a new `purchase/7` fact in the Prolog system.

#### `verVendasPorData`

**Connections and Calls:**
- **Java Method:** `store.getVendasPorData(data)`
  - **Store:** Queries Prolog to obtain sales by date.
  - **Prolog:** Retrieves `purchase/7` records related to the specified date.

#### `verVendasPorCliente`

**Connections and Calls:**
- **Java Method:** `store.getVendasPorCliente(clienteID)`
  - **Store:** Queries Prolog to obtain sales by client ID.
  - **Prolog:** Retrieves `purchase/7` records related to the specified client ID.

#### `verVendasPorDistrito`

**Connections and Calls:**
- **Java Method:** `store.getVendasPorDistrito(distrito)`
  - **Store:** Queries Prolog to obtain sales by district.
  - **Prolog:** Retrieves `purchase/7` records related to the specified district.

#### `verTotaisPorDistrito`

**Connections and Calls:**
- **Java Method:** `store.getTotaisPorDistrito(distrito)`
  - **Store:** Queries Prolog to obtain totals of sales, discounts, and shipping costs by district.
  - **Prolog:** Retrieves `totais_por_distrito/5` records.

#### `verTotaisPorData`

**Connections and Calls:**
- **Java Method:** `store.getTotaisPorData(data)`
  - **Store:** Queries Prolog to obtain totals of sales, discounts, and shipping costs by date.
  - **Prolog:** Retrieves `totais_por_data/5` records.

#### `verDistritoMaisDescontos`

**Connections and Calls:**
- **Java Method:** `store.getDistritoMaisDescontos()`
  - **Store:** Queries Prolog to determine the district with the most discounts.
  - **Prolog:** Calculates the district based on discount records.

## Example

```bash
Last login: Sat May 25 03:53:19 on ttys000
(base) brunoferreira@Air-de-Bruno ~ % cd /Users/brunoferreira/Downloads/jpl-complied

(base) brunoferreira@Air-de-Bruno jpl-complied % javac -cp .:/opt/homebrew/opt/swi-prolog/lib/swipl/lib/jpl.jar Main.java Store.java Cliente.java Item.java Cart.java

Note: Store.java uses or overrides a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
(base) brunoferreira@Air-de-Bruno jpl-complied % java -Djava.library.path=/opt/homebrew/opt/swi-prolog/lib/swipl/lib -cp .:/opt/homebrew/opt/swi-prolog/lib/swipl/lib/jpl.jar:. Main

Prolog file loaded successfully.
Select an option:
1: Register a new sale
2: Sales History
3: Inventory Management
4: Cost and Discount Management
5: Customer Management
0: Exit
Select an option:
