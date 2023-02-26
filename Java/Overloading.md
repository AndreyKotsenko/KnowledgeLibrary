# Перегрузка

Перегрузка (overloading) в Java - это возможность определять несколько методов с одним и тем же именем внутри одного класса, но с разными параметрами (типами, количеством или порядком аргументов).

При вызове перегруженного метода компилятор Java определяет, какой метод должен быть вызван, на основе типов и количества аргументов, переданных в вызов.

Пример: 
```
public class Overload {

    int addTwoDigits(int a, int b){
        return a + b;
    }

    double addTwoDigits(double a, double b){
        return a + b;
    }

    String addTwoDigits(double a, double b, String hi){
        return hi + " " + (a + b);
    }
}
```
Здесь мы определили класс с 3 методами. 

Теперь мы создадим новый класс и унаследуемся от выше указаного:
```
class OverloadChild extends Overload {
    void addTwoDigits(int j){
        System.out.println(j);
    }
}

```

При наследовании перегрузка так же сохраняется. 


Посмотри на main функцию:

```
public class Main {

    public static void main(String[] args) {
        Overload test = new Overload();

        System.out.println(test.addTwoDigits(1, 2));
        System.out.println(test.addTwoDigits(1.56, 2.23));

        OverloadChild test2 = new OverloadChild();

        System.out.println(test2.addTwoDigits(1, 2));
        System.out.println(test2.addTwoDigits(1.56, 2.23));
        System.out.println(test2.addTwoDigits(20.45, 34.5, "hi"));
        test2.addTwoDigits(1);
    }
}
```