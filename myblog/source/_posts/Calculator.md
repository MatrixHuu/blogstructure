```java
package com.mxy.lesson02;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TestCalc {
    public static void main(String[] args) {
        Calculator calculator = new Calculator();
        TestActionEvent.windowClose(calculator);
    }
}

//计算器类
class Calculator extends Frame {
    public Calculator(){
        //3个文本框
        TextField num1 = new TextField(10);//字符数
        TextField num2 = new TextField(10);//字符数
        TextField num3 = new TextField(20);//字符数

        //1个按钮
        Button button = new Button("=");
        button.addActionListener(new MyCalcListener(num1,num2,num3));

        //1个标签
        Label label = new Label("+");

        //布局
        setLayout(new FlowLayout());

        add(num1);
        add(label);
        add(num2);
        add(button);
        add(num3);

        pack();
        setVisible(true);


    }
}

//监听器类
class MyCalcListener implements ActionListener {

    //获取3个变量
    private TextField num1,num2, num3;

    public MyCalcListener(TextField num1, TextField num2, TextField num3) {
        this.num1 = num1;
        this.num2 = num2;
        this.num3 = num3;
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        //1.获得加数和被加数

        int n1 = Integer.parseInt(num1.getText());
        int n2 = Integer.parseInt(num2.getText());


        //2.将这个值+运算后，放到第3个框
        num3.setText("" + (n1+n2));

        //3.清除前两个框
        num1.setText("");
        num2.setText("");

    }
}

```









```java
//java里面的经典用法：在一个类里面持有另一个类的引用
package com.mxy.lesson02;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TestCalc{

    public static void main(String[] args){
        new Calculator().launchFrame();
    }
}

//做好计算器的窗体界面
class Calculator extends Frame {

    //属性(成员变量)
    TextField num1,num2,num3;

    //把设计计算器窗体的代码封装成一个方法
    public void launchFrame(){
        num1 = new TextField(10);
        num2 = new TextField(10);
        num3 = new TextField(15);

        Label plSign = new Label("+");
        Button eqlSign = new Button("=");

        eqlSign.addActionListener(new MyMonitorEqlSign	(this));

        setLayout(new FlowLayout());
        add(num1);
        add(plSign);
        add(num2);
        add(eqlSign);
        add(num3);

        pack();
        setVisible(true);
    }
}
//监听器中引用类
class MyMonitorEqlSign implements ActionListener {
    Calculator calc = null;

    public MyMonitorEqlSign(Calculator calc){
        this.calc = calc;
    }

    @Override
    public void actionPerformed(ActionEvent e){
        int n1 = Integer.parseInt(calc.num1.getText());
        int n2 = Integer.parseInt(calc.num2.getText());
        calc.num3.setText(""+(n1+n2));
        calc.num1.setText("");
        calc.num2.setText("");
    }
}
```

