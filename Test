public class Main {
    public static void main(String[] args) {

        // Тесты для класса ShoppingList
        ShoppingList shoppingList = new ShoppingList(3);
        shoppingList.addProduct("Товар 1", 100.0, 1);
        shoppingList.addProduct("Товар 2", 50.0, 2);
        shoppingList.addProduct("Товар 3", 200.0, 1);

        // Установка бюджета
        shoppingList.setBudget(400.0);
        System.out.println("Бюджет: " + shoppingList.budget);  // Ожидается 400.0

        // Добавление денег в бюджет
        shoppingList.addMoney(100.0);
        System.out.println("Бюджет после добавления: " + shoppingList.budget);  // Ожидается 500.0


        // Проверка общей стоимости
        System.out.println("Общая стоимость всех товаров: " + shoppingList.totalCost());  // Ожидается 400.0

        // Проверка возможности покупки товара
        System.out.println("Можно ли купить Товар 2: " + shoppingList.canPurchase("Товар 2"));  // Ожидается true
        System.out.println("Можно ли купить Товар 3: " + shoppingList.canPurchase("Товар 3"));  // Ожидается true

        // Проверка покупки всех товаров
        shoppingList.purchaseAll();
        System.out.println("Все товары куплены?");
        shoppingList.displayProducts();  // Ожидается, что все товары будут помечены как купленные

        // Сортировка товаров по цене (по возрастанию)
        shoppingList.sortProducts(true);
        System.out.println("Товары после сортировки по цене (по возрастанию):");
        shoppingList.displayProducts();  // Ожидается сортировка по цене

        // Сортировка товаров по цене (по убыванию)
        shoppingList.sortProducts(false);
        System.out.println("Товары после сортировки по цене (по убыванию):");
        shoppingList.displayProducts();  // Ожидается сортировка по убыванию цены

        // Нахождение самого дешевого и самого дорогого товара
        shoppingList.findCheapestProduct();
        shoppingList.findMostExpensiveProduct();
    }
}
