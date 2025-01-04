# [2270. Number of Ways to Split Array](https://leetcode.com/problems/number-of-ways-to-split-array/description)

## Masala sharti

Sizga `n` uzunlikdagi **0 indeksli** butun sonli `nums` massivi berilgan.

Agar:

* Massivning birinchi yarmi `nums[0:i]` ikkinchi yarmidan `nums[i:]`dan katta yoki teng bo'lsa
* Ikkinchi yarmida kamida 1ta element bo'lsa

bu bo'linishi `to'g'ri bo'ladi`.

Sizdan talab qilinadi: **Berilgan massivdagi to'g'ri bo'linishlar sonini topish.**

---

### Kirish

* `nums`: Hamma elementlari butun son bo‘lgan massiv, uzunligi $2 \leq |nums| \leq 10^5$.
* Har bir element uchun $-10^6 \leq nums[i] \leq 10^6$.

### Chiqish

Chap qism o‘ng qismdan katta yoki teng bo‘lishi mumkin bo‘lgan bo‘laklashlar soni.

---

## Kod

```go
func waysToSplitArray(nums []int) int {
    sum := 0
    for _, num := range nums {
        sum += num
    }

    var (
        count   = 0
        leftSum = 0
    )
    for i := 0; i < len(nums)-1; i++ {
        leftSum += nums[i]
        if leftSum >= (sum - leftSum) {
            count++
        }
    }

    return count
}
```

## Tushuntirish

1. **To‘liq yig‘indini hisoblash:**
   Oldin `nums` yig'indisini hisoblab olamiz

2. **Iteratsiya orqali bo‘laklash:**
   * Har bir `nums[i]`ni `leftSum`ga hisoblab ketamiz.
   * `nums[i:]` ni hisoblash uchun `leftSum`ni `sum`dan ayirib qo'yamiz. Bu bizga `rightSum`ni beradi
   * Agar `leftSum >= rightSum` bo'lsa `count` o'zgaruvchisini 1ta oshirib qo'yamiz

3. **Natija qaytarish:**
   Natijada barcha mos keladigan bo‘laklashlar soni qaytariladi.

---

[Go Playground](https://go.dev/play/p/IJjovynGb6b)

## Murakkablik tahlili

**Vaqt murakkabligi:**

* To‘liq yig‘indini hisoblash: O(n).
* Bo‘laklarni tekshirish: O(n).
* Umumiy: **O(n)**.

**Xotira murakkabligi:**

* Ortiqcha ma'lumotlar tuzilmasi ishlatmaganligimiz uchun **O(1)**.
