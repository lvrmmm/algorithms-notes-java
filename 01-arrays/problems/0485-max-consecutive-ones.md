# 485. Max Consecutive Ones

- Сложность: Easy
- Темы: массив
- Ссылка: https://leetcode.com/problems/max-consecutive-ones/

## Условие

Дан бинарный массив. Нужно вернуть максимальное количество единиц, идущих подряд.

```text
Вход:  [1, 1, 0, 1, 1, 1]
Ответ: 3
```

## Решение

`count` хранит длину текущей серии единиц, а `maxConsecutiveOnes` — максимальную длину среди завершённых серий.

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int count = 0;
        int maxConsecutiveOnes = 0;

        for (int num : nums) {
            if (num == 1) {
                count++;
            } else {
                maxConsecutiveOnes = Math.max(count, maxConsecutiveOnes);
                count = 0;
            }
        }

        maxConsecutiveOnes = Math.max(count, maxConsecutiveOnes);
        return maxConsecutiveOnes;
    }
}
```

## Почему нужна проверка после цикла

Последняя серия может завершиться вместе с массивом, без нуля справа. Например, для `[1, 1, 0, 1, 1, 1]` перед выходом из цикла `count == 3`, а сохранённый максимум ещё равен двум.

## Сложность

- Время: `O(n)`.
- Дополнительная память: `O(1)`.

Чтобы узнать ответ, в общем случае необходимо проверить каждый элемент массива.
