# Python Practice: If, Else, and Loops

These 50 beginner problems build from simple decisions to loops that process repeated input. Try each problem before reading its solution. Unless a problem says otherwise, assume its input is already stored in the named variable.

## Quick Explanation

- `if` runs a block when a condition is true.
- `elif` checks another condition when earlier conditions were false. You can use several `elif` branches.
- `else` runs when none of the preceding conditions matched.
- A `for` loop repeats once for each item in a sequence, or for each number produced by `range()`.
- A `while` loop repeats as long as its condition remains true. Update the condition's variables so it eventually stops.
- `break` exits the current loop. `continue` skips to the next iteration.
- Indentation defines which statements belong to a branch or loop.

## A. Decisions With `if`, `elif`, and `else`

### 1. Positive, negative, or zero

**Problem:** Given `number`, print whether it is positive, negative, or zero.

**Hints:** Compare the number with zero. There are three mutually exclusive cases, so use `if`, `elif`, and `else`.

**Solution:**
```python
number = -4

if number > 0:
    print("Positive")
elif number < 0:
    print("Negative")
else:
    print("Zero")
```
The first true comparison selects the matching message; zero fits neither comparison, so `else` handles it.

### 2. Even or odd

**Problem:** Given an integer `number`, print `Even` or `Odd`.

**Hints:** Use `%` to find the remainder after division by 2. What remainder does an even number have?

**Solution:**
```python
number = 13

if number % 2 == 0:
    print("Even")
else:
    print("Odd")
```
The remainder operator `%` returns zero when the number is divisible by 2.

### 3. Adult or minor

**Problem:** Given `age`, print `Adult` if it is at least 18; otherwise print `Minor`.

**Hints:** This has two outcomes. The phrase "at least 18" means 18 should pass the check.

**Solution:**
```python
age = 16

if age >= 18:
    print("Adult")
else:
    print("Minor")
```
`>=` includes 18 itself.

### 4. Larger of two numbers

**Problem:** Given `first` and `second`, print the larger one, or `They are equal` if they match.

**Hints:** Compare the values in both directions. If neither is greater, they must be equal.

**Solution:**
```python
first = 8
second = 12

if first > second:
    print(first)
elif second > first:
    print(second)
else:
    print("They are equal")
```
The final branch handles equality after both greater-than checks fail.

### 5. Temperature description

**Problem:** Given temperature in Celsius as `temperature`, print `Freezing` below 0, `Cold` from 0 through 14, `Mild` from 15 through 24, or `Warm` at 25 and above.

**Hints:** Test the lowest temperature ranges first. Once earlier cases fail, each next upper-bound check is enough.

**Solution:**
```python
temperature = 18

if temperature < 0:
    print("Freezing")
elif temperature < 15:
    print("Cold")
elif temperature < 25:
    print("Mild")
else:
    print("Warm")
```
Branches are checked from top to bottom, so each later comparison only needs its upper boundary.

### 6. Letter grade

**Problem:** Given a score from 0 to 100, print `A` for 90+, `B` for 80-89, `C` for 70-79, `D` for 60-69, and `F` below 60.

**Hints:** Check score thresholds from highest to lowest. `elif` prevents one score from receiving multiple grades.

**Solution:**
```python
score = 84

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
elif score >= 60:
    print("D")
else:
    print("F")
```
Descending thresholds ensure the highest applicable grade wins.

### 7. Divisible by 3 and 5

**Problem:** Given `number`, print whether it is divisible by both 3 and 5.

**Hints:** A number is divisible when its remainder is zero. Use `and` to require both tests to pass.

**Solution:**
```python
number = 30

if number % 3 == 0 and number % 5 == 0:
    print("Divisible by both")
else:
    print("Not divisible by both")
```
`and` requires both comparisons to be true.

### 8. Leap year check

**Problem:** Given `year`, determine whether it is a leap year. A year is a leap year if divisible by 400, or divisible by 4 but not by 100.

