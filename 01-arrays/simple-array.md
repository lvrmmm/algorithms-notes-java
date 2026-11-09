# Неупорядоченный массив

## Назначение

`SimpleArray` хранит целые числа в порядке добавления. Ёмкость задаётся при создании и не меняется.

## Внутреннее устройство

```java
private final int[] data;
private final int capacity;
private int currentSize;
```

- `data` хранит значения;
- `capacity` задаёт максимальное число элементов;
- `currentSize` хранит логический размер.

Рабочая часть массива занимает диапазон `[0, currentSize)`.

## Реализация

```java
public class SimpleArray {
    private final int[] data;
    private final int capacity;
    private int currentSize;

    public SimpleArray(int capacity) {
        data = new int[capacity];
        this.capacity = capacity;
        currentSize = 0;
    }

    public boolean add(int value) {
        if (currentSize == capacity) {
            return false;
        }

        data[currentSize] = value;
        currentSize++;
        return true;
    }

    public int search(int value) {
        for (int i = 0; i < currentSize; i++) {
            if (data[i] == value) {
                return i;
            }
        }

        return -1;
    }

    public boolean delete(int value) {
        int index = search(value);

        if (index == -1) {
            return false;
        }

        for (int i = index; i < currentSize - 1; i++) {
            data[i] = data[i + 1];
        }

        currentSize--;
        data[currentSize] = 0;
        return true;
    }

    public boolean isEmpty() {
        return currentSize == 0;
    }

    public boolean isFull() {
        return currentSize == capacity;
    }
}
```

Обнуление освободившейся позиции после удаления не требуется для корректности. Оно делает внутреннее состояние удобнее для просмотра.

## Сложность операций

| Операция | Сложность |
|---|---:|
| Добавление | `O(1)` |
| Поиск | `O(n)` |
| Удаление | `O(n)` |
| `isEmpty` | `O(1)` |
| `isFull` | `O(1)` |

## Обнаруженные ошибки

### Поиск по физической ёмкости

Цикл поиска должен завершаться на `currentSize`, а не на `capacity`. Свободные ячейки массива заполнены нулями, поэтому поиск нуля по всей ёмкости может вернуть позицию, которая не является элементом структуры.

### Неправильный индекс при сдвиге

При удалении нужно использовать переменную цикла:

```java
data[i] = data[i + 1];
```

Если постоянно записывать в `data[index]`, остальные элементы не сдвинутся.
