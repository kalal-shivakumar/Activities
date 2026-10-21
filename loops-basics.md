# Python Loops: 100 Problems, Basic to Advanced

A workbook that teaches Python loops and iteration through 100 progressively harder problems.

Every problem uses the same four steps:

1. **Problem**: read it and try to solve it yourself first.
2. **Hint**: open it only if you are stuck.
3. **Solution**: compare it with your own attempt.
4. **Concept Explanation**: understand why it works and what pitfall to avoid.

Run every solution yourself and change values to see what happens. Typing the code beats reading it. Requires Python 3.8 or later and no external packages.

## Contents

| Section | Problems | Topics |
|---|---|---|
| A | 1-15 | `for` over strings and lists, accumulators, basic searching |
| B | 16-30 | `range()`, counters, numeric patterns, FizzBuzz, primes |
| C | 31-45 | `while`, sentinels, validation, termination, number algorithms |
| D | 46-60 | `break`, `continue`, loop `else`, early exit |
| E | 61-75 | Nested loops, patterns, 2D lists (matrices) |
| F | 76-90 | `enumerate`, `zip`, dictionaries, sets, classic algorithms |
| G | 91-100 | Comprehensions, iterators, generators, `itertools`, pitfalls, capstone |

---

## Section A: Fundamentals (1-15)

### Problem 1: Print every fruit

**Problem:** Given `fruits = ["apple", "banana", "cherry"]`, print each fruit on its own line.

**Hint:** A `for` loop gives you one element at a time: `for item in collection:`.

**Solution:**
```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

**Concept Explanation:** A `for` loop visits each element of an *iterable* (list, string, tuple, dict, range...) in order. On each pass the loop variable (`fruit`) is bound to the next element, and the indented block runs. Indentation defines the loop body. Forgetting the colon or the indent is a `SyntaxError` / `IndentationError`.

### Problem 2: Print every character

**Problem:** Print each character of `"python"` on its own line.

**Hint:** Strings are iterable too.

**Solution:**
```python
for ch in "python":
    print(ch)
```

**Concept Explanation:** A string is a sequence of characters, so it can be looped over exactly like a list. Each element is itself a one-character string.

### Problem 3: Numbers 1 to 10

**Problem:** Print the numbers 1 to 10.

**Hint:** `range(start, stop)` stops *before* `stop`.

**Solution:**
```python
for n in range(1, 11):
    print(n)
```

**Concept Explanation:** `range(1, 11)` produces 1, 2, ..., 10. The stop value is exclusive. This off-by-one rule is the most common beginner mistake. `range` is lazy: it does not build a list of numbers in memory, it generates them on demand.

### Problem 4: Sum of a list

**Problem:** Compute the sum of `[4, 8, 15, 16, 23, 42]` without using `sum()`.

**Hint:** Start a variable at 0 before the loop and add to it inside.

**Solution:**
```python
numbers = [4, 8, 15, 16, 23, 42]
total = 0
for n in numbers:
    total += n
print(total)  # 108
```

**Concept Explanation:** This is the **accumulator pattern**: initialise a variable before the loop, update it each iteration, use it after the loop. Initialise *outside* the loop; if you put `total = 0` inside, it resets every pass.

### Problem 5: Count items manually

**Problem:** Count how many items are in `["a", "b", "c", "d"]` without `len()`.

**Hint:** Add 1 to a counter every iteration.

**Solution:**
```python
items = ["a", "b", "c", "d"]
count = 0
for _ in items:
    count += 1
print(count)  # 4
```

**Concept Explanation:** A **counter** is an accumulator that adds 1. The name `_` is a convention meaning "I do not use this value". In real code, prefer `len(items)`; the manual version teaches what `len` does conceptually.

### Problem 6: Largest value

**Problem:** Find the largest number in `[12, 45, 7, 89, 34]` without `max()`.

**Hint:** Keep a "best so far" variable and update it when you see something bigger.

**Solution:**
```python
numbers = [12, 45, 7, 89, 34]
largest = numbers[0]
for n in numbers:
    if n > largest:
        largest = n
print(largest)  # 89
```

**Concept Explanation:** This is the **running maximum** pattern. Start with the first element (not `0`, which would be wrong for all-negative lists), then compare each element. It assumes the list is non-empty; an empty list would raise `IndexError`.

### Problem 7: Smallest value and its position

**Problem:** Find the smallest number in `[12, 45, 7, 89, 34]` and the index where it occurs.

**Hint:** `range(len(numbers))` gives you indices.

**Solution:**
```python
numbers = [12, 45, 7, 89, 34]
min_index = 0
for i in range(len(numbers)):
    if numbers[i] < numbers[min_index]:
        min_index = i
print(numbers[min_index], "at index", min_index)  # 7 at index 2
```

**Concept Explanation:** Looping over indices (`range(len(x))`) lets you access position as well as value. Tracking the *index* of the best element, rather than the value, gives you both. Problem 76 shows the more Pythonic `enumerate()`.

### Problem 8: Uppercase every word

**Problem:** Build a new list with every word of `["red", "green", "blue"]` in uppercase.

**Hint:** Create an empty list first and use `.append()`.

**Solution:**
```python
words = ["red", "green", "blue"]
upper_words = []
for w in words:
    upper_words.append(w.upper())
print(upper_words)  # ['RED', 'GREEN', 'BLUE']
```

**Concept Explanation:** The **build-a-new-list** pattern: start with `[]`, append transformed items. Strings are immutable, so `w.upper()` returns a new string rather than changing `w`. Problem 91 shows the comprehension shortcut.

### Problem 9: Reverse iteration

**Problem:** Print the characters of `"python"` from last to first.

**Hint:** The built-in `reversed()` works on sequences.

**Solution:**
```python
word = "python"
for ch in reversed(word):
    print(ch)
```

**Concept Explanation:** `reversed()` returns an iterator that walks the sequence backwards without copying it. The slice `word[::-1]` is an alternative that builds a reversed copy. Use `reversed()` when you only need to loop.

### Problem 10: Count vowels

**Problem:** Count the vowels in `"Programming is fun"`.

**Hint:** Convert to lowercase, then test with `in "aeiou"`.

**Solution:**
```python
text = "Programming is fun"
vowel_count = 0
for ch in text.lower():
    if ch in "aeiou":
        vowel_count += 1
print(vowel_count)  # 5
```

**Concept Explanation:** Combining a loop with a condition gives **filtered counting**. `ch in "aeiou"` is a membership test that is true if `ch` is a substring. Lowercasing first handles both `A` and `a`. Watch out for the empty string: `"" in "aeiou"` is `True`, but here each `ch` is exactly one character.

### Problem 11: Count one letter

**Problem:** Count how many times `"a"` appears in `"banana"`.

**Hint:** Compare each character with `==`.

**Solution:**
```python
word = "banana"
count = 0
for ch in word:
    if ch == "a":
        count += 1
print(count)  # 3
```

**Concept Explanation:** Same counter pattern as Problem 10 with an equality test. `word.count("a")` does the same job in one call, but writing the loop shows what it does internally.

### Problem 12: List of squares

**Problem:** Build a list of squares of `[1, 2, 3, 4, 5]`.

**Hint:** Square a number with `n ** 2`.

**Solution:**
```python
squares = []
for n in [1, 2, 3, 4, 5]:
    squares.append(n ** 2)
print(squares)  # [1, 4, 9, 16, 25]
```

**Concept Explanation:** Transforming every element is called **mapping**. `**` is the power operator. The result list is a separate object; the source list is unchanged.

### Problem 13: Average

**Problem:** Compute the average of `[70, 85, 90, 65]`.

**Hint:** You need both a sum and a count.

**Solution:**
```python
scores = [70, 85, 90, 65]
total = 0
count = 0
for s in scores:
    total += s
    count += 1
