# CaféStock — Team Conventions

One page. Read this before your first pull request.

---

## 1. Naming

| Thing | Convention | Example |
| --- | --- | --- |
| Database table | plural, snake_case | `stock_records` |
| Model | singular, PascalCase | `StockRecord` |
| Controller | singular + `Controller` | `IngredientController` |
| Route name | `module.action` | `ingredients.index` |
| Blade view | `module/action` | `ingredients/index.blade.php` |
| Branch | `type/short-description` | `feature/ingredients-crud` |

Branch prefixes: `feature/`, `fix/`, `docs/`.

---

## 2. Routes

Everyone adds routes to `routes/web.php`. Add **only your own lines**, grouped under a comment with your module name, and merge quickly — this file is the most common source of conflicts.

```php
// --- Ingredients, Categories, Suppliers (Member 3) ---
Route::resource('ingredients', IngredientController::class);
```

Use resource routes: `index`, `create`, `store`, `show`, `edit`, `update`, `destroy`.

---

## 3. Controllers

**One short comment above every method**, saying what it does in plain words. Not what the code does — what the *user* gets.

```php
// Show the ingredient list with search, filters and pagination
public function index()
{
    // ...
}
```

Anonymous filler comments are worse than none. If you can't describe it plainly, the method is doing too much.

---

## 4. Views

Every page extends Member 2's layout. Use Member 2's ready-made pieces for:

- success and error messages
- tables and forms
- the status badge
- the delete confirmation

Do not write your own button, table or badge styles. If something is missing, ask Member 2 — don't fork the design.

---

## 5. Styling (owned by Member 2)

- **Bootstrap 5**, installed via the Laravel UI package
- Brand colours: _[Member 2 to fill in]_
- Page-specific CSS goes in the one shared stylesheet, not inline in Blade

---

## 6. Database

**Only Member 1 creates or changes migrations.**

Need a new field? Post it in the group chat, wait for approval, then Member 1 adds it. Never edit an existing migration that has already been pushed — write a new one.

---

## 7. Shared files — ask before touching

| File or folder | Owner |
| --- | --- |
| `routes/web.php` | everyone — but add only your own lines |
| `resources/views/layouts/` | Member 2 |
| `database/migrations/` | Member 1 |
| `app/Models/Ingredient.php` | Member 3 (Member 4 reads it) |
| `docs/` | Member 5 |

---

## 8. Pull requests

- One task per pull request — reviewable in about 15 minutes
- Branch from `develop`, merge into `develop`
- **Never merge your own pull request**
- Fill in every section of the template, including the AI line
- Keep branches short — merge every 2–3 days, not every 2 weeks

---

## 9. The rule that matters most

**AI drafts about 40%. You own the other 60% — the decisions, the logic, the testing and the explanation.**

If you cannot explain a line to your teammates, do not merge it.