**Hints:** Translate the rule into two valid paths: divisible by 400, or divisible by 4 and not by 100. Use parentheses to group the second path.

**Solution:**
```python
year = 2024

if year % 400 == 0 or (year % 4 == 0 and year % 100 != 0):
    print("Leap year")
else:
    print("Not a leap year")
```
Parentheses make the intended combination of `and` and `or` clear.

### 9. Simple login check

**Problem:** Given `username` and `password`, print `Access granted` only when they match the expected values.

**Hints:** Compare each value with its expected text. Both comparisons must be true.

**Solution:**
```python
username = "learner"
password = "python123"

if username == "learner" and password == "python123":
    print("Access granted")
else:
    print("Access denied")
```
This is a learning example only; real applications should not store passwords in source code.

### 10. Vowel or consonant

**Problem:** Given a single-letter string `letter`, print whether it is a vowel or a consonant.

**Hints:** Check whether the letter appears in the string `"aeiou"`. Normalize its case first so uppercase vowels work too.

**Solution:**
```python
letter = "e".lower()

if letter in "aeiou":
    print("Vowel")
else:
    print("Consonant")
```
The `in` operator checks whether the letter appears in the vowel string.

### 11. Ticket price by age

**Problem:** A ticket costs 0 for ages under 5, 8 for ages 5-17, 12 for ages 18-64, and 7 for ages 65 and above. Given `age`, print the price.

**Hints:** Assign one price in each branch, then print once after the conditional. Check the age boundaries in increasing order.

**Solution:**
```python
age = 70

if age < 5:
    price = 0
elif age < 18:
    price = 8
elif age < 65:
    price = 12
else:
    price = 7

print(price)
```
Each branch assigns a value; printing after the conditional avoids repeating the `print` statement.

### 12. Triangle classification

**Problem:** Given side lengths `a`, `b`, and `c`, first reject impossible triangle sides. Otherwise print `Equilateral` if all sides match, `Isosceles` if two match, or `Scalene` if none match.

**Hints:** First check the triangle inequality for all three pairs. Only classify the sides if the triangle is valid; check equal-all before equal-pair.

**Solution:**
```python
a, b, c = 5, 5, 8

if a + b <= c or a + c <= b or b + c <= a:
    print("Not a valid triangle")
elif a == b == c:
    print("Equilateral")
elif a == b or a == c or b == c:
    print("Isosceles")
else:
    print("Scalene")
```
The triangle inequality must pass before classifying the side lengths.

### 13. Simple calculator choice

**Problem:** Given `first`, `operator`, and `second`, perform addition, subtraction, or multiplication. Print an error for an unsupported operator.

**Hints:** Compare `operator` with each supported symbol. Use the matching arithmetic operation in that branch, and keep a final fallback.

**Solution:**
```python
first = 9
operator = "*"
second = 4

if operator == "+":
    print(first + second)
elif operator == "-":
    print(first - second)
elif operator == "*":
    print(first * second)
else:
    print("Unsupported operator")
```
Each `elif` maps one operator to its operation.

### 14. Shipping cost

**Problem:** Shipping costs 0 when `order_total` is at least 50, otherwise 6.99. Print the shipping cost.

**Hints:** There are only two cases. Store the chosen cost in a variable, then print it after the `if`/`else`.

**Solution:**
```python
order_total = 42.50

if order_total >= 50:
    shipping = 0
else:
    shipping = 6.99

print(shipping)
```
The condition separates the free-shipping case from all other orders.

### 15. Username length check

**Problem:** Given `username`, print `Too short` for fewer than 4 characters, `Too long` for more than 12, and `Valid length` otherwise.

**Hints:** Use `len()` for the character count. Check the minimum and maximum boundaries; the remaining lengths are valid.

**Solution:**
```python
username = "samwise"

if len(username) < 4:
    print("Too short")
elif len(username) > 12:
    print("Too long")
else:
    print("Valid length")
```
`len()` returns the number of characters in the string.

