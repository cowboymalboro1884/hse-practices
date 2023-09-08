# Гайд по написанию лабораторных работ 
> ревизия от 01.09.2023

## Содержание
1. Введение (личная репа с лабами, цикл отправки лаб {пулл реквест, тесты, код ревью, исправления}, ссылка на CSC Wiki)
1. Инструкция по сдаче лабораторных работ (пока предполагается, что окружение уже настроено)
    1. TODO: Начало работы (как скачать zip папочку, куда писать код, всякие запреты и условия)
    1. Локальное тестирование
        1. Компиляция (какие флаги, требование zero-warning под *всеми* компиляторами)
        1. clang-format
        1. TODO: cppcheck
        1. TODO: clang-tidy
        1. TODO: Открытые тесты
        1. если все предыдущие пункты норм -- переходим к следующему
    1. Как загрузить лабу
        1. В какую ветку загружать
        1. Какие кнопочки нажимать, чтобы загрузить
        1. Требования к Pull Request (из какой ветки в какую, автопроверки на сервере, требования к названию PR, аппрув от бота)
        1. 
    1. Общие советы
1. TODO: Частозадаваемые вопросы
    1. Кому писать если:
        1. не получается подступиться к домашке
        1. что-то отвалилось (склоненный репозиторий, не работают анализаторы\компиляторы)
        1. есть вопросы по языку или по стилю кода
        1. не уверен, что загрузил работу корректно 
    1. Что делать, если запушил не туда? (в main в частности)
    1. ...? 
1. Материалы (ссылки на чаты, людей; ссылки на доки гитхаба; хабр статьи; что угодно, что имеет отношение к лабам и плюсам)

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
У каждого из вас есть личный репозиторий ‘labs-<github-username>’, работать Вы будете исключительно с ним. Для каждой выданной лабораторной работы в нём есть отдельная ветка (например, lab00-entry), в которую вы загружаете Ваше решение. По мере выдачи новых домашек в вашем личном репозитории будут появляться новые ветки.

Сдача домашнего задания происходит итеративно (в среднем 2-3 итерации), цикл выглядит следующим образом:
- написание и локальное тестирование Вашего решения
- корректное оформление Pull Request с прохождением всех открытых автопроверок и "ОК" от бота
- проверяющий делает код-ревью Вашего Pull Request'а, выставляет баллы за стиль и корректность
- внимательное чтение замечаний и осознание того, что нужно исправить

## Инструкция по сдаче лабораторных работ
__ВАЖНО__: прочитайте гайд полностью перед тем как загружать домашнее задание.
### Начало работы
Для начала нужно скачать ваш репозиторий с лабораторной работой. Рассмотрим на примере `lab00-demo`.

// скриншот

В условии каждой лабы четко прописано, в каких файлах должно находиться ваше решение. __Нельзя__ переименовывать, удалять или создавать новые файлы.

Для `lab00-demo` это `overview.cpp`.

## Локальное тестирование
И вот вы написали какой-то код в `overview.cpp`.
### Компиляция
Компиляция - преобразование всех *.cpp файлов в один исполняемый бинарный .exe файл 

Перед прочтением этой главы у вас должны быть установлены хотя бы два компилятора.

Чтобы проверить, что всё установлено нормально запустите:

* `g++ --version` или `g++-12 –v` - чтобы проверить g++

* `clang++ -v` или `clang++-15 -v` - чтобы проверить clang++
  *если версии без суффикса одинаковые, можно его не приписывать*

#### Компиляция из консоли

Шаблон команды выглядит таким образом:

`g++-12|clang++-15 path/to/source.cpp -std=c++17 -Wall -Wextra -Werror -o path/to/output_executable `

Расшифровка:

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
clang-format -i путь-до-файла
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
clang-format -i путь-до-файла1 путь-до-файла2 путь-до-файла3
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

Там прописаны настройки clang-format, которые потребуются для успешной сдачи лабораторных работ.
Необходимые вам настройки clang-format (содержание файла .clang-format):
```
BasedOnStyle: Chromium
IndentWidth: 4
AccessModifierOffset: -4
PointerAlignment: Right
IncludeBlocks: Merge
AllowShortBlocksOnASingleLine: false
AllowShortFunctionsOnASingleLine: false
AllowShortIfStatementsOnASingleLine: false
AllowShortLoopsOnASingleLine: false

# Only from clang-format 14.0.0
AlignAfterOpenBracket: BlockIndent
QualifierAlignment: Left
SeparateDefinitionBlocks: Always
EmptyLineAfterAccessModifier: Never
```

## Материалы
* о том, что такое git можно почитать [тут](https://docs.github.com/ru/get-started/using-git/about-git) (официальная дока) и [тут](https://habr.com/ru/articles/588801/) (статья на хабре)
* ещё какие-нибудь материалы
* если очень хочется продвинуться в гите -- [обучалка](https://learngitbranching.js.org/?locale=ru_RU)
