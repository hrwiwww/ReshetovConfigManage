## 3 практическая конфигурационное управление икбо-52-23 Решетов К.С
Разобраться, что собой представляют программируемые конфигурационные языки (Jsonnet, Dhall, CUE).
## Задача 1
Реализовать на Jsonnet приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.<br>
```
local groups = [
  "ИКБО-1-24",
  "ИКБО-2-24",
  "ИКБО-3-24",
  "ИКБО-4-24",
  "ИКБО-5-24",
  "ИКБО-6-24",
  "ИКБО-7-24",
  "ИКБО-8-24",
  "ИКБО-9-24",
  "ИКБО-10-24",
  "ИКБО-11-24",
  "ИКБО-12-24",
  "ИКБО-13-24",
  "ИКБО-14-24",
  "ИКБО-15-24",
  "ИКБО-16-24",
  "ИКБО-17-24",
  "ИКБО-18-24",
  "ИКБО-19-24",
  "ИКБО-20-24",
  "ИКБО-21-24",
  "ИКБО-22-24",
  "ИКБО-23-24",
  "ИКБО-24-24"
];

local student(name, age, group, subject) = {
  name: name,
  age: age,
  group: group,
  subject: subject,
};

local students = [
  student("Иванов И.И.", 19, "ИКБО-4-24", "Конфигурационное управление"),
  student("Петров П.П.", 18, "ИКБО-5-24", "Конфигурационное управление"),
  student("Сидоров С.С.", 18, "ИКБО-5-24", "Конфигурационное управление"),
  student("Решетов К.С.", 19, "ИКБО-52-23", "Конфигурационное управление")
];

{
  groups: groups,
  students: students,
}
```
Установим Jsonnet на свой компьютер с помощью терминала:<br>
```
brew install jsonnet
```
Далее создадим файл prkt3.jsonnet, в который добавим приведенный в дано код, и скомпилируем файл в JSON, выполнив:<br>
```
jsonnet prktr3.jsonnet -o prktr3_1zd.json
```
Просмотреть содержимое файла JSON можно с помощью команды cat:<br>
```
cat prktr3_1zd.json
```
Результат:<br>