print(total / count)  # 77.5
```

**Concept Explanation:** One loop can maintain several accumulators at once. `/` always returns a float in Python 3. If the list could be empty, guard against `ZeroDivisionError` with `if count:` first.

### Problem 14: Build a sentence

**Problem:** Join `["Python", "loops", "are", "fun"]` into one string separated by spaces using a loop.

**Hint:** Add the word and a space each time, then remove the extra space at the end.

**Solution:**
```python
words = ["Python", "loops", "are", "fun"]
sentence = ""
for w in words:
    sentence += w + " "
sentence = sentence.strip()
print(sentence)  # Python loops are fun
```

**Concept Explanation:** String accumulation works because `+=` creates a new string each time. For long lists this is slow; the idiom `" ".join(words)` is better. `strip()` removes leading and trailing whitespace.

### Problem 15: Index and value together

**Problem:** For `["x", "y", "z"]` print lines like `0 -> x`.

**Hint:** Loop over `range(len(letters))` and use `letters[i]`.

**Solution:**
```python
letters = ["x", "y", "z"]
for i in range(len(letters)):
    print(i, "->", letters[i])
```

**Concept Explanation:** Indices start at 0. `range(len(seq))` is the classic way to get positions. It works, but `enumerate()` (Problem 76) is usually cleaner.

---

## Section B: range(), Counters and Numeric Patterns (16-30)

### Problem 16: Start and stop

**Problem:** Print the numbers from 5 to 15 inclusive.

**Hint:** The stop value is exclusive, so use 16.

**Solution:**
```python
for n in range(5, 16):
    print(n)
```

**Concept Explanation:** `range(start, stop)` includes `start` and excludes `stop`. The number of items is `stop - start` (here 11).

### Problem 17: Even numbers using a step

**Problem:** Print the even numbers from 2 to 20.

**Hint:** `range(start, stop, step)`.

**Solution:**
```python
for n in range(2, 21, 2):
    print(n)
```

**Concept Explanation:** The third argument is the step. `range(2, 21, 2)` yields 2, 4, ..., 20. The step is more efficient than looping through every number and testing `n % 2 == 0`.

### Problem 18: Countdown

**Problem:** Print 10 down to 1, then `Liftoff!`.

**Hint:** A negative step counts down, so the stop must be *below* the last value you want.

**Solution:**
```python
for n in range(10, 0, -1):
    print(n)
print("Liftoff!")
```

**Concept Explanation:** With a negative step, the sequence runs while the value is greater than `stop`. `range(10, 0, -1)` ends at 1. Code after the loop (unindented) runs once, when the loop finishes.

### Problem 19: Multiplication table

**Problem:** Print the 7 times table up to 7 x 10.

**Hint:** Use an f-string: `f"{a} x {b} = {a * b}"`.

**Solution:**
```python
for i in range(1, 11):
    print(f"7 x {i} = {7 * i}")
```

**Concept Explanation:** The loop variable is just a normal variable you can use in expressions. f-strings embed expressions inside `{}` and are the modern way to format output.

### Problem 20: Sum 1 to 100

**Problem:** Find the sum of the integers from 1 to 100.

**Hint:** Accumulator plus `range(1, 101)`.

**Solution:**
```python
total = 0
for n in range(1, 101):
    total += n
print(total)  # 5050
```

**Concept Explanation:** A numeric accumulator over a range. Check your answer with the formula $\frac{n(n+1)}{2} = \frac{100 \cdot 101}{2} = 5050$. Loops are for when no formula exists.

### Problem 21: Factorial

**Problem:** Compute `5!` (5 x 4 x 3 x 2 x 1).

**Hint:** Start the accumulator at 1, not 0. Multiply instead of add.

**Solution:**
```python
n = 5
result = 1
for i in range(2, n + 1):
    result *= i
print(result)  # 120
```

**Concept Explanation:** A **product accumulator** starts at 1 (the multiplicative identity). If it started at 0 the result would always be 0. `0!` and `1!` both correctly return 1 because the loop does not run.

### Problem 22: Sum of even numbers

**Problem:** Sum the even numbers from 1 to 50.

**Hint:** Either filter with `%` or step through `range(2, 51, 2)`.

**Solution:**
```python
total = 0
for n in range(1, 51):
    if n % 2 == 0:
        total += n
print(total)  # 650
```

**Concept Explanation:** `%` gives the remainder; `n % 2 == 0` means even. This combines a range, a condition, and an accumulator, the three most common loop ingredients.

### Problem 23: Count digits using a string

**Problem:** Count the digits of `n = 90210`.

**Hint:** Convert the number to a string and loop over it.

**Solution:**
```python
n = 90210
count = 0
for _ in str(n):
    count += 1
print(count)  # 5
```

**Concept Explanation:** `str(n)` turns the number into text so you can iterate over its digits. Converting between types is a common trick for digit problems. Problem 34 does it without conversion.

### Problem 24: Sum of digits

**Problem:** Compute the sum of the digits of `n = 2468`.

**Hint:** Each character of `str(n)` can be converted back with `int()`.

**Solution:**
```python
n = 2468
total = 0
for ch in str(n):
    total += int(ch)
print(total)  # 20
```

**Concept Explanation:** Iterating characters gives strings, so you must convert with `int()` before doing arithmetic. Adding a string to an int raises `TypeError`.

### Problem 25: Powers of 2

**Problem:** Print 2^0 through 2^10.

**Hint:** Use `**` with the loop variable as the exponent.

**Solution:**
```python
for exp in range(11):
    print(f"2^{exp} = {2 ** exp}")
```

**Concept Explanation:** `range(11)` is shorthand for `range(0, 11)`. A single argument means "from 0 to n-1".

### Problem 26: FizzBuzz

**Problem:** For 1 to 30: print `Fizz` for multiples of 3, `Buzz` for multiples of 5, `FizzBuzz` for both, else the number.

**Hint:** Test for "both" (multiple of 15) first.

**Solution:**
```python
for n in range(1, 31):
    if n % 15 == 0:
        print("FizzBuzz")
    elif n % 3 == 0:
        print("Fizz")
    elif n % 5 == 0:
        print("Buzz")
    else:
        print(n)
```

**Concept Explanation:** The order of `if/elif` branches matters: the first true branch wins. If you tested `% 3` first, 15 would print `Fizz` and never reach the combined case.

### Problem 27: Collect multiples

**Problem:** Build a list of the numbers below 50 that are multiples of 3 or 5.

**Hint:** Combine conditions with `or`.

**Solution:**
```python
multiples = []
for n in range(1, 50):
    if n % 3 == 0 or n % 5 == 0:
        multiples.append(n)
print(multiples)
```

**Concept Explanation:** Boolean operators (`and`, `or`, `not`) combine conditions. Each number is added once even if it is a multiple of both, which is why `or` is right here rather than two separate `if` blocks.

### Problem 28: Compound growth

**Problem:** Deposit 1000 at 10% yearly interest. Print the balance after each of 3 years.

**Hint:** Update the balance in each iteration: `balance *= 1.10`.

**Solution:**
```python
balance = 1000
for year in range(1, 4):
    balance *= 1.10
    print(f"Year {year}: {balance:.2f}")
```

**Concept Explanation:** The loop state (`balance`) carries over between iterations, so each year builds on the last. `:.2f` formats a float to 2 decimal places. For real money use `decimal.Decimal`, because floats are inexact.

### Problem 29: Temperature table

**Problem:** Print Celsius 0 to 100 in steps of 20 with the Fahrenheit equivalent.

**Hint:** $F = C \times 9/5 + 32$.

**Solution:**
```python
for c in range(0, 101, 20):
    f = c * 9 / 5 + 32
    print(f"{c:>3} C = {f:>5.1f} F")
