# [2381. Shifting Letters II](https://leetcode.com/problems/shifting-letters-ii/description)

## Masala sharti

Sizga `s` satr va `shifts` ko‘rinishidagi surishlar ro‘yxati berilgan. Har bir surish `[boshlanish, tugash, yo'nalish]` shaklida bo‘ladi:

* `boshlanish` va `tugash` — ko‘rsatilgan segmentning boshlanish va tugash indekslari.
* `yo'nalish`:
  * `1` bo‘lsa, **o‘ngga siljitish** (masalan, `'a' -> 'b', 'z' -> 'a'`).
  * `0` bo‘lsa, **chapga siljitish** (masalan, `'b' -> 'a', 'a' -> 'z'`).

Barcha so‘rovlarni qo‘llab chiqing va olingan natijani qaytaring.

---

### Kirish

* s = "abc", shifts = [[0,1,0],[1,2,1],[0,2,1]]

### Chiqish

* s = "ace"

```text
1. [0, 1, 0] boshlanish = 0, tugash = 1, yo'nalish = 0 (chapga)
s = "abc" -> "zac"
2. [1, 2, 1] boshlanish = 1, tugash = 2, yo'nalish = 1 (o‘ngga)
s = "zac" -> "zbd"
3. [0, 2, 1] boshlanish = 0, tugash = 2, yo'nalish = 1 (o‘ngga)
s = "zbd" -> "ace"
```

---

## Kod

```go
func shiftingLetters(s string, shifts [][]int) string {
    nums := make([]int, len(s)+1)
    bytes := []byte(s)
    for _, shift := range shifts {
        if shift[2] == 1 {
            nums[shift[0]]++
            nums[shift[1]+1]--
        } else {
            nums[shift[0]]--
            nums[shift[1]+1]++
        }
    }

    for i:=1; i<len(nums); i++ {
        nums[i]+=nums[i-1]
    }
    
    for i, b := range bytes {
        numberShift := (int(b-'a')+(26+nums[i])%26)%26
        for numberShift < 0 || numberShift > 25 {
            numberShift += 26
            numberShift %= 26
        }
        bytes[i] = byte('a'+byte(numberShift))
    }

    return string(bytes)
}
```

## Tushuntirish

1. **Surishlarni hisoblash**
   * Har bir surish uchun biz satrni surmasdan faqat farqini `nums`ga hisoblab ketamiz, o'zgarishning boshlanishi va tugashini.
   * Agar surish o'ngga bo'lsa, biz `nums[i]`ni `+1`, `nums[i+1]`ni `-1` qilib qo'ymiz, aks holda `nums[i]`ni `-1`, `nums[i+1]`ni `+1` qilib qo'yamiz.
   * `-1` qilinishiga sabab, qayerda o'zgarishni bilish.
   * `[0, 0, 0, 0]`
   * `[1, 0, -1, 0]` - Birinchi shift misolida

2. **Prefix orqali o'zgarishni hisoblash**
   * `nums[i]`gacha bo'lgan o'zgarishlar sonini hisoblaymiz
   * `[1, 1, 0, 0]` - Birinchi shift misolida `boshlanish`(nums[0]) va tugash`(nums[1]) orasidagi belgilarni o'ngga siljitishni hisobladik

3. **Iteratsiya orqali belgilarni o'zgartirish**
   * Golangda string `immutable` bo'lgani uchun `bytes` o'zgaruvchisiga `byte` tipida saqlab olamiz.
   * `numberShift` yordamida qanchaga surish kerakligini hisoblab olamiz
   * Agar `numberShift` 0 dan kichik yoki 25 dan katta bo'lsa, 26 ga bo'lib qo'ymiz (Alifbo takrorlanishi uchun)

4. **Natija qaytarish:**
   `bytes`ni string shaklida qaytaramiz

---

[Go Playground](https://go.dev/play/p/Vf-pjVDMo40)

## Murakkablik tahlili

**Vaqt murakkabligi:**

* O'zgarishlarni hisoblash: O(n).
* Prefix orqali o'zgarishni hisoblash: O(n).
* Satrni o'zgartirish: O(n).
* Umumiy: O(n) + O(n) + O(n) = O(3n): **O(n)**.

**Xotira murakkabligi:**

* satr uzunligida o'zgarishlarni hisoblash `nums`ga: **O(n)**.
* satr uzunligida o'zgartirish uchun `bytes`ga: **O(n)**.
* Umumiy: O(n) + O(n) = O(2n): **O(n)**
