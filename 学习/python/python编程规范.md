## 常用习惯

- 让代码既可以执行，又可以被导入

  - ```python
    if __name__ == '__main__':
    ```

- 用下面的方式判断真假

  - ```python
    if x:
    if not x:
    ```

     好的代码	

    ```python
    name = 'jackfrued'
    fruits = ['apple', 'orange', 'grape']
    owners = {'1001': '罗浩', '1002': '王大锤'}
    
    if name and fruits and owners:
        print("i love fruits!")
    ```

- 善于使用in

  - ```
    if x in items: # 包含
    for x in items: # 迭代
    ```

    ```python
    name = "luo hao"
    if 'l' in name:
        print("the name has an l in it!")
    ```

- 不使用临时变量交换两个值。

  - `a, b  = b, a`

- 使用序列构造字符串

  - ```python
    chars = ['j', 'a', 'c', 'c', 'd', 'k']
    name = ''.join(chars)
    
    print(name)
    ```

- 经常使用异常捕捉

  - ```python
    d = {'x': 'a'}
    try:
        value = int(d['x'])
        print(value)
    except (KeyError, TypeError, ValueError) as e:
        print("出错啦:{}".format(e))
    ```

- 使用enumerate进行迭代

  - ```python
    fruits = ['orange', 'grape', 'pitaya', 'watermelon']
    
    for index, fruit in enumerate(fruits):
        print(index, ":", fruit)
    ```

- 用生成式生成列表

  - ```python
    data = [7, 20, 3, 15, 11]
    
    res = [i*3 for i in data]
    print(res)
    ```

- 用zip组合键值来创建字典

  - ```python
    keys = ['1001', '1002', '1003']
    values = ['罗浩', '志龙', '大锤']
    
    d = dict(zip(keys, values))
    print(d)
    ```