```

**Concept Explanation:** Variables created inside the loop body (`f`) are recomputed each pass. Format specs such as `:>3` right-align in a field of width 3, which makes tables line up.

### Problem 30: Is it prime?

**Problem:** Decide whether `n = 29` is prime. A prime is greater than 1 and divisible only by 1 and itself.

**Hint:** Try divisors from 2 up to the square root of `n`. Use a flag variable.

**Solution:**
```python
n = 29
is_prime = n > 1
for d in range(2, int(n ** 0.5) + 1):
    if n % d == 0:
        is_prime = False
print(is_prime)  # True
```

**Concept Explanation:** A **flag** is a boolean set before the loop and flipped when a condition is met. You only need to test divisors up to $\sqrt{n}$ because any factor above that pairs with one below it. This version keeps looping after finding a factor; Problem 50 stops early with `break`.

---

## Section C: while Loops (31-45)

### Problem 31: Count to 5 with while

**Problem:** Print 1 to 5 using a `while` loop.

**Hint:** You need three things: initialise, condition, update.

**Solution:**
```python
n = 1
while n <= 5:
    print(n)
    n += 1
```

**Concept Explanation:** A `while` loop repeats as long as its condition is true. Use it when you do not know in advance how many iterations you need. The three parts are initialisation (`n = 1`), the condition (`n <= 5`), and the update (`n += 1`). Forgetting the update creates an **infinite loop**; stop it with Ctrl+C.

### Problem 32: Run until a limit is passed

**Problem:** Add 1, 2, 3, ... until the running total exceeds 100. Print the last number added and the total.

**Hint:** The number of iterations is unknown, which is a good fit for `while`.

**Solution:**
```python
total = 0
n = 0
while total <= 100:
    n += 1
    total += n
print(n, total)  # 14 105
```

**Concept Explanation:** The condition is checked *before* each iteration. The loop exits only after `total` has already passed 100, so the final iteration overshoots. Think about whether you need the value before or after the change.

### Problem 33: Countdown with while

**Problem:** Count down from 5 to 1 using `while`, then print `Go!`.

**Hint:** Decrease the counter instead of increasing it.

**Solution:**
```python
n = 5
while n > 0:
    print(n)
    n -= 1
print("Go!")
```

**Concept Explanation:** The update can move in either direction. The condition must eventually become false, so the update must move toward it. If the loop used `n += 1` here, it would never end.

### Problem 34: Count digits without strings

**Problem:** Count the digits of `n = 90210` using arithmetic only.

**Hint:** Integer division `// 10` removes the last digit.

**Solution:**
```python
n = 90210
count = 0
while n > 0:
    n //= 10
    count += 1
print(count)  # 5
```

**Concept Explanation:** `//` is floor division. Repeatedly dividing by 10 strips digits one at a time until 0 is reached. Note this prints 0 for `n = 0`, which really has one digit; special-case it if needed.

### Problem 35: Reverse a number

**Problem:** Reverse `n = 12345` to get `54321`.

**Hint:** `n % 10` gives the last digit; build the result with `result * 10 + digit`.

**Solution:**
```python
n = 12345
reversed_n = 0
while n > 0:
    digit = n % 10
    reversed_n = reversed_n * 10 + digit
    n //= 10
print(reversed_n)  # 54321
```

**Concept Explanation:** `%` extracts the last digit, `//` removes it, and multiplying by 10 shifts the digits already collected one place left. This is the foundation of many digit algorithms.

### Problem 36: Sentinel loop

**Problem:** Keep asking the user for numbers and add them up. Stop when the user types `0`.

**Hint:** Read the first value *before* the loop, then read again at the end of each iteration.

**Solution:**
```python
total = 0
number = int(input("Enter a number (0 to stop): "))
while number != 0:
    total += number
    number = int(input("Enter a number (0 to stop): "))
print("Total:", total)
```

**Concept Explanation:** A **sentinel** is a special value that signals "stop". The "read, test, process, read again" structure (a priming read) ensures the sentinel itself is not added to the total. Entering text that is not a number raises `ValueError`; Problem 37 handles bad input.

### Problem 37: Input validation

**Problem:** Ask for a positive integer and repeat the question until the user gives a valid one.

**Hint:** Start with a "not valid yet" state and use `try/except` around `int()`.

**Solution:**
```python
value = None
while value is None:
    text = input("Enter a positive integer: ")
    try:
        number = int(text)
    except ValueError:
        print("That is not an integer.")
        continue
    if number > 0:
        value = number
    else:
        print("The number must be positive.")
print("You entered", value)
```

**Concept Explanation:** A validation loop keeps going until it has acceptable data. `None` serves as "no valid value yet". `try/except` catches `ValueError` from `int()`. `continue` jumps straight to the next iteration and is covered fully in Section D.

### Problem 38: Collatz sequence

**Problem:** Starting from `n = 6`, repeat: if even, `n = n / 2`; if odd, `n = 3n + 1`, until `n` is 1. Print every value.

**Hint:** Use `//` so values stay integers.

**Solution:**
```python
n = 6
print(n)
while n != 1:
    if n % 2 == 0:
        n //= 2
    else:
        n = 3 * n + 1
    print(n)
# 6 3 10 5 16 8 4 2 1
```

**Concept Explanation:** Nobody has proven that this loop terminates for every starting value, yet it does for every number tested. That makes it a good example of a `while` loop whose length cannot be predicted in advance.

### Problem 39: Greatest common divisor

**Problem:** Compute the GCD of 48 and 18 with Euclid's algorithm.

**Hint:** Replace `(a, b)` with `(b, a % b)` until `b` is 0.

**Solution:**
```python
a, b = 48, 18
while b != 0:
    a, b = b, a % b
print(a)  # 6
```

**Concept Explanation:** `a, b = b, a % b` is **tuple unpacking**: both right-hand values are computed first, then assigned together, so no temporary variable is needed. Euclid's algorithm shrinks the problem each pass, which guarantees termination.

### Problem 40: Number guessing game

**Problem:** The secret number is 42. Keep asking for guesses, tell the user "too low" or "too high", and report how many tries it took.

**Hint:** Keep a `tries` counter and loop until the guess equals the secret.

**Solution:**
```python
secret = 42
tries = 0
guess = None
while guess != secret:
    guess = int(input("Guess the number: "))
    tries += 1
    if guess < secret:
        print("Too low")
    elif guess > secret:
        print("Too high")
print(f"Correct! It took {tries} tries.")
```

**Concept Explanation:** Initialising `guess = None` guarantees the condition is true on the first check so the loop body runs at least once. This game is a classic "repeat until success" loop. Later, `random.randint` can supply the secret.

### Problem 41: Decimal to binary

**Problem:** Convert `n = 10` to binary without using `bin()`.

**Hint:** Repeatedly divide by 2 and collect remainders; the first remainder is the *last* bit.

**Solution:**
```python
n = 10
bits = ""
while n > 0:
    bits = str(n % 2) + bits
    n //= 2
print(bits)  # 1010
```

**Concept Explanation:** Prepending (`str(...) + bits`) puts each new remainder in front, which fixes the reversed order. The loop runs about $\log_2 n$ times. For `n = 0` this prints an empty string, so handle that case if it matters.

### Problem 42: Growth until a target

**Problem:** A population of 1000 grows 10% per year. How many years until it reaches 2000 or more?

**Hint:** Count years inside the loop; the loop condition is the target.

**Solution:**
```python
population = 1000
years = 0
while population < 2000:
    population *= 1.10
    years += 1
print(years)  # 8
```