## B. Repetition With `for`

### 16. Print numbers 1 through 10

**Problem:** Use a `for` loop to print every whole number from 1 to 10.

**Hints:** Use `range(start, stop)`. Remember that the stop number is not included.

**Solution:**
```python
for number in range(1, 11):
    print(number)
```
The stop value in `range()` is excluded, so use 11 to include 10.

### 17. Count down from 5

**Problem:** Print 5, 4, 3, 2, 1, then print `Go!`.

**Hints:** Give `range()` a negative step. Choose a stop value just past the last number you want.

**Solution:**
```python
for number in range(5, 0, -1):
    print(number)
print("Go!")
```
The third `range()` argument is the step; `-1` counts backward.

### 18. Sum numbers 1 through 100

**Problem:** Use a loop to calculate and print the sum from 1 through 100.

**Hints:** Start a running total at zero. Add each number from a `range()` that includes 100.

**Solution:**
```python
total = 0

for number in range(1, 101):
    total += number

print(total)
```
`total += number` adds the current number to the running total.

### 19. Multiplication table

**Problem:** Given `number`, print its multiplication table from 1 through 10.

**Hints:** Loop over the multipliers. On each pass, multiply the fixed number by the current multiplier.

**Solution:**
```python
number = 7

for multiplier in range(1, 11):
    print(f"{number} x {multiplier} = {number * multiplier}")
```
Each iteration uses a new multiplier and calculates one product.

### 20. Print each character

**Problem:** Given `word`, print one character per line.

**Hints:** A string can be looped over directly. Use a loop variable to hold the current character.

**Solution:**
```python
word = "Python"

for character in word:
    print(character)
```
A string is iterable, so the loop visits its characters in order.

### 21. Count vowels

**Problem:** Given `text`, count and print its vowels. Treat uppercase and lowercase letters the same.

**Hints:** Start a counter at zero, normalize the text's case, then test each character for membership in the vowels.

**Solution:**
```python
text = "Learning Python"
vowel_count = 0

for character in text.lower():
    if character in "aeiou":
        vowel_count += 1

print(vowel_count)
```
The loop checks each lowercase character and increments only for vowels.

### 22. Sum a list

**Problem:** Given `numbers`, calculate the sum using a loop, then print it.

**Hints:** Create a total before the loop. Add the current list value during each iteration.

**Solution:**
```python
numbers = [3, 8, 2, 7]
total = 0

for number in numbers:
    total += number

print(total)
```
The loop processes each list item once.

### 23. Find the largest number

**Problem:** Given a non-empty list `numbers`, find its largest value using a loop.

**Hints:** Initialize the largest value from the list itself. Compare each item and update the saved value when needed.

**Solution:**
```python
numbers = [12, 4, 27, 9]
largest = numbers[0]

for number in numbers:
    if number > largest:
        largest = number

print(largest)
```
Start with a real list value, then replace it whenever a larger one appears.

### 24. Count positive numbers

**Problem:** Given `numbers`, count how many values are greater than zero.

**Hints:** Use a counter initialized to zero. Increment it only inside an `if` that checks whether the current number is positive.

**Solution:**
```python
numbers = [-2, 5, 0, 11, -1]
positive_count = 0

for number in numbers:
    if number > 0:
        positive_count += 1

print(positive_count)
```
The conditional inside the loop filters which items increase the count.

### 25. Make a new list of squares

**Problem:** Given `numbers`, build and print a new list containing each number squared.

**Hints:** Start with an empty list. Square each number with `** 2` and add the result using `.append()`.

**Solution:**
```python
numbers = [2, 3, 4]
squares = []

for number in numbers:
    squares.append(number ** 2)

print(squares)
```
Append one square for each original number.

### 26. FizzBuzz from 1 through 20

