# [1408. String Matching in an Array](https://leetcode.com/problems/string-matching-in-an-array/)

## Masala sharti
Satrlardan tashkil topgan `words` massiv berilgan. Shunday hamma satrlarni qaytaringki, ular `words` massivdagi boshqa bir satrning qism-satri (`substring`) bo'lsin.  
Natijani har qanday tartibda qaytarshingiz mumkin.   

### Kirish 
- `words = ["mass","as","hero","superhero"]`

### Chiqish
- `ans = ["as","hero"]`

### Izoh
- `"as" - "mass"-ning qism-satri va "hero" - "superhero"-ning qism-satri.`
- `["hero","as"] ham to'g'ri javob bo'la oladi.`

## Kod

```csharp
public class Solution {
    public IList<string> StringMatching(string[] words) {
        List<string> res = new();
        int n = words.Length;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (i == j) continue;
                if (words[j].Contains(words[i])) {
                    res.Add(words[i]);
                    break;
                }
            }
        }

        return res;
    }
}
```

### Tushuntirish

- Har bir so'zni boshqa bir so'zning qism-satri ekanligini tekshirib chiqamiz, agar shunday bo'lsa u so'zni natijamizga  
qo'shib boramiz.  

## Murakkablik tahlili

- **Vaqt murakkabligi:**  
  - O(n^2)

- **Xotira murakkabligi:**  
  - O(1)