**Concept Explanation:** When you want to know "how long until...", `while` with a counter is the natural tool, because a `for` loop needs the number of iterations up front.

### Problem 43: Withdrawals until empty

**Problem:** A balance of 500 allows withdrawals of 120. How many withdrawals can be made, and what is left?

**Hint:** Only withdraw while the balance covers the amount.

**Solution:**
```python
balance = 500
withdrawals = 0
while balance >= 120:
    balance -= 120
    withdrawals += 1
print(withdrawals, balance)  # 4 20
```

**Concept Explanation:** The loop condition protects the operation inside it: the balance never goes negative because the check happens first. Choosing `>=` rather than `>` decides whether a balance of exactly 120 can be withdrawn.

### Problem 44: Palindrome number

**Problem:** Check whether `n = 12321` reads the same forwards and backwards, using arithmetic only.

**Hint:** Reverse it as in Problem 35, then compare with the original; keep a copy.

**Solution:**
```python
n = 12321
original = n
reversed_n = 0
while n > 0:
    reversed_n = reversed_n * 10 + n % 10
    n //= 10
print(original == reversed_n)  # True
```

**Concept Explanation:** The loop destroys `n`, so you save it first. Reusing a previous algorithm (reversal) as a building block is a core programming skill.

### Problem 45: Menu loop

**Problem:** Show a menu repeatedly: `1) Say hello`, `2) Say goodbye`, `q) Quit`. Exit only when the user types `q`.

**Hint:** Initialise the choice to something that is not `q`.

**Solution:**
```python
choice = ""
while choice != "q":
    print("1) Say hello")
    print("2) Say goodbye")
    print("q) Quit")
    choice = input("Choose: ").strip().lower()
    if choice == "1":
        print("Hello!")
    elif choice == "2":
        print("Goodbye!")
    elif choice != "q":
        print("Invalid choice")
```

**Concept Explanation:** Interactive programs are driven by a `while` loop that runs until the user asks to quit. `.strip().lower()` normalises input, so `" Q "` still works. The last `elif` reports invalid input without treating `q` as an error.

---

## Section D: break, continue and loop else (46-60)

### Problem 46: First even number

**Problem:** Print the first even number in `[7, 3, 9, 12, 5, 8]` and stop looking.

**Hint:** `break` exits the loop immediately.

**Solution:**
```python
for n in [7, 3, 9, 12, 5, 8]:
    if n % 2 == 0:
        print("First even:", n)
        break
```

**Concept Explanation:** `break` terminates the *innermost* loop at once. It saves work: once the answer is found there is no reason to scan the rest. Output is `First even: 12`; `8` is never examined.

### Problem 47: Stop at a negative

**Problem:** Print numbers from `[4, 8, 15, -3, 9]` until a negative one appears. Do not print the negative.

**Hint:** Test for the stop condition before printing.

**Solution:**
```python
for n in [4, 8, 15, -3, 9]:
    if n < 0:
        break
    print(n)
```

**Concept Explanation:** Placing the `break` check *before* the work decides whether the stopping item is processed. Put it after `print(n)` and the negative would be printed.

### Problem 48: Skip odd numbers

**Problem:** Print only the even numbers from 1 to 10, using `continue`.

**Hint:** `continue` skips the rest of the current iteration.

**Solution:**
```python
for n in range(1, 11):
    if n % 2 != 0:
        continue
    print(n)
```

**Concept Explanation:** `continue` jumps back to the loop header and moves to the next item. Use it to filter out unwanted cases early and avoid deep nesting. `break` leaves the loop; `continue` only leaves the current pass.

### Problem 49: Print only consonants

**Problem:** Print the consonants of `"education"`, skipping vowels.

**Hint:** If the character is a vowel, `continue`.

**Solution:**
```python
for ch in "education":
    if ch in "aeiou":
        continue
    print(ch)  # d c t n
```

**Concept Explanation:** A guard clause with `continue` keeps the main logic at one indentation level, which is easier to read than wrapping the whole body in `if ch not in "aeiou":`.

### Problem 50: for-else prime check

**Problem:** Check whether 29 and 15 are prime. Stop at the first divisor and report using a loop `else`.

**Hint:** An `else` on a loop runs only if the loop finished *without* hitting `break`.

**Solution:**
```python
for n in (29, 15):
    for d in range(2, int(n ** 0.5) + 1):
        if n % d == 0:
            print(n, "is not prime (divisible by", d, ")")
            break
    else:
        print(n, "is prime")
```

**Concept Explanation:** Loop `else` means "no break happened". It replaces the flag variable from Problem 30. A common mistake is reading it as "else for the last `if`"; it belongs to the loop. Note this simple version would call 1 prime, so check `n > 1` for general use.

### Problem 51: Search with not-found

**Problem:** Check whether `"Dave"` is in `["Ann", "Bob", "Cara"]`. Print where it was found or `Not found`.

**Hint:** Use `for ... else` and `break`.

**Solution:**
```python
names = ["Ann", "Bob", "Cara"]
target = "Dave"
for i in range(len(names)):
    if names[i] == target:
        print("Found at index", i)
        break
else:
    print("Not found")
```

**Concept Explanation:** Search loops have two outcomes, found or not found. `for/else` handles both without an extra variable. In everyday code `target in names` is simpler; this teaches the underlying mechanism.

### Problem 52: Limited password attempts

**Problem:** Let the user try a password up to 3 times. The right password is `"secret"`. Print `Access granted` on success or `Locked out` after 3 failures.

**Hint:** Use `for attempt in range(3)` plus `else`.

**Solution:**
```python
for attempt in range(3):
    if input("Password: ") == "secret":
        print("Access granted")
        break
    print("Wrong password")
else:
    print("Locked out")
```

**Concept Explanation:** A bounded retry is better expressed with `for` than `while`, because the maximum is known. The `else` runs only if every attempt failed.

### Problem 53: Sum until a negative

**Problem:** Add numbers from `[5, 10, 15, -1, 20]` until the first negative. Print the total.

**Hint:** Combine accumulator and `break`.

**Solution:**
```python
total = 0
for n in [5, 10, 15, -1, 20]:
    if n < 0:
        break
    total += n
print(total)  # 30
```

**Concept Explanation:** The accumulator survives the `break`; the code after the loop can still use `total`. This is a typical pattern for "process until an invalid or stop item".

### Problem 54: First number matching two rules

**Problem:** Find the first number greater than 100 that is divisible by both 5 and 7.

**Hint:** An endless `while True` with `break` fits when you do not know the range.

**Solution:**
```python
n = 101
while True:
    if n % 5 == 0 and n % 7 == 0:
        print(n)  # 105
        break
    n += 1
```

**Concept Explanation:** `while True` creates an intentionally infinite loop that is exited by `break`. It is acceptable when the exit condition is awkward to put in the header, but make sure a `break` is reachable.

### Problem 55: Skip multiples of 3

**Problem:** Print 1 to 20 but skip every multiple of 3.

**Hint:** Guard with `continue`.

**Solution:**
```python
for n in range(1, 21):
    if n % 3 == 0:
        continue
    print(n)
```

**Concept Explanation:** Same technique as Problem 48 with a different condition. Notice that in a `while` loop `continue` can cause an infinite loop if the update step is skipped, so put the update *before* `continue` in such cases.

### Problem 56: Ignore blank entries

**Problem:** From `["apple", "", "  ", "banana", "cherry"]`, print only non-blank entries.

**Hint:** `.strip()` returns an empty string for whitespace-only text, which is falsy.

**Solution:**
```python
entries = ["apple", "", "  ", "banana", "cherry"]
for entry in entries:
    if not entry.strip():
        continue
    print(entry)
```

