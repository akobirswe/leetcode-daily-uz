# [1408. String Matching in an Array](https://leetcode.com/problems/string-matching-in-an-array/)

### Masala
Berilgan so'zlar ro'yxatida (`words`), har bir so'zni tekshirib, agar bu so'z boshqa so'zlar ichida mavjud bo'lsa (ya'ni, bu so'z boshqa so'zga kiritilgan bo'lsa), uni ro'yxatga qo'shish kerak.

### Yechim
Yechim quyidagicha ishlaydi:

1. **So'zlarni bitta satrga birlashtirish:**
   - Dastlab, barcha so'zlarni bitta satrga birlashtiramiz. Bu satrni yaratish uchun `String.join(" ", words)` metodidan foydalanamiz. Bu metod so'zlarni bo'shliq bilan ajratib birlashtiradi.

2. **So'zlarni tekshirish:**
   - Har bir so'zni tekshiramiz. Agar so'zning birinchi joylashuvi (`indexOf`) va oxirgi joylashuvi (`lastIndexOf`) bir xil bo'lmasa, demak bu so'z boshqa joyda ham takrorlanadi. Shunday bo'lsa, biz bu so'zni natija ro'yxatiga qo'shamiz.

3. **Natijani qaytarish:**
   - Barcha so'zlarni tekshirib bo'lgach, natijani (ro'yxatni) qaytaramiz.

### Kod

```java
class Solution {
    public List<String> stringMatching(String[] words) {
        // Barcha so'zlarni bitta satrga birlashtiramiz
        String str = String.join(" ", words);
        
        // Natija ro'yxatini yaratamiz
        List<String> res = new ArrayList<>();

        // Har bir so'zni tekshirib chiqamiz
        for (String word : words) {
            // Agar so'z satrning bir nechta joylarida mavjud bo'lsa, uni natijaga qo'shamiz
            if (str.indexOf(word) != str.lastIndexOf(word)) {
                res.add(word);
            }
        }

        // Natija ro'yxatini qaytaramiz
        return res;
    }
}
```

### Yechimni tushuntirish:

1. **`String.join(" ", words)`**:  
   - Bu metod yordamida biz `words` massividagi barcha so'zlarni bitta satrga birlashtiramiz va ular orasiga bo'shliq qo'yamiz. Masalan, agar `words` massivida `["massala", "so'z", "mavjud"]` bo'lsa, u holda `str` quyidagi ko'rinishga ega bo'ladi: `"massala so'z mavjud"`.

2. **`indexOf(word)` va `lastIndexOf(word)` metodlari:**
   - `indexOf(word)` metodidan foydalanib, biz so'zni satrda birinchi marta qayerda uchrashishini bilib olamiz.
   - `lastIndexOf(word)` metodidan foydalanib, biz so'zni satrda oxirgi marta qayerda uchrashishini bilib olamiz.
   - Agar bu ikkala qiymat teng bo'lsa, demak, so'z faqat bitta joyda mavjud. Agar teng bo'lmasa, so'z boshqa joylarda ham takrorlanadi, shuning uchun uni natijaga qo'shamiz.

3. **Natija ro'yxatini qaytarish:**
   - So'zlarni tekshirgandan so'ng, takrorlangan so'zlarni ro'yxatga qo'shamiz va oxir-oqibat bu ro'yxatni qaytaramiz.

### Misol:

Agar `words` ro'yxati quyidagicha bo'lsa:
```java
String[] words = {"massala", "so'z", "mavjud", "so'z"};
```

- `str` quyidagi satrga aylanadi: `"massala so'z mavjud so'z"`.
- So'zlarni tekshirib chiqqanimizda:
  - `"massala"` faqat bir marta mavjud, shuning uchun uni natijaga qo'shmaymiz.
  - `"so'z"` ikki marta mavjud, shuning uchun uni natijaga qo'shamiz.
  - `"mavjud"` faqat bitta joyda mavjud, shuning uchun uni ham natijaga qo'shmaymiz.

Natijada, `res` ro'yxati quyidagicha bo'ladi:
```java
["so'z"]
```

## Misol.2 Kirish 
- `words = ["mass","as","hero","superhero"]`

## Chiqish
- `ans = ["as","hero"]`

## Izoh
- `"as" - "mass"-ning qism-satri va "hero" - "superhero"-ning qism-satri.`
- `["hero","as"] ham to'g'ri javob bo'la oladi.`

### Murakkablik tahlili:

- **Vaqt murakkabligi:** O(n * m), bunda `n` - so'zlar soni, va `m` - eng uzun so'zning uzunligi. Chunki har bir so'zni tekshirishda `indexOf` va `lastIndexOf` metodlari satrni oxirigacha tekshiradi.
- **Xotira murakkabligi:** O(n * m), chunki biz barcha so'zlarni bitta satrga birlashtiramiz va so'zlarni saqlash uchun ro'yxat ishlatamiz.
