### Этот код создает DataFrame с двумя столбцами: 'whoAmI' и 'tmp'. Значения в столбце 'whoAmI' представляют собой случайное перемешивание строк 'robot' и 'human'. Затем столбец 'tmp' заполняется значениями 1.

```
lst = ['robot'] * 10
lst += ['human'] * 10
random.shuffle(lst)
data = pd.DataFrame({'whoAmI': lst})
print(data)
data['temp'] = 1
```

### Далее код устанавливает мультииндекс в DataFrame, используя индексы и столбец 'whoAmI'. Затем он преобразует DataFrame в новую форму, используя метод unstack, который преобразует индексы в столбцы. Значения, отсутствующие после такого преобразования, заполняются 0 с помощью параметра fill_value. Код удаляет имя столбцов и выводит измененный DataFrame.
```
data.set_index([data.index, 'whoAmI'], inplace=True)
data = data.unstack(level=-1, fill_value = 0).astype(int)
data.columns = data.columns.droplevel(0)
data.columns.name = None
print(data)
```


###  Итак, в результате будет выведен DataFrame, у которого 'whoAmI' стал именем строки, 'robot' и 'human' стали столбцами, и их значения - количество вхождений каждого значения 'whoAmI'.

## Пример

На входе:
```
0   robot
1   robot
2   human
3   robot
4   robot
5   robot
6   human
7   human
8   human
9   human
10  human
11  human
12  robot
13  robot
14  human
15  robot
16  robot
17  human
18  human
19  robot
```
На выходе:

```
    human  robot
0       0      1
1       0      1
2       1      0
3       0      1
4       0      1
5       0      1
6       1      0
7       1      0
8       1      0
9       1      0
10      1      0
11      1      0
12      0      1
13      0      1
14      1      0
15      0      1
16      0      1
17      1      0
18      1      0
19      0      1
```
