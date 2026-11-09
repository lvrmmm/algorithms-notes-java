# Простые сортировки

В разделе рассматриваются три алгоритма со временем `O(n²)` в худшем случае:

- пузырьковая сортировка;
- сортировка выбором;
- сортировка вставками.

Все три алгоритма сортируют массив на месте и используют `O(1)` дополнительной памяти.

## Сравнение

| Алгоритм | Лучший случай | Худший случай | Устойчивость | Особенность |
|---|---:|---:|---|---|
| Пузырьковая | `O(n)` с ранним выходом | `O(n²)` | Да | Много обменов |
| Выбором | `O(n²)` | `O(n²)` | Обычно нет | Мало обменов |
| Вставками | `O(n)` | `O(n²)` | Да | Хороша для почти отсортированных данных |

## Общая реализация

```java
public class Sortings {
    public static void bubbleSort(int[] array) {
        for (int i = 0; i < array.length - 1; i++) {
            boolean swapped = false;

            for (int j = 0; j < array.length - i - 1; j++) {
                if (array[j] > array[j + 1]) {
                    int temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
                    swapped = true;
                }
            }

            if (!swapped) {
                return;
            }
        }
    }

    public static void selectionSort(int[] array) {
        for (int out = 0; out < array.length - 1; out++) {
            int minIndex = out;

            for (int in = out + 1; in < array.length; in++) {
                if (array[in] < array[minIndex]) {
                    minIndex = in;
                }
            }

            if (minIndex != out) {
                int temp = array[out];
                array[out] = array[minIndex];
                array[minIndex] = temp;
            }
        }
    }

    public static void insertionSort(int[] array) {
        for (int out = 1; out < array.length; out++) {
            int value = array[out];
            int in = out;

            while (in > 0 && array[in - 1] > value) {
                array[in] = array[in - 1];
                in--;
            }

            array[in] = value;
        }
    }
}
```

## Практика

- [1051. Height Checker](problems/1051-height-checker.md) — одна задача, решённая тремя сортировками.
