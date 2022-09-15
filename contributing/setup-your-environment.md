---
description: >-
  Create a containerized development environment so you can build, test and
  contribute to Speedtest Tracker.
---

# Setup Your Environment

Speedtest Tracker is built on the [Laravel](https://laravel.com/) framework, this means we get to use some awesome 1st party packages like [Laravel Sail](https://laravel.com/docs/9.x/sail) to create a local containerized development environment.

These directions will walk you through the steps of setting up that environment.

{% hint style="info" %}
These directions assume you have a working knowledge of the Laravel framework. If you have questions on how to use it the [Laravel Docs](https://laravel.com/docs/9.x) and [Laracasts series](https://laracasts.com/series/laravel-8-from-scratch) on "Laravel from Scratch" are a good place to start.
{% endhint %}

### 1. Clone the repository

First let's clone the [repository](https://github.com/alexjustesen/speedtest-tracker) to your machine, I prefer [GitHub's CLI](https://cli.github.com/) so that command is included below.

```bash
gh repo clone alexjustesen/speedtest-tracker \
    && cd speedtest-tracker
```

### 2. Make a copy of \`.env.example\` and update DB variables

Next we need to make a copy of `.env.example`, the environment file is what Laravel uses.

```bash
cp .env.example .env
```

You'll also want to fill in a few `DB_` variables here as well which will control which database Laravel will use. I've included PostgreSQL as the default database system.

```
DB_CONNECTION=pgsql
DB_HOST=pgsql
DB_PORT=5432
DB_DATABASE=speedtest_tracker
DB_USERNAME=sail
DB_PASSWORD=password
```

### 3. Install Composer dependencies

We'll use a temporary container to install the Composer dependencies for the application.

```bash
docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v $(pwd):/var/www/html \
    -w /var/www/html \
    laravelsail/php81-composer:latest \
    composer install --ignore-platform-reqs
```

### 4. Starting a development environment

To start up the environment we can now use the Sail binary that is included with the package to build our development image and spin up a network with a database container.

```bash
./vendor/bin/sail up -d

# or if you have a Sail alias setup..
sail up -d
```

### 5. Stopping the development environment

```bash
./vendor/bin/sail down

# or if you have a Sail alias setup..
sail down
```
