# Library Manager

A small OOP program for a campus library: books, magazines and DVDs, members who borrow and return them, and clear errors instead of crashes.

Run with `python3 main.py` (Python 3.12+, no external packages).

## Reflection

**1. Why is `LibraryItem` abstract, and what happens if `DVD` forgets to write `late_fee()`?**
`LibraryItem` is abstract because a generic "item" has no late-fee rate of its own; only Book, Magazine and DVD do. Marking `late_fee()` with `@abstractmethod` forces every child class to supply it. If `DVD` forgets, Python raises a `TypeError` as soon as you try to create a `DVD`, so the mistake is caught immediately rather than at fee time.

**2. What happens when you read `item.__available` from outside the class, and why do we use `is_available()`?**
It raises an `AttributeError`, because Python renames the private attribute to `_LibraryItem__available` (name mangling), so `item.__available` doesn't exist from outside. We use `is_available()` so availability can only be changed through `mark_borrowed()` and `mark_returned()`, which keeps the state consistent and lets the class change its internals later without breaking other code.

**3. What is the difference between `LibraryItem.total_items` and `self.title`?**
`total_items` is a class attribute: one value shared by every item, used here to count all items created. `self.title` is an instance attribute: each object has its own copy, so every item stores its own title.