**Concept Explanation:** Empty strings, `0`, `None`, and empty collections are **falsy**, so `if not value:` tests for emptiness. Cleaning data by skipping bad rows is one of the most common uses of `continue`.

### Problem 57: Retry until success

**Problem:** A flaky operation succeeds on the third try. Retry up to 5 times and report how many attempts were needed.

**Hint:** Simulate the operation with a function that checks the attempt number.

**Solution:**
```python
def flaky(attempt):
    return attempt >= 3

for attempt in range(1, 6):
    if flaky(attempt):
        print(f"Succeeded on attempt {attempt}")
        break
    print(f"Attempt {attempt} failed")
else:
    print("Gave up after 5 attempts")
```

**Concept Explanation:** Retry loops are everywhere in real systems (network calls, deployments). `range(1, 6)` makes the attempt numbers start at 1, and the `else` branch handles "all attempts failed".

### Problem 58: First duplicate

**Problem:** Find the first value that repeats in `[3, 1, 4, 1, 5, 9, 2, 6, 5]`.

**Hint:** Remember what you have seen. A `set` makes lookups fast.

**Solution:**
```python
seen = set()
for n in [3, 1, 4, 1, 5, 9, 2, 6, 5]:
    if n in seen:
        print("First duplicate:", n)  # 1
        break
    seen.add(n)
```

**Concept Explanation:** A set stores unique items and tests membership in roughly constant time, whereas `n in some_list` scans the list each time. "Seen so far" sets are a standard technique for duplicate problems.

### Problem 59: First repeated character

**Problem:** Find the first character in `"programming"` that has already appeared earlier.

**Hint:** Same idea as Problem 58, applied to a string.

**Solution:**
```python
seen = set()
for ch in "programming":
    if ch in seen:
        print("First repeated:", ch)  # r
        break
    seen.add(ch)
else:
    print("No repeats")
```

**Concept Explanation:** The same algorithm works on any iterable because loops treat lists, strings, and ranges uniformly. The `else` covers the case where no repeats exist.

### Problem 60: Perfect numbers

**Problem:** Find the perfect numbers up to 1000. A perfect number equals the sum of its proper divisors (for example 6 = 1 + 2 + 3).

**Hint:** For each number, sum its divisors from 1 to `n // 2`.

**Solution:**
```python
for n in range(2, 1001):
    divisor_sum = 0
    for d in range(1, n // 2 + 1):
        if n % d == 0:
            divisor_sum += d
    if divisor_sum == n:
        print(n)  # 6, 28, 496
```

**Concept Explanation:** An outer loop picks candidates and an inner loop gathers evidence. This is brute force: about $n^2/2$ operations in total. It is fine for 1000 but slow for millions, which is why algorithm choice matters (Problem 97 discusses efficiency).

---

## Section E: Nested Loops and 2D Data (61-75)

### Problem 61: Multiplication grid

**Problem:** Print a 5 x 5 multiplication table, one row per line.

**Hint:** An outer loop for rows, an inner loop for columns. Use `end=""` to stay on the same line.

**Solution:**
```python
for row in range(1, 6):
    for col in range(1, 6):
        print(f"{row * col:4}", end="")
    print()
```

**Concept Explanation:** For every iteration of the outer loop, the inner loop runs to completion. Total work is rows x columns. `end=""` suppresses the newline, and the bare `print()` after the inner loop moves to the next line. `:4` pads each number to width 4.

### Problem 62: Right triangle

**Problem:** Print a right triangle of stars with 5 rows.

```
*
**
***
****
*****
```

**Hint:** Row `i` has `i` stars; string repetition `"*" * i` helps.

**Solution:**
```python
for i in range(1, 6):
    print("*" * i)
```

**Concept Explanation:** Pattern problems often need only one loop when you use string multiplication. Here the row number controls the width. The nested equivalent is `for _ in range(i): print("*", end="")`.

### Problem 63: Inverted triangle

**Problem:** Print the triangle upside down (5 stars on the first row, down to 1).

**Hint:** Count down with a negative step.

**Solution:**
```python
for i in range(5, 0, -1):
    print("*" * i)
```

**Concept Explanation:** Reversing a pattern is usually a matter of reversing the range. Compare with Problems 18 and 62.

### Problem 64: Pyramid

**Problem:** Print a centred pyramid with 5 rows.

```
    *
   ***
  *****
 *******
*********
```

**Hint:** Row `i` needs `rows - i` leading spaces and `2*i - 1` stars.

**Solution:**
```python
rows = 5
for i in range(1, rows + 1):
    print(" " * (rows - i) + "*" * (2 * i - 1))
```

**Concept Explanation:** Spaces and stars are both formulas of the row number. Deriving the formulas on paper with small examples (row 1: 4 spaces and 1 star, row 2: 3 spaces and 3 stars) is the real skill being practiced.

### Problem 65: Number triangle

**Problem:** Print rows `1`, `1 2`, `1 2 3`, ... up to 5.

**Hint:** The inner loop's `range` depends on the outer variable.

**Solution:**
```python
for i in range(1, 6):
    for j in range(1, i + 1):
        print(j, end=" ")
    print()
```

**Concept Explanation:** The inner loop's bounds can depend on the outer loop variable, so each row has a different length. This "triangular" nesting does 1 + 2 + ... + n iterations.

### Problem 66: Pascal's triangle

**Problem:** Print the first 5 rows of Pascal's triangle. Each inner value is the sum of the two values above it.

**Hint:** Build each new row from the previous row.

**Solution:**
```python
rows = 5
row = [1]
for _ in range(rows):
    print(" ".join(str(x) for x in row).center(20))
    new_row = [1]
    for i in range(len(row) - 1):
        new_row.append(row[i] + row[i + 1])
    new_row.append(1)
    row = new_row
```

**Concept Explanation:** The loop carries state (`row`) from one iteration to the next. `_` marks a loop variable that is intentionally unused. The inner loop adds adjacent pairs. `str.center(20)` pads text to a width of 20 with the text in the middle.

### Problem 67: Checkerboard

**Problem:** Print an 8 x 8 checkerboard using `#` and `.` alternately.

**Hint:** Cells where `(row + col)` is even get one symbol, odd get the other.

**Solution:**
```python
for r in range(8):
    line = ""
    for c in range(8):
        line += "#" if (r + c) % 2 == 0 else "."
    print(line)
```

**Concept Explanation:** The parity of `row + col` alternates along rows and columns, which creates the checker effect. `A if condition else B` is a *conditional expression*. Building a whole line first and printing it once is often cleaner than many `end=""` prints.

### Problem 68: All pairs

**Problem:** Given `sizes = ["S", "M", "L"]` and `colors = ["red", "blue"]`, print every size/colour combination.

**Hint:** One loop inside the other.

**Solution:**
```python
sizes = ["S", "M", "L"]
colors = ["red", "blue"]
for size in sizes:
    for color in colors:
        print(size, color)
```

**Concept Explanation:** Nested loops generate the **Cartesian product**: 3 x 2 = 6 combinations. `itertools.product(sizes, colors)` does the same in one loop (Problem 98).

### Problem 69: Sum of a matrix

**Problem:** Sum all the values of `[[1, 2, 3], [4, 5, 6], [7, 8, 9]]`.

**Hint:** A 2D list is a list of lists.

**Solution:**
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
total = 0
for row in matrix:
    for value in row:
        total += value
print(total)  # 45
```

**Concept Explanation:** The outer loop yields each inner list; the inner loop yields each number. Looping directly over elements, rather than indices, is the preferred style when positions do not matter.

### Problem 70: Row and column sums

**Problem:** For the same matrix print the sum of each row and each column.

**Hint:** Rows are direct; for columns, loop over column indices and add `row[c]` from every row.

**Solution:**
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

for row in matrix:
    print("Row sum:", sum(row))

for c in range(len(matrix[0])):
    col_total = 0
    for row in matrix:
        col_total += row[c]
    print("Column", c, "sum:", col_total)
```

