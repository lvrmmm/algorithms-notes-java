# 69. Sqrt(x)

- Сложность: Easy
- Темы: математика, бинарный поиск
- Ссылка: https://leetcode.com/problems/sqrtx/

## Условие

Нужно вернуть целую часть квадратного корня неотрицательного числа `x`, не используя встроенную операцию извлечения корня.

## Решение

```java
class Solution {
    public int mySqrt(int x) {
        if (x < 2) {
            return x;
        }

        int low = 1;
        int high = x / 2;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            long square = (long) mid * mid;

            if (square == x) {
                return mid;
            } else if (square > x) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return high;
    }
}
```

После завершения `low` указывает на первое число, квадрат которого больше `x`, а `high` — на последнее число с квадратом не больше `x`. Поэтому возвращается `high`.

Приведение к `long` выполняется до умножения:

```java
long square = (long) mid * mid;
```

Если сначала умножить два `int`, переполнение произойдёт до присваивания в `long`.

## Сложность

- Время: `O(log x)`.
- Дополнительная память: `O(1)`.
