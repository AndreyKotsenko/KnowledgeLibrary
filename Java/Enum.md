# Перечисления

В Java, enum (enumeration) - это тип данных, который представляет набор констант (enum-констант) с предопределенными значениями. Enum-константы - это именованные объекты типа enum, которые могут быть использованы для представления ограниченного набора значений, таких как месяцы года, дни недели, цвета и т. д.

Создание enum начинается с ключевого слова enum, за которым следует список именованных констант. Каждая enum-константа представляет собой отдельный объект, который имеет имя и опциональные дополнительные данные. Дополнительные данные могут быть определены при создании каждой enum-константы.

enum может содержать также методы, конструкторы и переменные-члены, что делает его более гибким и мощным инструментом, чем просто перечисление констант.

Пример:
```
public class Main {

    enum CoffeeSize { SMALL(100), MEDIUM(200), BIG(300);

        int milliliters;
        CoffeeSize(int milliliters) {
            this.milliliters = milliliters;
        }

        int getMilliliters() {
            return milliliters;
        }
    };

    public static void main(String[] args) {
        CoffeeSize coffeeSize = CoffeeSize.BIG;
        System.out.println(coffeeSize);
        System.out.println(coffeeSize.getMilliliters());
    }
}
```