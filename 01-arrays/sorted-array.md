# Отсортированный массив

## Назначение

`SortedArray` хранит целые числа в неубывающем порядке. Сортировка позволяет использовать бинарный поиск.

## Инварианты

- Рабочая часть занимает диапазон `[0, currentSize)`.
- Значения в рабочей части расположены в неубывающем порядке.
- `currentSize` находится между нулём и ёмкостью массива.

## Реализация

В этой версии `add` вставляет новое значение после уже существующих равных значений, а `delete` удаляет все вхождения указанного значения.

```java
public class SortedArray {
    private final int[] data;
    private final int capacity;
    private int currentSize;

    public SortedArray(int capacity) {
        data = new int[capacity];
        this.capacity = capacity;
        currentSize = 0;
    }

    public boolean isEmpty() {
        return currentSize == 0;
    }

    public boolean isFull() {
        return currentSize == capacity;
    }

    public int search(int value) {
        int left = 0;
        int right = currentSize - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (data[mid] == value) {
                return mid;
            } else if (data[mid] > value) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return -1;
    }

    public boolean add(int value) {
        if (currentSize == capacity) {
            return false;
        }

        int left = 0;
        int right = currentSize - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (data[mid] <= value) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        for (int i = currentSize; i > left; i--) {
            data[i] = data[i - 1];
        }

        data[left] = value;
        currentSize++;
        return true;
    }

    public boolean delete(int value) {
        int first = findFirst(value);

        if (first == -1) {
            return false;
        }

        int last = findLast(value);
        int count = last - first + 1;
        int oldSize = currentSize;

        for (int i = first; i + count < oldSize; i++) {
            data[i] = data[i + count];
        }

        currentSize -= count;

        for (int i = currentSize; i < oldSize; i++) {
            data[i] = 0;
        }

        return true;
    }

    private int findFirst(int value) {
        int answer = -1;
        int left = 0;
        int right = currentSize - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (data[mid] == value) {
                answer = mid;
                right = mid - 1;
            } else if (data[mid] < value) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return answer;
    }

    private int findLast(int value) {
        int answer = -1;
        int left = 0;
        int right = currentSize - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (data[mid] == value) {
                answer = mid;
                left = mid + 1;
            } else if (data[mid] < value) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return answer;
    }
}
```

## Сложность операций

| Операция | Сложность | Причина |
|---|---:|---|
| Поиск | `O(log n)` | Бинарный поиск |
| Добавление | `O(n)` | Сдвиг элементов вправо |
| Удаление | `O(n)` | Сдвиг элементов влево |
| Проверки состояния | `O(1)` | Сравнение полей |

## Важные выводы

Позиция вставки находится за `O(log n)`, но до `n` элементов приходится сдвинуть. Поэтому вся вставка выполняется за `O(n)`.

Количество элементов между первой и последней позицией включительно вычисляется так:

```java
int count = last - first + 1;
```

Бинарный поиск должен использовать `currentSize - 1` как правую границу. Свободная часть физического массива не участвует в операциях структуры.
