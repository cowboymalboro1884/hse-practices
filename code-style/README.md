# Правила код-ревью

## Общие правила
* В именах должны использоваться только английские слова. Транслитерации русских слов не допускаются.
Например, имя функции `f` является недопустимым. Имена функций `calculate_square_root` и `calc_sqrt` допустимы, но последнее предпочтительнее, так как короче и использует общепринятые сокращения. Имя функции `vychislenie_kornya` недопустимо, так как использует русские слова.
* Имена констант записываются полностью заглавными буквами. Если имя константы состоит из нескольких слов, для их разделения используются подчеркивания. Например, `RED`, `POLL_INTERVAL`.
* Имена не должны вызывать визуальные затруднения при прочтении. Например, переменная с именем `l` или константа с именем `I` недопустимы, так как могут быть спутаны с числом 1. То же правило применимо к константе O.
* Однобуквенные названия переменных в промышленном коде запрещены. Они уместны только в алгоритмах или математических формулах. Индекс `i` в цикле -- ок (но если массив n-мерный, то лучше использовать `row`,`column` или `dx`, `dy` etc.
* Названия переменных -- полные слова, без сокращений. Достаточно точные, но не излишне длинные. Они должны легко читаться.
* Переменные и классы назваются существительными.
* Методы и функции называются глаголами.
* Название булевых переменных должно быть вопросом с ответом да или нет, а точне - с префиксами `is_`, `are_`, `has_`, `have_`, `do_`, `does_`, `should_` и т.д. Например: `is_weekend`, `has_active_customers`, `should_finish`.
Иногда префикс можно опустить, например: `found_max`, `needs_spaces`.
Плохо называть переменную `flag`: так можно назвать любую булеву переменную, а значит, это не даёт дополнительной информации.
* Плохо называть что угодно с префиксом `my_`, например: `my_class`. Это не даёт никакой дополнительной информации.
* Используйте `this->` внутри класса тогда и только тогда, когда есть коллизии имён.
## Форматирование кода
Соответствует форматированию из открытого `clang-format`-конфига -- [вот он](https://github.com/hse-spb-2023-cpp/all-labs/blob/main/.clang-format).
## Cases
1. Имена классов и структур пишутся в `CamelCase`.
```c++
struct GoodStruct {
    int field1;
    char* field2;
}
```
3. Имена функций и методов пишутся в `snake_case`.
```c++
void print_vector_int(const std::vector<int>& vector_to_print) {
    for(int elem : vector_to_print) {
        std::cout << elem << ' ';
    }
    std::cout << std::endl;
}
```
5. Имена переменных пишутся в `snake_case`.
```c++
int ref_counter;
std::string new_username;
bool is_door_open;
```
