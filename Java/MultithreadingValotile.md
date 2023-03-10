# Volatile

В Java ключевое слово volatile используется для обозначения переменных, значения которых могут быть изменены несколькими потоками одновременно.

Когда переменная объявлена как volatile, это означает, что операции чтения и записи для этой переменной должны быть атомарными, т.е. эти операции не могут быть разделены на более мелкие операции и должны быть выполнены полностью до перехода к другому потоку.

Это гарантирует, что изменения переменной, сделанные одним потоком, будут видны другим потокам сразу же, без необходимости использования блокировок или синхронизации. Без использования volatile переменные могут кэшироваться в памяти каждого потока, что может привести к ошибкам синхронизации и неопределенному поведению.

Таким образом, использование ключевого слова volatile обеспечивает безопасность и правильность выполнения операций чтения и записи переменных в многопоточной среде.

Пример:
```
public class Main {

    volatile static int i = 0;

    public static void main(String[] args) {
        new MyThreadRead().start();
        new MyThreadWrite().start();

    }

    static class MyThreadWrite extends Thread {
        @Override
        public void run() {
            while (i < 5) {
                System.out.println("increment i to " + (++i));
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    static class MyThreadRead extends Thread {
        @Override
        public void run() {
            int localVar = i;
            while(localVar < 5) {
                if(localVar != i) {
                    System.out.println("new value of i is " + i);
                    localVar = i;
                }
            }
        }
    }
}

```

Если бы мы не использовали **volatile** то MyThreadRead выполнился бы всего один раз.