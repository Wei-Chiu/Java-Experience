# 数组和list相互转换

### int[] 和 List 相互转换：

https://blog.csdn.net/PitBXu/article/details/97672145

一些例子:

```java
int[] intArray = new int[5];
        for (int i = 0; i < intArray.length; i++) {
            intArray[i] = i;
        }
        // int[] -> List<Integer>
        List<Integer> intList = Arrays.stream(intArray).boxed().collect(Collectors.toList());
        // list -> int[]
        int[] ints = intList.stream().mapToInt(Integer::valueOf).toArray();
        // list -> Integer[]
        Integer[] integers = intList.toArray(new Integer[intList.size()]);
        // int[] -> Integer[]
        Integer[] integers1 = Arrays.stream(intArray).boxed().toArray(Integer[]::new);
        // Integer[] -> int[]
        int[] ints1 = Arrays.stream(integers1).mapToInt(Integer::valueOf).toArray();
        // Integer[] -> list<Integer>
        List<Integer> collect = Arrays.stream(integers1).collect(Collectors.toList());
```

