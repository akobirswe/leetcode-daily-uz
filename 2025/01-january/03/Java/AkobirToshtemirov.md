# [2270. Number of Ways to Split Array](https://leetcode.com/problems/number-of-ways-to-split-array/description/?envType=daily-question&envId=2025-01-03)

## Masala sharti
Berilgan `nums` massivini shunday ajratish kerakki, har bir ajratish uchun chap qismning yig'indisi o'ng qismning yig'indisidan katta yoki teng bo'lsin. Boshqacha qilib aytganda:

- Ajratish amalga oshirilgandan keyin chap qismning yig'indisi (har bir elementni qabul qilganda) o'ng qismning yig'indisidan katta yoki teng bo'lishi kerak.
- Misol: `[1, 2, 3, 4, 5]` massivini ajratamiz. Agar chap qism `[1, 2, 3]` va o'ng qism `[4, 5]` bo'lsa, chap qismning yig'indisi 6 (1+2+3) va o'ng qismning yig'indisi 9 (4+5). Bu holda chap qismning yig'indisi o'ng qismga teng emas, shuning uchun bu ajratish noto'g'ri bo'ladi.

### Input
- `nums = [10, 4, -8, 7]`

### Output
- `ans = 2`

## Kod

```java
class Solution {
    public int waysToSplitArray(int[] nums) {
        long sum = 0;
        for (int num : nums) {
            sum += num;
        }

        int len = nums.length;
        int count = 0;
        long leftSum = 0;
        int i = 0;
        while (i < len - 1) {
            leftSum += nums[i];
            long rightSum = sum - leftSum;
            if (leftSum >= rightSum) {
                count++;
            }
            i++;
        }
        return count;
    }
}
```

## Tushuntirish

1. **Jami yig'indini hisoblash:**
   - Avvalo, massivning barcha elementlarini yig'ib, umumiy yig'indi `sum`ni hisoblaymiz. Bu yig'indini keyinchalik ajratishlar o'rtasida solishtirishda ishlatamiz.

2. **Chap va o'ng qismlarni hisoblash:**
   - `leftSum` o'zgaruvchisi yordamida chap qismining yig'indisini hisoblaymiz. Ya'ni, har bir yangi elementni qo'shgan sari chap qismning yig'indisi ortadi.
   - `rightSum` o'zgaruvchisi esa o'ng qismning yig'indisini ifodalaydi, ya'ni `rightSum = sum - leftSum`. Bu, massivning umumiy yig'indisidan chap qism yig'indisini olib tashlab, o'ng qismining yig'indisini topadi.

3. **Ajratish shartlarini tekshirish:**
   - Har bir ajratish uchun `leftSum >= rightSum` shartini tekshiramiz. Agar chap qismning yig'indisi o'ng qismning yig'indisidan katta yoki teng bo'lsa, bu ajratish to'g'ri hisoblanadi, shuning uchun `count` (sanash) o'zgaruvchisini oshiramiz.

4. **Takrorlash va natijani qaytarish(return):**
   - Massivdagi har bir elementni tekshirib chiqqach, `count` o'zgaruvchisi natijada to'g'ri ajratishlar sonini beradi. Mana shu orqali biz javobni topamiz.

## Yechim samaradorligi tahlili

- **Vaqt:**  
  - Massivning yig'indisini hisoblash O(n), bu yerda `n` — massivning uzunligi.  
  - Har bir elementni tekshirish uchun bir marta iteratsiya qilinadi, bu ham O(n).  
  - Umumiy: O(n).

- **Xotira:**  
  - Yig'indini saqlash uchun faqat O(1) xotira kerak.
