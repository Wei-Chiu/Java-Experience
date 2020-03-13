# 修饰符

### 权限修饰符

- 同包下：
  继承调用：public protect default
  对象调用：public protect default
- 不同包下：
  继承调用：public protect
  对象调用：public

### “…” 动态参数

可变长参数，也就是相当于一个数组,能够传入0个至n个参数，用法：

```java
public static void main(String[] args) {
        String[] t1 = {};
        String[] t2 = {"java","C++"};
        String t3 = "java";
        threePoint("java","C++","Python");
        threePoint(t1);
        threePoint(t2);
        threePoint(t3);
        //threePoint(t3,t2);//类型错误,数组只能传一个
    }

    public static void threePoint(String... s) {
        if (s == null) {
            return;
        }
        int len = s.length;
        if (len == 0) {
            System.out.println("没有字符");
        } else {
            for (String s1 : s
            ) {
                System.out.println(s1 + " ");
            }
        }
        System.out.println("==============================");
    }
————————————————
版权声明：本文为CSDN博主「左高右低」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/zjgyjd/article/details/98883516
```

可以看出即可以直接传一个String，也可以直接传String[]的数组，更可以在传递参数时，用逗号把每一个参数隔开。但是由于三个点就代表数组类型，所以传数组的时候，就只能传一个参数，不能再用逗号传其他参数。

### “ :: ”双冒号的使用

jdk8 中使用了 :: 的用法。就是把方法当做参数传到 stream 内部，使 stream 的每个元素都传入到该方法里面执行一下，相当于 lambda 表达式。