**Concept Explanation:** Row access is natural in a list of lists; column access needs an index. Row sums: 6, 15, 24. Column sums: 12, 15, 18.

### Problem 71: Transpose

**Problem:** Transpose `[[1, 2, 3], [4, 5, 6]]` so rows become columns.

**Hint:** The result has `len(matrix[0])` rows. Build each new row by collecting one column.

**Solution:**
```python
matrix = [[1, 2, 3], [4, 5, 6]]
transposed = []
for c in range(len(matrix[0])):
    new_row = []
    for r in range(len(matrix)):
        new_row.append(matrix[r][c])
    transposed.append(new_row)
print(transposed)  # [[1, 4], [2, 5], [3, 6]]
```

**Concept Explanation:** `matrix[r][c]` reads row `r`, column `c`. Swapping the roles of the two loops swaps rows and columns. The shortcut `list(zip(*matrix))` returns tuples instead of lists.

### Problem 72: Find a value in a grid

**Problem:** Find the position of `8` in `[[1, 2, 3], [4, 5, 6], [7, 8, 9]]` and stop all looping once found.

**Hint:** `break` exits only the inner loop. Use a flag or a function with `return`.

**Solution:**
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
target = 8
position = None

for r in range(len(matrix)):
    for c in range(len(matrix[r])):
        if matrix[r][c] == target:
            position = (r, c)
            break
    if position is not None:
        break

print(position)  # (2, 1)
```

**Concept Explanation:** `break` only leaves the innermost loop, so breaking out of nested loops needs a second `break` guarded by a flag. Putting the search in a function and using `return` is an even cleaner way to exit both loops at once.

### Problem 73: Diamond

**Problem:** Print a diamond with a widest row of 7 stars (4 rows growing, then 3 shrinking).

**Hint:** Print the pyramid from Problem 64, then a reversed pyramid without the middle row.

**Solution:**
```python
n = 4
for i in range(1, n + 1):
    print(" " * (n - i) + "*" * (2 * i - 1))
for i in range(n - 1, 0, -1):
    print(" " * (n - i) + "*" * (2 * i - 1))
```

**Concept Explanation:** Complex shapes are compositions of simple ones. The second loop starts at `n - 1` so the middle row is not printed twice.

### Problem 74: Pythagorean triples

**Problem:** Find all triples `a < b < c <= 30` where `a**2 + b**2 == c**2`.

**Hint:** Three nested loops, each starting after the previous variable to avoid duplicates.

**Solution:**
```python
for a in range(1, 31):
    for b in range(a + 1, 31):
        for c in range(b + 1, 31):
            if a * a + b * b == c * c:
                print(a, b, c)
# starts: 3 4 5, 5 12 13, 6 8 10, 7 24 25 ...
```

**Concept Explanation:** Starting each inner range one past the outer variable enforces `a < b < c` and removes repeats like (4, 3, 5). Three nested loops over 30 values is fine, but the cost grows as $n^3$, so brute force quickly becomes impractical.

### Problem 75: Diagonals

**Problem:** For `[[1, 2, 3], [4, 5, 6], [7, 8, 9]]` compute the main diagonal sum and the anti-diagonal sum.

**Hint:** Main diagonal cells are `[i][i]`; anti-diagonal cells are `[i][n - 1 - i]`.

**Solution:**
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
n = len(matrix)
main = 0
anti = 0
for i in range(n):
    main += matrix[i][i]
    anti += matrix[i][n - 1 - i]
print(main, anti)  # 15 15
```

**Concept Explanation:** A single loop over `i` can address both diagonals. Matching the loop structure to the data's structure avoids unnecessary nesting: a diagonal has `n` cells, so you need `n` iterations, not `n * n`.

---

## Section F: Pythonic Iteration and Classic Algorithms (76-90)

### Problem 76: enumerate

**Problem:** Print a numbered list starting at 1 for `["tea", "coffee", "juice"]`, for example `1. tea`.

**Hint:** `enumerate(iterable, start=1)`.

**Solution:**
```python
drinks = ["tea", "coffee", "juice"]
for number, drink in enumerate(drinks, start=1):
    print(f"{number}. {drink}")
```

**Concept Explanation:** `enumerate` yields `(index, value)` pairs, and the `for number, drink` header unpacks each pair. It replaces `range(len(x))` and is the preferred way to get indices. `start` changes the first number.

### Problem 77: zip

**Problem:** Print each student with their score from `names = ["Ann", "Bob", "Cara"]` and `scores = [90, 72, 85]`.

**Hint:** `zip(a, b)` walks both lists in parallel.

**Solution:**
```python
names = ["Ann", "Bob", "Cara"]
scores = [90, 72, 85]
for name, score in zip(names, scores):
    print(f"{name}: {score}")
```

**Concept Explanation:** `zip` pairs elements by position and yields tuples. It is safer and clearer than indexing both lists with the same `i`.

### Problem 78: zip with unequal lengths

**Problem:** What does `zip([1, 2, 3, 4], ["a", "b"])` produce? Print the pairs.

**Hint:** Think about which list runs out first.

**Solution:**
```python
for pair in zip([1, 2, 3, 4], ["a", "b"]):
    print(pair)
# (1, 'a')
# (2, 'b')
```

**Concept Explanation:** `zip` stops at the *shortest* input, silently dropping the rest. From Python 3.10, `zip(a, b, strict=True)` raises an error on a length mismatch, and `itertools.zip_longest` pads the shorter one.

### Problem 79: Looping over a dictionary

**Problem:** Given `ages = {"Ann": 30, "Bob": 25, "Cara": 41}`, print keys, then values, then key/value pairs.

**Hint:** Use `.keys()`, `.values()`, `.items()`.

**Solution:**
```python
ages = {"Ann": 30, "Bob": 25, "Cara": 41}

for name in ages:
    print(name)
for age in ages.values():
    print(age)
for name, age in ages.items():
    print(name, "is", age)
```

**Concept Explanation:** Looping over a dict directly gives its keys. `.items()` yields `(key, value)` tuples and is the most common form. Since Python 3.7, dictionaries keep insertion order. Do not add or remove keys while looping (Problem 99).

### Problem 80: Word frequency

**Problem:** Count how many times each word appears in `"the cat and the hat and the bat"`.

**Hint:** `counts.get(word, 0) + 1`.

**Solution:**
```python
text = "the cat and the hat and the bat"
counts = {}
for word in text.split():
    counts[word] = counts.get(word, 0) + 1
print(counts)
# {'the': 3, 'cat': 1, 'and': 2, 'hat': 1, 'bat': 1}
```

**Concept Explanation:** A dictionary used as a counter is one of the most important loop patterns. `.get(key, default)` returns a default when the key is missing, which avoids `KeyError`. `collections.Counter` does this automatically.

### Problem 81: Most common character

**Problem:** Find the most frequent character in `"mississippi"` and its count.

**Hint:** Count with a dict, then loop again to find the highest.

**Solution:**
```python
counts = {}
for ch in "mississippi":
    counts[ch] = counts.get(ch, 0) + 1

best_char = None
best_count = 0
for ch, n in counts.items():
    if n > best_count:
        best_char, best_count = ch, n
print(best_char, best_count)  # i 4
```

**Concept Explanation:** Two loops, two jobs: count, then pick the maximum. `i` and `s` both appear 4 times; because `>` is strict, the first one found (`i`) wins. Using `>=` would make the last one win. Always decide how ties should be handled.

