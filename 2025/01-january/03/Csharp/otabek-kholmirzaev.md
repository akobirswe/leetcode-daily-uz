# [Number of Ways to Split an Array](https://leetcode.com/problems/number-of-ways-to-split-array/)

## Masala sharti
Butun sonlardan iborat `nums` massiv berilgan. Massivni ikkita bo‘lakka bo‘lish uchun `pivot` indeksi tanlanadi, shunda:

1. **Chap qism:** `nums[0]` dan `nums[pivot]` gacha (pivot indeksi ham qo‘shiladi).
2. **O'ng qism:** `nums[pivot + 1]` dan oxirigacha.

Masalan, `nums = [10,4,-8,7]` bo‘lsa:

- `pivot = 0` uchun:
  - Chap: `[10]`, O'ng: `[4, -8, 7]`
- `pivot = 1` uchun:
  - Chap: `[10, 4]`, O'ng: `[-8, 7]`

Sizdan talab qilinadi: **Berilgan massivdagi shunday pivot indekslar sonini topingki, chap bo‘lakning yig‘indisi o‘ng bo‘lakning yig‘indisidan katta yoki teng bo‘lsin.**

---

### Kirish
- `nums`: Hamma elementlari butun son bo‘lgan massiv, uzunligi $2 \leq |nums| \leq 10^5$.
- Har bir element uchun $-10^6 \leq nums[i] \leq 10^6$.

### Chiqish
Chap qism o‘ng qismdan katta yoki teng bo‘lishi mumkin bo‘lgan bo‘laklashlar soni.

---

## Kod

```csharp
public class Solution {
    public int WaysToSplitArray(int[] nums) {
        long totalSum = 0;
        foreach (var num in nums) {
            totalSum += num;
        }

        long leftSum = 0;
        int count = 0;
        for (int i = 0; i < nums.Length - 1; i++) {
            leftSum += nums[i];
            long rightSum = totalSum - leftSum;
            if (leftSum >= rightSum) {
                count++;
            }
        }

        return count;
    }
}
```

## Tushuntirish
1. **To‘liq yig‘indini hisoblash:**
   Barcha elementlarning umumiy yig‘indisi `totalSum` hisoblanadi.

2. **Iteratsiya orqali bo‘laklash:**
   - Har bir indeksda `leftSum` yangilanadi.
   - O‘ng qism yig‘indisi `rightSum = totalSum - leftSum` orqali hisoblanadi.
   - Agar `leftSum >= rightSum` bo‘lsa, hisoblagichni `count` oshiramiz.

3. **Natija qaytarish:**
   Natijada barcha mos keladigan bo‘laklashlar soni qaytariladi.

---

## Murakkablik tahlili
- **Vaqt murakkabligi:**
  - To‘liq yig‘indini hisoblash: O(n).
  - Bo‘laklarni tekshirish: O(n).
  - Umumiy: **O(n)**.

- **Xotira murakkabligi:**
  - Hech qanday qo‘shimcha massiv ishlatilmagan, shuning uchun **O(1)**.

