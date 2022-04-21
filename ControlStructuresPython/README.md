# Управляющие структуры Python
1. [Операторы сравнения](#comparison)
2. [Операторы ветвления](#statements)
3. Цикл while
4. Цикл for

### <a name='comparison'>Операторы сравнения</a>
- Операторы сравнения возвращают булевое значение. Оператор - это знак операции, например `==`, `>`, `!=`. Операнды - сравниваемые значения, в случае выражение `5 == 5` оператор - `==`, операнды - `5` и `5`.

- Оператор равенства `==`, возвращает `True` если операнды равны:
    ```python
    print(5 == 5) # True
    print(5 == 6) # False

    print([1,2,3] == [1,2,3]) # True
    ```

- Оператор неравенства `!=`, возвращает `True`, если операнды не равны:
    ```python
    print(5 != 6) # True
    print(5 != 5) # False
    ```

- Оператор тождественности `is`, на простых структурах данных работает так же как и `==`, но на самом деле этот оператор сравнивает адреса в памяти, например:
    ```python
    print(5 is 5) #True
    ```
    но
    ```python
    [1,2,3] == [1,2,3] # True
    [1,2,3] is [1,2,3] # False
    a = b = [1,2,3]
    a is b # True
    ```
    В последнем выражении `True` потому что оба операнда(`a`, `b`) указывают на одну структуру данных.

- Группа операторов: больше `>`, больше или равно `>=`, меньше `<`, меньше или равно `<=`:
    ```python
    print(5 < 6) # True
    print(5 < 4) # False
    print(4 <= 4) # True

    print(5 > 4) # True
    print(5 > 6) # False
    print(5 >= 5) # True
    ```
    Кроме того данные операторы можно комбинировать, можно писать следующие структуры:
    ```python
    a = 5
    print(5 <= a <= 10) # True
    print(5 < a < 10) # False
    print(10 <= a <= 5) # Всегда False, при любых значениях a, нет такого числа, которое больше десяти и меньше 5
    ```

- Оператор принадлежности `in`, возвращает `True`, если элемент есть в какой-либо коллекции:
    ```python
    print(1 in [1,2,3]) # True
    print(4 in [1,2,3]) # False

    print(2 in {"Alex": 2}.values()) # True
    print('Alex' in {"Alex": 2}.keys()) # True

    print("a" in "abc") # True, символ в строке тоже можно так искать
    ```

- Так как результатом операций сравнения является булевое значение, к результату можно примерять логические операнды `and`, `or`, `not`:
    ```python
    a = 5
    b = 7
    d_list = [1,2,3,4,5,6]
    print((0 <= a <= 10) and (not (b in d_list))) # True
    ```


### <a name='statements'> Операторы ветвления </a>
- Операторы ветвления - самые базовые логические составляющие вашей программы, они говорят, как программа должна реагировать на данные, которые она принимает.
- Операторы ветвления в Python представлены командой `if`, она еще называется **условным оператором**. После нее пишется условие и исполняемый код. Если условие правдиво `True`, то код исполняется. Условие пишется сразу после `if`, потом ставится двоеточие `:` и на следующей строке, с отступом в один tab, пишется исполняемый код. Чтобы писать код, который не входит в `if`, нужно сместить убрать отступ. Например, программа которая спрашивает желает ли пользователь вывести приветственное сообщение:
    ```python
    name = input("Enter your name: ")
    answer = input("Do you want to see greeting message?(yes/no): ")

    if answer == "yes":
        print("Hello", name, sep=',', end='!')

    if answer == "no":
        print("OK.")
    ```
    Если запустить данную программу, ввести свое имя, а потом ответить `yes`, то программы выведет `"Hello, name!"` - исполнится первое условие. Если ответить `no`, то программа не выведет `"Hello, name!"`, а просто напишет `"OK."` - первое условие не исполнится, а второе исполнится.
    Также можно переписать программу, чтобы она понимала больше ответов, используя коллекции верных и неверных ответов:
    ```python
    name = input("Enter your name: ")
    answer = input("Do you want to see greeting message?(yes/no): ")

    positive_answers = ('yes', 'y', 'yep', 'yeah') # кортеж положительных ответов
    negative_answers = ('no', 'n', 'nope') # кортеж отрицательных ответов

    if answer in positive_answers:
        print("Hello", name, sep=',', end='!')

    if answer is negative_answers:
        print("OK.")
    ```

- Так же можно сделать так, чтобы при неисполнении какого-либо условия, исполнялся другой код. Для этого есть специальное слово `else`. В нем отсутствует условие, и этот оператор срабатывает, когда условие в конструкции `if` ложно. Он ставится после исполняемого когда в `if`, и после него ставится просто двоеточие `:`. Например, можно переписать нашу программу и сделать ее более читаемой:
    ```python
    name = input("Enter your name: ")
    answer = input("Do you want to see greeting message?(yes/no): ")

    positive_answers = ('yes', 'y', 'yep', 'yeah')
    #negative_answers = ('no', 'n', 'nope')

    if answer in positive_answers:
        print("Hello", name, sep=',', end='!')
    else:
        print("OK.")
    ```
    Работать она будет так же, если вводить значения `yes`, 'no'.

- Условия могут быть вложены друг в друга. Например наша программа приветствия будет работать не совсем очевидно, если мы ответим на вопрос не `yes`/`no`, а `maybe`. Для исправления этой проблемы можно написать еще одну условную конструкцию:
    ```python
    name = input("Enter your name: ")
    answer = input("Do you want to see greeting message?(yes/no): ")

    positive_answers = ('yes', 'y', 'yep', 'yeah')
    negative_answers = ('no', 'n', 'nope')

    if answer in positive_answers:
        print("Hello", name, sep=',', end='!')
    else:
        if answer in negative_answers: # вложенная условная конструкция
            print("OK.")
        else:
            print("I don't understand you.")
    ```
    Условия можно улаживать до бесконечности, главное не забывать ставить отступ.

- Если очень вложенных много условий, то код очень быстр может уйти за пределы экрана, для этого в Python введена специальная конструкция `elif` - это совмещение команды `else` и `if`. После нее так же требуется указывать условие исполнение кода. Перепишем наш пример более правильно:
    ```python
    name = input("Enter your name: ")
    answer = input("Do you want to see greeting message?(yes/no): ")

    positive_answers = ('yes', 'y', 'yep', 'yeah')
    negative_answers = ('no', 'n', 'nope')

    if answer in positive_answers:
        print("Hello", name, sep=',', end='!')
    elif answer in negative_answers: # использование оператора elif
        print("OK.")
    else: # и в этом же коде можно использовать сразу else
        print("I don't understand you.")
    ```
    В нашем примере сразу используются команды `if`, `elif` и `else`. Так делать можно.