**Problem:** For each number from 1 through 20, print `FizzBuzz` if divisible by both 3 and 5, `Fizz` if only by 3, `Buzz` if only by 5, or the number otherwise.

**Hints:** Loop through the required range. Test divisibility by both numbers before testing either one individually.

**Solution:**
```python
for number in range(1, 21):
    if number % 3 == 0 and number % 5 == 0:
        print("FizzBuzz")
    elif number % 3 == 0:
        print("Fizz")
    elif number % 5 == 0:
        print("Buzz")
    else:
        print(number)
```
Check divisibility by both first, because those numbers also pass the individual checks.

### 27. Print only even numbers

**Problem:** Given `numbers`, print only the even values.

**Hints:** Visit each item in the list and print it only when its remainder after division by 2 is zero.

**Solution:**
```python
numbers = [1, 4, 7, 10, 13, 16]

for number in numbers:
    if number % 2 == 0:
        print(number)
```
The `if` condition filters the values handled by the loop.

### 28. Search for a name

**Problem:** Given `names` and `target`, print `Found` if the target is present, otherwise print `Not found`.

**Hints:** Use a Boolean flag to remember whether you found a match. Once it is found, `break` can end the search early.

**Solution:**
```python
names = ["Ava", "Noah", "Mia"]
target = "Mia"
found = False

for name in names:
    if name == target:
        found = True
        break

if found:
    print("Found")
else:
    print("Not found")
```
`break` stops the search as soon as a match is found.

### 29. Skip multiples of 3

**Problem:** Print numbers from 1 through 15, skipping multiples of 3.

**Hints:** Check each number's remainder. Use `continue` to skip the print for multiples of 3.

**Solution:**
```python
for number in range(1, 16):
    if number % 3 == 0:
        continue
    print(number)
```
`continue` skips the print for the current iteration and advances the loop.

### 30. Nested loop pattern

**Problem:** Use nested loops to print a 3-row by 4-column rectangle of `*` characters.

**Hints:** The outer loop controls rows; the inner loop builds the characters in one row. Print only after the inner loop finishes.

**Solution:**
```python
for row in range(3):
    line = ""
    for column in range(4):
        line += "*"
    print(line)
```
The inner loop builds one row; the outer loop repeats that process three times.

## C. Repetition With `while`

### 31. Count from 1 through 5

**Problem:** Use a `while` loop to print 1 through 5.

**Hints:** Initialize a counter before the loop. Make the condition include 5 and increase the counter each pass.

**Solution:**
```python
number = 1

while number <= 5:
    print(number)
    number += 1
```
Incrementing `number` moves it toward the stopping condition.

### 32. Countdown to zero

**Problem:** Given a positive integer `number`, print it down to 0.

**Hints:** Continue while the value is at least zero. Decrease it once per iteration so the loop eventually ends.

**Solution:**
```python
number = 4

while number >= 0:
    print(number)
    number -= 1
```
Subtract one each time so the condition eventually becomes false.

### 33. Sum until the user enters zero

**Problem:** Repeatedly ask for a number and add it to a total. Stop when the user enters 0, then print the total. (Try it in a Python terminal.)

**Hints:** Read one value before the loop. While it is not zero, add it and read the next value.

**Solution:**
```python
total = 0
number = int(input("Enter a number (0 to stop): "))

while number != 0:
    total += number
    number = int(input("Enter a number (0 to stop): "))

print("Total:", total)
```
The first input happens before the loop; each loop pass reads the next value.

### 34. Keep asking until a positive number

**Problem:** Ask the user for a number until they enter a positive one, then print it.

**Hints:** Repeat while the entered value is zero or negative. Make sure each repeat asks for a new value.

**Solution:**
```python
number = int(input("Enter a positive number: "))

while number <= 0:
    number = int(input("Try again: "))

print("You entered", number)
```
The loop repeats only while the input is not positive.

### 35. Double until at least 100

**Problem:** Start with `value = 3`. Double it repeatedly until it reaches or exceeds 100, then print it.

