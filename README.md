# 🍔 Food Court Ordering System (Advanced Python Project)
WVC Advanced Python Midterm Project Fall 2025
## Table of Contents

1. [Overview](#overview)  
2. [Features](#features)  
3. [Project Structure](#project-structure)  
4. [Installation](#installation)  
5. [Usage](#usage)  
6. [UML Diagrams](#uml-diagrams)  
7. [Design Details](#design-details)  
8. [Examples](#examples)  
9. [Testing](#testing)  
10. [Future Improvements](#future-improvements)  
11. [Contributing](#contributing)  
12. [License](#license)

## Overview
This project is an **Advanced Python application** that models a Food Court Ordering System.  
It demonstrates:
- Object-oriented programming with abstract classes and interfaces  
- UML-driven design  
- Clear separation between entities like Customer, MenuItem, Order, and Restaurant  

---

## Features
- Place and track customer orders  
- Add menu items from multiple restaurants  
- Abstract `Item` and `Order` interfaces with concrete implementations (`MenuItem`, `MenuOrder`)  
- Calculate totals and manage order status  
- Extendable design for payment and delivery modules  

---

## Project Structure

---

## Installation
1. Clone this repository:  
   ```bash
   git clone https://github.com/your-username/food-court-ordering.git
   cd food-court-ordering
   ```
2. Set up a virtual environment (optional but recommended):
  ```bash
  python -m venv venv
  source venv/bin/activate   # macOS/Linux
  venv\Scripts\activate      # Windows
  ``` 
3. Install dependencies:
  ```bash
   pip install -r requirements.txt
   ```
## Usage 
Run the main program:
  ```bash
  python src/main.py
  ```
Example:
  ``` bash
  Welcome to the Food Court!
  Customer places an order...
  Order total: $24.99
  ```

## Food Court UML Diagram (Mermaid)
Here is the high-level UML class diagram of the system:

```mermaid
classDiagram
  class Item {
    <<abstract>>
    +float getPrice()
    +str getName()
  }

  class Order {
    <<abstract>>
    +void addItem(item: Item)
    +float calculateTotal()
    +str getStatus()
  }

  class MenuItem {
    -int itemID
    -str name
    -float price
    -str category
    +float getPrice()
    +str getName()
  }

  class MenuOrder {
    -int orderID
    -List~Item~ items
    -str status
    +void addItem(item: Item)
    +float calculateTotal()
    +str getStatus()
  }

  class Restaurant {
    -str name
    -str location
    -List~MenuItem~ menu
    +void addMenuItem(item: MenuItem)
    +void prepareOrder(order: MenuOrder)
  }

  class Customer {
    -str name
    -str contactInfo
    +void placeOrder(order: MenuOrder)
    +void trackOrder(order: MenuOrder)
  }

  MenuItem ..|> Item
  MenuOrder ..|> Order

  Customer "1" --> "0..*" MenuOrder : places
  MenuOrder "1" o-- "1..*" Item : contains
  Restaurant "1" --> "0..*" MenuItem : offers
  Restaurant "1" --> "0..*" MenuOrder : prepares
  ```
## Design Details
• Item (abstract): defines the interface for all purchasable items
•	MenuItem: implements Item, represents food or drink on the menu
•	Order (abstract): defines the contract for any type of order
•	MenuOrder: implements Order, manages items and totals
•	Restaurant: owns menu items and prepares orders
•	Customer: places and tracks orders
  
## Examples

  ```python
  # Create menu items
  burger = MenuItem(1, "Burger", 8.99, "Food")
  soda = MenuItem(2, "Soda", 1.99, "Drink")

  # Create an order
  order = MenuOrder(101)
  order.addItem(burger)
  order.addItem(soda)

  print(order.calculateTotal())  # Output: 10.98
  ```

## Testing
Run unit tests with:
```bash
  pytest tests/
```

## Future Improvements

  •	Add Payment interface for multiple payment methods (card, cash, app)
  •	Implement a small CLI or GUI for user interaction
  •	Connect to a database for persistent storage

## Contributing

## Lisence
This project is licensed under the MIT License — see the LICENSE file for details.