### Problem 82: Unique values in order

**Problem:** Remove duplicates from `[3, 1, 3, 2, 1, 4]` while keeping the original order.

**Hint:** Use a `seen` set and a result list.

**Solution:**
```python
seen = set()
unique = []
for n in [3, 1, 3, 2, 1, 4]:
    if n not in seen:
        seen.add(n)
        unique.append(n)
print(unique)  # [3, 1, 2, 4]
```

**Concept Explanation:** `set(values)` would remove duplicates but loses order. Combining a set (fast lookup) with a list (order) gives both. Elements must be hashable (numbers, strings, tuples) to go in a set.

### Problem 83: Find all duplicates

**Problem:** List every value that appears more than once in `[1, 2, 3, 2, 4, 3, 3, 5]`.

**Hint:** Track values seen once and values already reported.

**Solution:**
```python
seen = set()
duplicates = set()
for n in [1, 2, 3, 2, 4, 3, 3, 5]:
    if n in seen:
        duplicates.add(n)
    else:
        seen.add(n)
print(sorted(duplicates))  # [2, 3]
```

**Concept Explanation:** Adding to a set that already holds the value does nothing, so `3` is recorded once even though it repeats twice. `sorted()` returns a new sorted list because sets have no defined order.

### Problem 84: Two sum

**Problem:** Find the indices of two numbers in `[2, 7, 11, 15]` that add up to 9.

**Hint:** Brute force with nested loops where `j` starts at `i + 1`; then think about a dictionary approach.

**Solution:**
```python
nums = [2, 7, 11, 15]
target = 9

# Brute force: O(n^2)
for i in range(len(nums)):
    for j in range(i + 1, len(nums)):
        if nums[i] + nums[j] == target:
            print(i, j)  # 0 1

# Faster: O(n) with a dictionary of value -> index
seen = {}
for i, n in enumerate(nums):
    if target - n in seen:
        print(seen[target - n], i)  # 0 1
        break
    seen[n] = i
```

**Concept Explanation:** The nested version checks every pair. The dictionary version asks "have I already seen the number that completes this one?", which needs only one pass. Trading memory for speed with a hash table is a core technique.

### Problem 85: Bubble sort

**Problem:** Sort `[5, 2, 9, 1, 6]` in ascending order without `sort()`.

**Hint:** Repeatedly compare neighbours and swap them if out of order. After each pass the largest unsorted value sits at the end.

**Solution:**
```python
data = [5, 2, 9, 1, 6]
n = len(data)
for i in range(n - 1):
    for j in range(n - 1 - i):
        if data[j] > data[j + 1]:
            data[j], data[j + 1] = data[j + 1], data[j]
print(data)  # [1, 2, 5, 6, 9]
```

**Concept Explanation:** Each outer pass bubbles the largest remaining value to its final position, so the inner loop can shrink by one each time (`n - 1 - i`). Bubble sort takes $O(n^2)$ time and is for learning only; use `sorted()` or `.sort()` in real code.

### Problem 86: Linear search

**Problem:** Write a function that returns the index of a value in a list, or `-1` if absent.

**Hint:** `return` inside a loop ends both the loop and the function.

**Solution:**
```python
def linear_search(items, target):
    for i, value in enumerate(items):
        if value == target:
            return i
    return -1

print(linear_search([10, 20, 30], 20))  # 1
print(linear_search([10, 20, 30], 99))  # -1
```

**Concept Explanation:** `return` is the cleanest way to exit nested logic early. The `-1` after the loop runs only when nothing matched. It is $O(n)$, since each element may be checked.

### Problem 87: Binary search

**Problem:** Search the sorted list `[2, 5, 8, 12, 16, 23, 38]` for 23 by repeatedly halving the search range.

**Hint:** Keep `low` and `high` indices and check the middle.

**Solution:**
```python
def binary_search(items, target):
    low, high = 0, len(items) - 1
    while low <= high:
        mid = (low + high) // 2
        if items[mid] == target:
            return mid
        if items[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

print(binary_search([2, 5, 8, 12, 16, 23, 38], 23))  # 5
```

**Concept Explanation:** Each iteration discards half the remaining range, so it needs only about $\log_2 n$ steps (1,000,000 items need about 20 comparisons). It requires sorted data. The `while low <= high` condition and the `mid + 1` / `mid - 1` updates must be exact or the loop can run forever.

### Problem 88: Fibonacci numbers

**Problem:** Print the first 10 Fibonacci numbers: 0 1 1 2 3 5 8 13 21 34.

**Hint:** Two variables, updated together.

**Solution:**
```python
a, b = 0, 1
for _ in range(10):
    print(a, end=" ")
    a, b = b, a + b
```

**Concept Explanation:** Simultaneous assignment (`a, b = b, a + b`) updates both values from the old ones. Each iteration needs only the previous two values, so the loop uses constant memory.

### Problem 89: Reverse a list in place

**Problem:** Reverse `[1, 2, 3, 4, 5]` in place without `reverse()` or slicing.

**Hint:** Swap the first and last, then move both pointers toward the middle.

**Solution:**
```python
data = [1, 2, 3, 4, 5]
left, right = 0, len(data) - 1
while left < right:
    data[left], data[right] = data[right], data[left]
    left += 1
    right -= 1
print(data)  # [5, 4, 3, 2, 1]
```

**Concept Explanation:** This is the **two-pointer technique**: two indices move toward each other. The condition `left < right` stops at the middle, so the centre element of an odd-length list is untouched. No extra list is created.

### Problem 90: Group words by first letter

**Problem:** Group `["apple", "avocado", "banana", "blueberry", "cherry"]` into a dictionary keyed by first letter.

**Hint:** `dict.setdefault(key, [])` creates the list if the key is new.

**Solution:**
```python
words = ["apple", "avocado", "banana", "blueberry", "cherry"]
groups = {}
for word in words:
    groups.setdefault(word[0], []).append(word)
print(groups)
# {'a': ['apple', 'avocado'], 'b': ['banana', 'blueberry'], 'c': ['cherry']}
```

**Concept Explanation:** **Grouping** is one of the most common data-processing loops. `setdefault` returns the existing list or inserts a new empty one, then `.append` adds to it. `collections.defaultdict(list)` is the equivalent shortcut.

---

## Section G: Comprehensions, Iterators, Generators and Capstone (91-100)

### Problem 91: List comprehension

**Problem:** Rewrite Problem 12 (squares of 1 to 5) in a single line.

**Hint:** `[expression for item in iterable]`.

**Solution:**
```python
squares = [n ** 2 for n in range(1, 6)]
print(squares)  # [1, 4, 9, 16, 25]
```

**Concept Explanation:** A comprehension is a compact loop that builds a list. It is equivalent to creating `[]` and appending in a `for` loop. Use it when the loop is a simple transformation; use a normal loop when the body is complicated.

### Problem 92: Comprehension with a condition

**Problem:** From `range(1, 21)` build a list of even numbers, then a list where odd numbers become `0`.

**Hint:** A trailing `if` filters; `A if cond else B` placed *before* the `for` transforms.

**Solution:**
```python
evens = [n for n in range(1, 21) if n % 2 == 0]
zeroed = [n if n % 2 == 0 else 0 for n in range(1, 11)]
print(evens)   # [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
print(zeroed)  # [0, 2, 0, 4, 0, 6, 0, 8, 0, 10]
```

**Concept Explanation:** Two different positions, two different meanings: a trailing `if` *removes* items; a conditional expression at the front *changes* items but keeps all of them. Mixing these up is a common source of syntax errors.

### Problem 93: Dictionary comprehension

**Problem:** Build `{word: length}` for `["apple", "fig", "banana"]`.

**Hint:** `{key: value for item in iterable}`.

