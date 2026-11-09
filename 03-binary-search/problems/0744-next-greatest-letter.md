# 744. Find Smallest Letter Greater Than Target

- Сложность: Easy
- Темы: массив, бинарный поиск
- Ссылка: https://leetcode.com/problems/find-smallest-letter-greater-than-target/

## Условие

В отсортированном массиве букв нужно найти наименьшую букву, которая строго больше `target`. Если такой буквы нет, возвращается первый элемент массива.

## Решение

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int left = 0;
        int right = letters.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (letters[mid] <= target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        int index = left == letters.length ? 0 : left;
        return letters[index];
    }
}
```

При равенстве поиск продолжается справа, потому что требуется строго большая буква. Это также пропускает все повторения `target`.

Символы Java можно сравнивать напрямую. Вычитание `'0'` из обеих сторон не меняет результат сравнения, но здесь не требуется.

## Сложность

- Время: `O(log n)`.
- Дополнительная память: `O(1)`.
