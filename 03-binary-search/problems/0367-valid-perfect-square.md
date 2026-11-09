# 367. Valid Perfect Square

- Сложность: Easy
- Темы: математика, бинарный поиск
- Ссылка: https://leetcode.com/problems/valid-perfect-square/

## Условие

Нужно определить, является ли положительное целое число точным квадратом, не используя встроенное извлечение квадратного корня.

## Решение

```java
class Solution {
    public boolean isPerfectSquare(int num) {
        int low = 0;
        int high = num;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            long square = (long) mid * mid;

            if (square == num) {
                return true;
            } else if (square > num) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return false;
    }
}
```

Решение использует ту же монотонность квадратов, что и задача `Sqrt(x)`, но возвращает `true` только при точном совпадении.

Для `num >= 2` правую границу можно сократить до `num / 2`. На асимптотическую сложность это не влияет.

## Сложность

- Время: `O(log num)`.
- Дополнительная память: `O(1)`.
