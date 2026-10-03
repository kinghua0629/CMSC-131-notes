# Notes for writing code on paper

1. 注意大括号！特别是最后一个

2. 写代码的时候尽量把变量名命名得清晰一点，不要就用一个字母

3. 注意Scope！尽量在第一行就把要return的变量定义好，否则到最后很难分清return写在哪里

4. 三角形使用：（假设n行的直角三角形）

   ```java
   for (int i = 1; i <= n; i++){
        for (int j = 1; j <= i; j++ ){
            ...
        }
   }
   ```

    正方形使用：

    ```java
    for (int i = 1; i <= n; i++){
        for (int j = 1; j <= n; j++ ){
            ...
        }
   }
   ```

5. 比较```String```的时候不要用```==```，要用```.equals()```

6. 不要忘记```;```
7. 