**Hints:** Continue while the value is below the target. Multiply the value by 2 during each iteration.

**Solution:**
```python
value = 3

while value < 100:
    value *= 2

print(value)
```
Each pass increases `value`, guaranteeing the condition will eventually become false.

### 36. Count digits in a positive integer

**Problem:** Given a positive integer `number`, count its digits using a `while` loop.

**Hints:** Each integer division by 10 removes one digit. Count how many times you can do this before the number reaches zero.

**Solution:**
```python
number = 5832
digit_count = 0

while number > 0:
    digit_count += 1
    number //= 10

print(digit_count)
```
Integer division by 10 removes the last digit on each pass.

### 37. Reverse the digits

**Problem:** Given a positive integer `number`, reverse its digits using arithmetic and a `while` loop.

**Hints:** `% 10` gets the last digit and `// 10` removes it. Build the reversed result by shifting its digits left before adding the next digit.

**Solution:**
```python
number = 482
reversed_number = 0

while number > 0:
    last_digit = number % 10
    reversed_number = reversed_number * 10 + last_digit
    number //= 10

print(reversed_number)
```
Take the last digit with `% 10`, add it to the reversed result, then remove it with `// 10`.

### 38. Simple password retry

**Problem:** Keep asking for a password until the user enters `open-sesame`, then print `Welcome`. (Try it in a Python terminal.)

**Hints:** Start with a value that will not match. Keep asking while the password differs from the expected text.

**Solution:**
```python
password = ""

while password != "open-sesame":
    password = input("Password: ")

print("Welcome")
```
The loop condition compares each attempt with the expected value.

### 39. Three attempts

**Problem:** Give the user at most three chances to guess `7`. Print `Correct` if guessed, otherwise print `Out of attempts`.

**Hints:** Track attempts with a counter and success with a Boolean. Continue only while attempts remain and success is false.

**Solution:**
```python
secret = 7
attempts = 0
guessed = False

while attempts < 3 and not guessed:
    guess = int(input("Guess the number: "))
    attempts += 1
    if guess == secret:
        guessed = True

if guessed:
    print("Correct")
else:
    print("Out of attempts")
```
The loop stops when either the user wins or all three attempts are used.

### 40. Repeatedly halve a number

**Problem:** Start with `number = 1000`; repeatedly use integer division by 2 until the value is below 10. Count and print the number of divisions.

**Hints:** The loop condition checks whether the number is still at least 10. Each pass halves it and increments a separate counter.

**Solution:**
```python
number = 1000
divisions = 0

while number >= 10:
    number //= 2
    divisions += 1

print(divisions)
```
The counter records each loop pass.

## D. Mixed Practice

### 41. Sum even numbers in a range

**Problem:** Find the sum of all even numbers from 1 through 50.

**Hints:** Loop over 1 through 50, use an `if` to identify even values, and add only those values to a running total.

**Solution:**
```python
total = 0

for number in range(1, 51):
    if number % 2 == 0:
        total += number

print(total)
```
The loop visits every number and the conditional adds only even ones.

### 42. Average positive values

**Problem:** Given `numbers`, calculate the average of only its positive values. If there are none, print `No positive values`.

**Hints:** Keep both a sum and a count for positive values. Check the count before dividing so an empty selection is handled.

**Solution:**
```python
numbers = [-3, 6, 9, 0, -2]
total = 0
count = 0

for number in numbers:
    if number > 0:
        total += number
        count += 1

if count > 0:
    print(total / count)
else:
    print("No positive values")
```
Count and sum the same selected values, then guard against dividing by zero.

### 43. Find the first number over a limit

**Problem:** Given `numbers` and `limit`, print the first value greater than `limit`. If there is no such value, print `None found`.

**Hints:** Use a placeholder to mean "not found yet." Save the first value over the limit and stop the loop immediately.

