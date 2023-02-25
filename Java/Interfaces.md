# Интерфесы

В Java интерфейс - это коллекция методов без тела (без реализации), которые должны быть реализованы в классе, который реализует данный интерфейс.

Интерфейсы позволяют создавать абстрактные типы данных, определяя только сигнатуры методов, которые должны быть реализованы классами. Они являются основой для реализации полиморфизма в Java, позволяя различным объектам обмениваться сообщениями между собой, используя один и тот же интерфейс.

Для определения интерфейса используется ключевое слово interface, а для реализации интерфейса в классе используется ключевое слово implements. Класс, который реализует интерфейс, должен реализовать все методы, указанные в интерфейсе, иначе этот класс должен быть также объявлен как абстрактный.

Пример:
```
package com.company.akotsenko;

public interface ISomeInterface extends IOtherInterface {
    void addTwoDigits(int one, int two);

}


interface IOtherInterface {
    int SOME_VARIABLE = 5;  // public static final
    void someMethod();  // abstract public
}

interface IBouncable {
    void bounce();
}

class Example implements ISomeInterface, IBouncable {

    @Override
    public void addTwoDigits(int one, int two) {
        System.out.println(one+two);
    }

    @Override
    public void someMethod() {
        System.out.println("Something");
    }

    @Override
    public void bounce() {
        System.out.println("bounce");
    }
}
```

В этом примере мы создали 3 интерфеса и 1 класс который имплементирует 2 интерфеса. ( множественное наследование классов запрещено, а вот интерфесов можно)

Функция main:
```
    public static void main(String[] args) {
      ISomeInterface test = new Example();

      test.addTwoDigits(5, 10);
      //test.bounce(); error because interface ISomeInterface haven't this method

        Example testTwo = new Example();

        testTwo.addTwoDigits(6, 10);
        testTwo.bounce();
        testTwo.someMethod();
    }
```