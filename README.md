# CaféStock

A small web application that helps a café kitchen track its ingredients — what is in stock, what is running low, and what is about to expire.

Built with **Laravel 10**, **MySQL** and **Bootstrap 5** for a university group project. All data is fake.

---

## What it does

- **Login** — register, login and logout. Every other page requires a login.
- **Categories and Suppliers** — full add / view / edit / delete.
- **Ingredients** — name, unit, quantity, low-stock level, expiry date, category and supplier.
- **Stock log** — record stock in and stock out. The ingredient's quantity updates automatically.
- **Status badges** — Expired (red), Expiring soon (yellow, within 7 days), Low stock (orange).
- **Search and filter** — by name, category, supplier and status.
- **PDF export** — the stock list, with quantities, expiry dates and status.
- **Dashboard** — total ingredients, low-stock count, expiring-soon count, and the five most recent stock records.

---

## Requirements

| Tool | Version | Notes |
| --- | --- | --- |
| PHP | 8.1 or higher | Laravel 10 minimum |
| Composer | any recent version | Installed with Laragon |
| MySQL | 5.7+ / MariaDB 10.3+ | Run through Laragon |
| Laragon | any | Runs PHP, MySQL and Composer together |
| Git | any | |

---

## Setup — first time on your laptop

Follow these **in order**. Step 2 is not optional and the order matters.

### 1. Clone the project into Laragon's `www` folder

```
cd C:\laragon\www
git clone -b develop https://github.com/danialdondol/cafestock.git
cd cafestock
```

### 2. Allow Laravel 10 to install

```
composer config policy.advisories.block false
```

> **Why?** Laravel 10 is past end-of-life, so Composer now refuses to install it by default because of known security advisories. This line tells Composer to go ahead for this project only. Skip it and the next command fails with *"Your requirements could not be resolved to an installable set of packages."*

### 3. Install the PHP packages

```
composer install
```

> This downloads Laravel and everything it needs into a `vendor` folder. It takes a minute. That folder is **never** committed to GitHub.

### 4. Create your private environment file

```
copy .env.example .env
```

This gives you your own `.env`. It is ignored by Git — each person has their own, and it never goes to GitHub.

### 5. Generate your application key

```
php artisan key:generate
```

You should see *"Application key set successfully."*

### 6. Create your database

In Laragon, click **Database** (opens phpMyAdmin) → **New** → name it `cafestock` → **Create**.

Then open `.env` in VS Code and check these lines:

```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=cafestock
DB_USERNAME=root
DB_PASSWORD=
```

An empty password is normal on a default Laragon install.

### 7. Build the tables

```
php artisan migrate
```

### 8. Run it

Click **Start All** in Laragon, then open the project in your browser at the address Laragon shows next to it — usually `http://cafestock.test`.

Alternatively run `php artisan serve` and open `http://127.0.0.1:8000`.

---

## Demo account

The demo seeder is still being written. Once it lands, this section will list the login details, and you will be able to load the fake data with:

```
php artisan migrate:fresh --seed
```

---

## Working on the project

**Use the `develop` branch. Never push to `main`.**

```
git checkout develop
git pull
git checkout -b feature/your-task
```

Make your changes, then:

```
git add .
git commit -m "Describe what you did"
git push -u origin feature/your-task
```

Then open a pull request **into `develop`** on GitHub. Fill in the template. Someone else reviews it and merges it with **Squash and merge**.

Branch prefixes: `feature/`, `fix/`, `docs/`.

Read **[CONVENTIONS.md](CONVENTIONS.md)** before your first pull request — it covers naming, routes, controller comments and which files belong to whom.

---

## Troubleshooting

| Problem | Fix |
| --- | --- |
| `Your requirements could not be resolved...` | You skipped step 2. Run `composer config policy.advisories.block false`, then `composer install` again |
| `Could not open input file: artisan` | You are in the wrong folder. `cd C:\laragon\www\cafestock` |
| `SQLSTATE[HY000] [1049] Unknown database 'cafestock'` | The database does not exist yet — do step 6 |
| `No application encryption key has been specified` | Do step 5: `php artisan key:generate` |
| Composer warns about 5 security advisories | Expected. Laravel 10 is end-of-life; the project is pinned to it deliberately |
| `LF will be replaced by CRLF` warning | Harmless Windows line-ending notice. Ignore it |

---

## Team

| Member | Role |
| --- | --- |
| 1 | Backend lead and project manager — repository, database design, authentication |
| 2 | Interface and navigation — layout, navbar, badges, dashboard |
| 3 | Ingredients, categories and suppliers — CRUD, validation, search, status rule |
| 4 | Stock log and PDF export |
| 5 | Documentation, testing and slides |

---

<sub>Built with [Laravel 10](https://laravel.com). Laravel is open-source software licensed under the [MIT license](https://opensource.org/licenses/MIT).</sub>
