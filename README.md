# Dart OOP Assignment: Kigali Bus Card

**Name:** Ahmed Abass Mohammed
**Student ID:** 25968

## My numbers

- D = 68, L = 8
- Starting balance = 1000 + (68 × 10) = 1680 RWF
- Bus fare = 200 + 68 = 268 RWF
- Student discount = 10 + 8 = 18%

## Output of main.dart

```
Error: name too short
Owner: Ahmed | Balance: 1680 RWF
Owner: Ahmed Abass Mohammed | Balance: 1680 RWF
Error: top-up must be 500 to 50000 RWF
Topped up 2000 RWF
Paid 268 RWF
Paid 268 RWF
Owner: Ahmed Abass Mohammed | Balance: 3144 RWF
Student discount: 48 RWF
Paid 220 RWF
Owner: Ahmed Abass Mohammed | Balance: 1460 RWF
Student card: 18% off
```

## Part 1: Why no setter for balance?

A setter would let any code write `card.balance = 999999` and give itself free money. Without a setter, the balance can only change through `topUp()` and `pay()`, and both methods check the rules first (top-up must be 500 to 50000, and a fare cannot be more than the balance). So the balance is always correct and can never be negative or changed by mistake.

## Part 2: What does ~/ do?

`~/` is integer division. It divides and then throws away the part after the decimal point, so the answer is an `int`.

- `print(237 * 17 / 100);` prints `40.29` (normal division, the answer is a `double`)
- `print(237 * 17 ~/ 100);` prints `40` (integer division, the answer is an `int`)

We need `~/` here because the discount `off` is an `int` and money in RWF has no decimals.

## Part 4: Bug table

| Bug | The line | Why it is wrong | My fix |
|-----|----------|-----------------|--------|
| 1 | `String _brand;` and `int _battery;` | The fields are not nullable and have no starting value. Dart does not allow this, because the constructor body runs after the fields must already have a value. | `String _brand = '';` and `int _battery = 0;` |
| 2 | `SmartPhone(String brand, int battery, String system) {` | The parent `Phone` has no empty constructor, so the child must call the parent's constructor and pass `brand` and `battery`. | Added `: super(brand, battery)` before the `{` |
| 3 | `@override void restart()` | `@override` means "the parent has this method and I am replacing it", but `Phone` has no `restart()`. | Added a `restart()` method to `Phone` |
| 4 | `p.battery = 100;` | `battery` only has a getter, so we cannot assign a value to it. | Added `set battery(int value)` to `Phone` that accepts only 0 to 100 |
| 5 | `print(p.battery());` | `battery` is a getter, not a method, so it is used without `()`. | `print(p.battery);` |

| Not a bug | Why is this line fine? |
|-----------|------------------------|
| `Phone p = new Phone('Tecno', 50);` | The word `new` is old style and not needed in modern Dart, but it is still allowed and works the same as `Phone('Tecno', 50)`. |

The fixed program prints `100`.

## Part 5

My prediction:

```
1
5
```

Why:

- `a.add()` makes `_items` 1. Then `a.items = -5` is ignored, because the setter only accepts values `>= 0`. So the first print is `1`.
- `BigBag.add()` calls `super.add()` two times, so each `b.add()` adds 2. After two calls `_items` is 4. Then `b.items = b.items + 1` sets it to 5 (accepted because 5 >= 0). So the second print is `5`.

Real output:

Was I right?
