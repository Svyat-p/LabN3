## Отчет по лабораторной работе № 3

#### № группы: `ПМ-2402`

#### Выполнил: `Бронников Святослав Викторович`

#### Вариант: `4`

### Cодержание:

- [Постановка задачи](#1-постановка-задачи)
- [Выбор структуры данных](#2-выбор-структуры-данных)
- [Алгоритм](#3-алгоритм)
- [Программа](#4-программа)
- [Анализ правильности решения](#5-анализ-правильности-решения)

### 1. Постановка задачи

Разработать систему управления списком покупок с функциями анализа бюджета и
стоимости товаров. Обеспечить возможность работы с данными о товарах, их ценах и
доступных средствах, включая проверку соответствия стоимости покупок бюджету.

Данную задачу можно разделить на подзадачи:
1. Создание класса Товар, хранящего в себе название товара, его цену, статус куплено/не куплено, необходимое количество.
2. Создание методов в классе Товар, позволяющих находить стоимость товара, а также выводить в формате Название:  Цена:   Количество:   Статус: 
3. Создание класса Список Покупок.
4. Создание метода для указания бюджета.
5. Создание метода для обавления денег в бюджет.
6. Создание метода для проверки возможности покупки товара.
7. Создание метода для покупки товара.
8. Создание метода для вычисления общей стоимости списка.
9. Создание метода для вычисления общей стоимости оставшихся товаров.
10. Создание метода для проверки возможности покупки всего списка.
11. Создание метода для подсчёта недостающей суммы.
12. Создание функции «Купить всё».
13. Создание метода для сортировки товаров по цене.
14. Создание метода для определения количества товаров, которые можно купить.
15. Создание функций нахождения самого дешёвого или дорогого товара.

### 2. Выбор структуры данных

| название переменной | Тип (в Java) | 
|---------------------|--------------|
| `temp`              | `Product`    |
| `product`           | `Product`    |
| `name`              | `String`     |
| `isPurchased`       | `boolean`    |
| `ind`               | `boolean`    |
| `quantity`          | `int`        |
| `productCount`      | `int`        |
| `count`             | `int`        |
| `index`             | `int`        |
| `budget`            | `double`     |
| `rem`               | `double`     |
| `total`             | `double`     |
| `remcost`           | `double`     |
| `cheap`             | `double`     |
| `exp`               | `double`     |

### 3. Алгоритм

#### Алгоритм выполнения программы:

1. **Класс Product**
   Используется для хранения всей необходимой информации о товаре в одном месте. Позволяет по отдельности получать название товара, его цену, количество и статус.
   
3. **Класс ShoppingList**
   Используется для создания списка покупок, а также для получения всей необходимой информации о списке.
   - **ShoppingList**
     Создает список покупок
   - **addProduct**
     Добавляет товар в список покупок
   - **setBudget**
     Устанавливает бюджет
   - **addMoney**
     Добавляет деньги в бюджет
   - **RemainingBudget**
     Считает оставшиеся после покупок деньги
   - **canPurchase**
     Проверяет возможность покупки товара
   - **purchaseProduct**
     Покупает товар
   - **totalCost**
     Находит общую стоимость списка
   - **remainingCost**
     Находит общую стоимость некупленных товаров
   - **canPurchaseAll**
     Проверяет, можно ли купить все товары из списка
   - **missingAmount**
     Считает недостающую до покупки всех товаров суммы
   - **purchaseAll**
     Пытается купить все товары
   - **sortProducts**
     Сортирует товары в списке по стоимости по возрастанию или по убыванию в зависимости от настроек
   - **PurchaseCertainAmount**
     Находит количество товаров, которые можно купить, начиная с самого дешевого или с самого дорогого в зависимости от настроек
   - **findCheapestProduct**
     Выводит самый дешевый товар
   - **findMostExpensiveProduct**
     Выводит самый дорогой товар
   - **displayProducts**
     Выводит все товары

### 4. Программа
   
```java
// Создание класса Товар
class Product {

    // Создание полей в классе Товар
    String name;
    double price;
    boolean isPurchased;
    int quantity;

    // Конструктор класса Товар
    public Product(String name, double price, int quantity) {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
        this.isPurchased = false;
    }

    // Геттеры класса Товар
    public String getName(){
        return name;
    }

    public double getPrice(){
        return price;
    }

    public boolean getIsPurchased(){
        return isPurchased;
    }

    // Вычисление стоимости товара
    public double Cost() {
        return price * quantity;
    }

    // Вывод товара
    @Override
    public String toString() {
        return "Название:" + name + " | Цена: " + price + " | Количество: " + quantity + " | Статус: " + isPurchased;
    }
}

// Создание класса Список Покупок
class ShoppingList {
    // Создание полей класса список сокупок
    Product[] product;
    int productCount;
    double budget;

    // Конструктор класса список покупок
    public ShoppingList(int CountOfProducts) {
        this.product = new Product[CountOfProducts];
        this.productCount = 0;
        this.budget = 0.0;
    }

    // Добавление товара в список покупок
    public void addProduct(String name, double price, int quantity) {
        product[productCount] = new Product(name, price, quantity);
        productCount++;
    }

    // Указание бюджета
    public void setBudget(double budget) {
        this.budget = budget;
    }

    // Добавление денег в бюджет
    public void addMoney(double money) {
        this.budget += money;
    }

    // Подсчет оставшихся в бюджете денег после покупок товаров
    public double RemainingBudget() {
        double rem = budget;
        for (int i = 0; i < productCount; i++)
            if (product[i].isPurchased)
                rem -= product[i].Cost();
        return rem;
    }

    // Проверка возможности покупки товара по его названию
    public boolean canPurchase(String name) {
        boolean ind = false;
        for (int i = 0; i < productCount; i++)
            if (product[i].name.equals(name) && product[i].Cost() <= RemainingBudget())
                ind = true;
        return ind;
    }

    // Проверка возможности покупки товара по его номеру
    public boolean canPurchase(int number) {
        boolean ind = product[number - 1].Cost() <= RemainingBudget();
        return ind;
    }

    // Покупка товара
    public void purchaseProduct(String name) {
        for (int i = 0; i < productCount; i++)
            if (product[i].name.equals(name) && canPurchase(name))
                product[i].isPurchased = true;
    }

    // Общая стоимость списка
    public double totalCost() {
        double total = 0;
        for (int i = 0; i < productCount; i++)
            total += product[i].Cost();
        return total;
    }

    // Общая стоимость некупленных товаров
    public double remainingCost() {
        double remcost = 0;
        for (int i = 0; i < productCount; i++)
            remcost += product[i].Cost();
        return remcost;
    }

    // Проверка возможности покупки всего списка
    public boolean canPurchaseAll() {
        return budget >= remainingCost();
    }

    // Подсчет недостающей суммы
    public double missingAmount() {
        if (remainingCost() - budget > 0)
            return remainingCost() - budget;
        else
            return 0;
    }

    // Функция "Купить всё"
    public void purchaseAll() {
        for (int i = 0; i < productCount; i++)
            if (!product[i].isPurchased && budget >= product[i].Cost()) {
                budget -= product[i].Cost();
                product[i].isPurchased = true;
            }
    }

    // Сортировка товаров по цене
    public void sortProducts(boolean ascending) {
        Product temp;
        for (int i = 0; i < productCount - 1; i++)
            for (int j = 0; j < productCount - i - 1; j++)
                if ((ascending && product[j].price > product[j + 1].price) ||
                        (!ascending && product[j].price < product[j + 1].price)) {
                    temp = product[j];
                    product[j] = product[j + 1];
                    product[j + 1] = temp;
                }
    }

    // Покупка определённого количества товаров
    public int PurchaseCertainAmount(boolean ascending) {
        int count = 0;
        sortProducts(ascending);
        for (int i = 0; i < productCount; i++)
            if (product[i].Cost() <= budget) {
                budget -= product[i].Cost();
                count++;
            }
        return count;
    }

    // Нахождение самого дешёвого товара
    public void findCheapestProduct() {
        double cheap = -1.0;
        int index = -1;
        for (int j = 0; j < productCount; j++)
            if (!product[j].isPurchased) {
                cheap = product[j].price;
                index = j;
                break;
            }

        for (int i = 0; i < productCount; i++)
            if (!product[i].isPurchased && product[i].price < cheap) {
                cheap = product[i].price;
                index = i;
            }
        if (index == -1)
            System.out.println("Все товары куплены.");
        else
            System.out.println(product[index].toString());
    }

    // Нахождение самого дорогого товара
    public void findMostExpensiveProduct() {
        double exp = -1.0;
        int index = -1;
        for (int i = 0; i < productCount; i++)
            if (!product[i].isPurchased && product[i].price > exp) {
                exp = product[i].price;
                index = i;
            }
        if (exp == -1.0)
            System.out.println("Все товары куплены.");
        else
            System.out.println(product[index].toString());
    }
}
```

### 5. Анализ правильности решения
1. Тест setBudget
   
**Input**:

400.0
   
**Output**:

400.0

2. Тест addMoney
   
   **Input**:
   
   100.0
   
   **Output**:
   
   500.0
   
4. Тест canPurchase
   
   **Output**:
   
   Товар 1: true
   Товар 1: true


