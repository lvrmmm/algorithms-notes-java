# 66. Plus One

- Сложность: Easy
- Темы: массив, математика
- Ссылка: https://leetcode.com/problems/plus-one/

## Условие

Массив цифр представляет неотрицательное целое число. Нужно прибавить к числу единицу и вернуть массив цифр результата.

```text
[1, 2, 3] -> [1, 2, 4]
[1, 2, 9] -> [1, 3, 0]
[9, 9]    -> [1, 0, 0]
```

## Решение 1. Явный перенос

```java
class Solution {
    public int[] plusOne(int[] digits) {
        List<Integer> result = new ArrayList<>();
        int carry = 0;

        for (int i = digits.length - 1; i >= 0; i--) {
            int increment = i == digits.length - 1 ? 1 : 0;
            int sum = digits[i] + carry + increment;

            result.add(sum % 10);
            carry = sum / 10;
        }

        if (carry > 0) {
            result.add(carry);
        }

        Collections.reverse(result);
        return result.stream().mapToInt(Integer::intValue).toArray();
    }
}
```

Решение напрямую моделирует сложение столбиком. Оно использует `O(n)` дополнительной памяти и всегда проходит весь массив.

## Решение 2. Перенос через продолжение цикла

```java
class Solution {
    public int[] plusOne(int[] digits) {
        for (int i = digits.length - 1; i >= 0; i--) {
            digits[i]++;

            if (digits[i] == 10) {
                digits[i] = 0;
            } else {
                return digits;
            }
        }

        int[] result = new int[digits.length + 1];
        result[0] = 1;
        return result;
    }
}
```

Если цифра после увеличения не равна десяти, перенос закончился и можно сразу вернуть массив. Если цикл прошёл весь массив, все исходные цифры были девятками. Новый `int[]` уже заполнен нулями, поэтому достаточно записать единицу в начало.

## Сложность второго решения

- Лучший случай: `O(1)`.
- Худший случай: `O(n)`.
- Вспомогательная память: `O(1)`, если расширение не требуется.

Второе решение изменяет входной массив. При расширении создаётся новый массив длины `n + 1`.
