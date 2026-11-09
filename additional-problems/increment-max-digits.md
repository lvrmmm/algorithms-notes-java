# Увеличение максимальных цифр с переносом

## Условие

Непустой массив цифр от `0` до `9` представляет целое число. Нужно увеличить на единицу каждую цифру, которая была максимальной в исходном массиве. Перенос распространяется влево как при обычном сложении.

Максимальные позиции определяются по исходному массиву. Цифры, изменившиеся из-за переноса, заново не выбираются.

```text
[3, 1, 3] -> [4, 1, 4]
[1, 9]    -> [2, 0]
[9, 9]    -> [1, 1, 0]
[9, 1, 9] -> [1, 0, 2, 0]
```

## Решение через список

```java
public int[] incrementMaxDigits(int[] digits) {
    int maxDigit = 0;

    for (int digit : digits) {
        maxDigit = Math.max(maxDigit, digit);
    }

    List<Integer> result = new ArrayList<>();
    int carry = 0;

    for (int i = digits.length - 1; i >= 0; i--) {
        int increment = digits[i] == maxDigit ? 1 : 0;
        int sum = digits[i] + increment + carry;

        result.add(sum % 10);
        carry = sum / 10;
    }

    if (carry > 0) {
        result.add(carry);
    }

    Collections.reverse(result);
    return result.stream().mapToInt(Integer::intValue).toArray();
}
```

## Решение через массив

Список, разворот и Stream можно убрать. Результат заполняется сразу справа налево.

```java
public int[] incrementMaxDigits(int[] digits) {
    int maxDigit = 0;

    for (int digit : digits) {
        maxDigit = Math.max(maxDigit, digit);
    }

    int[] result = new int[digits.length];
    int carry = 0;

    for (int i = digits.length - 1; i >= 0; i--) {
        int increment = digits[i] == maxDigit ? 1 : 0;
        int sum = digits[i] + increment + carry;

        result[i] = sum % 10;
        carry = sum / 10;
    }

    if (carry == 0) {
        return result;
    }

    int[] extended = new int[result.length + 1];
    extended[0] = carry;
    System.arraycopy(result, 0, extended, 1, result.length);
    return extended;
}
```

## Сложность

- Время: `O(n)`.
- Память результата: `O(n)`.

Название `incrementMaxDigits` отделяет эту задачу от LeetCode 66 `Plus One`, где единица прибавляется ко всему числу один раз.
