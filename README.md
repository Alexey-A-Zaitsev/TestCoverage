# Домашнее задание к занятию «Выстраивание процесса непрерывной интеграции»

# Задание 1. Синдром 100% (обязательное к выполнению)

Вы попали в команду максималистов, которые хотят, чтобы те автотесты, которые вы пишете, покрывали код на 100%.

Но вот незадача:
* непонятно, что такое 100%;
* непонятно, как это сделать.

Вспоминаем: покрытием кода у нас занимается JaCoCo, но он просто сигнализирует о том, что конкретно пошло не так.

Большинство подобных плагинов, помимо целей отчётности (`report`), содержат ещё цель `check`, которая обрушает сборку, если не выполнены определённые проверки.

Что вам нужно
1. Создать Мавен-проект с тестируемым кодом из листинга кода, он указан ниже по условию.
1. Изучить [документацию на плагин](https://www.eclemma.org/jacoco/trunk/doc/maven.html), а конкретно — на цель `check`.
1. Внедрить эту цель во фазу `verify`. Обратите внимание, что эта цель и так публикуется в эту фазу.
1. Настроить правила по покрытию на 100%. При этом нужно изучить разницу между счётчиками `INSTRUCTION`, `LINE`, `BRANCH`, `COMPLEXITY`.
1. Вникнуть в тестируемый код.
1. Выбрать один из счётчиков и добиться 100% покрытия через добавление новых тестов.

**Важно**: использовать можно только один из следующих: 
1. `INSTRUCTION`
1. `LINE`
1. `BRANCH`

Обратите внимание на чеклист в начале условия, он содержит подсказки по внедрению JaCoCo в ваш Мавен-проект.

Тестируемый код, его как-либо редактировать **нельзя**:
```java
package ru.netology.statistic;

public class StatisticsService {
  /**
   * Calculate index of max income
   *
   * @param incomes - array of incomes
   * @return - index of first max value
   */
  public long findMax(long[] incomes) {
    long current_max_index = 0;
    long current_max = incomes[0];
    for (long income : incomes)
      if (current_max < income)
        current_max = income;
        return current_max;
  }
}
```

Класс с тестами, его надо будет расширить новыми тестами:
```java
package ru.netology.statistic;

import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.*;

public class StatisticsServiceTest {

  @Test
  void findMax() {
    StatisticsService service = new StatisticsService();

    long[] incomesInBillions = {12, 5, 8, 4, 5, 3, 8, 6, 11, 11, 12};
    long expected = 12;

    long actual = service.findMax(incomesInBillions);

    assertEquals(expected, actual);
  }
}
```

Итого: отправьте на проверку ссылку на репозиторий GitHub с вашим проектом.

# Задание 2*. Пусть плагин ищет баги (необязательная задача)

[SpotBugs](https://spotbugs.github.io) и [Maven Plugin для него](https://spotbugs.readthedocs.io/en/latest/maven.html) предоставляют возможность производить статический анализ, то есть анализ кода без его запуска, для выявления наиболее часто встречающихся багов.

[Список багов, которые ищет SpotBugs](https://spotbugs.readthedocs.io/en/latest/bugDescriptions.html).

Ваша задача
1. Подключить плагин к вашему проекту. Возьмите проект из первой задачи или создайте новый на его базе.
1. Настроить goal `check` в фазу `verify`.
1. Удостовериться, что код проходит проверки SpotBugs, если не проходит, то пофиксить.
1. Сделать push в GitHub и удостовериться, что сборка проходит.
