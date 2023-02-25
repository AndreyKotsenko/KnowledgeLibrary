# Инкапсуляция и можификаторы доступа

Инкапсуляция в Java - это механизм, который позволяет скрыть внутреннюю реализацию объектов от внешнего мира. Она позволяет создавать классы и объекты, которые имеют свойства и методы, доступ к которым контролируется и ограничивается.

Основная идея инкапсуляции заключается в том, что данные и методы, которые работают с этими данными, объединены в одном классе, и доступ к ним осуществляется только через специальные методы - геттеры и сеттеры. Такой подход обеспечивает безопасность данных, скрывая их от прямого доступа, и предотвращает неправильное использование.

Кроме того, использование инкапсуляции позволяет улучшить переносимость кода, так как при изменении реализации класса, необходимо изменять только его внутреннюю логику, а внешний код, который использует класс, останется неизменным.

В Java инкапсуляция реализуется с помощью модификаторов доступа (public, private, protected и default), которые определяют, какие части класса доступны для использования извне. По умолчанию все члены класса имеют модификатор доступа default, который означает, что они доступны только из других классов в том же пакете. Кроме того, в Java есть ключевое слово "this", которое позволяет обращаться к текущему объекту класса и его свойствам и методам.

**public** - наиболее открытый модификатор доступа. Поля и методы, объявленные с модификатором public, доступны из любого места в программе. Так, например, классы, объявленные с модификатором public, могут быть использованы в других классах без ограничений.

**private** - наиболее строгий модификатор доступа. Поля и методы, объявленные с модификатором private, доступны только внутри того же класса, где они были объявлены. Таким образом, доступ к таким элементам класса извне будет невозможен.

**protected** - поля и методы, объявленные с модификатором protected, доступны внутри того же пакета, где они были объявлены, а также в подклассах (наследниках) этого класса. Такой модификатор используется, когда требуется ограничить доступ к членам класса, но при этом дать доступ наследникам.

**default** (иногда называется package-private) - это модификатор доступа, который не указывается явно, а используется по умолчанию, если не указан никакой другой модификатор. Поля и методы, объявленные без модификатора доступа, доступны только внутри того же пакета, где они были объявлены. Такой модификатор используется, когда требуется ограничить доступ к членам класса только внутри того же пакета.

Пример:
```
package test;

public class Test {

    public int a = 5;
    private int b = 10;
    protected int c = 15;
    int d = 20;

}

class SecondTest extends Test {

    public int getC(){
        return c;     // we have access because it protected
    }
}
```
Здесь мы создали 2 класса в пакете **test**

```
package com.company.akotsenko;

public class Person {
    public String name = "Max"; //bad code cause we use public for field

    private int age = 10;

    int count = 5;
    protected String secondName = "Jojo";

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

}
```

Здесь мы создали класс в пакете **com.company.akotsenko**

Посмотрим на вызов полей этих классов с мейн-функции в том же пакете **com.company.akotsenko**

```
package com.company.akotsenko;

import test.Test;

public class Main {

    public static void main(String[] args) {

        // here we will use public field.
        Person person = new Person();
        System.out.println(person.name);

        // here we will use private field

        person.setAge(20);
        System.out.println(person.getAge());


        //access modifiers
        Test test = new Test();

        System.out.println(test.a);
        //System.out.println(test.b); error because private
        //System.out.println(test.c); error because protected
        //System.out.println(test.d); error because default

        Person testPerson = new Person();

        System.out.println(testPerson.name);
        System.out.println(testPerson.count); // it is works because default modifier available at package level
        System.out.println(testPerson.secondName); // it is works because protected modifier available at package level and child classes
        //System.out.println(testPerson.age); error because private

    }
}

```