# Переопределние 

Переопределение (override) в Java - это процесс определения метода в подклассе с той же сигнатурой (именем и параметрами) какого-то метода из его суперкласса, чтобы заменить его функциональность.

Когда метод в подклассе имеет ту же сигнатуру, что и метод в его суперклассе, то при вызове метода из объекта подкласса будет вызван метод подкласса, а не метод суперкласса. Это называется "переопределением" метода.

Важно отметить, что при переопределении метода в подклассе необходимо сохранять сигнатуру (имя метода, типы и порядок параметров), чтобы Java могла правильно определить, какой метод вызывать во время выполнения программы. Кроме того, возвращаемый тип переопределяемого метода должен быть тот же или подтипом возвращаемого типа в методе суперкласса.

Пример:
```
class Parent {

    protected void printSmt() {
        System.out.println("Something");
    }

    Parent test(){
        return new Parent();
    }

    void go() throws Exception {
        System.out.println(" go ");
    }

    void run() throws IOException {
        System.out.println(" go ");
    }


    void ex() throws Exception {

    }
}

class Child extends Parent {

//    @Override          // error because protected higher level than default
//    void printSnt() {
//        System.out.println("Something else");
//    }

    @Override
    public void printSmt() {
        System.out.println("Something else");
    }

    @Override
    Child test(){
        return new Child();
    }

    @Override
    void go() throws IOException {
        System.out.println(" go ");
    }

//    @Override                   // error because Exception higher level than IOException
//    void run() throws Exception {
//        System.out.println(" go ");
//    }

    @Override
    void ex() {

    }

}
```

Здесь мы создали 2 класса которые показывают различные способы переопределения методов.

Main функция:
```
public class Main {

    public static void main(String[] args) {

        Parent parent = new Parent();
        Parent child = new Child();

        parent.printSmt();
        child.printSmt();

        System.out.println(parent.test());
        System.out.println(child.test());

        try {
            parent.ex();
        } catch (Exception e) {
            e.printStackTrace();
        }

        try {
            child.ex();
        } catch (Exception e) {
            e.printStackTrace();
        }

    }
}
```

По этим примерам можно выделить главыне правила переопределения:
 - имя функции должно совпадать
 - тип и количество аргументов должно сохраняться
 - возвращаемое значение должно сохраняться или можно изменить его на дочерний от суперкласса.
 - модификаторы доступа можно менять только в сторону расширения области доступа. К примеру **protected** можно менять на **public** так как паблик дает больше доступа, но нельзя менять на **default** так как он виден только на уровне пакета, и урезает доступ, в то время как **protected** виден на уровне пакета и наследуемых классов.
 - исключения можно изменять только если они являються дочерними от суперкласса. 
 - аргументы метода не могут принимать дочерние обьекты при переопределении.