**Solution:**
```python
numbers = [3, 8, 12, 20]
limit = 10
match = None

for number in numbers:
    if number > limit:
        match = number
        break

if match is None:
    print("None found")
else:
    print(match)
```
Saving the match and breaking ensures later values cannot replace the first one.

### 44. Count words longer than five letters

**Problem:** Given a list `words`, count how many words contain more than five characters.

**Hints:** Loop over the words and use `len()` in a conditional. Increase the count only when the length is greater than five.

**Solution:**
```python
words = ["apple", "banana", "kiwi", "orange"]
count = 0

for word in words:
    if len(word) > 5:
        count += 1

print(count)
```
`len(word)` supplies the value tested in each iteration.

### 45. Print a right triangle

**Problem:** Given `height`, print a left-aligned triangle of stars with that many rows.

**Hints:** The row number can also be the number of stars. Python can repeat a string by multiplying it by an integer.

**Solution:**
```python
height = 5

for row in range(1, height + 1):
    print("*" * row)
```
String multiplication repeats `*` once for each row number.

### 46. Guess the secret number

**Problem:** Keep asking the user to guess a secret number. Print `Too low` or `Too high` after each wrong guess, and stop when correct. (Try it in a Python terminal.)

**Hints:** Repeat until the guess equals the secret. Inside the loop, compare the guess to decide whether it is too low or too high.

**Solution:**
```python
secret = 14
guess = None

while guess != secret:
    guess = int(input("Guess: "))
    if guess < secret:
        print("Too low")
    elif guess > secret:
        print("Too high")

print("Correct!")
```
The equality condition ends the loop after a correct guess.

### 47. Validate a menu choice

**Problem:** Keep asking until the user enters `1`, `2`, or `3`, then print the accepted choice. (Try it in a Python terminal.)

**Hints:** Store input as text. Check whether it is in a tuple of allowed choices, and repeat while it is not.

**Solution:**
```python
choice = ""

while choice not in ("1", "2", "3"):
    choice = input("Choose 1, 2, or 3: ")

print("You chose", choice)
```
The loop continues while the choice is not one of the allowed strings.

### 48. Collatz sequence

**Problem:** Given a positive integer `number`, print each value in the Collatz sequence until it reaches 1. If it is even, divide by 2; otherwise multiply by 3 and add 1.

**Hints:** Keep looping until the value becomes 1. Use an `if`/`else` inside the loop to select the next value based on whether it is even.

**Solution:**
```python
number = 6

while number != 1:
    print(number)
    if number % 2 == 0:
        number //= 2
    else:
        number = number * 3 + 1

print(1)
```
The conditional chooses the next value, and the loop stops at 1.

### 49. Password strength check

**Problem:** Given `password`, print `Strong` if it has at least 8 characters and contains both a digit and an uppercase letter. Otherwise print `Weak`.

**Hints:** Use a loop to inspect every character and update two Boolean flags. After the loop, combine the length and flags in one condition.

**Solution:**
```python
password = "Hello2026"
has_digit = False
has_uppercase = False

for character in password:
    if character.isdigit():
        has_digit = True
    if character.isupper():
        has_uppercase = True

if len(password) >= 8 and has_digit and has_uppercase:
    print("Strong")
else:
    print("Weak")
```
The loop records whether each required character type appears; the final condition checks all requirements.

### 50. Number statistics

**Problem:** Given `numbers`, use a loop to count how many are negative, zero, and positive. Print all three counts.

**Hints:** Create three counters. For each number, exactly one of the negative, zero, or positive branches should run.

**Solution:**
```python
numbers = [-4, 0, 7, -1, 0, 12]
negative_count = 0
zero_count = 0
positive_count = 0

for number in numbers:
    if number < 0:
        negative_count += 1
    elif number == 0:
        zero_count += 1
    else:
        positive_count += 1

print("Negative:", negative_count)
print("Zero:", zero_count)
print("Positive:", positive_count)
```
Each number belongs to exactly one branch, so each counter tracks a separate group.
