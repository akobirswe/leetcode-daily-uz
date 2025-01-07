# [1930. Unique Length-3 Palindromic Subsequences](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/)

### Masala
Berilgan satrdagi uzunligi 3 bo'lgan palindromik subsequence-larni (ketma-ketliklarni) topish kerak. Palindromik subsequence deganda, boshlanish va tugash belgisi bir xil bo'lib, oradagi belgi har qanday bo'lishi mumkin bo'lgan ketma-ketlik tushuniladi. Masalan, `"aba"`, `"aca"`, `"aaa"` — bu palindromik subsequence-lardir.

### Yechim

1. **Birinchi va oxirgi indekslarni saqlash:**  
   Dastlab har bir harf uchun uning satrdagi birinchi va oxirgi joylashgan indekslarini aniqlaymiz. Buning uchun ikkita massiv yaratamiz:
   - `first[]`: Harflarning birinchi joylashuvlarini saqlaydi.
   - `last[]`: Harflarning oxirgi joylashuvlarini saqlaydi.

2. **Subsequence-larni hisoblash:**  
   Har bir harf uchun uning birinchi va oxirgi joylashuvlari orasidagi noyob (unique) belgilarni hisoblaymiz. Buni qilish uchun `HashSet` ma'lumotlar tuzilmasidan foydalanamiz.

3. **Natijani hisoblash:**  
   Har bir harf uchun o'sha harfning birinchi va oxirgi joylashuvlari orasidagi noyob belgilarni hisoblab, umumiy `count` (yig'indi) ni oshiramiz.

### Kod

```java
class Solution {
    public int countPalindromicSubsequence(String s) {
        // Harflarning birinchi va oxirgi indekslarini saqlash uchun massivlar
        int[] first = new int[26];  // 'a' dan 'z' gacha bo'lgan harflar uchun
        int[] last = new int[26];   // 'a' dan 'z' gacha bo'lgan harflar uchun

        // Dastlab har bir harf uchun indekslarni -1 ga o'rnatamiz
        for (int i = 0; i < 26; i++) {
            first[i] = -1;  // Birinchi indeksni belgilaymiz
            last[i] = -1;   // Oxirgi indeksni belgilaymiz
        }

        // Satrning har bir harfi uchun birinchi joylashuvni topamiz
        for (int i = 0; i < s.length(); i++) {
            int idx = s.charAt(i) - 'a';  // Harfning indeksi
            if (first[idx] == -1) {  // Agar bu harfning birinchi indeksi hali belgilamagan bo'lsa
                first[idx] = i;  // Birinchi joylashuvni saqlaymiz
            }
        }

        // Satrning oxiridan boshlab har bir harf uchun oxirgi joylashuvni topamiz
        for (int i = s.length() - 1; i >= 0; i--) {
            int idx = s.charAt(i) - 'a';  // Harfning indeksi
            if (last[idx] == -1) {  // Agar bu harfning oxirgi indeksi hali belgilamagan bo'lsa
                last[idx] = i;  // Oxirgi joylashuvni saqlaymiz
            }
        }

        // Palindromik subsequence-larni hisoblash
        int count = 0;
        for (int i = 0; i < 26; i++) {
            Set<Character> secondChars = new HashSet<>();  // Noyob harflarni saqlash uchun HashSet
            // Birinchi va oxirgi indekslar orasidagi noyob harflarni topamiz
            for (int j = first[i] + 1; j < last[i]; j++) {
                secondChars.add(s.charAt(j));  // Harfni HashSet-ga qo'shamiz
                if (secondChars.size() == 26) {  // Agar 26 ta noyob harfni topgan bo'lsak, to'xtatamiz
                    break;
                }
            }
            // Noyob harflar sonini countga qo'shamiz
            count += secondChars.size();
        }

        // Yakuniy natijani qaytaramiz
        return count;
    }
}
```

### Yechimni tushuntirish:

1. **`first[]` va `last[]` massivlari:**
   - `first[]` massivida har bir harfning satrdagi birinchi joylashuvi saqlanadi.
   - `last[]` massivida har bir harfning satrdagi oxirgi joylashuvi saqlanadi.

2. **`secondChars` Seti:**
   - Har bir harf uchun, uning birinchi va oxirgi joylashuvlari orasida joylashgan noyob harflarni aniqlash uchun `secondChars` nomli `HashSet` ishlatamiz. `HashSet` orqali harflarning takrorlanishini oldini olamiz.

3. **Hisoblash jarayoni:**
   - Har bir harf uchun uning birinchi va oxirgi joylashuvlari orasidagi barcha noyob belgilarni topamiz. Keyin bu noyob belgilarni `secondChars`ga qo'shamiz. Har bir harf uchun olingan noyob belgilar sonini `count`ga qo'shamiz.

4. **Natija:**
   - Barcha harflar bo'yicha hisoblashni yakunlagach, `count` qiymatini qaytaramiz. Bu qiymat satrda nechta uzunligi 3 bo'lgan palindromik subsequence borligini ko'rsatadi.

### Murakkablik tahlili:

- **Vaqt murakkabligi:** O(n), chunki biz har bir harfni bir marta tekshiramiz.
- **Xotira murakkabligi:** O(1), chunki faqat 26 ta harf uchun massivlar va `HashSet` ishlatamiz.
