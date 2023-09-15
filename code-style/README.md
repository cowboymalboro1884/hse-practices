# Правила код-ревью

## Общие правила
* Однобуквенные названия переменных в промышленном коде запрещены. Они уместны только в алгоритмах или математических формулах. Индекс i в цикле -- ок.
* Названия переменных -- полные слова, без сокращений. Достаточно точные, но не излишне длинные. Они должны легко читаться.
* Переменные и классы назваются существительными.
* Методы и функции называются глаголами.
* Название булевых переменных должно быть вопросом с ответом да или нет, а точне - с префиксами is_, are_, has_, have_, do_, does_, should_ и т.д. Например: is_weekend, has_active_customers, should_finish.
Иногда префикс можно опустить, например: found_max, needs_spaces.
Плохо называть переменную flag: так можно назвать любую булеву переменную, а значит, это не даёт дополнительной информации.
* Плохо называть что угодно с префиксом my_, например: my_class. Это не даёт никакой дополнительной информации.
* Используйте `this->` внутри класса тогда и только тогда, когда есть коллизии имён.
## Форматирование кода
Соответствует форматированию из открытого `clang-format`-конфига -- [вот он](https://github.com/hse-spb-2023-cpp/all-labs/blob/main/.clang-format).
## Cases
1. Имена классов и структур пишутся в `CamelCase`.
2. Имена функций и методов пишутся в `snake_case`.
3. Имена переменных пишутся в `snake_case`.

## Пример:
// TODO : clang-format
```c++
struct KryakvaTelegramBot {

  KryakvaTelegramBot() = default;
  KryakvaTelegramBot(const std::string& user_name) : m_current_user(std::move(user_name)), available_stickers() {};
  KryakvaTelegramBot(const std::string& user_name, const std::vector<TelegramSticker>& available_stickers) : m_current_user(std::move(user_name)), m_available_stickers(std::move(available_stickers)) {};

  void say_yappy() {
    std::cout << "тяв-тяв\n" << *m_available_stickers.find("Генерал Горо");
  }

  void say_meow() {
    std::cout << "миу-миу\n" << *m_available_stickers.find("Котик");
  }

  const std::string& get_user() {
    return m_current_user;
  }

  void set_new_user(const std::string& new_user) {
    m_current_user = std::move(new_user);
  }

  const std::vector<TelegramStickers>& get_available_stickers() {
    return m_available_stickers;
  }

  void add_new_sticker(const TelegramSticker& new_sticker) {
    m_available_stickers.push_back(std::move(new_sticker));
  }

private:
  std::string m_current_user;
  std::vector<TelegramStickers> m_available_stickers;
}
```
