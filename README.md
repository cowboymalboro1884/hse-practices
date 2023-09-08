# Гайд по написанию лабораторных работ 
> ревизия от 08.09.2023

## Содержание
1. Введение 
1. Инструкция по сдаче лабораторных работ
    1. Начало работы
    1. Локальное тестирование
        1. Компиляция 
        1. clang-format
        1. cppcheck
        1. clang-tidy
        1. Открытые тесты
    1. Как загрузить лабу
        1. В какую ветку загружать
        1. Какие кнопочки нажимать, чтобы загрузить
        1. Требования к Pull Request
 1. Общие советы
---


## Введение
В течение годового курса по C++ вам предстоит делать лабораторные работы на отработку пройденного на лекциях материала. Получать и сдавать домашние задания вы будете через Github.

### Про вопросы
__Можно и нужно__ обсуждать друг с другом, преподавателями и кем угодно:
- Содержимое лекций
- Не связанные с домашкой куски кода, вроде "нет ли UB в этой программе?" или "за сколько работает vector::push_back в каких случаях?"
- Настройку среды разработки, запуск компиляторов, отладчиков, и анализаторов
- Вопросы на StackOverflow
- Чисто алгоритмическую часть заданий по C++, вообще не зависящую от языка программирования, вроде "какую структуру данных надо использовать, чтобы работало за линию вместо квадрата"

__Следует__ спрашивать напрямую у своего практика (лектора, проверяющего — если практик недоступен), чтобы получить надёжную информацию:
- Вопросы по условию
- Подсказки

### Цикл сдачи лабораторных работ
У каждого из вас есть личный репозиторий `labs-<github-username>`, работать Вы будете исключительно с ним. Для каждой выданной лабораторной работы в нём есть отдельная ветка (например, `lab00-demo`), в которую вы загружаете Ваше решение. По мере выдачи новых домашек в вашем личном репозитории будут появляться новые ветки.

Сдача домашнего задания происходит итеративно (в среднем 2-3 итерации), цикл выглядит следующим образом:
- написание и локальное тестирование Вашего решения
- корректное оформление Pull Request с прохождением всех открытых автопроверок и "ОК" от бота
- проверяющий делает код-ревью Вашего Pull Request'а, выставляет баллы за стиль и корректность
- внимательное чтение замечаний и осознание того, что нужно исправить

## Инструкция по сдаче лабораторных работ
__ВАЖНО__: прочитайте гайд полностью перед тем как загружать домашнее задание.
### Начало работы
Для начала нужно скачать ваш репозиторий с лабораторной работой. Рассмотрим на примере `lab00-demo`.

![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/764de8dd-d127-4cb7-89f1-4452ea294317)

В условии каждой лабы четко прописано, в каких файлах должно находиться ваше решение. __Нельзя__ переименовывать, удалять или создавать новые файлы.

Для `lab00-demo` это `overview.cpp`.

## Локальное тестирование
И вот вы написали какой-то код в `overview.cpp` и по готовности лабораторной работы изменили `tests.txt`.

### clang-format
Для успешного прохождения тестов для лабораторных работ
необходимо чтобы код был корректно отформатирован.
Например, есть вот такой код(по мотивам `overview.cpp`):

```c++
int main() {
  int case_number = 0;
  while (true) {
    std::cin >> case_number;
    switch (case_number) {
    case -1:
      return 0;
    case 1: {
      int a = 0;
      int b = 0;
      std::cin >> a >> b;
      std::cout << a + b << std::endl;
      break;
    }
    default:
      std::cout << "Undefined case number!\n";
    }
  }
}
```
Чтобы его отформатировать следует зайти в
терминал и прописать команду.

```
clang-format-15 -i путь-до-файла
```
Результат форматирования:
```c++
int main() {
    int case_number = 0;
    while (true) {
        std::cin >> case_number;
        switch (case_number) {
            case -1:
                return 0;
            case 1: {
                int a = 0;
                int b = 0;
                std::cin >> a >> b;
                std::cout << a + b << std::endl;
                break;
            }
            default:
                std::cout << "Undefined case number!\n";
        }
    }
}
```

Так же мы можем форматировать несколько файлов командой

```
clang-format-15 -i путь-до-файла1 путь-до-файла2 путь-до-файла3
```

-i - это флаг, который означает, что
код отформатируется и запишется в тот же файл.

Если бы этого флага не было, то результат форматирования
вывелся бы в терминал.

Clang-format имеет разные настройки форматирования.
Эти настройки можно написать в файле
под названием .clang-format. Если запустить clang-format
в этой же директории, то код отформатируется
в соответствии с этими настройками.
В репозитории labs-ник_на_github есть файл .clang-format.

![](clang-format-file-in-repository.png)

### clang-tidy

clang-tidy - это средство анализа кода, помогает замечать логические ошибки и писать более оптимальный код. 

Запускается следующей командой:
`clang-tidy имя-файла`

Аналогично, `clang-tidy` имеет разные настройки форматирования.
Если запустить clang-tidy в директории с лабораторной работой, то код отформатируется
в соответствии с необходимыми настройками.
В репозитории `labs-ник_на_github` есть файл `.clang-tidy`.

### cppcheck
cppcheck - это статический анализатор, нужный для выявления ошибок, на которые компиляторы не обращают внимания, 
таких как ошибка в логическом выражении в условном операторе ветвления (if) и использование shadows и unusable variable

Команда для запуска (в консоли):
```
cppcheck --language=c++ -DSOME_DEFINE_TO_FIX_CONFIG --enable=all --error-exitcode=1 --inline-suppr путь-до-файла
```

Заметим, что путь до файла можно заменить названием файла, если запускать cppcheck из директории с этим файлом.

