### Создание метода

Прежде чем мы начнем разбираться с методами класса, посмотрим пример функции, которая ожидает как аргумент экземпляр класса Switch и выводит информацию о нем, используя переменные экземпляра hostname и mode:
```python
In [3]: class Switch:
   ...:    pass
   ...:

In [4]: sw1 = Switch()

In [5]: sw1.hostname = 'sw1'

In [6]: sw1.model = 'Cisco 3850'

In [7]: def info(sw_obj):
   ...:     print('Hostname: {}\nModel: {}'.format(sw_obj.hostname, sw_obj.model))
   ...:

In [8]: info(sw1)
Hostname: sw1
Model: Cisco 3850
```

В функции info параметр `sw_obj` ожидает экземпляр класса `Switch`. Скорее всего, в этом примере нет ничего нового, ведь аналогичным образом ранее мы писали функции, которые ожидают строку, как аргумент, а затем вызывают какие-то методы у этой строки.

Этот пример поможет разобраться с методом info, который мы добавим в класс Switch.


Для добавления метода, необходимо создать функцию внутри класса:
```python
In [15]: class Switch:
    ...:     def info(self):
    ...:         print('Hostname: {}\nModel: {}'.format(self.hostname, self.model))
    ...:
```

Если присмотреться, метод info выглядит точно так же, как функция info, только вместо имени sw_obj, используется self. Почему тут используется странное имя self, мы разберемся позже, а пока посмотрим как вызвать метод info:
```python
In [16]: sw1 = Switch()

In [17]: sw1.hostname = 'sw1'

In [18]: sw1.model = 'Cisco 3850'

In [19]: sw1.info()
Hostname: sw1
Model: Cisco 3850
```

В примере выше сначала создается экземпляр класса Switch, затем в экземпляр добавляются переменные hostname и model, и только после этого вызывается метод info.
Метод info выводит информацию про коммутатор, используя значения, которые хранятся в переменных экземпляра.

Вызов метода отличается, от вызова функции: мы не передаем ссылку на экземпляр класса Switch. Нам это не нужно, потому что мы вызываем метод у самого экземпляра. Еще один непонятный момент - зачем же мы тогда писали self.

Все дело в том, что Python преобразует такой вызов:
```python
In [39]: sw1.info()
Hostname: sw1
Model: Cisco 3850
```

Вот в такой:
```python
In [38]: Switch.info(sw1)
Hostname: sw1
Model: Cisco 3850
```

Во втором случае, в параметре self уже больше смысла, он действительно принимает ссылку на экземпляр и на основании этого выводит информацию.

С точки зрения использования объектов, удобней вызывать методы используя первый вариант синтаксиса, поэтому, практически всегда именно он и используется.

> При вызове метода экземпляра класса, ссылка на экземпляр передается первым аргументом. При этом, экземпляр передается неявно, но параметр надо указывать явно.

Такое преобразование не является особенностью пользовательских классов и работает и для встроенных типов данных аналогично. Например, стандартный способ вызова метода append в списке, выглядит так:
```python
In [4]: a = [1,2,3]

In [5]: a.append(5)

In [6]: a
Out[6]: [1, 2, 3, 5]
```

При этом, то же самое можно сделать и используя второй вариант, вызова через класс:
```python
In [7]: a = [1,2,3]

In [8]: list.append(a, 5)

In [9]: a
Out[9]: [1, 2, 3, 5]
```