**Solution:**
```python
words = ["apple", "fig", "banana"]
lengths = {w: len(w) for w in words}
print(lengths)  # {'apple': 5, 'fig': 3, 'banana': 6}
```

**Concept Explanation:** The same idea applies to dictionaries (`{k: v ...}`) and sets (`{x ...}`). Duplicate keys overwrite earlier ones, so the last value wins.

### Problem 94: Nested comprehensions

**Problem:** Flatten `[[1, 2], [3, 4], [5, 6]]` into one list, and build a 3 x 3 multiplication table as a list of lists.

**Hint:** The `for` clauses appear in the same order as nested loops.

**Solution:**
```python
matrix = [[1, 2], [3, 4], [5, 6]]
flat = [value for row in matrix for value in row]
print(flat)  # [1, 2, 3, 4, 5, 6]

table = [[r * c for c in range(1, 4)] for r in range(1, 4)]
print(table)  # [[1, 2, 3], [2, 4, 6], [3, 6, 9]]
```

**Concept Explanation:** In `for row in matrix for value in row`, read left to right as you would nested loops (outer first). A comprehension *inside* a comprehension builds a 2D structure. If it takes more than a moment to read, use ordinary loops.

### Problem 95: How `for` really works

**Problem:** Walk through `[10, 20, 30]` manually with `iter()` and `next()`, then show what happens when it runs out.

**Hint:** `iter()` creates an iterator; `next()` fetches the next item; the end raises `StopIteration`.

**Solution:**
```python
it = iter([10, 20, 30])
print(next(it))  # 10
print(next(it))  # 20
print(next(it))  # 30

try:
    next(it)
except StopIteration:
    print("No more items")

# This is roughly what `for x in [10, 20, 30]` does:
it = iter([10, 20, 30])
while True:
    try:
        x = next(it)
    except StopIteration:
        break
    print(x)
```

**Concept Explanation:** An **iterable** (list, str, dict, range) can produce an **iterator**; the iterator remembers its position and gives items one at a time. A `for` loop calls `iter()` once, then `next()` repeatedly and swallows the `StopIteration` that signals the end. An iterator is single-use: once exhausted it stays empty.

### Problem 96: Generator function

**Problem:** Write a generator `fibonacci(limit)` that yields Fibonacci numbers up to `limit`, and loop over it.

**Hint:** Use `yield` instead of `return` and keep state in local variables.

**Solution:**
```python
def fibonacci(limit):
    a, b = 0, 1
    while a <= limit:
        yield a
        a, b = b, a + b

for n in fibonacci(50):
    print(n, end=" ")  # 0 1 1 2 3 5 8 13 21 34
```

**Concept Explanation:** A function containing `yield` returns a generator object. Each `next()` resumes execution just after the last `yield`, with local variables preserved. Values are produced lazily, one at a time, so you can represent huge or even infinite sequences without storing them.

### Problem 97: Generator expressions and efficiency

**Problem:** Compare the memory used by a list of the first million squares and the equivalent generator, then sum the squares.

**Hint:** Use `sys.getsizeof`; a generator expression looks like a list comprehension but with parentheses.

**Solution:**
```python
import sys

as_list = [n * n for n in range(1_000_000)]
as_gen = (n * n for n in range(1_000_000))

print(sys.getsizeof(as_list))  # several MB (about 8 MB)
print(sys.getsizeof(as_gen))   # a couple of hundred bytes at most

print(sum(n * n for n in range(1_000_000)))  # 333332833333500000
```

**Concept Explanation:** The list holds a million values at once; the generator computes each value on demand and holds only its current state. When you only need to loop once (to `sum`, `max`, `any`, or in a `for`), prefer a generator expression. Choose the right *algorithm* first (Problem 87 versus 86), then pick lazy structures to save memory.

### Problem 98: itertools

**Problem:** Use `itertools` to: (a) take the first 5 even numbers from an endless counter, (b) chain two lists, (c) generate all size/colour pairs from Problem 68 in one loop.

**Hint:** `count`, `islice`, `chain`, `product`.

**Solution:**
```python
from itertools import count, islice, chain, product

evens = list(islice(count(0, 2), 5))
print(evens)  # [0, 2, 4, 6, 8]

for x in chain([1, 2], ["a", "b"]):
    print(x)  # 1 2 a b

for size, color in product(["S", "M", "L"], ["red", "blue"]):
    print(size, color)
```

**Concept Explanation:** `itertools` provides efficient, lazy loop building blocks. `count` is an infinite counter, so it must be limited, here by `islice`. `chain` links iterables end to end, and `product` replaces nested loops. Never wrap an infinite iterator in `list()` directly.

### Problem 99: Loop pitfalls

**Problem:** Predict the result of removing even numbers from `data = [1, 2, 3, 4, 6, 8]` by calling `data.remove(x)` inside `for x in data`. Then fix it. Also, what is `i` after `for i in range(3): pass`?

**Hint:** Removing items shifts the later ones left while the loop's position still advances.

**Solution:**
```python
data = [1, 2, 3, 4, 6, 8]
for x in data:
    if x % 2 == 0:
        data.remove(x)
print(data)  # [1, 3, 6] -- wrong, 6 is still there

# Fix 1: iterate over a copy
data = [1, 2, 3, 4, 6, 8]
for x in data[:]:
    if x % 2 == 0:
        data.remove(x)
print(data)  # [1, 3]

# Fix 2 (usually best): build a new list
data = [1, 2, 3, 4, 6, 8]
data = [x for x in data if x % 2 != 0]
print(data)  # [1, 3]

for i in range(3):
    pass
print(i)  # 2
```

**Concept Explanation:** Never add or remove items from the collection you are iterating over: the iterator tracks an index that no longer matches the data, so elements are skipped. Iterate over a copy or build a new list. Also, the loop variable remains defined after the loop ends (`i` is 2), and it is undefined only if the loop never ran.

### Problem 100: Capstone, text analyser

**Problem:** For `text = "the quick brown fox jumps over the lazy dog the end"`, report: (a) total words, (b) the top 3 words by frequency (ties alphabetical), (c) the longest word (first one wins ties), (d) the number of vowels.

**Hint:** Combine a dictionary counter, `sorted` with a key, a running maximum, and a loop over characters.

**Solution:**
```python
text = "the quick brown fox jumps over the lazy dog the end"
words = text.split()

# (a) total words
print("Words:", len(words))  # 11

# (b) frequencies, then top 3 (highest count first, then alphabetical)
freq = {}
for w in words:
    freq[w] = freq.get(w, 0) + 1

ranked = sorted(freq.items(), key=lambda item: (-item[1], item[0]))
for word, n in ranked[:3]:
    print(word, n)
# the 3
# brown 1
# dog 1

# (c) longest word
longest = ""
for w in words:
    if len(w) > len(longest):
        longest = w
print("Longest:", longest)  # quick

# (d) vowels
vowels = 0
for ch in text:
    if ch in "aeiou":
        vowels += 1
print("Vowels:", vowels)  # 13
```

**Concept Explanation:** Real tasks combine several patterns: splitting and iterating, the dictionary counter (Problem 80), sorting with a composite key (negating the count sorts it descending while the word sorts ascending), the running maximum (Problem 6, where the strict `>` makes the first word win a tie), and filtered counting (Problem 10). Try extending it: ignore punctuation, handle uppercase, or rewrite each part as a comprehension or with `collections.Counter`.

---

## Where to Go Next

- Rewrite your favourite problems three ways: `for`, `while`, and comprehension.
- Ask "what is the cost?" of each solution: $O(n)$, $O(n^2)$, $O(\log n)$.
- Move on to functions, `collections`, and file processing, which use the same loop patterns.