Так же можно проверить несколько файлов, если заменить название файла на *.cpp (или другое расширение) 

### Компиляция и тесты
Как правило, к лабораторной работе прилагается набор открытых тестов. Для их прохождения сначала необходимо скомпилировать программу.

Компиляция - преобразование всех *.cpp файлов в один исполняемый бинарный .exe файл 

Перед прочтением этой главы у вас должны быть установлены хотя бы два компилятора.

Чтобы проверить, что всё установлено нормально запустите:

* `g++ --version` или `g++-12 –v` - чтобы проверить g++

* `clang++ -v` или `clang++-15 -v` - чтобы проверить clang++
  *если версии без суффикса одинаковые, можно его не приписывать*

Шаблон команды выглядит таким образом:

`g++-12|clang++-15 path/to/source.cpp -std=c++17 -Wall -Wextra -Werror -o path/to/output_executable `

*Расшифровка:*

`g++-12|clang++-15` -- выбираем одним из двух компиляторов

`path/to/source.cpp` -- путь до каждой единицы трансляции (компилятору можно передать через пробел каждый `*.cpp` файл, который нужно скомпилировать)

`-std=c++98|c++11|c++14|c++17|c++20` -- выбираем стандарт C++, с которым хотим скомпилировать

`-Wall -Wextra -Werror` -- включаем предупреждения компилятора и говорим ему трактовать предупреждения, как ошибки

`-o path/to/output_executable` -- флаг `-o` (от слова output) позволяет указать, куда положить результат компиляции (по умолчанию создаётся `.out`)  
 
Теперь скомпилируем `overview.cpp` следующей командой:

`g++-12 overview.cpp -std=c++17 -Wall -Wextra -Werror  -o result` 

![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/faa3e6a7-0a3a-40e1-9c3e-5995341d1fb7)

Пропишем `ls` и убедимся, что появился `res`

![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/149d0cc1-ee36-47b2-84be-726b7bfbe072)

Запустить скомпилированную программу можно командой `./path/to/exe`

![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/9e307410-4c04-4508-a1e8-8bf9672f6f7d)

Теперь можем протестировать программу.
Тесты можно запустить командой:
`bash /path/to/run-test-data.sh ./path/to/exe`

![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/d7157e70-02d0-46d2-b338-0645272cf0fd)


## Как загрузить лабу

#### Теперь, когда мы протестировали, отформатировали программу, прошли проверки cppcheck и clang-tidy, можем загружать наше решение на GitHub.

### Открываем ваш репозиторий на github и меняем ветку с main на ветку соответствующей лабы (например, lab00-demo) (очень важный момент). 
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/2cd380b4-13ac-4708-9d6a-2843814459dd)
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/ddef8f22-f375-4795-affd-a9980b887c23)

__Убедитесь, что__ находитесь в ветке lab00-demo, сверху слева написано название ветки в которой вы находитесь. После этого, заходим в lab00-demo/solution/tests.txt и оставляем только те подзадачи, которые уже выполнили. 
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/0fa52ae7-5f83-49db-81aa-8582ca88895e)
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/9e84ff9f-4ac9-4321-b6a4-f81b076271a8)
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/42fd05dc-7321-4b74-9d66-0a02384d825a)

Теперь можем изменить файл `overview.cpp`. Ещё раз __внимательно смотрим__, что находимся в __нужной__ ветке (сейчас для нас это -- `lab00-demo`)
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/e298dc6b-bb4b-4447-8df2-0306dbf8252b)
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/df9fc353-b353-4b68-8672-34689062369a)

__Смотрим в какой ветке мы находимся__, должны быть в lab00-demo. После вставки своего кода, жмем commit changes.
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/b56052a1-eeaa-46c8-ade7-22cc969db427)

После этого, должно появиться окно в главном окне вашего репозитория,  которое предлагает создать pull request. Жмем на Compare & pull request.
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/ea355ba7-5cd1-488f-94b6-ff52b2774d46)

Меняем название pull request на ваше имя и вашу лабораторную работу. Вводите имя и название лабораторной аккуратно, пробелы важны. После этого жмем на кнопку Create pull request.
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/3bf618f7-3a3e-471f-82d6-f02a8338bd04)

После этого появится окно. Здесь оно показывает, что некоторые тесты не были пройдены.
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/5282f9cc-ead3-4d07-8c51-b047b27013fb)

Заходим в Pull Requests и видим там свой Pull Request, заходим туда и смотрим какие тесты пройдены. Исправляем, изменяем файлы ещё раз.
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/56d3caa6-1742-49b2-bf68-5368468b566d)

Если горит зеленая галочка - то все ок, мы сдали подзадачу лабораторной работы.
Вас может привлечь огромная зелёная кнопка `Squash and merge` -- её __нельзя__ нажимать. Оставьте всё, как есть.
![image](https://github.com/cowboymalboro1884/hse-practices/assets/112244451/5ee72c9e-597e-4e46-b435-aa7ff8b3bede)

## Советы
* если в чем-то не уверены -- пишите практику\флудилку. Вам __очень__ хотят помочь и __очень__ не хотят возиться с возможными последствиями Ваших ошибок, так что дешевле -- переспросить.
* каждый раз смотрите, в какой ветке вы находитесь -- в __main коммитить нельзя__.

## Материалы
* о том, что такое git можно почитать [тут](https://docs.github.com/ru/get-started/using-git/about-git) (официальная дока) и [тут](https://habr.com/ru/articles/588801/) (статья на хабре)
* ещё какие-нибудь материалы
* если очень хочется продвинуться в гите -- [обучалка](https://learngitbranching.js.org/?locale=ru_RU)
