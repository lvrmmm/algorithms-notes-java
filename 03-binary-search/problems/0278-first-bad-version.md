# 278. First Bad Version

- Сложность: Easy
- Темы: бинарный поиск
- Ссылка: https://leetcode.com/problems/first-bad-version/

## Условие

Версии нумеруются от `1` до `n`. Начиная с некоторой версии, все последующие версии являются плохими. Через API `isBadVersion(version)` нужно найти первую плохую версию с минимальным числом вызовов.

## Решение

```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 1;
        int right = n;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (isBadVersion(mid)) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}
```

Если `mid` — плохая версия, она может быть ответом, но слева может находиться более ранняя плохая версия. Если версия хорошая, все версии слева тоже хорошие.

После завершения `left` указывает на первую позицию, где условие становится истинным.

## Сложность

- Время и число вызовов API: `O(log n)`.
- Дополнительная память: `O(1)`.
