FAQ
---

  - Почему отсутствует поддержка градусов цельсия и фаренгейта?

    В отличие от единицы измерения температуры в системе СИ, [Kelvin](https://en.wikipedia.org/wiki/Kelvin),
    и в отличие всех остальных, цельсий и фаренгейт требуют специфическое преобразование в дргугие единицы
    измерения температуры. Это специфическое преобразование ведет к неясности значений.
    К примеру сложение двух значений температур цельсия будет иметь значение только если одно
    из них имеет специфическое преобразование (а не как абсолютное значение).
    
    хоть и *°C* и *°F* это не встроенные единицы измерения, все же есть вспомогательные функции
    для их преобразований:

      - `fromCelsius` от цельсия к кельвину:

        ```
        > fromCelsius(0)

           = 273.15 K

        > k_B * fromCelsius(23) to meV

           = 25.5202 meV
        ```

      - `toCelsius` От кельвина к цельсию:

        ```
        > toCelsius(70 K)

           = -203.15

        > toCelsius(25 meV / k_B)

           = 16.963
        ```

  - Почему `1/2 x` представлен как `1/(2x)`?

    Не явное умножение имеет приоритет больше деления
    (см. [operator precedence rules](#reference)). это позволяет соблюдать правильность входных данных, папример:
    `50 cm / 2 m` как `(50 cm) / (2 m)`. В остальных случаях используйте явное умножение *½ · x*, write `1/2 * x`.

  - Точность вычислений.

    Insect Показывает 6 точных цифр после запятой. но,
    Внутренняя логика точнее (30 точных цифр после запятой).

  - Оператор преобразования

    Оператор преобразования `->` преобразовывает значение (в левой части)
    в единицу измерения указанную в правой части выражения (в правой части может быть произвольное выражение).
    Пример:

    ```
    # Простое преобразование:
    > 120 km/h -> mph

      = 74.5645 mi/h

    # Выражение на правой стороне:
    > 120 m^3 -> km * m^2

      = 0.12 m²·km

    # Преобразование x2 к единице измерения x1:
    > x1 = 50 km / h
    > x2 = 3 m/s -> x1

      x2 = 10.8 km/h
    ```

  - What is the relation between the units `RPM`, `rad/s`, `deg/s` and `Hz`?

    The unit [`RPM`](https://en.wikipedia.org/wiki/Revolutions_per_minute) (revolutions per
    minute) is defined via `1 RPM = 1 / minute` where the `1` on the right hand side symbolizes
    "1 revolution".

    As the base unit is the same (`1 / second`), `RPM` can be converted to `rad / s`, `deg / s` or
    `Hz`. Note, however, that `1 RPM` does *not* equal `2π rad / min` or `360° / min` or `1 Hz`, as
    some might expect. If you're interested in computing the traversed angle of something that
    rotates with a given number of revolutions per minute, you need to multiply by `2π rad` or
    `360°` because:
    ```
    1 RPM · (360°/revolution) = (1 revolution / minute) · (360° / revolution) = 360° / minute
    ```
