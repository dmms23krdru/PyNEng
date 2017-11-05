## Аргументы переменной длины

Иногда необходимо сделать так, чтобы функция принимала не фиксированное количество аргументов, а любое.
Для такого случая в Python можно создавать функцию со специальным параметром, который принимает аргументы переменной длины.
Такой параметр может быть как ключевым, так и позиционным.


> Даже если вы не будете использовать этот прием в своих скриптах, есть большая вероятность, что вы встретите его в чужом коде.

### Позиционные аргументы переменной длины

Параметр, который принимает позиционные аргументы переменной длины, создается добавлением перед именем параметра звездочки.
Имя параметра может быть любым, но, по договоренности, чаще всего, используют имя ```*args```

Пример функции:
```python
In [1]: def sum_arg(a,*args):
  ....:     print(a, args)
  ....:     return a + sum(args)
  ....: 
```

Функция sum_arg создана с двумя параметрами:
* параметр ```a```
 * если передается как позиционный аргумент, должен идти первым
 * если передается как ключевой аргумент, то порядок не важен
* параметр ```*args``` - ожидает аргументы переменной длины
 * сюда попадут все остальные аргументы в виде кортежа
 * эти аргументы могут отсутствовать

Вызов функции с разным количеством аргументов:
```python
In [2]: sum_arg(1,10,20,30)
1 (10, 20, 30)
Out[2]: 61

In [3]: sum_arg(1,10)
1 (10,)
Out[3]: 11

In [4]: sum_arg(1)
1 ()
Out[4]: 1
```

Можно создать и такую функцию:
```python
In [5]: def sum_arg(*args):
  ....:     print(args)
  ....:     return sum(args)
  ....: 

In [6]: sum_arg(1, 10, 20, 30)
(1, 10, 20, 30)
Out[6]: 61

In [7]: sum_arg()
()
Out[7]: 0
```

### Ключевые аргументы переменной длины

Параметр, который принимает ключевые аргументы переменной длины, создается добавлением перед именем параметра двух звездочек.
Имя параметра может быть любым, но, по договоренности, чаще всего, используют имя ```**kwargs``` (от keyword arguments).


Пример функции:
```python
In [8]: def sum_arg(a,**kwargs):
  ....:     print(a, kwargs)
  ....:     return a + sum(kwargs.values())
  ....: 
```

Функция sum_arg создана с двумя параметрами:
* параметр ```a```
 * если передается как позиционный аргумент, должен идти первым
 * если передается как ключевой аргумент, то порядок не важен
* параметр ```**kwargs``` - ожидает ключевые аргументы переменной длины
 * сюда попадут все остальные ключевые аргументы в виде словаря
 * эти аргументы могут отсутствовать

Вызов функции с разным количеством ключевых аргументов:
```python
In [9]: sum_arg(a=10,b=10,c=20,d=30)
10 {'c': 20, 'b': 10, 'd': 30}
Out[9]: 70

In [10]: sum_arg(b=10,c=20,d=30,a=10)
10 {'c': 20, 'b': 10, 'd': 30}
Out[10]: 70
```

Обратите внимание, что, хотя ```a``` можно указывать как позиционный аргумент, нельзя указывать позиционный аргумент после ключевого:
```python
In [11]: sum_arg(10,b=10,c=20,d=30)
10 {'c': 20, 'b': 10, 'd': 30}
Out[11]: 70

In [12]: sum_arg(b=10,c=20,d=30,10)
  File "<ipython-input-14-71c121dc2cf7>", line 1
    sum_arg(b=10,c=20,d=30,10)
                          ^
SyntaxError: positional argument follows keyword argument
```