![2](https://github.com/user-attachments/assets/95305d41-8cf6-48c4-829e-d5149acb73c2)



# Задача 2
Реализовать на Dhall приведенный выше пример в формате JSON. Использовать в реализации свойство программируемости и принцип Dry<br>

Установим Dhall нас свой компьютер с помощью терминала:<br>
```
brew install dhall-json
```
Далее создадим файл prktr3.dhall, в который добавим код пример, и скомпилируем файл в JSON, выполнив:<br>
```
dhall-to-json --file prktr3.dhall > Pr3_2zd.json
```
Просмотреть содержимое файла JSON можно с помощью команды cat:<br>
```
cat prktr3_2zd.json
```
Результат:<br>

![3](https://github.com/user-attachments/assets/4f484270-e76f-4dd8-a53d-9ed5f2aa69d4)


# Задача 3
Для решения дальнейших задач потребуется программа на Питоне, представленная в методичке к 3 практической работе. Разбираться в самом языке Питон при этом необязательно.<br>
Реализовать грамматики, описывающие следующие языки (для каждого решения привести БНФ). Код решения должен содержаться в переменной BNF:<br>

Язык нулей и единиц.<br>
10<br>
100<br>
11<br>
101101<br>
000<br>
<br>

Создадим файл pktr3_3zd.python и оформим в нем решение 3 задачи:<br>
```
import random

def parse_bnf(text):
    grammar = {}
    rules = [line.split('=') for line in text.strip().split('\n')]
    for name, body in rules:
        grammar[name.strip()] = [alt.split() for alt in body.split('|')]
    return grammar

def generate_phrase(grammar, start):
    if start in grammar:
        seq = random.choice(grammar[start])
        return ''.join(generate_phrase(grammar, name) for name in seq)
    return str(start)

BNF = """
E = "0" E | "1" E | ""
"""

for i in range(10):
    phrase = generate_phrase(parse_bnf(BNF), 'E')
    if phrase:
        print(phrase.replace('"', ''))
```
В результате при запуске выполнения файла получим:<br>

![3](https://github.com/user-attachments/assets/906b4e1b-3f39-4820-bf6e-eb64cca5b4fc)


# Задача 4
Язык правильно расставленных скобок двух видов.<br>
(({((()))}))<br>
{}<br>
{()}<br>
()<br>
{}<br>

```
import random

def parse_bnf(text):
    grammar = {}
    rules = [line.split('=') for line in text.strip().split('\n')]
    for name, body in rules:
        grammar[name.strip()] = [alt.split() for alt in body.split('|')]
    return grammar

def generate_phrase(grammar, start, max_depth=10, current_depth=0):
    if current_depth > max_depth:
        return ""
    if start in grammar:
        seq = random.choice(grammar[start])
        return ''.join(generate_phrase(grammar, name, max_depth, current_depth + 1) for name in seq)
    return str(start)

BNF = """
E = P E | F E | P | F 
P = "(" P ")" | "(" ")" 
F = "{" F "}" | "{}"
"""

for i in range(10):
    phrase = generate_phrase(parse_bnf(BNF), 'E')
    if phrase:
        print(phrase.replace('"', ''))
```

Часть результата вывода программы:<br>

![4](https://github.com/user-attachments/assets/dde71f6e-40b8-46ee-ba41-a49548569fa3)


# Задача 5
Язык выражений алгебры логики.<br>
((~(y & x)) | (y) & ~x | ~x) & x <br>
у & ~ (у) <br>
(~(y) & y & ~y) <br>
~x <br>
~((x) & y | (y) | (x)) & x | x | (y & ~y) <br>

```
import random

def parse_bnf(text):
    grammar = {}
    rules = [line.split('=') for line in text.strip().split('\n')]
    for name, body in rules:
        grammar[name.strip()] = [alt.split() for alt in body.split('|')]
    return grammar

def generate_phrase(grammar, start, max_depth=10, current_depth=0):
    if current_depth > max_depth:
        return ""
    if start in grammar:
        seq = random.choice(grammar[start])
        return ''.join(generate_phrase(grammar, name, max_depth, current_depth + 1) for name in seq)
    return str(start)

BNF = '''
E = ( E B F ) | U ( E ) | F
F = P B P | U P | P
P = x | y | (x) | (y)
U = ~
B = & | V
'''

def format_phrase(phrase):
    output = []
    prev_char = None
    open_count = 0

    for char in phrase:
        if char in ['x', 'y']:
            if prev_char in ['x', 'y']:
                continue
            output.append(char)
        elif char in ['&', '|']:
            if len(output) < 2 or output[-1] in ['&', '|'] or (prev_char in ['(', ')']):
                continue
            output.append(char)
        elif char == '(':
            if prev_char == '(':
                continue
            output.append(char)
            open_count += 1
        elif char == ')':
            if output and output[-1] == '(':
                output.pop()
                open_count -= 1
                continue
            if open_count > 0:
                output.append(char)
                open_count -= 1

        prev_char = char

    output = [c for c in output if not (c == '(' and (prev_char == '(' or (len(output) > 1 and output[-2] == '(')))]

    return ''.join(output)

for i in range(10):
    phrase = generate_phrase(parse_bnf(BNF), 'E')
    if phrase:
        formatted_phrase = format_phrase(phrase)
        if formatted_phrase:
            print(formatted_phrase.replace('"', ''))
```

Часть результата вывода программы:<br>

![5](https://github.com/user-attachments/assets/ef76c129-1a60-4a2b-97a6-ab1aeb559535)


# Полезные ссылки

[Configuration complexity clock<br>](https://mikehadlow.blogspot.com/2012/05/configuration-complexity-clock.html)<br>
[Json<br>](https://www.json.org/json-ru.html)<br>
[Язык Jsonnet<br>](https://jsonnet.org/learning/tutorial.html)<br>
[Язык Dhall<br>](https://dhall-lang.org/)<br>
[Учебник в котором темы построения синтаксических анализаторов (БНФ, Lex/Yacc)
изложены подробно<br>](https://ita.sibsutis.ru/sites/csc.sibsutis.ru/files/courses/trans/LanguagesAndTranslationMethods.pdf)<br>
[Полезные материалы для разработчика (очень рекомендую посмотреть слайды и прочие ссылки, все это актуально и для других тем нашего курса)<br>](https://habr.com/ru/company/JetBrains-education/blog/547768/)
