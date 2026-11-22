# Receipt Calculator Project 

A console application in **Haskell** that processes a product catalog, a
shopping cart, and an optional bonus card, then prints a receipt with all
applicable discounts applied.

Built with Stack. Uses only the `base`, `split`, `time`, and `code-page`
libraries — no heavy dependencies.

---

## 🎯 What it does

Given three text files (catalog, cart, bonus card), the program:

1. Loads and validates the product catalog.
2. Loads the shopping cart and filters out items that are not in the catalog
   (with a warning).
3. Loads the bonus card, if present; otherwise falls back to an empty card.
4. Calculates the total and applies discounts in the required order:
   - birthday discount,
   - large-order discount,
   - discount for having fruit items in the cart,
   - base discount from the bonus card.
5. Prints an itemised receipt with per-item prices, subtotal, discount, and
   final total.

Malformed lines and negative values are reported and skipped.

---

## 📄 Input format

**Catalog** (`itemss.txt`) — one item per line:
```
<name> <price> <category>
```
Example:
```
Яблоко 30.0 Фрукты
Груша 20.0 Фрукты
Круассан 50.0 Выпечка
```

**Cart** (`cartt.txt`) — one item per line:
```
<name> <quantity>
```
Example:
```
Яблоко 3
Груша 4
Круассан 5
```

**Bonus card** (`bonuss.txt`, optional) — two lines:
```
<YYYY.MM.DD>
<base discount 0–7>
```
Example:
```
2000.4.25
3
```

If the bonus card file is missing, the base discount is treated as zero.

---

## 🚀 Build and run

```bash
# build
stack build

# run without bonus card
stack run itemss.txt cartt.txt

# run with bonus card
stack run itemss.txt cartt.txt bonuss.txt
```

---

## 💻 Example output

```
Чек:
Яблоко - 3 шт. - 30.0 руб. за ед. - 90.0 руб.
Груша - 4 шт. - 20.0 руб. за ед. - 80.0 руб.
Круассан - 5 шт. - 50.0 руб. за ед. - 250.0 руб.
Мороженое - 2 шт. - 40.0 руб. за ед. - 80.0 руб.
Творог - 2 шт. - 50.0 руб. за ед. - 100.0 руб.
Итого без скидки: 600.0 руб.
Скидка: 30.0 руб. (5.0%)
Итого со скидкой: 570.0 руб.
```

---

## 🧩 Project structure

- `app/Main.hs` — entry point, calls `runProgram`.
- `src/Lib.hs` — core logic: file reading, validation, discount calculation,
  receipt printing.
- `test/` — placeholder for tests.
- `package.yaml`, `stack.yaml` — Stack project configuration.

Key functions in `Lib.hs`:

- `runProgram` — orchestrates the whole flow.
- `cartTotal` — subtotal without discounts.
- `calculateDiscount` — applies all discount rules.
- `printReceiptIO` — prints the final receipt.
- `readItemFile`, `readCartFile`, `readBonusFile` — file parsers.
- `checkItemLines`, `checkCartLines`, `checkBonusLines` — validators.

---

## 🛠️ What this project demonstrates

- Pure functional modelling of a real-world billing task.
- Robust parsing of semi-structured text files with error reporting.
- Handling of optional inputs (bonus card may be absent).
- Cross-platform console output with `code-page` for Cyrillic on Windows.

---

## 👤 Author

**Natachiazza** — [GitHub](https://github.com/Natachiazza)
