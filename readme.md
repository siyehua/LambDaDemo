# Lambda 表达式

Lambda 即 λ,就是我们以前学数学的"浪打",lambda 最重要的概念即闭包.
下面就传统的匿名内部类写法与 lambda 做一下总结

```java
package com.example;


import java.util.function.BiConsumer;

public class MyLamDaTest {

    public <T, U> void run(BiConsumer<T, U> a) {
        //do something
    }


    public void method_reference(String a, String b) {
        System.out.println("a: " + a + " b: " + b);
    }

    interface Action2 {
        void accept(int a, int b);
    }

    public void runInt(Action2 a) {
        //do something
    }

    public void reference(int a, int b) {
        System.out.println("a: " + a + " b: " + b);
    }


    public static void main(String[] args) {
        MyLamDaTest a = new MyLamDaTest();
        //匿名内部类写法
        a.run(new BiConsumer<String, String>() {
            @Override
            public void accept(String s1, String s2) {
                a.method_reference(s1, s2);
            }
        });

        //lambda 完整版
        a.run((String s1, String s2) -> {
            a.method_reference(s1, s2);
        });

        //lambda 精简版(去掉参数类型和{}花括号)
        a.run((BiConsumer<String, String>)
                (one, two) -> a.method_reference(one, two)
        );

        //lambda 方法引用版
        a.run(a::method_reference);


        //匿名内部类写法
        a.runInt(new Action2() {
            @Override
            public void accept(int t1, int t2) {
                a.reference(t1, t2);
            }
        });
        //lambda 完整版
        a.runInt((int i1, int i2) -> {
            a.reference(i1, i2);
        });
        //lambda 精简版(去掉参数类型和{}花括号)
        a.runInt((i1, i2) -> a.reference(i1, i2));
        //lambda 方法引用版
        a.runInt(a::reference);
    }
}

```