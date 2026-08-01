### **7. Problem Solving & Coding Tasks**

---

## Question Index

- [Q19. Write a Java code to identify a prime number. [Answered]](#q19-write-a-java-code-to-identify-a-prime-number-answered)
- [Q23. How to reverse a string without an in-build function? [Answered]](#q23-how-to-reverse-a-string-without-an-in-build-function-answered)
- [Q33. Write a code to check if a String is a Palindrome. [Answered]](#q33-write-a-code-to-check-if-a-string-is-a-palindrome-answered)
- [Q45. Find the 'n-th' highest in array. [Answered]](#q45-find-the-n-th-highest-in-array-answered)
- [Q61. Code to find the smallest element present in Array A but not in B (return -1 if not present). [Answered]](#q61-code-to-find-the-smallest-element-present-in-array-a-but-not-in-b-return-1-if-not-present-answered)
- [Q68. Count occurrences of each character in a string. [Answered]](#q68-count-occurrences-of-each-character-in-a-string-answered)
- [Q78. Second Max in array. [Answered]](#q78-second-max-in-array-answered)
- [Q118. Ways to iterate over `ArrayList`. [Answered]](#q118-ways-to-iterate-over-arraylist-answered)
- [Q130. How can you iterate over a Map? [Answered]](#q130-how-can-you-iterate-over-a-map-answered)
- [Q142. Find duplicates using Stream API. [To be Answered]](#q142-find-duplicates-using-stream-api-to-be-answered)
- [Q143. Put all zeroes at one end in an array. [Answered]](#q143-put-all-zeroes-at-one-end-in-an-array-answered)
- [Q144. Check if 2 strings are anagrams. [Answered]](#q144-check-if-2-strings-are-anagrams-answered)
- [Q145. Program to find duplicates in a string. [To be Answered]](#q145-program-to-find-duplicates-in-a-string-to-be-answered)
- [Q148. Code to swap 2 variables without a 3rd variable. [To be Answered]](#q148-code-to-swap-2-variables-without-a-3rd-variable-to-be-answered)

---

# Q19. Write a Java code to identify a prime number. [Answered]

- [Q19. Write a Java code to identify a prime number. [Answered]](#q19-write-a-java-code-to-identify-a-prime-number-answered)

**Priority:** P2

---

# 📌 One-Line Interview Answer

A prime number is a number greater than 1 that has exactly two factors, `1` and itself; we can efficiently check this by testing divisibility only up to `√n`.

---

# 💻 Java Code

```java
public class PrimeNumber {

    public static boolean isPrime(int n) {

        if (n <= 1) {
            return false;
        }

        if (n == 2) {
            return true;
        }

        if (n % 2 == 0) {
            return false;
        }

        for (int i = 3; i <= Math.sqrt(n); i += 2) {
            if (n % i == 0) {
                return false;
            }
        }

        return true;
    }

    public static void main(String[] args) {

        int number = 29;

        if (isPrime(number)) {
            System.out.println(number + " is a prime number");
        } else {
            System.out.println(number + " is not a prime number");
        }
    }
}
```

### Output

```text
29 is a prime number
```

---

# 📖 How Does It Work?

For a number to be prime:

```text
It must be > 1
AND
It must not be divisible by any number other than 1 and itself.
```

For example:

```text
29
```

We check:

```text
29 % 2 != 0
29 % 3 != 0
29 % 5 != 0
```

Since there is no divisor up to `√29`, the number is prime.

---

# 🔍 Why Check Only Up to √n?

This is an important interview follow-up.

Suppose:

```text
n = a × b
```

If both `a` and `b` were greater than `√n`, then:

```text
a × b > √n × √n
       > n
```

which is impossible.

Therefore, if a number has a factor, **at least one factor must be less than or equal to `√n`**.

So instead of:

```java
for (int i = 2; i < n; i++)
```

we can use:

```java
for (int i = 2; i <= Math.sqrt(n); i++)
```

This significantly reduces the number of checks.

---

# ⚡ Further Optimization

The code first handles even numbers:

```java
if (n % 2 == 0) {
    return false;
}
```

After that, we only check odd divisors:

```java
for (int i = 3; i <= Math.sqrt(n); i += 2)
```

Therefore:

```text
2 → handled separately

3, 5, 7, 9, 11, ...
```

are checked.

This avoids unnecessary checks against even numbers.

---

# 🧪 Example

For:

```text
n = 25
```

We check:

```text
25 % 3 != 0
25 % 5 == 0
```

Therefore:

```text
25 is not prime
```

For:

```text
n = 29
```

We check possible divisors up to:

```text
√29 ≈ 5.38
```

So we only need:

```text
3
5
```

Neither divides 29.

Therefore:

```text
29 is prime
```

---

# ⚠️ Important Edge Cases

### `0`

```text
0 → Not prime
```

### `1`

```text
1 → Not prime
```

A prime number must have exactly two positive factors.

### Negative numbers

```text
-7 → Not prime
```

### `2`

```text
2 → Prime
```

It is the only even prime number.

### Even numbers greater than 2

```text
4 → Not prime
6 → Not prime
8 → Not prime
10 → Not prime
```

---

# 📊 Complexity

### Time Complexity

```text
O(√n)
```

because we check divisors only up to the square root of `n`.

With the odd-number optimization, approximately half of those candidates are skipped.

### Space Complexity

```text
O(1)
```

because only a few variables are used.

---

# 🔄 Simple Version

If the interviewer wants a straightforward implementation:

```java
public static boolean isPrime(int n) {

    if (n <= 1) {
        return false;
    }

    for (int i = 2; i <= Math.sqrt(n); i++) {
        if (n % i == 0) {
            return false;
        }
    }

    return true;
}
```

This is easier to explain during an interview.

---

# 🎯 Which Version Should You Use?

For an interview:

### Beginner/simple coding round

Use:

```java
for (int i = 2; i <= Math.sqrt(n); i++)
```

### Senior-level discussion

Mention:

```text
Handle n <= 1
Handle 2
Reject even numbers
Check only odd divisors
Stop at √n
```

This demonstrates that you understand the optimization rather than simply memorizing the solution.

---

# 🔥 Common Follow-Up Questions

### 1. Why is `1` not a prime number?

Because `1` has only one positive factor:

```text
1
```

A prime number must have exactly two positive factors.

---

### 2. What is the only even prime number?

```text
2
```

Every other even number is divisible by `2`.

---

### 3. Why use `i <= Math.sqrt(n)`?

Because any composite number must have at least one factor less than or equal to its square root.

---

### 4. Can we avoid calling `Math.sqrt()` repeatedly?

Yes.

For example:

```java
int limit = (int) Math.sqrt(n);

for (int i = 3; i <= limit; i += 2) {
    ...
}
```

Or avoid floating-point calculation entirely:

```java
for (int i = 3; i <= n / i; i += 2) {
    if (n % i == 0) {
        return false;
    }
}
```

`n / i` also avoids potential overflow that could occur with `i * i`.

---

# 🧠 Interview Trap

A common inefficient solution is:

```java
for (int i = 2; i < n; i++) {
    if (n % i == 0) {
        return false;
    }
}
```

Although correct, it performs unnecessary checks.

A better solution is:

```java
for (int i = 2; i <= Math.sqrt(n); i++)
```

giving:

```text
O(n)      → basic approach
O(√n)     → optimized approach
```

---

# 🎤 60-Second Interview Answer

"A prime number is a number greater than 1 that has exactly two factors, 1 and itself. In Java, I first handle numbers less than or equal to 1 as non-prime. Then I can handle 2 separately and reject other even numbers. For the remaining odd numbers, I only check divisibility up to the square root of the number because if a number has a factor greater than its square root, it must have a corresponding factor smaller than the square root. If any divisor is found, the number is not prime; otherwise it is prime. The time complexity is O(√n) and the space complexity is O(1)."

---

# 📝 Quick Revision Notes

```text
Prime number:
    > 1
    Exactly 2 positive factors

Algorithm:
    n <= 1 → false
    n == 2 → true
    even → false
    check odd divisors up to √n
    divisor found → false
    otherwise → true

Time  → O(√n)
Space → O(1)
```

### Golden Rule

> **To determine whether `n` is prime, you only need to test possible divisors up to `√n`.**

---

[Q19. Write a Java code to identify a prime number. [Answered]](#q19-write-a-java-code-to-identify-a-prime-number-answered)

[⬆ Back to Question Index](#question-index)

---

# Q23. How to reverse a string without an in-build function? [Answered]

- [Q23. How to reverse a string without an in-build function? [Answered]](#q23-how-to-reverse-a-string-without-an-in-build-function-answered)

**Priority:** P1

---

# 📌 One-Line Interview Answer

We can reverse a Java `String` without using built-in reverse functions by iterating from the last character to the first and appending each character to a result.

---

# 💻 Approach 1 — Using a `for` Loop

```java
public class ReverseString {

    public static String reverse(String str) {

        String reversed = "";

        for (int i = str.length() - 1; i >= 0; i--) {
            reversed += str.charAt(i);
        }

        return reversed;
    }

    public static void main(String[] args) {

        String str = "Java";

        System.out.println(reverse(str));
    }
}
```

### Output

```text
avaJ
```

---

# 📖 How Does It Work?

Given:

```text
Java
```

Character indexes are:

```text
J → 0
a → 1
v → 2
a → 3
```

We iterate backwards:

```text
i = 3 → a
i = 2 → v
i = 1 → a
i = 0 → J
```

Result:

```text
avaJ
```

---

# ⚠️ Important Performance Issue

The above code is easy to understand, but:

```java
reversed += str.charAt(i);
```

creates new `String` objects because `String` is immutable.

For a large string, repeatedly concatenating strings can result in poor performance.

A better implementation is to use `StringBuilder`.

---

# 💻 Approach 2 — Using `StringBuilder`

If the interviewer says:

> "Don't use an in-built reverse function."

We can still use `StringBuilder` while manually iterating:

```java
public static String reverse(String str) {

    StringBuilder reversed = new StringBuilder(str.length());

    for (int i = str.length() - 1; i >= 0; i--) {
        reversed.append(str.charAt(i));
    }

    return reversed.toString();
}
```

This avoids repeated intermediate `String` objects.

---

# 💻 Approach 3 — Using a Character Array

Another common interview approach is:

```java
public static String reverse(String str) {

    char[] chars = str.toCharArray();

    int left = 0;
    int right = chars.length - 1;

    while (left < right) {

        char temp = chars[left];
        chars[left] = chars[right];
        chars[right] = temp;

        left++;
        right--;
    }

    return new String(chars);
}
```

For:

```text
Java
```

the array initially contains:

```text
J a v a
```

First swap:

```text
a a v J
```

Second swap:

```text
a v a J
```

Result:

```text
avaJ
```

---

# 💡 Approach 4 — Two-Pointer Technique

The character-array solution uses the **two-pointer approach**.

```text
left                     right
 ↓                         ↓
 J   a   v   a
```

Swap:

```text
a   a   v   J
```

Move pointers:

```text
    left             right
      ↓               ↓
 a    a   v   J
```

Swap again:

```text
a   v   a   J
```

Now:

```text
left >= right
```

Stop.

This approach is particularly useful because it demonstrates a common array/string manipulation pattern.

---

# 🔥 Approach 5 — Recursion

A recursive solution can also be written:

```java
public static String reverse(String str) {

    if (str == null || str.length() <= 1) {
        return str;
    }

    return reverse(str.substring(1)) + str.charAt(0);
}
```

For:

```text
Java
```

the calls conceptually become:

```text
reverse("Java")
    ↓
reverse("ava") + "J"
    ↓
reverse("va") + "a" + "J"
    ↓
reverse("a") + "v" + "a" + "J"
    ↓
"avaJ"
```

However, this isn't generally the preferred production implementation because recursion creates additional stack frames and repeated string operations.

---

# 📊 Complexity Comparison

| Approach | Time | Space | Interview Recommendation |
|---|---:|---:|---|
| String concatenation | O(n²) | O(n) | Simple demonstration |
| StringBuilder loop | O(n) | O(n) | ⭐ Recommended |
| Character array + two pointers | O(n) | O(n) | ⭐ Excellent |
| Recursion | Can be O(n²) | O(n) stack | Good for follow-up |

---

# 🎯 Best Interview Solution

For a typical coding interview, I would prefer the character-array approach:

```java
public static String reverse(String str) {

    char[] chars = str.toCharArray();

    int left = 0;
    int right = chars.length - 1;

    while (left < right) {

        char temp = chars[left];
        chars[left] = chars[right];
        chars[right] = temp;

        left++;
        right--;
    }

    return new String(chars);
}
```

Why?

Because it demonstrates:

```text
String manipulation
+
Arrays
+
Two pointers
+
Swapping
+
O(n) time
```

without relying on a built-in reverse operation.

---

# ⚠️ Edge Cases

### Empty String

```java
""
```

Result:

```text
""
```

### Single Character

```java
"A"
```

Result:

```text
"A"
```

### Null

If null is possible, explicitly handle it:

```java
if (str == null) {
    return null;
}
```

### Spaces

For:

```text
"Java Code"
```

the method produces:

```text
"edoC avaJ"
```

Spaces are treated as normal characters.

---

# 🧠 Important Interview Follow-Up

### What is wrong with this?

```java
String reversed = "";

for (int i = str.length() - 1; i >= 0; i--) {
    reversed += str.charAt(i);
}
```

`String` is immutable.

Every concatenation can create a new `String`, resulting in unnecessary object creation.

For example:

```text
""
 ↓
"a"
 ↓
"av"
 ↓
"ava"
 ↓
"avaJ"
```

For a large string, this can lead to **O(n²)** time behavior.

Using:

```java
StringBuilder
```

allows mutable character appends and gives an efficient O(n) approach.

---

# 🔍 `String` vs `StringBuilder`

### String

```java
String result = "";
result += 'a';
result += 'b';
```

Strings are immutable.

### StringBuilder

```java
StringBuilder result = new StringBuilder();
result.append('a');
result.append('b');
```

`StringBuilder` is mutable and is generally preferred for repeated modifications in a single-threaded context.

---

# 🎤 3-Minute Interview Explanation

"To reverse a string without using a built-in reverse function, there are several approaches. The simplest is to iterate from the last character to the first and append each character to the result. However, if I use normal String concatenation repeatedly, it can lead to O(n²) time because String is immutable and every concatenation can create a new object.

A better approach is to use StringBuilder. I create a StringBuilder with the original string's length and iterate from the last index to zero, appending each character. This gives O(n) time and O(n) space.

Another good interview solution is to convert the string into a character array and use two pointers, one at the beginning and one at the end. I swap the characters at those positions and move both pointers toward the center until they meet. This also takes O(n) time and O(n) additional space for the character array.

If the interviewer specifically wants to test algorithmic thinking, I would prefer the two-pointer solution because it demonstrates the technique without relying on a reverse API."

---

# ⏱️ 60-Second Interview Answer

"I can reverse a string without using a built-in reverse method by converting it into a character array and using two pointers. One pointer starts at index zero and the other at the last index. I swap the two characters, move the pointers toward the center, and continue until they meet. The time complexity is O(n), and because the character array is used, the additional space is O(n). Alternatively, I can iterate from the last character to the first using StringBuilder, which is also O(n). I would avoid repeatedly using String concatenation because String is immutable and that can lead to O(n²) behavior."

---

# 📝 Quick Revision Notes

```text
Input:
    "Java"

Output:
    "avaJ"

Best approaches:

1. Iterate backwards
2. StringBuilder
3. Character array + two pointers
4. Recursion

Recommended:
    Character array + two pointers

Time:
    O(n)

Space:
    O(n)

Avoid:
    Repeated String concatenation
```

### Golden Rule

> **For an efficient manual string reversal, use a two-pointer character-array approach or iterate backwards with `StringBuilder`; avoid repeated `String` concatenation for large inputs.**

---

[Q23. How to reverse a string without an in-build function? [Answered]](#q23-how-to-reverse-a-string-without-an-in-build-function-answered)

[⬆ Back to Question Index](#question-index)

---

# Q33. Write a code to check if a String is a Palindrome. [Answered]

- [Q33. Write a code to check if a String is a Palindrome. [Answered]](#q33-write-a-code-to-check-if-a-string-is-a-palindrome-answered)

**Priority:** P1

---

# 📌 One-Line Interview Answer

A String is a palindrome if it reads the same forward and backward; we can efficiently check this using two pointers starting from both ends and comparing characters until they meet.

---

# 💻 Approach 1 — Two-Pointer Technique

```java
public class PalindromeCheck {

    public static boolean isPalindrome(String str) {

        if (str == null) {
            return false;
        }

        int left = 0;
        int right = str.length() - 1;

        while (left < right) {

            if (str.charAt(left) != str.charAt(right)) {
                return false;
            }

            left++;
            right--;
        }

        return true;
    }

    public static void main(String[] args) {

        String str = "madam";

        if (isPalindrome(str)) {
            System.out.println(str + " is a palindrome");
        } else {
            System.out.println(str + " is not a palindrome");
        }
    }
}
```

### Output

```text
madam is a palindrome
```

---

# 📖 How Does It Work?

For:

```text
madam
```

Indexes:

```text
m a d a m
↑       ↑
L       R
```

Compare:

```text
m == m
```

Move inward:

```text
  a d a
  ↑   ↑
  L   R
```

Compare:

```text
a == a
```

Move inward:

```text
    d
    ↑
```

Both pointers meet.

Therefore:

```text
madam → Palindrome
```

---

# ❌ Example of a Non-Palindrome

Consider:

```text
hello
```

Compare:

```text
h != o
```

As soon as one mismatch is found:

```java
return false;
```

There is no need to check the remaining characters.

---

# 💻 Approach 2 — Reverse the String and Compare

Another common approach is to manually create the reversed String and compare it with the original.

```java
public static boolean isPalindrome(String str) {

    if (str == null) {
        return false;
    }

    StringBuilder reversed = new StringBuilder(str.length());

    for (int i = str.length() - 1; i >= 0; i--) {
        reversed.append(str.charAt(i));
    }

    return str.equals(reversed.toString());
}
```

For:

```text
madam
```

we get:

```text
Original  → madam
Reversed  → madam
```

Therefore:

```text
true
```

---

# ⚖️ Two-Pointer vs Reverse-and-Compare

| Approach | Time | Space | Recommendation |
|---|---:|---:|---|
| Two pointers | O(n) | O(1) | ⭐ Best |
| Reverse + compare | O(n) | O(n) | Simple |
| Recursion | O(n) | O(n) stack | Follow-up |

The two-pointer solution is generally preferable because it doesn't require creating another String.

---

# 💡 Why Is Two-Pointer Better?

Consider a String containing:

```text
1,000,000 characters
```

With reverse-and-compare:

```text
Original String
+
Reversed String
```

requires additional memory.

With two pointers:

```text
left  → beginning
right → end
```

we only need a few variables.

Therefore:

```text
Time  → O(n)
Space → O(1)
```

---

# 🔥 Case-Insensitive Palindrome

If the interviewer asks:

> "Should `Madam` be considered a palindrome?"

If case should be ignored:

```java
public static boolean isPalindrome(String str) {

    if (str == null) {
        return false;
    }

    int left = 0;
    int right = str.length() - 1;

    while (left < right) {

        if (Character.toLowerCase(str.charAt(left))
                != Character.toLowerCase(str.charAt(right))) {

            return false;
        }

        left++;
        right--;
    }

    return true;
}
```

Now:

```text
Madam → true
```

---

# 🔥 Ignore Spaces and Special Characters

Sometimes the requirement is:

> "Check whether a sentence is a palindrome while ignoring spaces, punctuation and case."

For example:

```text
"A man, a plan, a canal: Panama"
```

should return:

```text
true
```

One approach is to use two pointers and skip non-alphanumeric characters.

```java
public static boolean isPalindrome(String str) {

    if (str == null) {
        return false;
    }

    int left = 0;
    int right = str.length() - 1;

    while (left < right) {

        while (left < right && !Character.isLetterOrDigit(str.charAt(left))) {
            left++;
        }

        while (left < right && !Character.isLetterOrDigit(str.charAt(right))) {
            right--;
        }

        if (Character.toLowerCase(str.charAt(left))
                != Character.toLowerCase(str.charAt(right))) {

            return false;
        }

        left++;
        right--;
    }

    return true;
}
```

This avoids creating a cleaned-up copy of the String.

---

# 🧪 Examples

| Input | Result |
|---|---|
| `"madam"` | `true` |
| `"racecar"` | `true` |
| `"level"` | `true` |
| `"hello"` | `false` |
| `"Java"` | `false` |
| `"a"` | `true` |
| `""` | `true` |

For the standard definition, an empty String is generally considered a palindrome because it reads the same forwards and backwards.

---

# ⚠️ Edge Cases

### `null`

There is no String to evaluate.

A practical implementation can return:

```java
false
```

or throw an exception depending on the API contract.

### Empty String

```text
"" → true
```

### Single Character

```text
"a" → true
```

Any single character reads the same in both directions.

### Even Length

Example:

```text
"abba"
```

Comparison:

```text
a == a
b == b
```

Result:

```text
true
```

### Odd Length

Example:

```text
"madam"
```

The middle character doesn't need to be compared with anything.

---

# 🧠 Important Interview Follow-Ups

### 1. What is the time complexity?

```text
O(n)
```

At most, approximately half of the characters are compared, which is still O(n).

---

### 2. What is the space complexity of the two-pointer solution?

```text
O(1)
```

No additional data structure proportional to input size is required.

---

### 3. Why don't we compare every character?

Because once:

```text
str[left] != str[right]
```

is found, the String cannot be a palindrome.

Therefore we immediately return:

```java
false;
```

---

### 4. Can we use `StringBuilder.reverse()`?

Technically yes:

```java
return str.equals(new StringBuilder(str).reverse().toString());
```

But if the interviewer specifically asks:

> "Write the logic yourself."

then avoid it because the purpose is usually to test your understanding of the algorithm.

---

### 5. Is palindrome checking case-sensitive?

It depends on the requirement.

Standard String comparison:

```text
"Madam" != "madam"
```

If the requirement is case-insensitive, normalize or compare characters ignoring case.

---

# ⚠️ Common Interview Mistakes

### ❌ Mistake 1 — Using `==`

Wrong:

```java
str == reversed
```

`==` compares object references.

Use:

```java
str.equals(reversed)
```

for String content comparison.

---

### ❌ Mistake 2 — Forgetting `null`

If the method can receive null:

```java
str.length()
```

will throw:

```text
NullPointerException
```

---

### ❌ Mistake 3 — Checking the Entire String Twice

You don't need:

```text
first half
+
second half
```

The two-pointer approach naturally stops at the middle.

---

### ❌ Mistake 4 — Not Clarifying Requirements

Ask or state whether the comparison should:

```text
Ignore case?
Ignore spaces?
Ignore punctuation?
Handle Unicode?
```

The correct implementation depends on the requirement.

---

# 🎯 Best Interview Solution

For a standard coding interview, use:

```java
public static boolean isPalindrome(String str) {

    if (str == null) {
        return false;
    }

    int left = 0;
    int right = str.length() - 1;

    while (left < right) {

        if (str.charAt(left) != str.charAt(right)) {
            return false;
        }

        left++;
        right--;
    }

    return true;
}
```

It is:

```text
Simple
Efficient
No extra String
No built-in reverse
O(n) time
O(1) space
```

---

# 🎤 3-Minute Interview Explanation

"To check whether a String is a palindrome, I would use a two-pointer approach. I initialize one pointer at the beginning of the String and another at the end. Then I compare the characters at both positions. If they are different, I immediately return false because the String cannot be a palindrome. If they match, I move the left pointer forward and the right pointer backward and continue until the pointers meet.

For example, for 'madam', I compare 'm' with 'm', then 'a' with 'a', and the pointers eventually meet at the middle 'd'. Therefore the String is a palindrome.

This approach takes O(n) time and O(1) additional space because we don't create another String or array. If the requirement is case-insensitive or requires ignoring spaces and punctuation, I can modify the same two-pointer approach by normalizing or skipping those characters.

An alternative is to reverse the String and compare it with the original, but that requires additional O(n) space. Therefore, for an interview where I need to demonstrate the algorithm, I would prefer the two-pointer solution."

---

# ⏱️ 60-Second Interview Answer

"I would check a palindrome using two pointers. One starts at index zero and the other at the last index. I compare both characters; if they don't match, I immediately return false. If they match, I move the left pointer forward and the right pointer backward until they meet. If no mismatch is found, the String is a palindrome. This takes O(n) time and O(1) additional space. An alternative is to reverse the String and compare it with the original, but that requires O(n) additional space. If the requirement is case-insensitive or spaces and punctuation should be ignored, I can modify the two-pointer logic accordingly."

---

# 📝 Quick Revision Notes

```text
Palindrome:
    Same forward and backward

Best approach:
    Two pointers

left  → 0
right → length - 1

while left < right:
    compare characters
    mismatch → false
    left++
    right--

No mismatch:
    true

Time  → O(n)
Space → O(1)
```

### Golden Rule

> **Compare characters from both ends and move toward the center; the first mismatch proves that the String is not a palindrome.**

---

[Q33. Write a code to check if a String is a Palindrome. [Answered]](#q33-write-a-code-to-check-if-a-string-is-a-palindrome-answered)

[⬆ Back to Question Index](#question-index)

---

# Q45. Find the 'n-th' highest in array. [Answered]

- [Q45. Find the 'n-th' highest in array. [Answered]](#q45-find-the-n-th-highest-in-array-answered)

**Priority:** P1

---

# 📌 One-Line Interview Answer

To find the `n-th` highest element, I can either sort the array and select the required position, or use a `min-heap` of size `n` to achieve better performance when `n` is much smaller than the array size.

---

# 💻 Approach 1 — Sorting

The simplest approach is to sort the array in ascending order and access:

```text
array[length - n]
```

### Java Code

```java
import java.util.Arrays;

public class NthHighest {

    public static int findNthHighest(int[] arr, int n) {

        if (arr == null || arr.length == 0) {
            throw new IllegalArgumentException("Array cannot be empty");
        }

        if (n <= 0 || n > arr.length) {
            throw new IllegalArgumentException("Invalid value of n");
        }

        Arrays.sort(arr);

        return arr[arr.length - n];
    }

    public static void main(String[] args) {

        int[] arr = {10, 40, 20, 50, 30};
        int n = 2;

        System.out.println(findNthHighest(arr, n));
    }
}
```

### Output

```text
40
```

Because after sorting:

```text
[10, 20, 30, 40, 50]
```

The:

```text
1st highest → 50
2nd highest → 40
3rd highest → 30
```

Therefore:

```text
2nd highest = 40
```

---

# 📖 How Does the Index Work?

After sorting in ascending order:

```text
[10, 20, 30, 40, 50]
 0   1   2   3   4
```

For `n = 1`:

```text
index = length - n
      = 5 - 1
      = 4

arr[4] = 50
```

For `n = 2`:

```text
index = 5 - 2
      = 3

arr[3] = 40
```

Therefore:

```java
arr[arr.length - n]
```

gives the `n-th` highest element.

---

# ⚠️ Important Clarification — What About Duplicates?

This is one of the most important interview follow-ups.

Consider:

```text
[10, 20, 30, 30, 40, 50]
```

If we ask for the:

```text
2nd highest
```

There are two possible interpretations.

### Interpretation 1 — Position-based

Sorted:

```text
[10, 20, 30, 30, 40, 50]
```

Highest:

```text
50
```

2nd highest:

```text
40
```

### Interpretation 2 — Distinct values

Distinct values:

```text
[10, 20, 30, 40, 50]
```

2nd highest:

```text
40
```

These happen to give the same result here.

But consider:

```text
[50, 50, 40, 30]
```

Position-based:

```text
1st → 50
2nd → 50
```

Distinct:

```text
1st → 50
2nd → 40
```

Therefore, in an interview, clarify:

> "Should duplicate values count separately, or are we looking for the n-th distinct highest value?"

---

# 💻 Approach 2 — N-th Highest Distinct Value

If duplicates should not count, we can use a `TreeSet`.

```java
import java.util.TreeSet;

public class NthHighestDistinct {

    public static int findNthHighest(int[] arr, int n) {

        if (arr == null || arr.length == 0) {
            throw new IllegalArgumentException("Array cannot be empty");
        }

        if (n <= 0) {
            throw new IllegalArgumentException("n must be positive");
        }

        TreeSet<Integer> set = new TreeSet<>();

        for (int num : arr) {
            set.add(num);
        }

        if (n > set.size()) {
            throw new IllegalArgumentException(
                    "Not enough distinct elements"
            );
        }

        while (n-- > 1) {
            set.pollLast();
        }

        return set.last();
    }

    public static void main(String[] args) {

        int[] arr = {50, 50, 40, 30, 20};
        int n = 2;

        System.out.println(findNthHighest(arr, n));
    }
}
```

### Output

```text
40
```

The `TreeSet` automatically removes duplicates.

---

# 💻 Approach 3 — Min-Heap

For a large array, sorting the entire array may be unnecessary.

If:

```text
array size = 1,000,000
n = 3
```

we only need to keep track of the top 3 elements.

A `PriorityQueue` can be used as a **min-heap** of size `n`.

### Java Code

```java
import java.util.PriorityQueue;

public class NthHighest {

    public static int findNthHighest(int[] arr, int n) {

        if (arr == null || arr.length == 0) {
            throw new IllegalArgumentException("Array cannot be empty");
        }

        if (n <= 0 || n > arr.length) {
            throw new IllegalArgumentException("Invalid value of n");
        }

        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        for (int num : arr) {

            minHeap.offer(num);

            if (minHeap.size() > n) {
                minHeap.poll();
            }
        }

        return minHeap.peek();
    }

    public static void main(String[] args) {

        int[] arr = {10, 40, 20, 50, 30};
        int n = 2;

        System.out.println(findNthHighest(arr, n));
    }
}
```

### Output

```text
40
```

---

# 🔍 How Does the Min-Heap Work?

For:

```text
arr = [10, 40, 20, 50, 30]
n = 2
```

We maintain only the top 2 elements.

### Add `10`

```text
[10]
```

### Add `40`

```text
[10, 40]
```

### Add `20`

Heap temporarily contains:

```text
[10, 40, 20]
```

Size is greater than `2`, so remove the smallest:

```text
[20, 40]
```

### Add `50`

```text
[20, 40, 50]
```

Remove smallest:

```text
[40, 50]
```

### Add `30`

```text
[30, 50, 40]
```

Remove smallest:

```text
[40, 50]
```

Finally:

```text
minHeap.peek() = 40
```

Therefore:

```text
2nd highest = 40
```

---

# 🎯 Why Does `minHeap.peek()` Give the N-th Highest?

We maintain exactly:

```text
Top N elements
```

inside the min-heap.

The smallest among those top `N` elements is therefore:

```text
N-th highest
```

For example:

```text
Top 3:
[70, 80, 90]
```

Minimum:

```text
70
```

Therefore:

```text
3rd highest = 70
```

---

# 📊 Complexity Comparison

| Approach | Time | Space | Best Use Case |
|---|---:|---:|---|
| Sorting | O(n log n) | O(log n) / implementation-dependent | Simple solution |
| TreeSet | O(n log n) | O(n) | Distinct values |
| Min-Heap | O(n log k) | O(k) | Large array, small k |
| Quickselect | Average O(n) | O(1) | Performance-focused |

Here, `k` represents the requested rank.

For example:

```text
array size = 1,000,000
k = 3
```

Min-heap complexity:

```text
O(n log 3)
```

which is much better than sorting the entire array:

```text
O(n log n)
```

---

# 🔥 Approach 4 — Quickselect

For a more advanced interview, **Quickselect** can find the `n-th` highest element in average:

```text
O(n)
```

time.

The idea is based on the same partitioning concept used by QuickSort.

For example:

```text
[10, 40, 20, 50, 30]
```

We partition the array around a pivot.

Instead of recursively processing both sides as QuickSort does, Quickselect only processes the side containing the required element.

Therefore:

```text
QuickSort:
    Process left + right

Quickselect:
    Process only required side
```

Average complexity:

```text
O(n)
```

Worst case:

```text
O(n²)
```

---

# 🧠 Important Interview Follow-Up — Second Highest

If the interviewer changes the question to:

> "Find the second highest element."

We don't necessarily need sorting.

We can maintain:

```text
largest
secondLargest
```

### Java Code

```java
public static int findSecondHighest(int[] arr) {

    if (arr == null || arr.length < 2) {
        throw new IllegalArgumentException(
                "At least two elements are required"
        );
    }

    int largest = Integer.MIN_VALUE;
    int secondLargest = Integer.MIN_VALUE;

    for (int num : arr) {

        if (num > largest) {
            secondLargest = largest;
            largest = num;
        } else if (num > secondLargest && num != largest) {
            secondLargest = num;
        }
    }

    if (secondLargest == Integer.MIN_VALUE) {
        throw new IllegalArgumentException(
                "No distinct second highest value"
        );
    }

    return secondLargest;
}
```

For:

```text
[10, 40, 20, 50, 30]
```

Result:

```text
40
```

This is:

```text
Time  → O(n)
Space → O(1)
```

---

# ⚠️ Common Interview Trap — `Integer.MIN_VALUE`

Using:

```java
Integer.MIN_VALUE
```

as a sentinel can create edge cases if the array itself contains `Integer.MIN_VALUE`.

A more robust implementation can track whether values have actually been found.

For example:

```java
public static Integer findSecondHighest(int[] arr) {

    if (arr == null || arr.length < 2) {
        return null;
    }

    Integer largest = null;
    Integer secondLargest = null;

    for (int num : arr) {

        if (largest == null || num > largest) {
            secondLargest = largest;
            largest = num;
        } else if (num != largest &&
                   (secondLargest == null || num > secondLargest)) {
            secondLargest = num;
        }
    }

    return secondLargest;
}
```

---

# 🧪 Edge Cases

### Empty Array

```text
[]
```

There is no `n-th` highest element.

---

### Invalid `n`

```text
n <= 0
```

should be rejected.

---

### `n > array.length`

Example:

```text
[10, 20, 30]
n = 5
```

No such element exists.

---

### All Elements Equal

```text
[50, 50, 50]
```

For distinct values:

```text
2nd highest → does not exist
```

For position-based ranking:

```text
2nd highest → 50
```

Again, clarify the requirement.

---

### Negative Numbers

The algorithm should also work with:

```text
[-10, -50, -20, -5]
```

Highest:

```text
-5
```

Second highest:

```text
-10
```

---

# 🎯 Which Approach Should You Give in an Interview?

### If interviewer asks for a simple solution:

Use sorting:

```java
Arrays.sort(arr);
return arr[arr.length - n];
```

Then immediately mention:

> "This is O(n log n). If the array is large and `n` is small, I would use a min-heap of size `n`."

### If interviewer asks for optimized solution:

Use:

```text
Min-Heap
```

Complexity:

```text
O(N log K)
```

where:

```text
N = number of elements
K = requested rank
```

### If interviewer asks for the most optimal algorithmic solution:

Discuss:

```text
Quickselect
```

Average:

```text
O(N)
```

---

# ⚠️ Common Interview Mistakes

### ❌ Mistake 1 — Not clarifying duplicates

Always ask:

> "Should duplicate values count toward the rank?"

---

### ❌ Mistake 2 — Sorting unnecessarily

Sorting is easy, but:

```text
O(N log N)
```

may be unnecessary when:

```text
K << N
```

A heap can do:

```text
O(N log K)
```

---

### ❌ Mistake 3 — Using a max-heap

For `K-th largest`, a:

```text
min-heap of size K
```

is usually the appropriate heap.

For `K-th smallest`, use:

```text
max-heap of size K
```

---

### ❌ Mistake 4 — Forgetting invalid `n`

Handle:

```text
n <= 0
n > array.length
```

---

### ❌ Mistake 5 — Assuming "n-th highest" always means distinct

Clarify the requirement.

---

# 🎤 3-Minute Interview Explanation

"To find the n-th highest element, the simplest approach is to sort the array in ascending order and return the element at index length minus n. For example, after sorting [10, 40, 20, 50, 30], we get [10, 20, 30, 40, 50], so the second highest is at index 5 minus 2, which is 3, giving 40. The time complexity is O(N log N).

However, if the array is very large and n is relatively small, sorting the entire array is unnecessary. I would use a min-heap of size n. I iterate through the array, add each element to the heap, and whenever the heap size exceeds n, I remove the smallest element. At the end, the heap contains the n largest elements, and the smallest among them is the n-th largest. This gives O(N log N) for sorting versus O(N log K) for the heap, where K is n, and uses O(K) space.

For a performance-focused problem, I can also use Quickselect, which has average O(N) time. Before implementing, I would clarify whether duplicate values should count or whether the interviewer wants the n-th distinct highest value."

---

# ⏱️ 60-Second Interview Answer

"The simplest solution is to sort the array and return `arr[arr.length - n]`, which takes O(N log N). If the array is large and n is small, I would prefer a min-heap of size n. For every element, I add it to the heap and remove the smallest element whenever the heap size exceeds n. At the end, the heap contains the n largest elements, so its minimum is the n-th highest. This takes O(N log K) time and O(K) space, where K is n. For an advanced solution, Quickselect can achieve average O(N). I would also clarify whether duplicates should count toward the ranking."

---

# 📝 Quick Revision Notes

```text
Question:
    Find N-th highest

Simple:
    Sort
    index = length - n

Sorting:
    Time  → O(N log N)
    Space → implementation dependent

Optimized for small N-th:
    Min-Heap of size K

Heap:
    Time  → O(N log K)
    Space → O(K)

Advanced:
    Quickselect
    Average → O(N)
    Worst   → O(N²)

Important:
    Clarify duplicates
    Validate n
```

### Golden Rule

> **For a simple solution, sort the array; for a large array with a small `n`, maintain a min-heap of size `n`; for an advanced optimal-average solution, consider Quickselect.**

---

[Q45. Find the 'n-th' highest in array. [Answered]](#q45-find-the-n-th-highest-in-array-answered)

[⬆ Back to Question Index](#question-index)

---

# Q61. Code to find the smallest element present in Array A but not in B (return -1 if not present). [Answered]

- [Q61. Code to find the smallest element present in Array A but not in B (return -1 if not present). [Answered]](#q61-code-to-find-the-smallest-element-present-in-array-a-but-not-in-b-return-1-if-not-present-answered)

**Priority:** P2

---

# 📌 One-Line Interview Answer

We can put all elements of Array B into a `HashSet`, then iterate through Array A and keep track of the smallest element that is not present in B.

---

# 💻 Approach 1 — Using HashSet

```java
import java.util.HashSet;
import java.util.Set;

public class SmallestElementNotInB {

    public static int findSmallest(int[] a, int[] b) {

        if (a == null || b == null) {
            return -1;
        }

        Set<Integer> setB = new HashSet<>();

        for (int num : b) {
            setB.add(num);
        }

        Integer smallest = null;

        for (int num : a) {

            if (!setB.contains(num)) {

                if (smallest == null || num < smallest) {
                    smallest = num;
                }
            }
        }

        return smallest == null ? -1 : smallest;
    }

    public static void main(String[] args) {

        int[] a = {10, 5, 8, 3, 7};
        int[] b = {8, 10, 7};

        System.out.println(findSmallest(a, b));
    }
}
```

### Output

```text
3
```

---

# 📖 How Does It Work?

Given:

```text
A = [10, 5, 8, 3, 7]

B = [8, 10, 7]
```

First, put all elements of B into a `HashSet`:

```text
B Set = {8, 10, 7}
```

Now iterate through A:

```text
10 → present in B → ignore
5  → not present   → candidate
8  → present in B → ignore
3  → not present   → smaller candidate
7  → present in B → ignore
```

Therefore:

```text
Smallest element present in A but not B = 3
```

---

# 🔍 Algorithm

```text
Array A
   ↓
Iterate through B
   ↓
Store B elements in HashSet
   ↓
Iterate through A
   ↓
Is element present in B?
      |
   +--+--+
   |     |
  Yes    No
   |     |
 Ignore  Compare with smallest
         |
         ↓
       Return smallest
```

If no element from A is absent in B:

```text
return -1
```

---

# 💻 Approach 2 — Without HashSet

If the interviewer specifically asks:

> "Can you solve it without using extra space?"

We can use nested loops.

```java
public static int findSmallest(int[] a, int[] b) {

    if (a == null || b == null) {
        return -1;
    }

    Integer smallest = null;

    for (int x : a) {

        boolean found = false;

        for (int y : b) {

            if (x == y) {
                found = true;
                break;
            }
        }

        if (!found && (smallest == null || x < smallest)) {
            smallest = x;
        }
    }

    return smallest == null ? -1 : smallest;
}
```

This requires no additional data structure.

However, its time complexity is worse.

---

# 📊 Complexity Comparison

### HashSet Approach

Building the set:

```text
O(M)
```

Searching all elements of A:

```text
O(N)
```

Overall average:

```text
O(N + M)
```

Space:

```text
O(M)
```

where:

```text
N = size of A
M = size of B
```

---

### Nested Loop Approach

For every element of A, we potentially scan all of B:

```text
O(N × M)
```

Space:

```text
O(1)
```

Therefore:

```text
HashSet:
    O(N + M) time
    O(M) space

Nested loop:
    O(N × M) time
    O(1) space
```

---

# 🔥 Approach 3 — Sorting + Two Pointers

If modifying the arrays is allowed, another approach is to sort both arrays and use two pointers.

For example:

```text
A = [3, 5, 7, 8, 10]
B = [7, 8, 10]
```

We compare elements systematically.

### Java Code

```java
import java.util.Arrays;

public class SmallestElementNotInB {

    public static int findSmallest(int[] a, int[] b) {

        if (a == null || b == null || a.length == 0) {
            return -1;
        }

        Arrays.sort(a);
        Arrays.sort(b);

        int i = 0;
        int j = 0;

        while (i < a.length) {

            if (j >= b.length) {
                return a[i];
            }

            if (a[i] < b[j]) {
                return a[i];
            }

            if (a[i] == b[j]) {
                i++;
                j++;
            } else {
                j++;
            }
        }

        return -1;
    }
}
```

Because A is sorted, the **first element we find that isn't in B is automatically the smallest valid element**.

---

# ⚠️ Duplicate Values

Suppose:

```text
A = [2, 2, 3, 4]
B = [2, 4]
```

The answer is:

```text
3
```

because the value `2` exists in B, so all occurrences of `2` in A are excluded.

The HashSet approach handles this naturally because we are checking **value membership**, not occurrence counts.

---

# 🧠 Important Interview Clarification

There is a subtle difference between:

> "Present in A but not in B"

and:

> "Present more times in A than in B."

This question normally means **set membership**.

Example:

```text
A = [2, 2, 3]
B = [2]
```

Under set-membership interpretation:

```text
2 is present in B
3 is not present in B

Answer = 3
```

We do **not** return `2` just because A contains it twice.

If the interviewer means multiset difference, the solution would be different and would require frequency counting.

---

# ⚠️ Negative Numbers

The solution also works with negative values.

Example:

```text
A = [-10, -5, 2, 8]
B = [-5, 8]
```

Candidates:

```text
-10
2
```

Smallest:

```text
-10
```

Result:

```text
-10
```

This is another reason to avoid initializing:

```java
int smallest = 0;
```

because `0` may not actually exist in A and would produce incorrect results for positive or negative inputs.

Using:

```java
Integer smallest = null;
```

avoids that problem.

---

# ⚠️ Why Not Use `Integer.MAX_VALUE`?

You could write:

```java
int smallest = Integer.MAX_VALUE;
```

and later:

```java
return smallest == Integer.MAX_VALUE ? -1 : smallest;
```

But this has an edge case if:

```text
A contains Integer.MAX_VALUE
```

Using a nullable `Integer` or a separate boolean flag is safer.

---

# 🎯 Best Interview Solution

For most interviews, use the `HashSet` solution:

```java
public static int findSmallest(int[] a, int[] b) {

    Set<Integer> setB = new HashSet<>();

    for (int num : b) {
        setB.add(num);
    }

    Integer smallest = null;

    for (int num : a) {

        if (!setB.contains(num)) {

            if (smallest == null || num < smallest) {
                smallest = num;
            }
        }
    }

    return smallest == null ? -1 : smallest;
}
```

It is:

```text
Simple
Efficient
Easy to explain
Handles duplicates
Works with negative numbers
Average O(N + M)
```

---

# 🎤 3-Minute Interview Explanation

"To find the smallest element present in Array A but not in Array B, I would first store all elements of B in a HashSet. This gives average O(1) lookup time. Then I iterate through A and check whether each element exists in the set. If it doesn't exist, it is a candidate. I maintain a variable containing the smallest candidate found so far. After processing all elements, I return that value, or -1 if no such element exists.

For example, if A is [10, 5, 8, 3, 7] and B is [8, 10, 7], the set contains 8, 10 and 7. While scanning A, 10 and 8 and 7 are ignored, while 5 and 3 are candidates. Since 3 is smaller, the result is 3.

The time complexity is O(N + M) on average, where N is the size of A and M is the size of B, and the additional space is O(M) for the HashSet.

If extra space isn't allowed, I could use a nested-loop solution with O(N × M) time, or sort both arrays and use two pointers if modifying the arrays is acceptable."

---

# ⏱️ 60-Second Interview Answer

"I would put all elements of Array B into a HashSet and then iterate through Array A. For every element in A, I check whether it exists in the HashSet. If it doesn't, I compare it with the smallest candidate found so far. At the end, I return the smallest candidate, or -1 if no candidate exists. The average time complexity is O(N + M) and the space complexity is O(M). This also naturally handles duplicates because the question is based on whether a value exists in B. If extra space isn't allowed, I could use nested loops at O(N × M) or sort both arrays and use two pointers."

---

# 📝 Quick Revision Notes

```text
Goal:
    Smallest element in A
    that does NOT exist in B

Best general approach:
    HashSet

Steps:
    1. Add B elements to HashSet
    2. Iterate through A
    3. If A element not in Set:
           update smallest
    4. If no candidate:
           return -1

Time:
    O(N + M) average

Space:
    O(M)

Important:
    - Handle null/empty arrays
    - Handle duplicates
    - Handle negative values
    - Don't initialize smallest to 0
    - Clarify set vs frequency interpretation
```

### Golden Rule

> **Use a `HashSet` for fast membership checking and maintain the smallest qualifying element while scanning Array A.**

---

[Q61. Code to find the smallest element present in Array A but not in B (return -1 if not present). [Answered]](#q61-code-to-find-the-smallest-element-present-in-array-a-but-not-in-b-return-1-if-not-present-answered)

[⬆ Back to Question Index](#question-index)

---

# Q68. Count occurrences of each character in a string. [Answered]

- [Q68. Count occurrences of each character in a string. [Answered]](#q68-count-occurrences-of-each-character-in-a-string-answered)

**Priority:** P1

---

# 📌 One-Line Interview Answer

We can count character occurrences by using a `HashMap<Character, Integer>`, where each character is stored as a key and its occurrence count as the value.

---

# 💻 Java Code — Using HashMap

```java
import java.util.HashMap;
import java.util.Map;

public class CharacterCount {

    public static Map<Character, Integer> countCharacters(String str) {

        Map<Character, Integer> frequencyMap = new HashMap<>();

        if (str == null) {
            return frequencyMap;
        }

        for (char ch : str.toCharArray()) {
            frequencyMap.put(
                ch,
                frequencyMap.getOrDefault(ch, 0) + 1
            );
        }

        return frequencyMap;
    }

    public static void main(String[] args) {

        String str = "programming";

        Map<Character, Integer> result = countCharacters(str);

        System.out.println(result);
    }
}
```

### Example Output

The order of a `HashMap` is not guaranteed, so the output order may vary:

```text
{p=1, r=2, o=1, g=2, a=1, m=2, i=1, n=1}
```

---

# 📖 How Does It Work?

For:

```text
programming
```

we process one character at a time.

Initially:

```text
{}
```

After processing:

```text
p → {p=1}

r → {p=1, r=1}

o → {p=1, r=1, o=1}

g → {p=1, r=1, o=1, g=1}

r → {p=1, r=2, o=1, g=1}

...
```

For every character:

```java
frequencyMap.getOrDefault(ch, 0) + 1
```

means:

```text
If character exists:
    get its current count and increment it

If character doesn't exist:
    use 0 and increment to 1
```

---

# 🔍 Understanding `getOrDefault()`

This:

```java
frequencyMap.put(
    ch,
    frequencyMap.getOrDefault(ch, 0) + 1
);
```

is equivalent to:

```java
if (frequencyMap.containsKey(ch)) {
    frequencyMap.put(ch, frequencyMap.get(ch) + 1);
} else {
    frequencyMap.put(ch, 1);
}
```

`getOrDefault()` simply makes the code shorter and cleaner.

---

# 💻 Alternative — Using `merge()`

Java provides another elegant approach:

```java
public static Map<Character, Integer> countCharacters(String str) {

    Map<Character, Integer> frequencyMap = new HashMap<>();

    if (str == null) {
        return frequencyMap;
    }

    for (char ch : str.toCharArray()) {
        frequencyMap.merge(ch, 1, Integer::sum);
    }

    return frequencyMap;
}
```

Here:

```java
frequencyMap.merge(ch, 1, Integer::sum);
```

means:

```text
If key doesn't exist:
    insert 1

If key exists:
    add 1 to existing value
```

---

# 💻 Alternative — Using an Array

If the input is guaranteed to contain only standard ASCII characters, a `HashMap` is not strictly necessary.

We can use an array of size `256`:

```java
public static void countCharacters(String str) {

    int[] frequency = new int[256];

    for (char ch : str.toCharArray()) {
        frequency[ch]++;
    }

    for (int i = 0; i < frequency.length; i++) {

        if (frequency[i] > 0) {
            System.out.println(
                (char) i + " = " + frequency[i]
            );
        }
    }
}
```

For:

```text
"hello"
```

Output:

```text
h = 1
e = 1
l = 2
o = 1
```

---

# ⚖️ HashMap vs Array

| Approach | Time | Space | Best Use Case |
|---|---:|---:|---|
| `HashMap<Character, Integer>` | O(n) average | O(k) | General solution |
| Frequency array | O(n) | O(1) fixed size | Known character set |
| `TreeMap<Character, Integer>` | O(n log k) | O(k) | Sorted character output |

Where:

```text
n = length of String
k = number of distinct characters
```

For a normal interview, the `HashMap` solution is usually the safest answer because it works with a broad range of characters.

---

# 🔥 If Output Must Be in Alphabetical Order

A `HashMap` does not guarantee ordering.

If the interviewer asks:

> "Print the characters in sorted order."

Use `TreeMap`:

```java
import java.util.Map;
import java.util.TreeMap;

public static Map<Character, Integer> countCharacters(String str) {

    Map<Character, Integer> frequencyMap = new TreeMap<>();

    for (char ch : str.toCharArray()) {
        frequencyMap.put(
            ch,
            frequencyMap.getOrDefault(ch, 0) + 1
        );
    }

    return frequencyMap;
}
```

For:

```text
"banana"
```

the output will be ordered:

```text
{a=3, b=1, n=2}
```

---

# 🔥 If Case Should Be Ignored

Suppose:

```text
"JavaJAVA"
```

should treat:

```text
J == j
A == a
V == v
```

Then normalize the input:

```java
String str = input.toLowerCase();
```

Example:

```java
public static Map<Character, Integer> countCharacters(String str) {

    Map<Character, Integer> frequencyMap = new HashMap<>();

    if (str == null) {
        return frequencyMap;
    }

    for (char ch : str.toLowerCase().toCharArray()) {
        frequencyMap.put(
            ch,
            frequencyMap.getOrDefault(ch, 0) + 1
        );
    }

    return frequencyMap;
}
```

---

# 🔥 If Spaces Should Be Ignored

For:

```text
"hello world"
```

if spaces shouldn't be counted:

```java
for (char ch : str.toCharArray()) {

    if (ch == ' ') {
        continue;
    }

    frequencyMap.put(
        ch,
        frequencyMap.getOrDefault(ch, 0) + 1
    );
}
```

Similarly, you can define whether punctuation should be counted.

---

# ⚠️ Important Interview Question — Character vs Code Point

For basic Java interviews, this is usually sufficient:

```java
char
```

However, Java `char` represents a UTF-16 code unit, not necessarily a complete Unicode character.

Some Unicode characters require a **surrogate pair**, meaning they occupy two `char` values.

For full Unicode-aware processing, use code points:

```java
Map<Integer, Integer> frequencyMap = new HashMap<>();

str.codePoints().forEach(
    cp -> frequencyMap.merge(cp, 1, Integer::sum)
);
```

This is a useful senior-level discussion point.

---

# 🧠 Important Interview Follow-Ups

### 1. Why use HashMap?

Because we need:

```text
character → frequency
```

which naturally maps to:

```text
Map<Character, Integer>
```

Average lookup and insertion are:

```text
O(1)
```

---

### 2. What happens if the same character appears again?

Its existing count is incremented:

```java
getOrDefault(ch, 0) + 1
```

---

### 3. Can we use `TreeMap`?

Yes.

`TreeMap` maintains keys in sorted order, but operations are:

```text
O(log k)
```

instead of average O(1) with `HashMap`.

---

### 4. Can we solve it without HashMap?

Yes, if the character set is known and bounded.

For example:

```java
int[] frequency = new int[256];
```

---

### 5. What is the space complexity?

For a `HashMap`:

```text
O(k)
```

where `k` is the number of distinct characters.

In the worst case:

```text
k = n
```

so space can be:

```text
O(n)
```

---

# ⚠️ Common Interview Traps

### ❌ Trap 1 — Using `HashSet`

A `HashSet` only tells us whether a character exists.

It doesn't naturally store:

```text
character → count
```

Therefore, use:

```java
HashMap<Character, Integer>
```

---

### ❌ Trap 2 — Assuming HashMap maintains order

It does not guarantee iteration order.

If order matters, use:

```text
LinkedHashMap → insertion order
TreeMap       → sorted order
```

---

### ❌ Trap 3 — Ignoring case requirements

These are different characters:

```text
'A'
'a'
```

unless the requirement says the comparison is case-insensitive.

---

# 🎯 Best Interview Solution

For a general character-frequency problem, use:

```java
public static Map<Character, Integer> countCharacters(String str) {

    Map<Character, Integer> map = new HashMap<>();

    for (char ch : str.toCharArray()) {
        map.put(ch, map.getOrDefault(ch, 0) + 1);
    }

    return map;
}
```

This is concise, readable and demonstrates proper use of the Java Collections Framework.

---

# 🎤 3-Minute Interview Explanation

"To count the occurrences of each character, I would use a HashMap where the character is the key and its frequency is the value. I iterate through the String character by character. For every character, I retrieve its current count using getOrDefault and increment it. If the character hasn't been seen before, getOrDefault returns zero, so its first occurrence gets a count of one.

The average time complexity is O(n), where n is the length of the String, because HashMap insertion and lookup are O(1) on average. The space complexity is O(k), where k is the number of distinct characters.

If the character set is fixed, such as ASCII, I could use a frequency array instead of a HashMap. If the output needs to be sorted, I could use a TreeMap. I would also clarify whether spaces, punctuation and character case should be considered."

---

# ⏱️ 60-Second Interview Answer

"I would use a HashMap<Character, Integer>, where each character is the key and its occurrence count is the value. I iterate through the String and update the count using `getOrDefault(ch, 0) + 1`. This gives O(n) average time and O(k) space, where k is the number of distinct characters. If the character set is fixed, I could use a frequency array for better constant-factor performance. If sorted output is required, I would use a TreeMap."

---

# 📝 Quick Revision Notes

```text
Goal:
    Count every character

Best general approach:
    HashMap<Character, Integer>

Logic:
    for each character:
        map.put(
            ch,
            map.getOrDefault(ch, 0) + 1
        )

Time:
    O(n) average

Space:
    O(k)

Alternatives:
    int[]       → fixed character set
    TreeMap     → sorted output
    LinkedHashMap → insertion order

Clarify:
    Case sensitivity?
    Spaces?
    Punctuation?
    Unicode?
```

### Golden Rule

> **Use a `HashMap<Character, Integer>` to map each character to its frequency, giving O(n) average time and O(k) space for k distinct characters.**

---

[Q68. Count occurrences of each character in a string. [Answered]](#q68-count-occurrences-of-each-character-in-a-string-answered)

[⬆ Back to Question Index](#question-index)

---

# Q78. Second Max in array. [Answered]

- [Q78. Second Max in array. [Answered]](#q78-second-max-in-array-answered)

**Priority:** P1

---

# 📌 One-Line Interview Answer

We can find the second maximum element in a single pass by maintaining two variables, `max` and `secondMax`, giving **O(n) time and O(1) space**.

---

# 💻 Best Approach — Single Pass

```java
public class SecondMax {

    public static int findSecondMax(int[] arr) {

        if (arr == null || arr.length < 2) {
            throw new IllegalArgumentException(
                    "Array must contain at least two elements"
            );
        }

        int max = Integer.MIN_VALUE;
        int secondMax = Integer.MIN_VALUE;

        for (int num : arr) {

            if (num > max) {
                secondMax = max;
                max = num;
            } else if (num > secondMax && num != max) {
                secondMax = num;
            }
        }

        if (secondMax == Integer.MIN_VALUE) {
            throw new IllegalArgumentException(
                    "No distinct second maximum exists"
            );
        }

        return secondMax;
    }

    public static void main(String[] args) {

        int[] arr = {10, 40, 20, 50, 30};

        System.out.println(findSecondMax(arr));
    }
}
```

### Output

```text
40
```

---

# 📖 How Does It Work?

Given:

```text
[10, 40, 20, 50, 30]
```

We maintain:

```text
max
secondMax
```

Initially:

```text
max        = -∞
secondMax  = -∞
```

### Process `10`

```text
max       = 10
secondMax = -∞
```

### Process `40`

`40 > max`

```text
secondMax = 10
max       = 40
```

### Process `20`

```text
20 < 40
20 > 10
```

So:

```text
secondMax = 20
max       = 40
```

### Process `50`

`50 > 40`

```text
secondMax = 40
max       = 50
```

### Process `30`

```text
30 < 50
30 < 40
```

No change.

Final:

```text
max       = 50
secondMax = 40
```

Therefore:

```text
Second maximum = 40
```

---

# 🔍 Core Logic

The important part is:

```java
if (num > max) {
    secondMax = max;
    max = num;
}
```

Whenever a new maximum is found, the **old maximum automatically becomes the second maximum**.

Otherwise:

```java
else if (num > secondMax && num != max) {
    secondMax = num;
}
```

The second maximum is updated when the current number lies between:

```text
secondMax < num < max
```

---

# ⚠️ Why `num != max`?

Consider:

```text
[50, 50, 40]
```

If duplicates are not supposed to count, the second maximum is:

```text
40
```

not:

```text
50
```

Therefore:

```java
num != max
```

prevents the same maximum value from becoming the second maximum.

---

# 🧠 Important Clarification — What Does "Second Max" Mean?

This question can have two interpretations.

### 1. Second distinct maximum

```text
[50, 50, 40, 30]
```

Result:

```text
40
```

This is the interpretation normally expected in coding interviews.

### 2. Second element after sorting

```text
[50, 50, 40, 30]
```

Sorted descending:

```text
[50, 50, 40, 30]
```

Result:

```text
50
```

Therefore, clarify:

> "Should duplicate maximum values count, or are we looking for the second distinct maximum?"

---

# 💻 Alternative — Sorting

A simple solution is to sort the array.

```java
import java.util.Arrays;

public static int findSecondMax(int[] arr) {

    Arrays.sort(arr);

    for (int i = arr.length - 2; i >= 0; i--) {

        if (arr[i] != arr[arr.length - 1]) {
            return arr[i];
        }
    }

    throw new IllegalArgumentException(
            "No distinct second maximum exists"
    );
}
```

For:

```text
[10, 40, 20, 50, 30]
```

After sorting:

```text
[10, 20, 30, 40, 50]
```

Second maximum:

```text
40
```

### Complexity

```text
Time  → O(n log n)
Space → depends on sorting implementation
```

This works, but is less efficient than the single-pass approach.

---

# 💻 Alternative — Using a `TreeSet`

If we want distinct values automatically:

```java
import java.util.TreeSet;

public static int findSecondMax(int[] arr) {

    TreeSet<Integer> set = new TreeSet<>();

    for (int num : arr) {
        set.add(num);
    }

    if (set.size() < 2) {
        throw new IllegalArgumentException(
                "No distinct second maximum exists"
        );
    }

    set.pollLast();

    return set.last();
}
```

`TreeSet` stores values in sorted order and removes duplicates.

For:

```text
[50, 50, 40, 30]
```

the set becomes:

```text
[30, 40, 50]
```

Remove the maximum:

```text
[30, 40]
```

Then:

```text
last() = 40
```

### Complexity

```text
Time  → O(n log n)
Space → O(n)
```

---

# ⚠️ Edge Cases

### 1. Less than two elements

```text
[10]
```

No second maximum exists.

---

### 2. All elements are equal

```text
[50, 50, 50]
```

No **distinct** second maximum exists.

---

### 3. Negative numbers

```text
[-10, -30, -5, -20]
```

Result:

```text
-10
```

The algorithm works with negative numbers.

---

### 4. Two elements

```text
[10, 20]
```

Result:

```text
10
```

---

### 5. `Integer.MIN_VALUE`

A common implementation using:

```java
Integer.MIN_VALUE
```

as the initial value has a subtle edge case.

For example:

```text
[Integer.MIN_VALUE, 10, Integer.MIN_VALUE]
```

Using `Integer.MIN_VALUE` as a sentinel makes it difficult to distinguish:

```text
"second maximum hasn't been found"
```

from:

```text
"second maximum is actually Integer.MIN_VALUE"
```

A more robust implementation uses boolean flags or nullable `Integer` values.

---

# 💻 Robust Version

```java
public static Integer findSecondMax(int[] arr) {

    if (arr == null || arr.length < 2) {
        return null;
    }

    Integer max = null;
    Integer secondMax = null;

    for (int num : arr) {

        if (max == null || num > max) {

            secondMax = max;
            max = num;

        } else if (num != max &&
                   (secondMax == null || num > secondMax)) {

            secondMax = num;
        }
    }

    return secondMax;
}
```

This correctly handles:

```text
Integer.MIN_VALUE
negative values
duplicates
```

---

# 📊 Complexity Comparison

| Approach | Time | Space | Recommendation |
|---|---:|---:|---|
| Single pass | **O(n)** | **O(1)** | ⭐ Best |
| Sorting | O(n log n) | Depends | Simple |
| TreeSet | O(n log n) | O(n) | Good for distinct values |

---

# 🎯 Best Interview Solution

The preferred solution is the **single-pass approach**:

```java
int max = Integer.MIN_VALUE;
int secondMax = Integer.MIN_VALUE;

for (int num : arr) {

    if (num > max) {
        secondMax = max;
        max = num;
    } else if (num > secondMax && num != max) {
        secondMax = num;
    }
}
```

Why?

```text
One traversal
No sorting
No extra collection
O(n) time
O(1) space
```

---

# 🧠 Common Interview Follow-Ups

### 1. Can you find the second maximum without sorting?

Yes.

Use:

```text
max
secondMax
```

and scan the array once.

---

### 2. What if duplicates are present?

Clarify whether the interviewer wants:

```text
second distinct maximum
```

or:

```text
second position after sorting
```

For the distinct version, use:

```java
num != max
```

---

### 3. Can this be done in O(n)?

Yes.

A single pass is:

```text
O(n)
```

---

### 4. Can this be done with O(1) space?

Yes.

Only two variables are required:

```text
max
secondMax
```

---

### 5. What if the array contains negative numbers?

The algorithm still works, provided initialization and edge cases are handled correctly.

---

# 🎤 3-Minute Interview Explanation

"To find the second maximum distinct element, I don't need to sort the array. I can solve it in a single traversal by maintaining two variables: max and secondMax. Initially both are unset or initialized appropriately. For every element, if the element is greater than max, I move the current max into secondMax and update max. Otherwise, if the element is greater than secondMax but different from max, I update secondMax.

For example, with [10, 40, 20, 50, 30], after processing 40, max is 40 and secondMax is 10. When 50 is encountered, the previous maximum 40 becomes secondMax and 50 becomes max. The final second maximum is therefore 40.

The time complexity is O(n) because we traverse the array once, and the space complexity is O(1). I would also clarify whether duplicate maximum values should count. If the requirement is the second distinct maximum, duplicates must be ignored."

---

# ⏱️ 60-Second Interview Answer

"I would find the second distinct maximum using a single pass. I maintain `max` and `secondMax`. Whenever I find a value greater than `max`, I move the old `max` into `secondMax` and update `max`. Otherwise, if the value is greater than `secondMax` and different from `max`, I update `secondMax`. This gives O(n) time and O(1) space. I would clarify whether duplicates count, because for `[50, 50, 40]`, the second distinct maximum is 40, while position-based ranking would give 50."

---

# 📝 Quick Revision Notes

```text
Goal:
    Find second distinct maximum

Maintain:
    max
    secondMax

Logic:
    num > max:
        secondMax = max
        max = num

    num > secondMax && num != max:
        secondMax = num

Time:
    O(n)

Space:
    O(1)

Important:
    Clarify duplicates
    Handle < 2 elements
    Handle all-equal array
    Handle negative values
    Consider Integer.MIN_VALUE edge case
```

### Golden Rule

> **Track the largest and second-largest distinct values in one pass instead of sorting the entire array.**

---

[Q78. Second Max in array. [Answered]](#q78-second-max-in-array-answered)

[⬆ Back to Question Index](#question-index)

---

# Q118. Ways to iterate over `ArrayList`. [Answered]

- [Q118. Ways to iterate over `ArrayList`. [Answered]](#q118-ways-to-iterate-over-arraylist-answered)

**Priority:** P2

---

# 📌 One-Line Interview Answer

An `ArrayList` can be iterated using a traditional `for` loop, enhanced `for-each` loop, `Iterator`, `ListIterator`, `forEach()` with lambda, `Stream`, or `Spliterator`, with the choice depending on whether we need index access, modification, bidirectional traversal, or functional processing.

---

# 💻 1. Traditional `for` Loop

```java
import java.util.ArrayList;
import java.util.List;

public class ArrayListIteration {

    public static void main(String[] args) {

        List<String> names = new ArrayList<>();

        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        for (int i = 0; i < names.size(); i++) {
            System.out.println(names.get(i));
        }
    }
}
```

### Output

```text
Alice
Bob
Charlie
```

### Advantages

- Provides direct access to the index.
- Can iterate in either direction.
- Useful when we need to modify elements using their index.

### Important Performance Point

For an `ArrayList`:

```java
names.get(i)
```

is:

```text
O(1)
```

Therefore, a normal index-based loop is efficient for `ArrayList`.

---

# 💻 2. Enhanced `for-each` Loop

```java
for (String name : names) {
    System.out.println(name);
}
```

This is usually the cleanest option when we simply want to read every element.

### Advantages

- Simple and readable.
- No index management.
- Works with all `Iterable` collections.

### Limitation

You don't directly get the current index.

---

# 💻 3. Using `Iterator`

```java
Iterator<String> iterator = names.iterator();

while (iterator.hasNext()) {

    String name = iterator.next();

    System.out.println(name);
}
```

Import:

```java
import java.util.Iterator;
```

`Iterator` is particularly useful when elements need to be safely removed while iterating.

---

# 🔥 Removing Elements Using Iterator

Suppose we want to remove all names starting with `"A"`.

```java
Iterator<String> iterator = names.iterator();

while (iterator.hasNext()) {

    String name = iterator.next();

    if (name.startsWith("A")) {
        iterator.remove();
    }
}
```

This is the correct way to remove elements during iteration.

---

# ⚠️ Why Not Use `ArrayList.remove()` Directly?

This can cause:

```text
ConcurrentModificationException
```

Example:

```java
for (String name : names) {

    if (name.startsWith("A")) {
        names.remove(name);
    }
}
```

Instead, use:

```java
iterator.remove();
```

when removing during an iterator-based traversal.

---

# 💻 4. Using `ListIterator`

`ListIterator` extends the capabilities of `Iterator`.

```java
ListIterator<String> iterator = names.listIterator();

while (iterator.hasNext()) {

    String name = iterator.next();

    System.out.println(name);
}
```

Import:

```java
import java.util.ListIterator;
```

---

# 🔄 Bidirectional Iteration

Unlike `Iterator`, `ListIterator` can move both forward and backward.

```java
ListIterator<String> iterator = names.listIterator();

while (iterator.hasNext()) {
    System.out.println(iterator.next());
}

System.out.println("Reverse:");

while (iterator.hasPrevious()) {
    System.out.println(iterator.previous());
}
```

Output:

```text
Alice
Bob
Charlie

Reverse:
Charlie
Bob
Alice
```

---

# ✏️ Modifying Elements Using `ListIterator`

`ListIterator` supports:

```java
add()
remove()
set()
```

Example:

```java
ListIterator<String> iterator = names.listIterator();

while (iterator.hasNext()) {

    String name = iterator.next();

    if (name.equals("Bob")) {
        iterator.set("Robert");
    }
}
```

Now:

```text
[Alice, Robert, Charlie]
```

---

# 💻 5. Using `forEach()` with Lambda

Java 8 introduced the `forEach()` method on `Iterable`.

```java
names.forEach(name -> System.out.println(name));
```

Can also be written as a method reference:

```java
names.forEach(System.out::println);
```

This is concise and commonly used in modern Java code.

---

# 💻 6. Using Stream API

We can create a Stream from the `ArrayList`.

```java
names.stream()
     .forEach(System.out::println);
```

We can also perform operations while iterating.

```java
names.stream()
     .filter(name -> name.startsWith("A"))
     .forEach(System.out::println);
```

For example:

```text
Alice
Andrew
```

would be printed.

---

# 💻 7. Using `Spliterator`

An `ArrayList` also provides a `Spliterator`.

```java
Spliterator<String> spliterator = names.spliterator();

spliterator.forEachRemaining(System.out::println);
```

Import:

```java
import java.util.Spliterator;
```

`Spliterator` is particularly useful for:

- Parallel processing
- Stream implementation
- Splitting a data source into parts

---

# 🔥 Splitting the ArrayList

One of the important features of `Spliterator` is:

```java
trySplit()
```

Example:

```java
Spliterator<String> first =
        names.spliterator();

Spliterator<String> second =
        first.trySplit();
```

The original spliterator and the returned spliterator can then process different portions of the collection.

This is one of the mechanisms used to support parallel processing.

---

# 📊 Comparison

| Approach | Index Access | Remove During Iteration | Bidirectional | Functional Style |
|---|---:|---:|---:|---:|
| `for` loop | ✅ | ⚠️ Manual | ✅ | ❌ |
| `for-each` | ❌ | ❌ | ❌ | ❌ |
| `Iterator` | ❌ | ✅ | ❌ | ❌ |
| `ListIterator` | ❌ | ✅ | ✅ | ❌ |
| `forEach()` | ❌ | ❌ | ❌ | ✅ |
| `Stream` | ❌ | ❌ | ❌ | ✅ |
| `Spliterator` | ❌ | ❌ | ❌ | ✅ / Parallel |

---

# 🧠 Which One Should You Use?

### Need index?

Use:

```java
for (int i = 0; i < list.size(); i++)
```

---

### Simply read every element?

Use:

```java
for (String item : list)
```

or:

```java
list.forEach(System.out::println);
```

---

### Need to remove while iterating?

Use:

```java
Iterator
```

and:

```java
iterator.remove();
```

---

### Need forward and backward traversal?

Use:

```java
ListIterator
```

---

### Need functional processing?

Use:

```java
Stream
```

or:

```java
forEach()
```

---

### Need parallel/splitting behavior?

Use:

```java
Spliterator
```

or a Stream backed by the collection.

---

# ⚠️ Important Interview Question

## `for-each` vs `Iterator`

The enhanced `for` loop internally uses an iterator for an `ArrayList`.

Conceptually:

```java
for (String name : names) {
    System.out.println(name);
}
```

is translated by the compiler into logic equivalent to:

```java
Iterator<String> iterator = names.iterator();

while (iterator.hasNext()) {
    String name = iterator.next();
    System.out.println(name);
}
```

This is why modifying the collection structurally during a for-each loop can result in:

```text
ConcurrentModificationException
```

---

# ⚠️ Important Interview Question

## `Iterator` vs `ListIterator`

| Feature | `Iterator` | `ListIterator` |
|---|---|---|
| Forward traversal | ✅ | ✅ |
| Backward traversal | ❌ | ✅ |
| `remove()` | ✅ | ✅ |
| `set()` | ❌ | ✅ |
| `add()` | ❌ | ✅ |
| Index information | ❌ | Can obtain index |
| Works with | `Collection` | `List` |

`ListIterator` is specifically designed for `List` implementations.

---

# 🚀 Performance Considerations

For an `ArrayList`, accessing an element by index is:

```text
O(1)
```

Therefore:

```java
for (int i = 0; i < list.size(); i++) {
    list.get(i);
}
```

is efficient for `ArrayList`.

However, this same pattern can be problematic with a `LinkedList`:

```java
for (int i = 0; i < linkedList.size(); i++) {
    linkedList.get(i);
}
```

because indexed access in `LinkedList` is O(n).

This can make the complete traversal approach O(n²).

For general collection code, an iterator or enhanced for-loop avoids making assumptions about indexed access.

---

# 🎯 Best Interview Answer

If the interviewer asks:

> "What are the ways to iterate over an ArrayList?"

Mention these:

```text
1. Traditional for loop
2. Enhanced for-each loop
3. Iterator
4. ListIterator
5. forEach() + Lambda
6. Stream API
7. Spliterator
```

Then explain the use case for each rather than simply listing them.

---

# 🧠 Common Interview Traps

### ❌ Trap 1 — Saying `forEach()` and Stream are the same

They are not.

```java
list.forEach(...)
```

directly iterates over the collection.

```java
list.stream()
    .forEach(...)
```

creates a Stream pipeline first.

---

### ❌ Trap 2 — Saying `ListIterator` works with every Collection

It doesn't.

`ListIterator` is specific to `List`.

---

### ❌ Trap 3 — Removing directly inside for-each

Avoid:

```java
for (String name : names) {
    names.remove(name);
}
```

Use an `Iterator` when removal during traversal is required.

---

### ❌ Trap 4 — Assuming Stream is always faster

A Stream does not automatically mean better performance.

For simple iteration:

```java
for (String item : list)
```

may be simpler and have less overhead.

Streams become particularly useful when we need operations such as:

```text
filter
map
sort
reduce
collect
```

---

# 🎤 3-Minute Interview Explanation

"There are several ways to iterate over an ArrayList. The traditional for loop is useful when I need the index because ArrayList provides O(1) indexed access. The enhanced for-each loop is simpler when I only need the elements. We can also use Iterator, which is particularly useful when we need to safely remove elements during iteration using iterator.remove(). ListIterator extends this functionality by supporting bidirectional traversal and operations such as add, remove and set.

From Java 8 onwards, we can use forEach with a lambda or method reference for concise iteration. We can also create a Stream when we need functional-style processing such as filtering, mapping or collecting. Finally, ArrayList provides a Spliterator, which supports traversal and splitting and is useful for parallel processing.

The choice depends on the requirement: use a normal for loop for index-based access, Iterator for safe removal, ListIterator for bidirectional list manipulation, forEach for simple functional iteration, and Stream when we need a processing pipeline."

---

# ⏱️ 60-Second Interview Answer

"An ArrayList can be iterated in several ways: traditional for loop, enhanced for-each loop, Iterator, ListIterator, forEach with lambda, Stream API and Spliterator. I use a traditional for loop when I need indexes, for-each for simple traversal, Iterator when I need to remove elements safely during iteration, and ListIterator when I need bidirectional traversal or modification through set/add/remove. For functional processing such as filter and map, I prefer Streams. Spliterator is useful for splitting traversal and parallel processing."

---

# 📝 Quick Revision Notes

```text
ArrayList iteration:

1. for loop
   → index access

2. enhanced for
   → simple traversal

3. Iterator
   → safe removal

4. ListIterator
   → forward + backward
   → add / remove / set

5. forEach()
   → lambda / method reference

6. Stream
   → filter / map / reduce / collect

7. Spliterator
   → traversal + splitting
   → parallel processing

ArrayList get(index):
    O(1)
```

### Golden Rule

> **Choose the iteration mechanism based on the requirement: index access → `for`, safe removal → `Iterator`, bidirectional modification → `ListIterator`, functional processing → Stream, and splitting/parallel traversal → `Spliterator`.**

---

[Q118. Ways to iterate over `ArrayList`. [Answered]](#q118-ways-to-iterate-over-arraylist-answered)

[⬆ Back to Question Index](#question-index)

---

# Q130. How can you iterate over a Map? [Answered]

- [Q130. How can you iterate over a Map? [Answered]](#q130-how-can-you-iterate-over-a-map-answered)

**Priority:** P1

---

# 📌 One-Line Interview Answer

A `Map` can be iterated using `entrySet()`, `keySet()`, `values()`, `forEach()`, or an `Iterator`; `entrySet()` is generally preferred when both the key and value are required.

---

# 💻 1. Using `entrySet()` — Recommended

```java
Map<Integer, String> map = new HashMap<>();

map.put(1, "Java");
map.put(2, "Spring");
map.put(3, "Kafka");

for (Map.Entry<Integer, String> entry : map.entrySet()) {

    System.out.println(
        "Key: " + entry.getKey()
        + ", Value: " + entry.getValue()
    );
}
```

### Output

```text
Key: 1, Value: Java
Key: 2, Value: Spring
Key: 3, Value: Kafka
```

The actual order is **not guaranteed for `HashMap`**.

### Why is `entrySet()` preferred?

If we need both key and value:

```java
for (Map.Entry<Integer, String> entry : map.entrySet())
```

gives direct access to both:

```java
entry.getKey()
entry.getValue()
```

This is preferable to iterating over keys and then performing:

```java
map.get(key)
```

for every key.

---

# 💻 2. Using `keySet()`

If we only need the keys:

```java
for (Integer key : map.keySet()) {
    System.out.println(key);
}
```

If we need both key and value:

```java
for (Integer key : map.keySet()) {
    System.out.println(
        key + " = " + map.get(key)
    );
}
```

This works, but when both key and value are required, `entrySet()` is generally better.

---

# 💻 3. Using `values()`

If we only need the values:

```java
for (String value : map.values()) {
    System.out.println(value);
}
```

This avoids dealing with keys entirely.

---

# 💻 4. Using `forEach()` — Java 8+

Java 8 introduced a convenient `Map.forEach()` method.

```java
map.forEach((key, value) -> {
    System.out.println(key + " = " + value);
});
```

For simple output, we can write:

```java
map.forEach((key, value) ->
    System.out.println(key + " = " + value)
);
```

This is concise and commonly used in modern Java code.

---

# 💻 5. Using `Iterator` with `entrySet()`

We can explicitly obtain an iterator:

```java
Iterator<Map.Entry<Integer, String>> iterator =
        map.entrySet().iterator();

while (iterator.hasNext()) {

    Map.Entry<Integer, String> entry = iterator.next();

    System.out.println(
        entry.getKey() + " = " + entry.getValue()
    );
}
```

This is useful when we need to **remove entries safely during iteration**.

---

# 🔥 Removing Entries While Iterating

Suppose we want to remove all entries whose value is `"Java"`.

Using an `Iterator`:

```java
Iterator<Map.Entry<Integer, String>> iterator =
        map.entrySet().iterator();

while (iterator.hasNext()) {

    Map.Entry<Integer, String> entry = iterator.next();

    if (entry.getValue().equals("Java")) {
        iterator.remove();
    }
}
```

This is the safe iterator-based approach.

---

# 💻 6. Using `Map.Entry.comparingByValue()`

Although not strictly an iteration technique, this is a useful follow-up when the interviewer asks:

> "How would you iterate over a Map sorted by value?"

Example:

```java
map.entrySet()
   .stream()
   .sorted(Map.Entry.comparingByValue())
   .forEach(entry ->
       System.out.println(
           entry.getKey() + " = " + entry.getValue()
       )
   );
```

For descending order:

```java
map.entrySet()
   .stream()
   .sorted(
       Map.Entry.<Integer, String>comparingByValue()
           .reversed()
   )
   .forEach(entry ->
       System.out.println(
           entry.getKey() + " = " + entry.getValue()
       )
   );
```

---

# 📊 Different Ways to Iterate

| Method | Gets Keys | Gets Values | Best Use Case |
|---|---:|---:|---|
| `entrySet()` | ✅ | ✅ | ⭐ Both key and value |
| `keySet()` | ✅ | Via `get()` | Keys |
| `values()` | ❌ | ✅ | Values only |
| `forEach()` | ✅ | ✅ | Concise Java 8+ code |
| `Iterator` | ✅ | ✅ | Removal during iteration |
| `Stream` | ✅ | ✅ | Filtering/sorting/transforming |

---

# 🧠 `entrySet()` vs `keySet()`

This is a common interview question.

### Using `keySet()`

```java
for (Integer key : map.keySet()) {
    String value = map.get(key);
}
```

Conceptually:

```text
Get key
   ↓
Lookup value
   ↓
Process
```

### Using `entrySet()`

```java
for (Map.Entry<Integer, String> entry : map.entrySet()) {

    Integer key = entry.getKey();
    String value = entry.getValue();
}
```

The entry already contains:

```text
Key + Value
```

Therefore, if both are needed:

```text
entrySet() → preferred
```

---

# ⚡ Performance Consideration

For a `HashMap`, `get(key)` is average:

```text
O(1)
```

So iterating using `keySet()` and calling `get()` is generally still O(n) average.

However, `entrySet()` is cleaner and avoids an additional map lookup for each entry.

For other Map implementations, the distinction can matter more.

The important interview point is:

> **If both key and value are needed, prefer `entrySet()`.**

---

# ⚠️ Can You Modify a Map During a For-Each Loop?

This is dangerous:

```java
for (Integer key : map.keySet()) {

    if (key > 2) {
        map.remove(key);
    }
}
```

For fail-fast map implementations such as `HashMap`, this can result in:

```text
ConcurrentModificationException
```

Instead, use the iterator:

```java
Iterator<Integer> iterator = map.keySet().iterator();

while (iterator.hasNext()) {

    Integer key = iterator.next();

    if (key > 2) {
        iterator.remove();
    }
}
```

---

# 💻 Java 8+ Alternative — `removeIf()`

For a `Map`, you can also use `entrySet().removeIf()`:

```java
map.entrySet().removeIf(
    entry -> entry.getKey() > 2
);
```

This is concise and useful when the removal condition is simple.

---

# 🔥 `Map.forEach()` vs Stream

These are different.

### `Map.forEach()`

```java
map.forEach((key, value) ->
    System.out.println(key + " = " + value)
);
```

Best for straightforward iteration.

### Stream

```java
map.entrySet()
   .stream()
   .filter(entry -> entry.getKey() > 2)
   .forEach(System.out::println);
```

Best when we need operations such as:

```text
filter
map
sort
collect
transform
```

A Stream should not be used merely because it is available.

---

# 🧠 Important Interview Follow-Ups

### 1. What is the best way to iterate when both key and value are needed?

```java
map.entrySet()
```

---

### 2. How do you iterate only over keys?

```java
map.keySet()
```

---

### 3. How do you iterate only over values?

```java
map.values()
```

---

### 4. How do you remove entries during iteration?

Use:

```java
Iterator<Map.Entry<K, V>>
```

and:

```java
iterator.remove();
```

or use:

```java
map.entrySet().removeIf(...)
```

---

### 5. Does Map itself implement `Iterable`?

No.

`Map` does not extend `Collection` or `Iterable`.

Instead, it exposes collection views:

```java
keySet()
values()
entrySet()
```

This is an important distinction.

---

# 🔍 Why Doesn't Map Implement `Iterable`?

A `Map` represents mappings:

```text
Key → Value
```

rather than a simple sequence of individual elements.

Therefore, Java provides separate views:

```text
keySet()   → Set<K>
values()   → Collection<V>
entrySet() → Set<Map.Entry<K,V>>
```

These can then be iterated.

---

# 🎯 Best Interview Answer

If asked:

> "How can you iterate over a Map?"

A strong answer is:

```java
for (Map.Entry<K, V> entry : map.entrySet()) {
    System.out.println(
        entry.getKey() + " = " + entry.getValue()
    );
}
```

Then mention:

```text
keySet()   → keys only
values()   → values only
entrySet() → keys + values
forEach()  → concise Java 8+ iteration
Iterator   → useful for safe removal
Stream     → filtering/sorting/transformation
```

---

# 🎤 3-Minute Interview Explanation

"A Map doesn't implement Iterable directly because it represents key-value mappings rather than a simple collection of elements. To iterate over a Map, Java provides three main views: keySet, values and entrySet.

If I need both the key and value, I prefer entrySet. For example, I can use `for (Map.Entry<K,V> entry : map.entrySet())` and access the key with `getKey()` and the value with `getValue()`. If I only need keys, I use keySet, and if I only need values, I use values.

From Java 8 onwards, I can also use `map.forEach((key, value) -> ...)` for concise iteration. If I need to remove elements during iteration, I can use an Iterator and call `iterator.remove()`. For more complex operations such as filtering or sorting, I can use the Stream API.

In general, when both key and value are required, `entrySet()` is the preferred approach."

---

# ⏱️ 60-Second Interview Answer

"A Map can be iterated using `entrySet()`, `keySet()`, `values()`, `forEach()`, Iterator or Streams. If I need both key and value, I prefer `entrySet()` because each entry directly contains both. If I need only keys, I use `keySet()`, and for only values, `values()`. Java 8 also provides `map.forEach((key, value) -> ...)` for concise iteration. If I need to remove entries safely during iteration, I use an Iterator and call `iterator.remove()`. For filtering or sorting, Streams are useful."

---

# 📝 Quick Revision Notes

```text
Map iteration:

1. entrySet()
   → key + value
   → preferred when both needed

2. keySet()
   → keys

3. values()
   → values

4. forEach()
   → concise Java 8+ syntax

5. Iterator
   → safe removal during iteration

6. Stream
   → filter / sort / transform / collect

Important:
    Map does NOT implement Iterable

Map views:
    keySet()   → Set<K>
    values()   → Collection<V>
    entrySet() → Set<Map.Entry<K,V>>
```

### Golden Rule

> **Use `entrySet()` when you need both keys and values, `keySet()` for keys only, `values()` for values only, and `Iterator` when safe removal during traversal is required.**

---

[Q130. How can you iterate over a Map? [Answered]](#q130-how-can-you-iterate-over-a-map-answered)

[⬆ Back to Question Index](#question-index)

---

# Q142. Find duplicates using Stream API. [To be Answered]

- [Q142. Find duplicates using Stream API. [To be Answered]](#q142-find-duplicates-using-stream-api-to-be-answered)

**Priority:** P1

---

# 📌 One-Line Interview Answer

Duplicates can be identified using a `Set` inside a Stream's `filter()` operation: if `Set.add()` returns `false`, the element has already been encountered and is therefore a duplicate.

---

# 💻 Approach 1 — Using `Set.add()` with `filter()`

This is the most commonly expected Stream API solution.

```java
import java.util.Arrays;
import java.util.HashSet;
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;

public class FindDuplicates {

    public static <T> Set<T> findDuplicates(List<T> list) {

        Set<T> seen = new HashSet<>();

        return list.stream()
                .filter(element -> !seen.add(element))
                .collect(Collectors.toSet());
    }

    public static void main(String[] args) {

        List<Integer> numbers =
                Arrays.asList(10, 20, 30, 20, 40, 10, 50, 30);

        Set<Integer> duplicates = findDuplicates(numbers);

        System.out.println(duplicates);
    }
}
```

### Output

```text
[10, 20, 30]
```

The order is not guaranteed because the result is collected into a `HashSet`.

---

# 📖 How Does `Set.add()` Help?

This is the key part:

```java
.filter(element -> !seen.add(element))
```

`Set.add()` has an important property:

```text
New element:
    add() → true

Already existing element:
    add() → false
```

Therefore:

```java
!seen.add(element)
```

means:

```text
Element already exists?
        ↓
      true
        ↓
  It is a duplicate
```

---

# 🔍 Example

Input:

```text
[10, 20, 30, 20, 40, 10]
```

Processing:

```text
10 → seen.add(10) → true  → not duplicate
20 → seen.add(20) → true  → not duplicate
30 → seen.add(30) → true  → not duplicate
20 → seen.add(20) → false → duplicate
40 → seen.add(40) → true  → not duplicate
10 → seen.add(10) → false → duplicate
```

Therefore:

```text
Duplicates = [20, 10]
```

---

# 💻 Approach 2 — Preserve Duplicate Encounter Order

If we want duplicates in the order in which they are first detected, use `LinkedHashSet`.

```java
import java.util.Arrays;
import java.util.LinkedHashSet;
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;

public static <T> Set<T> findDuplicates(List<T> list) {

    Set<T> seen = new HashSet<>();

    return list.stream()
            .filter(element -> !seen.add(element))
            .collect(Collectors.toCollection(LinkedHashSet::new));
}
```

For:

```text
[10, 20, 30, 20, 40, 10, 30]
```

result:

```text
[20, 10, 30]
```

The order reflects the first time each duplicate was detected.

---

# 💻 Approach 3 — Find Elements That Occur More Than Once

Another Stream-based approach is to group elements and count their occurrences.

```java
import java.util.List;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

public static <T> List<T> findDuplicates(List<T> list) {

    return list.stream()
            .collect(Collectors.groupingBy(
                    Function.identity(),
                    Collectors.counting()
            ))
            .entrySet()
            .stream()
            .filter(entry -> entry.getValue() > 1)
            .map(Map.Entry::getKey)
            .toList();
}
```

For:

```text
[10, 20, 30, 20, 40, 10, 30]
```

we first create:

```text
10 → 2
20 → 2
30 → 2
40 → 1
```

Then:

```java
.filter(entry -> entry.getValue() > 1)
```

selects:

```text
10
20
30
```

---

# ⚖️ `Set` Approach vs `groupingBy()`

| Approach | Time | Space | Best Use |
|---|---:|---:|---|
| `Set.add()` | O(n) average | O(n) | ⭐ Simple duplicate detection |
| `groupingBy()` | O(n) average | O(n) | Need occurrence counts |

If the interviewer only asks:

> "Find duplicates."

I would prefer the `Set.add()` approach.

If they ask:

> "Find duplicates and their frequencies."

I would use:

```java
groupingBy()
```

---

# 🔥 Find Duplicate Characters Using Stream API

The same concept can be applied to a String.

```java
import java.util.HashSet;
import java.util.Set;

public static Set<Character> findDuplicateCharacters(String str) {

    Set<Character> seen = new HashSet<>();

    return str.chars()
            .mapToObj(c -> (char) c)
            .filter(ch -> !seen.add(ch))
            .collect(Collectors.toSet());
}
```

Example:

```text
Input:
programming
```

Duplicate characters:

```text
r
g
m
```

---

# 💻 Find Duplicate Words

For a String containing words:

```java
String sentence =
        "java spring java kafka spring java";
```

We can use:

```java
Set<String> seen = new HashSet<>();

Set<String> duplicates =
        Arrays.stream(sentence.split("\\s+"))
                .filter(word -> !seen.add(word))
                .collect(Collectors.toSet());
```

Result:

```text
[java, spring]
```

---

# 🧠 Important Interview Follow-Up — What Does "Duplicate" Mean?

There are several possible interpretations.

### 1. Return each duplicated value once

Input:

```text
[1, 2, 2, 2, 3, 3]
```

Output:

```text
[2, 3]
```

Use:

```java
Set
```

---

### 2. Return every duplicate occurrence

Input:

```text
[1, 2, 2, 2, 3, 3]
```

Possible output:

```text
[2, 2, 3]
```

The `!seen.add()` approach can produce this behavior depending on the result collection.

---

### 3. Return duplicate frequency

Input:

```text
[1, 2, 2, 2, 3, 3]
```

Output:

```text
2 → 3
3 → 2
```

Use:

```java
groupingBy(
    Function.identity(),
    Collectors.counting()
)
```

---

# ⚠️ Important Stream Concept

This code:

```java
Set<Integer> seen = new HashSet<>();

list.stream()
    .filter(n -> !seen.add(n))
```

uses **external mutable state** inside the Stream pipeline.

It is acceptable for a simple sequential interview example, but it has an important limitation.

It is **not safe to blindly convert this to a parallel stream**.

For example:

```java
list.parallelStream()
```

with a normal `HashSet` can cause thread-safety problems.

If parallel processing is required, prefer a proper reduction/collector approach or a concurrent data structure, depending on the requirement.

---

# 🚀 Better Functional Approach for Parallel-Friendly Processing

Using `groupingBy()` expresses the operation more declaratively:

```java
Map<Integer, Long> frequencyMap =
        list.stream()
                .collect(Collectors.groupingBy(
                        Function.identity(),
                        Collectors.counting()
                ));

List<Integer> duplicates =
        frequencyMap.entrySet()
                .stream()
                .filter(entry -> entry.getValue() > 1)
                .map(Map.Entry::getKey)
                .toList();
```

For a parallel stream, `groupingByConcurrent()` can also be considered:

```java
Map<Integer, Long> frequencyMap =
        list.parallelStream()
                .collect(Collectors.groupingByConcurrent(
                        Function.identity(),
                        Collectors.counting()
                ));
```

This is a more senior-level discussion because it avoids relying on an ordinary mutable `HashSet` shared across parallel operations.

---

# ⚠️ Common Interview Traps

### ❌ Trap 1 — Using `distinct()`

This:

```java
list.stream()
    .distinct()
```

does **not** find duplicates.

It removes duplicates and returns only unique elements.

Example:

```text
[1, 2, 2, 3, 3]
```

becomes:

```text
[1, 2, 3]
```

---

### ❌ Trap 2 — Using `Set` incorrectly

This:

```java
new HashSet<>(list)
```

only gives unique elements.

It does not tell you which elements were duplicated.

---

### ❌ Trap 3 — Forgetting that `Set.add()` returns a boolean

The key insight is:

```java
seen.add(element)
```

returns:

```text
true  → element was newly added
false → element already existed
```

Therefore:

```java
!seen.add(element)
```

identifies duplicates.

---

# 🎯 Best Interview Solution

For a straightforward:

> "Find duplicates using Stream API"

question, I would write:

```java
Set<Integer> seen = new HashSet<>();

Set<Integer> duplicates = list.stream()
        .filter(n -> !seen.add(n))
        .collect(Collectors.toSet());
```

Then explain:

> "`HashSet.add()` returns false when the element already exists, so filtering on `!seen.add()` gives us duplicate elements."

If the interviewer asks for **duplicate counts**, switch to:

```java
list.stream()
    .collect(Collectors.groupingBy(
        Function.identity(),
        Collectors.counting()
    ));
```

---

# 🎤 3-Minute Interview Explanation

"To find duplicates using the Stream API, I can maintain a HashSet containing elements that have already been encountered. I then stream through the list and use `filter(element -> !seen.add(element))`. The important point is that HashSet's `add()` returns true when the element is newly added and false when it already exists. Therefore, when `add()` returns false, the element is a duplicate. Finally, I collect those elements into a Set so each duplicate value appears only once.

For example, with [10, 20, 30, 20, 40, 10], the first 10, 20 and 30 are added successfully. When the second 20 and 10 are encountered, `add()` returns false, so they pass the filter.

This gives O(n) average time and O(n) additional space. However, this approach uses mutable external state inside the Stream and should not be blindly used with parallel streams. If I need occurrence counts or a more declarative approach, I would use `groupingBy()` with `Collectors.counting()`."

---

# ⏱️ 60-Second Interview Answer

"I can find duplicates using a HashSet inside the Stream's filter. `HashSet.add()` returns true for a new element and false if the element already exists. So `filter(element -> !seen.add(element))` selects duplicates. I then collect the result into a Set so each duplicated value appears only once. The average time complexity is O(n) and space complexity is O(n). If I need the frequency of each duplicate, I would instead use `groupingBy(Function.identity(), Collectors.counting())`. I would also avoid using the mutable HashSet approach directly with a parallel stream."

---

# 📝 Quick Revision Notes

```text
Basic solution:

Set<T> seen = new HashSet<>();

list.stream()
    .filter(x -> !seen.add(x))
    .collect(Collectors.toSet());

HashSet.add():

true  → first occurrence
false → duplicate

Complexity:
    Time  → O(n) average
    Space → O(n)

Need duplicate counts?
    groupingBy()
    + counting()

Need unique elements?
    distinct()

Important:
    !seen.add(x) → duplicate
    Avoid shared HashSet with parallelStream()
```

### Golden Rule

> **`!seen.add(element)` is the key Stream pattern for detecting repeated elements: `add()` returns `false` when the element has already been seen.**

---

[Q142. Find duplicates using Stream API. [To be Answered]](#q142-find-duplicates-using-stream-api-to-be-answered)

[⬆ Back to Question Index](#question-index)

---

# Q143. Put all zeroes at one end in an array. [Answered]

- [Q143. Put all zeroes at one end in an array. [Answered]](#q143-put-all-zeroes-at-one-end-in-an-array-answered)

**Priority:** P1

---

# 📌 One-Line Interview Answer

We can move all zeroes to one end using a **two-pointer approach** in O(n) time and O(1) extra space, while preserving the relative order of the non-zero elements.

---

# 💻 Approach 1 — Two Pointers / In-Place ⭐ Recommended

Assume the requirement is to move all zeroes to the **end**.

```java
public static void moveZeroesToEnd(int[] arr) {

    int insertPos = 0;

    // Place all non-zero elements at the beginning
    for (int num : arr) {

        if (num != 0) {
            arr[insertPos++] = num;
        }
    }

    // Fill the remaining positions with zero
    while (insertPos < arr.length) {
        arr[insertPos++] = 0;
    }
}
```

### Example

Input:

```text
[0, 1, 0, 3, 12]
```

After execution:

```text
[1, 3, 12, 0, 0]
```

The relative order of the non-zero elements remains:

```text
1 → 3 → 12
```

---

# 🔍 How Does It Work?

We maintain:

```java
insertPos
```

which represents the position where the next non-zero element should be placed.

For:

```text
[0, 1, 0, 3, 12]
```

### Step 1

`0` → ignore.

```text
insertPos = 0
```

### Step 2

`1` → non-zero:

```text
arr[0] = 1
insertPos = 1
```

### Step 3

`0` → ignore.

### Step 4

`3` → non-zero:

```text
arr[1] = 3
insertPos = 2
```

### Step 5

`12` → non-zero:

```text
arr[2] = 12
insertPos = 3
```

Now:

```text
[1, 3, 12, ?, ?]
```

Finally, fill the remaining positions with zero:

```text
[1, 3, 12, 0, 0]
```

---

# 💻 Approach 2 — Two-Pointer Swap

Another common solution is to swap each non-zero element into its correct position.

```java
public static void moveZeroesToEnd(int[] arr) {

    int left = 0;

    for (int right = 0; right < arr.length; right++) {

        if (arr[right] != 0) {

            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;

            left++;
        }
    }
}
```

For:

```text
[0, 1, 0, 3, 12]
```

the result is:

```text
[1, 3, 12, 0, 0]
```

This approach performs the operation completely in-place.

---

# ⚖️ Approach 1 vs Approach 2

| Approach | Time | Extra Space | Stable? | Recommendation |
|---|---:|---:|---:|---|
| Copy non-zero + fill zero | O(n) | O(1) | ✅ | ⭐ Excellent |
| Two-pointer swap | O(n) | O(1) | ✅ | ⭐ Excellent |
| Temporary array | O(n) | O(n) | ✅ | Simple but extra space |
| Sorting | O(n log n) | Depends | ❌ | ❌ Not recommended |

Both two-pointer approaches satisfy the optimal complexity:

```text
Time  → O(n)
Space → O(1)
```

---

# 💻 Approach 3 — Using an Extra Array

A simpler but less memory-efficient approach:

```java
public static int[] moveZeroesToEnd(int[] arr) {

    int[] result = new int[arr.length];

    int index = 0;

    for (int num : arr) {

        if (num != 0) {
            result[index++] = num;
        }
    }

    return result;
}
```

Since a newly created `int[]` is initialized with zeroes, the remaining positions automatically contain:

```text
0
```

### Example

Input:

```text
[0, 1, 0, 3, 12]
```

Result:

```text
[1, 3, 12, 0, 0]
```

### Complexity

```text
Time  → O(n)
Space → O(n)
```

---

# 🔄 What If Zeroes Need to Go to the Beginning?

Simply reverse the placement strategy.

One option is to traverse from right to left:

```java
public static void moveZeroesToBeginning(int[] arr) {

    int insertPos = arr.length - 1;

    for (int i = arr.length - 1; i >= 0; i--) {

        if (arr[i] != 0) {
            arr[insertPos--] = arr[i];
        }
    }

    while (insertPos >= 0) {
        arr[insertPos--] = 0;
    }
}
```

Example:

```text
Input:
[0, 1, 0, 3, 12]

Output:
[0, 0, 1, 3, 12]
```

The non-zero elements maintain their relative order.

---

# 🧠 Important Requirement — Preserve Relative Order

Consider:

```text
[0, 5, 0, 2, 8]
```

A good solution should produce:

```text
[5, 2, 8, 0, 0]
```

not:

```text
[8, 2, 5, 0, 0]
```

The first solution preserves the order:

```text
5 → 2 → 8
```

This property is called **stability**.

---

# ⚠️ Why Sorting Is a Bad Solution

Someone might try:

```java
Arrays.sort(arr);
```

For:

```text
[0, 1, 0, 3, 12]
```

this gives:

```text
[0, 0, 1, 3, 12]
```

It puts zeroes at one end, but:

1. It puts them at the beginning rather than the requested end.
2. It is O(n log n).
3. It does more work than necessary.
4. The interviewer is generally testing array manipulation/two-pointer logic.

Therefore, sorting is not the preferred solution.

---

# ⚠️ Common Interview Traps

### ❌ Trap 1 — Creating another array unnecessarily

If the interviewer asks:

> "Do it in-place."

Don't use:

```java
int[] result = new int[arr.length];
```

Use the two-pointer approach.

---

### ❌ Trap 2 — Losing the order of non-zero elements

A solution should generally preserve:

```text
relative order of non-zero elements
```

unless the interviewer explicitly says that order doesn't matter.

---

### ❌ Trap 3 — Using nested loops

An approach that repeatedly searches for a zero/non-zero pair can easily become:

```text
O(n²)
```

The two-pointer solution achieves:

```text
O(n)
```

---

# 🔥 Interview Follow-Up: Can You Do It Without Swapping?

Yes.

The copy-and-fill approach:

```java
int insertPos = 0;

for (int num : arr) {
    if (num != 0) {
        arr[insertPos++] = num;
    }
}

while (insertPos < arr.length) {
    arr[insertPos++] = 0;
}
```

doesn't require explicit swaps.

This is often very easy to explain and is optimal in complexity.

---

# 🔥 Interview Follow-Up: What About Negative Numbers?

Negative numbers are treated as non-zero values.

For:

```text
[0, -2, 0, 5, -7]
```

the result is:

```text
[-2, 5, -7, 0, 0]
```

---

# 🔥 Interview Follow-Up: What About All Zeroes?

Input:

```text
[0, 0, 0, 0]
```

Output:

```text
[0, 0, 0, 0]
```

No changes are required.

---

# 🔥 Interview Follow-Up: What About No Zeroes?

Input:

```text
[1, 2, 3, 4]
```

Output:

```text
[1, 2, 3, 4]
```

Again, no changes are required.

---

# 🎯 Best Interview Solution

For an interview, I would use:

```java
public static void moveZeroesToEnd(int[] arr) {

    int insertPos = 0;

    for (int num : arr) {

        if (num != 0) {
            arr[insertPos++] = num;
        }
    }

    while (insertPos < arr.length) {
        arr[insertPos++] = 0;
    }
}
```

It provides:

```text
O(n) time
O(1) extra space
Stable non-zero ordering
In-place modification
```

---

# 🎤 3-Minute Interview Explanation

"I would solve this using a two-pointer or insertion-position technique. I maintain an `insertPos` variable that represents where the next non-zero element should be placed. I traverse the array once and whenever I encounter a non-zero element, I place it at `insertPos` and increment the position. After processing all elements, all non-zero values are at the beginning of the array, so I fill the remaining positions with zeroes.

For example, for `[0, 1, 0, 3, 12]`, the non-zero elements are placed as `[1, 3, 12]`, and then the remaining two positions are filled with zeroes, resulting in `[1, 3, 12, 0, 0]`.

The solution takes O(n) time because we make a constant number of passes over the array, and O(1) extra space because we modify the original array. It also preserves the relative order of the non-zero elements. If the interviewer instead wants zeroes at the beginning, I can apply the same concept from the opposite direction."

---

# ⏱️ 60-Second Interview Answer

"I would use a two-pointer approach. I maintain an `insertPos` pointing to the next position where a non-zero element should go. I scan the array, copy every non-zero element to `insertPos`, and increment it. Once all non-zero elements have been placed, I fill the remaining positions with zeroes. For example, `[0,1,0,3,12]` becomes `[1,3,12,0,0]`. This is O(n) time, O(1) extra space, works in-place, and preserves the relative order of the non-zero elements."

---

# 📝 Quick Revision Notes

```text
Goal:
    Move all zeroes to the end

Best technique:
    Two pointers / insertion position

Logic:
    insertPos = 0

    for each num:
        if num != 0:
            arr[insertPos++] = num

    fill remaining positions with 0

Example:
    [0,1,0,3,12]
          ↓
    [1,3,12,0,0]

Complexity:
    Time  → O(n)
    Space → O(1)

Properties:
    In-place
    Stable
    No sorting required

If zeroes → beginning:
    Traverse from right to left
```

### Golden Rule

> **Move all non-zero elements forward in one pass, then fill the remaining positions with zeroes — O(n) time and O(1) extra space.**

---

[Q143. Put all zeroes at one end in an array. [Answered]](#q143-put-all-zeroes-at-one-end-in-an-array-answered)

[⬆ Back to Question Index](#question-index)

---

# Q144. Check if 2 strings are anagrams. [Answered]

- [Q144. Check if 2 strings are anagrams. [Answered]](#q144-check-if-2-strings-are-anagrams-answered)

**Priority:** P1

---

# 📌 One-Line Interview Answer

Two strings are anagrams if they contain the same characters with the same frequencies, regardless of their order; this can be checked efficiently using a frequency array or `HashMap`.

---

# 🧠 What Is an Anagram?

Two strings are anagrams when:

1. They contain the same characters.
2. Each character occurs the same number of times.
3. The order of characters does not matter.

Example:

```text
"listen"
"silent"
```

Both contain:

```text
l → 1
i → 1
s → 1
t → 1
e → 1
n → 1
```

Therefore:

```text
listen → silent → Anagram
```

Another example:

```text
"race"
"care"
```

Result:

```text
Anagram
```

But:

```text
"hello"
"world"
```

are not anagrams.

---

# 💻 Approach 1 — Frequency Array ⭐ Recommended

If the problem specifies lowercase English letters (`a-z`), a frequency array is the most efficient solution.

```java
public static boolean areAnagrams(String s1, String s2) {

    if (s1 == null || s2 == null) {
        return s1 == s2;
    }

    if (s1.length() != s2.length()) {
        return false;
    }

    int[] frequency = new int[26];

    for (int i = 0; i < s1.length(); i++) {
        frequency[s1.charAt(i) - 'a']++;
        frequency[s2.charAt(i) - 'a']--;
    }

    for (int count : frequency) {
        if (count != 0) {
            return false;
        }
    }

    return true;
}
```

### Example

```java
System.out.println(
    areAnagrams("listen", "silent")
);
```

Output:

```text
true
```

---

# 🔍 How Does It Work?

For:

```text
s1 = "listen"
s2 = "silent"
```

We increment the count for every character in `s1` and decrement the count for every character in `s2`.

For example:

```text
l → +1 from s1
l → -1 from s2
```

So:

```text
l → 0
```

The same happens for every character.

If both strings contain exactly the same characters with the same frequencies, every frequency becomes:

```text
0
```

Therefore:

```java
if (count != 0)
    return false;
```

detects a mismatch.

---

# ⚡ Why Check Length First?

This is an important optimization:

```java
if (s1.length() != s2.length()) {
    return false;
}
```

If the strings have different lengths, they cannot possibly be anagrams.

For example:

```text
"cat"   → length 3
"tacx"  → length 4
```

Immediately:

```text
false
```

No further processing is necessary.

---

# 💻 Approach 2 — Using `HashMap`

For a more general character set, use a `HashMap`.

```java
import java.util.HashMap;
import java.util.Map;

public static boolean areAnagrams(String s1, String s2) {

    if (s1 == null || s2 == null) {
        return s1 == s2;
    }

    if (s1.length() != s2.length()) {
        return false;
    }

    Map<Character, Integer> frequencyMap = new HashMap<>();

    for (char ch : s1.toCharArray()) {
        frequencyMap.put(
            ch,
            frequencyMap.getOrDefault(ch, 0) + 1
        );
    }

    for (char ch : s2.toCharArray()) {

        Integer count = frequencyMap.get(ch);

        if (count == null) {
            return false;
        }

        if (count == 1) {
            frequencyMap.remove(ch);
        } else {
            frequencyMap.put(ch, count - 1);
        }
    }

    return frequencyMap.isEmpty();
}
```

This approach works beyond the simple `a-z` assumption.

---

# 💻 Approach 3 — Sorting

A simple alternative is to sort both strings and compare them.

```java
import java.util.Arrays;

public static boolean areAnagrams(String s1, String s2) {

    if (s1 == null || s2 == null) {
        return s1 == s2;
    }

    if (s1.length() != s2.length()) {
        return false;
    }

    char[] arr1 = s1.toCharArray();
    char[] arr2 = s2.toCharArray();

    Arrays.sort(arr1);
    Arrays.sort(arr2);

    return Arrays.equals(arr1, arr2);
}
```

For:

```text
"listen"
"silent"
```

After sorting:

```text
eilnst
eilnst
```

Therefore:

```text
true
```

### Complexity

```text
Time  → O(n log n)
Space → O(n)
```

This is easy to understand but less efficient than frequency counting.

---

# 📊 Approach Comparison

| Approach | Time | Extra Space | Best Use |
|---|---:|---:|---|
| Frequency array | **O(n)** | **O(1)** | ⭐ Fixed alphabet |
| HashMap | **O(n)** average | O(k) | General characters |
| Sorting | O(n log n) | O(n) | Simple implementation |

Where:

```text
n = length of the string
k = number of distinct characters
```

---

# 🔥 Case-Insensitive Anagrams

Consider:

```text
"Listen"
"Silent"
```

If the requirement says case should be ignored:

```java
s1 = s1.toLowerCase();
s2 = s2.toLowerCase();
```

Then perform the normal comparison.

Example:

```java
public static boolean areAnagramsIgnoreCase(
        String s1,
        String s2) {

    if (s1 == null || s2 == null) {
        return s1 == s2;
    }

    s1 = s1.toLowerCase();
    s2 = s2.toLowerCase();

    return areAnagrams(s1, s2);
}
```

For production-grade Unicode text, `Locale` considerations should also be taken into account when normalizing case.

---

# 🔥 Ignore Spaces and Special Characters

Suppose:

```text
"conversation"
"voices rant on"
```

These can be considered anagrams if spaces are ignored.

We can normalize the strings first:

```java
s1 = s1.replaceAll("[^a-zA-Z]", "")
       .toLowerCase();

s2 = s2.replaceAll("[^a-zA-Z]", "")
       .toLowerCase();
```

Then perform the anagram check.

Example:

```text
"conversation"
"voices rant on"
```

Both normalize to the same character collection.

---

# 🧠 Important Interview Clarification

Before coding, clarify:

> "Should the comparison be case-sensitive, and should spaces or special characters be considered?"

Because these requirements change the implementation.

For example:

```text
"Listen"
"silent"
```

Case-sensitive:

```text
false
```

Case-insensitive:

```text
true
```

---

# ⚠️ Unicode Consideration

A Java `char` represents a UTF-16 code unit, not always a complete Unicode character.

For simple English interview questions:

```java
char
```

is sufficient.

For full Unicode-aware processing, code points may be more appropriate:

```java
Map<Integer, Long> frequency =
        s.codePoints()
         .boxed()
         .collect(
             Collectors.groupingBy(
                 Function.identity(),
                 Collectors.counting()
             )
         );
```

This is a useful senior-level discussion point if the interviewer asks about international text.

---

# 💻 Stream-Based Solution

Since this is a Java interview, the interviewer may ask:

> "Can you solve it using Streams?"

One approach is to build frequency maps.

```java
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

public static boolean areAnagrams(String s1, String s2) {

    if (s1 == null || s2 == null) {
        return s1 == s2;
    }

    if (s1.length() != s2.length()) {
        return false;
    }

    Map<Character, Long> map1 =
            s1.chars()
              .mapToObj(c -> (char) c)
              .collect(Collectors.groupingBy(
                  Function.identity(),
                  Collectors.counting()
              ));

    Map<Character, Long> map2 =
            s2.chars()
              .mapToObj(c -> (char) c)
              .collect(Collectors.groupingBy(
                  Function.identity(),
                  Collectors.counting()
              ));

    return map1.equals(map2);
}
```

This is valid, but for a straightforward coding interview question, the frequency-array solution is simpler and more efficient when the input is restricted to `a-z`.

---

# ⚠️ Common Interview Traps

### ❌ Trap 1 — Only checking whether characters exist

Consider:

```text
"abbc"
"abcc"
```

Both contain:

```text
a
b
c
```

but they are not anagrams because their frequencies differ.

Therefore, we must compare **frequency**, not just presence.

---

### ❌ Trap 2 — Forgetting the length check

Always consider:

```java
if (s1.length() != s2.length()) {
    return false;
}
```

It provides an immediate rejection.

---

### ❌ Trap 3 — Using `HashSet`

A `HashSet` only tracks unique characters.

It cannot distinguish:

```text
"ab"
```

from:

```text
"aabb"
```

because both have the same set:

```text
[a, b]
```

Anagram checking requires frequencies.

---

### ❌ Trap 4 — Sorting without considering complexity

Sorting works, but:

```text
O(n log n)
```

is not optimal when a fixed alphabet allows:

```text
O(n)
```

frequency counting.

---

# 🎯 Best Interview Solution

If the interviewer says:

> "Check whether two lowercase English strings are anagrams."

Use:

```java
public static boolean areAnagrams(String s1, String s2) {

    if (s1.length() != s2.length()) {
        return false;
    }

    int[] frequency = new int[26];

    for (int i = 0; i < s1.length(); i++) {
        frequency[s1.charAt(i) - 'a']++;
        frequency[s2.charAt(i) - 'a']--;
    }

    for (int count : frequency) {
        if (count != 0) {
            return false;
        }
    }

    return true;
}
```

It is:

```text
O(n) time
O(1) space
```

and requires only one frequency array.

---

# 🎤 3-Minute Interview Explanation

"Two strings are anagrams if they contain exactly the same characters with the same frequencies, regardless of their order. I would first compare their lengths because strings with different lengths cannot be anagrams.

If the input is restricted to lowercase English letters, I can use an integer array of size 26. While traversing both strings, I increment the frequency for each character from the first string and decrement it for the corresponding character from the second string. At the end, if every frequency is zero, both strings contain exactly the same characters with the same frequencies, so they are anagrams.

This takes O(n) time and O(1) extra space because the frequency array always contains only 26 entries.

If the character set isn't fixed, I would use a HashMap instead. Another simple alternative is to sort both strings and compare them, but that takes O(n log n), so frequency counting is preferable when possible."

---

# ⏱️ 60-Second Interview Answer

"Two strings are anagrams if they contain the same characters with the same frequencies. I first check whether their lengths are equal. For lowercase English letters, I use an integer array of size 26. I increment the count for every character in the first string and decrement it for every character in the second. If all counts are zero, they're anagrams. This gives O(n) time and O(1) space. For a general character set, I would use a HashMap, while sorting both strings is a simpler but O(n log n) alternative."

---

# 📝 Quick Revision Notes

```text
Anagram:
    Same characters
    Same frequency
    Different order allowed

Example:
    listen ↔ silent
    race   ↔ care

Best approach:
    Frequency counting

Steps:
    1. Compare lengths
    2. Count s1 characters
    3. Subtract s2 characters
    4. Check all counts == 0

Complexity:
    Time  → O(n)
    Space → O(1) for a-z

General character set:
    HashMap<Character, Integer>

Alternative:
    Sort both strings
    O(n log n)

Clarify:
    Case sensitivity?
    Spaces?
    Special characters?
    Unicode?
```

### Golden Rule

> **Anagram checking is a frequency-comparison problem: if both strings produce identical character frequencies, they are anagrams.**

---

[Q144. Check if 2 strings are anagrams. [Answered]](#q144-check-if-2-strings-are-anagrams-answered)

[⬆ Back to Question Index](#question-index)

---

# Q145. Program to find duplicates in a string. [To be Answered]

- [Q145. Program to find duplicates in a string. [To be Answered]](#q145-program-to-find-duplicates-in-a-string-to-be-answered)

**Priority:** P1

---

# 📌 One-Line Interview Answer

We can find duplicate characters in a String by maintaining a `Set` of characters already seen; if adding a character to the set returns `false`, that character is a duplicate.

---

# 💻 Approach 1 — Using `HashSet` ⭐ Recommended

```java
import java.util.HashSet;
import java.util.Set;

public class DuplicateCharacters {

    public static void findDuplicates(String str) {

        if (str == null || str.isEmpty()) {
            return;
        }

        Set<Character> seen = new HashSet<>();
        Set<Character> duplicates = new HashSet<>();

        for (char ch : str.toCharArray()) {

            if (!seen.add(ch)) {
                duplicates.add(ch);
            }
        }

        System.out.println("Duplicate characters: " + duplicates);
    }

    public static void main(String[] args) {

        findDuplicates("programming");
    }
}
```

### Example Output

```text
Duplicate characters: [r, g, m]
```

The order may vary because `HashSet` does not guarantee iteration order.

---

# 🔍 How Does It Work?

For:

```text
programming
```

we maintain:

```text
seen
duplicates
```

Initially:

```text
seen       = {}
duplicates = {}
```

Process each character:

```text
p → new      → seen = {p}
r → new      → seen = {p,r}
o → new      → seen = {p,r,o}
g → new      → seen = {p,r,o,g}
r → exists   → duplicate = {r}
a → new
m → new
m → exists   → duplicate = {r,m}
i → new
n → new
g → exists   → duplicate = {r,m,g}
```

Final result:

```text
[r, m, g]
```

---

# 🧠 Key Concept — `Set.add()`

This is the most important part:

```java
if (!seen.add(ch)) {
    duplicates.add(ch);
}
```

`Set.add()` returns:

```text
true  → character was not already present
false → character already existed
```

Therefore:

```java
!seen.add(ch)
```

means:

```text
This character has already appeared.
```

---

# 💻 Approach 2 — Using a `HashMap`

If the interviewer wants to know **how many times each character occurs**, use a `HashMap`.

```java
import java.util.HashMap;
import java.util.Map;

public static void findDuplicateCharacters(String str) {

    Map<Character, Integer> frequencyMap = new HashMap<>();

    for (char ch : str.toCharArray()) {

        frequencyMap.put(
            ch,
            frequencyMap.getOrDefault(ch, 0) + 1
        );
    }

    for (Map.Entry<Character, Integer> entry
            : frequencyMap.entrySet()) {

        if (entry.getValue() > 1) {
            System.out.println(
                entry.getKey() + " = " + entry.getValue()
            );
        }
    }
}
```

For:

```text
programming
```

the result would be approximately:

```text
r = 2
g = 2
m = 2
```

The order is not guaranteed with `HashMap`.

---

# ⚖️ HashSet vs HashMap

| Requirement | Recommended |
|---|---|
| Find which characters are duplicated | `HashSet` |
| Count occurrences | `HashMap` |
| Find first duplicate | `HashSet` + ordered traversal |
| Preserve duplicate order | `LinkedHashSet` |
| Sort duplicate characters | `TreeSet` |

---

# 💻 Approach 3 — Preserve Duplicate Order

If the interviewer expects duplicates in the order they are first encountered, use `LinkedHashSet`.

```java
import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.Set;

public static Set<Character> findDuplicates(String str) {

    Set<Character> seen = new HashSet<>();
    Set<Character> duplicates = new LinkedHashSet<>();

    for (char ch : str.toCharArray()) {

        if (!seen.add(ch)) {
            duplicates.add(ch);
        }
    }

    return duplicates;
}
```

For:

```text
programming
```

the result will be:

```text
[r, m, g]
```

because:

```text
r → first duplicate
m → second duplicate
g → third duplicate
```

---

# 💻 Approach 4 — Using a Frequency Array

If the String contains only lowercase English letters:

```java
public static void findDuplicates(String str) {

    int[] frequency = new int[26];

    for (char ch : str.toCharArray()) {
        frequency[ch - 'a']++;
    }

    for (int i = 0; i < frequency.length; i++) {

        if (frequency[i] > 1) {
            System.out.println(
                (char) ('a' + i) + " = " + frequency[i]
            );
        }
    }
}
```

For:

```text
programming
```

output:

```text
g = 2
m = 2
r = 2
```

This uses a fixed amount of additional space.

---

# 💻 Approach 5 — Using Java Streams

Since this is a Java interview, the interviewer may specifically ask:

> "Can you find duplicate characters using Streams?"

Yes.

```java
import java.util.HashSet;
import java.util.Set;
import java.util.stream.Collectors;

public static Set<Character> findDuplicates(String str) {

    Set<Character> seen = new HashSet<>();

    return str.chars()
            .mapToObj(c -> (char) c)
            .filter(ch -> !seen.add(ch))
            .collect(Collectors.toSet());
}
```

Example:

```java
System.out.println(
    findDuplicates("programming")
);
```

Possible output:

```text
[r, g, m]
```

Again, the order is not guaranteed.

---

# 💻 Stream Approach — Preserve Order

Use `LinkedHashSet` for the result:

```java
import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.Set;
import java.util.stream.Collectors;

public static Set<Character> findDuplicates(String str) {

    Set<Character> seen = new HashSet<>();

    return str.chars()
            .mapToObj(c -> (char) c)
            .filter(ch -> !seen.add(ch))
            .collect(
                Collectors.toCollection(
                    LinkedHashSet::new
                )
            );
}
```

Result:

```text
[r, m, g]
```

---

# 🔥 Find Duplicate Characters and Their Counts Using Streams

If the interviewer asks:

> "Find duplicate characters along with their frequency."

Use:

```java
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

public static Map<Character, Long> findDuplicateCharacters(
        String str) {

    return str.chars()
            .mapToObj(c -> (char) c)
            .collect(Collectors.groupingBy(
                Function.identity(),
                Collectors.counting()
            ))
            .entrySet()
            .stream()
            .filter(entry -> entry.getValue() > 1)
            .collect(Collectors.toMap(
                Map.Entry::getKey,
                Map.Entry::getValue
            ));
}
```

For:

```text
programming
```

result:

```text
r → 2
g → 2
m → 2
```

---

# 🔥 Find Only the First Duplicate

If the interviewer changes the question to:

> "Find the first duplicate character."

Use:

```java
public static Character firstDuplicate(String str) {

    Set<Character> seen = new HashSet<>();

    for (char ch : str.toCharArray()) {

        if (!seen.add(ch)) {
            return ch;
        }
    }

    return null;
}
```

For:

```text
"programming"
```

the first duplicate is:

```text
r
```

because `r` is encountered twice before `m` and `g` become duplicates.

---

# 🔥 Find the First Non-Repeating Character

A common follow-up is:

> "Now find the first non-repeating character."

Use a frequency map:

```java
public static Character firstNonRepeating(String str) {

    Map<Character, Integer> frequency =
            new LinkedHashMap<>();

    for (char ch : str.toCharArray()) {
        frequency.put(
            ch,
            frequency.getOrDefault(ch, 0) + 1
        );
    }

    for (Map.Entry<Character, Integer> entry
            : frequency.entrySet()) {

        if (entry.getValue() == 1) {
            return entry.getKey();
        }
    }

    return null;
}
```

`LinkedHashMap` preserves insertion order, which is important because we need the **first** non-repeating character.

---

# ⚠️ Case Sensitivity

By default:

```text
'A' != 'a'
```

Therefore:

```text
"Apple"
```

contains no duplicate `A/a` if case is treated as significant.

If the requirement is case-insensitive:

```java
str = str.toLowerCase();
```

before processing.

Example:

```text
"Apple"
```

becomes:

```text
"apple"
```

Now:

```text
p
```

is detected as a duplicate.

---

# ⚠️ Should Spaces Be Considered?

This depends on the requirement.

For:

```text
"hello world"
```

the space character occurs once.

If spaces should be ignored:

```java
if (ch == ' ') {
    continue;
}
```

Or normalize the input before processing.

The same clarification applies to:

```text
punctuation
special characters
case
Unicode characters
```

---

# 🧠 Unicode Consideration

For basic interview questions involving English characters, this is sufficient:

```java
char
```

However, Java `char` represents a UTF-16 code unit, not always a complete Unicode code point.

For Unicode-aware processing, code points can be used:

```java
Set<Integer> seen = new HashSet<>();

Set<Integer> duplicates =
        str.codePoints()
           .filter(cp -> !seen.add(cp))
           .boxed()
           .collect(Collectors.toSet());
```

This is a useful senior-level discussion point.

---

# 📊 Complexity

### HashSet Approach

For a String of length `n`:

```text
Time  → O(n) average
Space → O(k)
```

where:

```text
k = number of distinct characters
```

In the worst case:

```text
k = n
```

so:

```text
Space → O(n)
```

---

### Frequency Array

For a fixed alphabet such as lowercase `a-z`:

```text
Time  → O(n)
Space → O(1)
```

because the array always contains:

```text
26 elements
```

---

# ⚠️ Common Interview Traps

### ❌ Trap 1 — Using `HashSet` alone

This:

```java
Set<Character> set =
        new HashSet<>(...);
```

can tell you unique characters, but you need to detect whether `add()` fails to identify duplicates during traversal.

---

### ❌ Trap 2 — Using `distinct()`

This:

```java
str.chars()
   .distinct()
```

removes duplicates.

It does **not** find which characters were duplicated.

---

### ❌ Trap 3 — Using nested loops unnecessarily

A solution like:

```java
for (...) {
    for (...) {
        ...
    }
}
```

can easily become:

```text
O(n²)
```

A `HashSet` or frequency array gives:

```text
O(n)
```

average/linear processing.

---

### ❌ Trap 4 — Using a shared `HashSet` with `parallelStream()`

This:

```java
Set<Character> seen = new HashSet<>();

str.parallelStream()
   ...
```

is unsafe because `HashSet` is not thread-safe.

For a normal interview problem, use a sequential stream unless parallel processing is specifically required.

---

# 🎯 Best Interview Solution

If the interviewer simply asks:

> "Find duplicate characters in a String."

Use:

```java
public static Set<Character> findDuplicates(String str) {

    Set<Character> seen = new HashSet<>();
    Set<Character> duplicates = new LinkedHashSet<>();

    for (char ch : str.toCharArray()) {

        if (!seen.add(ch)) {
            duplicates.add(ch);
        }
    }

    return duplicates;
}
```

This is:

```text
O(n) average time
O(n) worst-case space
```

and preserves the order in which duplicates are first detected.

If they specifically ask for **Stream API**, use:

```java
Set<Character> seen = new HashSet<>();

Set<Character> duplicates =
        str.chars()
           .mapToObj(c -> (char) c)
           .filter(ch -> !seen.add(ch))
           .collect(Collectors.toSet());
```

---

# 🎤 3-Minute Interview Explanation

"To find duplicate characters in a String, I can maintain a Set of characters that I've already encountered. I iterate through the String, and whenever I encounter a character, I try to add it to the Set. `Set.add()` returns true if the character was not present and false if it was already present. Therefore, a false return tells me that the character is a duplicate.

If I want each duplicate character only once and want to preserve the order in which duplicates were first detected, I can store the duplicates in a LinkedHashSet.

If the interviewer asks for the frequency as well, I would use a HashMap to count each character and then select entries whose count is greater than one. For a fixed alphabet such as lowercase English letters, a frequency array is also possible and gives O(1) auxiliary space.

The basic HashSet approach takes O(n) average time and O(k) space, where k is the number of distinct characters."

---

# ⏱️ 60-Second Interview Answer

"I would use a HashSet to track characters already seen. For every character, I call `seen.add(ch)`. If it returns false, the character has already appeared, so it is a duplicate. I can store duplicates in a LinkedHashSet if I want to preserve their detection order. This takes O(n) average time and O(n) worst-case space. If I also need the frequency of each duplicate, I would use a HashMap with `getOrDefault()` or `groupingBy()` with Streams."

---

# 📝 Quick Revision Notes

```text
Goal:
    Find duplicate characters

Best general approach:
    HashSet

Logic:
    if (!seen.add(ch)):
        duplicate

Need duplicate order:
    LinkedHashSet

Need frequency:
    HashMap<Character, Integer>

Need fixed alphabet:
    int[26]

Stream:
    str.chars()
       .mapToObj(c -> (char) c)
       .filter(ch -> !seen.add(ch))

Complexity:
    HashSet → O(n) average
    Frequency array → O(n), O(1) space for fixed alphabet

Clarify:
    Case sensitivity?
    Spaces?
    Special characters?
    Unicode?
```

### Golden Rule

> **Use a `Set` to track characters already seen; when `add()` returns `false`, the character is a duplicate.**

---

[Q145. Program to find duplicates in a string. [To be Answered]](#q145-program-to-find-duplicates-in-a-string-to-be-answered)

[⬆ Back to Question Index](#question-index)

---

# Q148. Code to swap 2 variables without a 3rd variable. [To be Answered]

- [Q148. Code to swap 2 variables without a 3rd variable. [To be Answered]](#q148-code-to-swap-2-variables-without-a-3rd-variable-to-be-answered)

**Priority:** P2

---

# 📌 One-Line Interview Answer

Two variables can be swapped without a third variable using **arithmetic operations**, **XOR**, or Java's built-in `Math`/utility approaches, but arithmetic and XOR have important limitations; for interviews, XOR is useful to know while a temporary variable is generally the clearest production solution.

---

# 💻 Approach 1 — Using Addition and Subtraction

```java
public static void swap(int a, int b) {

    a = a + b;
    b = a - b;
    a = a - b;

    System.out.println("a = " + a);
    System.out.println("b = " + b);
}
```

### Example

```java
int a = 10;
int b = 20;

swap(a, b);
```

Output:

```text
a = 20
b = 10
```

### How It Works

Initially:

```text
a = 10
b = 20
```

Step 1:

```java
a = a + b;
```

```text
a = 30
b = 20
```

Step 2:

```java
b = a - b;
```

```text
b = 30 - 20
b = 10
```

Step 3:

```java
a = a - b;
```

```text
a = 30 - 10
a = 20
```

Final:

```text
a = 20
b = 10
```

---

# ⚠️ Problem With Addition/Subtraction

The arithmetic approach can cause **integer overflow**.

For example:

```java
int a = Integer.MAX_VALUE;
int b = 10;
```

This:

```java
a = a + b;
```

can overflow because the result exceeds the range of `int`.

Therefore, although this solution is commonly asked in interviews, it is not the safest production implementation.

---

# 💻 Approach 2 — Using XOR ⭐ Interview Favorite

For integer values, XOR can swap two variables without an additional variable.

```java
public static void swap(int a, int b) {

    a = a ^ b;
    b = a ^ b;
    a = a ^ b;

    System.out.println("a = " + a);
    System.out.println("b = " + b);
}
```

Example:

```text
a = 10
b = 20
```

After execution:

```text
a = 20
b = 10
```

---

# 🧠 How XOR Swapping Works

XOR has three important properties:

```text
x ^ x = 0
x ^ 0 = x
x ^ y ^ x = y
```

Suppose:

```text
a = A
b = B
```

### Step 1

```java
a = a ^ b;
```

Now:

```text
a = A ^ B
b = B
```

### Step 2

```java
b = a ^ b;
```

Substitute:

```text
b = (A ^ B) ^ B
```

Because:

```text
B ^ B = 0
```

we get:

```text
b = A
```

### Step 3

```java
a = a ^ b;
```

Now:

```text
a = (A ^ B) ^ A
```

Therefore:

```text
a = B
```

Final:

```text
a = B
b = A
```

---

# ⚠️ Important XOR Limitation

The XOR trick is intended for integer/bitwise-compatible primitive types.

It is **not** a general-purpose swapping technique for:

```java
String
Object
double
```

etc.

Also, using it can make code less readable than simply using a temporary variable.

---

# ⚠️ Special XOR Problem — Same Variable

Consider:

```java
int a = 10;

a = a ^ a;
a = a ^ a;
a = a ^ a;
```

The value becomes:

```text
0
```

Therefore, the classic XOR swap should not be used blindly when both references point to the **same storage location**.

This matters more in low-level programming than in normal Java code, where you typically have separate local variables.

---

# 💻 Approach 3 — Using Multiplication and Division

Another mathematical approach is:

```java
a = a * b;
b = a / b;
a = a / b;
```

Example:

```text
a = 10
b = 20
```

Step 1:

```text
a = 200
```

Step 2:

```text
b = 200 / 20 = 10
```

Step 3:

```text
a = 200 / 10 = 20
```

Result:

```text
a = 20
b = 10
```

However, this approach is generally **not recommended**.

---

# ⚠️ Problems With Multiplication/Division

There are several problems:

### 1. Integer overflow

```java
a * b
```

can easily exceed the range of the data type.

### 2. Division by zero

If:

```java
b = 0;
```

then:

```java
a / b
```

causes:

```text
ArithmeticException
```

### 3. Loss of precision

For floating-point values, multiplication/division can introduce precision issues.

Therefore, this is mostly a theoretical interview technique.

---

# 📊 Comparison of Approaches

| Approach | Extra Variable | Overflow Risk | Division by Zero | Recommended |
|---|---:|---:|---:|---|
| Addition/Subtraction | No | ⚠️ Yes | No | Interview |
| XOR | No | No arithmetic overflow | No | ⭐ Interview |
| Multiplication/Division | No | ⚠️ Yes | ⚠️ Yes | ❌ Generally avoid |
| Temporary variable | Yes | No | No | ⭐ Production |

---

# 💻 The Normal Production Solution

In real-world Java code, simply use a temporary variable:

```java
int temp = a;
a = b;
b = temp;
```

This is:

```text
Simple
Readable
Safe
Easy to maintain
```

The interviewer may specifically prohibit this because the purpose of the question is to test alternative techniques.

---

# 🧠 Important Java Interview Point

Java is **pass-by-value**.

Therefore, this method:

```java
public static void swap(int a, int b) {

    int temp = a;
    a = b;
    b = temp;
}
```

does **not** swap variables in the caller.

For example:

```java
int x = 10;
int y = 20;

swap(x, y);

System.out.println(x);
System.out.println(y);
```

still prints:

```text
10
20
```

because `a` and `b` are copies of `x` and `y`.

This is an important follow-up question.

---

# 🔥 How Can We Swap Values in Java From a Method?

Since Java passes primitive values by value, one option is to return the swapped values.

For example:

```java
public static int[] swap(int a, int b) {

    return new int[]{b, a};
}
```

Usage:

```java
int a = 10;
int b = 20;

int[] result = swap(a, b);

a = result[0];
b = result[1];
```

Now:

```text
a = 20
b = 10
```

But this creates an additional array, so it is not really the purpose of the original "without a third variable" question.

---

# ⚠️ Common Interview Traps

### ❌ Trap 1 — Saying Java has pass-by-reference

Java is:

> **Pass-by-value.**

Even when passing objects, the value being passed is a copy of the reference.

---

### ❌ Trap 2 — Recommending multiplication/division

Although it works mathematically, it has:

```text
overflow
division-by-zero
precision
```

issues.

---

### ❌ Trap 3 — Saying XOR works for everything

XOR swapping is applicable to integer/bitwise operations, not arbitrary Java types.

---

### ❌ Trap 4 — Claiming no temporary memory is involved

The algorithms don't explicitly declare a third variable, but the JVM/compiler may use registers or other internal storage. "Without a third variable" means without an explicit third program variable.

---

# 🎯 Best Interview Answer

If the interviewer specifically says:

> "Swap two integers without using a third variable."

A good answer is:

```java
a = a ^ b;
b = a ^ b;
a = a ^ b;
```

Then explain the XOR properties.

Alternatively:

```java
a = a + b;
b = a - b;
a = a - b;
```

but immediately mention the integer overflow limitation.

For production code, prefer:

```java
int temp = a;
a = b;
b = temp;
```

because readability and correctness are more important than avoiding one temporary variable.

---

# 🎤 3-Minute Interview Explanation

"There are several ways to swap two variables without explicitly using a third variable. One common approach is addition and subtraction: first add the two values, then subtract the original values in reverse order to recover the swapped values. However, this can cause integer overflow.

Another approach, and a common interview favorite, is XOR. We perform `a = a ^ b`, then `b = a ^ b`, and finally `a = a ^ b`. XOR works because a value XORed with itself produces zero and XOR with zero produces the original value.

For example, if `a` is A and `b` is B, after the first operation `a` becomes A XOR B. The second operation produces A in `b`, and the third produces B in `a`.

In real production code, I would generally use a temporary variable because it is much more readable and avoids the overflow and readability issues of arithmetic tricks. Also, in Java, if the swap is placed inside a method taking primitive parameters, it won't modify the caller's variables because Java is pass-by-value."

---

# ⏱️ 60-Second Interview Answer

"For two integer variables, I can swap them without a third variable using XOR:

```java
a = a ^ b;
b = a ^ b;
a = a ^ b;
```

XOR works because `x ^ x` is zero and `x ^ 0` is x. Another option is addition and subtraction, but that can overflow. In production code, I'd normally use a temporary variable because it's clearer and safer. Also, if the variables are passed to a Java method as primitives, swapping the method parameters won't change the caller's variables because Java uses pass-by-value."

---

# 📝 Quick Revision Notes

```text
Goal:
    Swap two variables without a third variable

XOR:
    a = a ^ b
    b = a ^ b
    a = a ^ b

Arithmetic:
    a = a + b
    b = a - b
    a = a - b

Multiplication:
    a = a * b
    b = a / b
    a = a / b

Best production approach:
    int temp = a;
    a = b;
    b = temp;

Important:
    Java is pass-by-value
    Arithmetic approach can overflow
    Multiplication can divide by zero
    XOR is for integer/bitwise values
```

### Golden Rule

> **Know XOR swapping for interviews, but prefer a temporary variable in production code because clarity and safety matter more than eliminating one local variable.**

---

[Q148. Code to swap 2 variables without a 3rd variable. [To be Answered]](#q148-code-to-swap-2-variables-without-a-3rd-variable-to-be-answered)

[⬆ Back to Question Index](#question-index)

---

