# java

1. [修饰符作用范围](../Java/modifier.md)：
2. try catch finally 执行顺序：
   try 或 catch 执行至遇到 return 语句时，将 return 语句缓存跳转去执行 finally ，finally 执行完成后，再执行缓存的 return 语句
3. 多个 JPanel 嵌套时，repaint 的执行顺序是从外到内。
4. updateUI () 和 repaint()：
   在操作 JTable 更新时，只有直接调用 JTable 对象的 updateUI 方法才能正确更新。 调用父对象的 updateUI 会使 JTable 没有数据显示。（和没有调用一样的，说明 updateUI 不会像 repaint 一样调用传递）
   调用父对象的 repaint，等价于调用 JTable 的 repaint ，很奇怪，只显示和初始条目数量同样多的记录数。比方说开始有 2 条，增加数据库中的数据后，也只显示 2 条，但减少的话，可以显示更少。
5. 记账 APP，1. 分为 Panel 等包。 2. Panel 设为静态面板，方便调用。3. 共同的方法抽象出来，定义为一个抽象类，用类去实现。4. 要判断某一个对象，是否有某个方法，可以把这个方法放到抽象类中，判断这个对象是否这个抽象类的实例，是的话代表有这个方法。