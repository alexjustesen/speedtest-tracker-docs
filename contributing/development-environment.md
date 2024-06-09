---
description: >-
  Create a containerized development environment so you can build, test and
  contribute to Speedtest Tracker.
---

# Development Environment

Speedtest Tracker is built on the [Laravel](https://laravel.com/) framework, this means we get to use some awesome 1st party packages like [Laravel Sail](https://laravel.com/docs/10.x/sail) to create a local containerized development environment.

These directions will walk you through the steps of setting up that environment.

{% hint style="info" %}
These directions assume you have a working knowledge of the Laravel framework. If you have questions on how to use it the [Laravel Docs](https://laravel.com/docs/9.x) and [Laracasts series](https://laracasts.com/series/laravel-8-from-scratch) on "Laravel from Scratch" are a good place to start.
{% endhint %}

***

### Setup and Start the Development Environment

#### 1. Clone the repository

First let's clone the [repository](https://github.com/alexjustesen/speedtest-tracker) to your machine, I prefer [GitHub's CLI](https://cli.github.com/) so that command is included below.

```bash
gh repo clone alexjustesen/speedtest-tracker \
    && cd speedtest-tracker
```

#### 2. Make a copy of \`.env.example\` and update DB variables

Next we need to make a copy of `.env.example`, the environment file is what Laravel uses.

```bash
cp .env.example .env
```

You'll also want to fill in a few `DB_` variables here as well which will control which database Laravel will use. I've included MySQL as the default database for the development environment.

```
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=speedtest_tracker
DB_USERNAME=sail
DB_PASSWORD=password
```

#### 3. Install Composer dependencies

We'll use a temporary container to install the Composer dependencies for the application.

```bash
docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v "$(pwd):/var/www/html" \
    -w /var/www/html \
    laravelsail/php83-composer:latest \
    composer install --ignore-platform-reqs
```

#### 4. Build Sail development container

We utilize [Laravel Sail](https://laravel.com/docs/10.x/sail) for a local development environment this way on your machine the only requirements are Git and Docker. To build the development environment run the commands below.

```bash
./vendor/bin/sail build --no-cache

# or if you have a Sail alias setup...
sail build --no-cache
```

#### 5. Start the development environment

To start up the environment we can now use the Sail binary that is included with the package to start our development environment.

```bash
./vendor/bin/sail up -d

# or if you have a Sail alias setup...
sail up -d
```

#### 6. Installing the application

Once the environment is setup you can install a fresh version of the application by running the following command. Keep in mind this WILL refresh the entire database.

```bash
./vendor/bin/sail artisan app:install --force

# or if you have a Sail alias setup...
sail artisan app:install --force
```

{% hint style="info" %}
You can reset your development environment at any time by running the `app:install` command.
{% endhint %}

***

### Processing Jobs in the Queue using a Worker

Processes like running a speedtest and sending notifications are offloaded to be run by a worker process. If you're testing or developing anything requiring the queue jobs be processed run the command below.

```bash
./vendor/bin/sail artisan queue:work

# or if you have a Sail alias setup...
sail artisan queue:work
```

***

### Lint your code before opening a PR or committing changes

To keep PHP's code style consistant across multiple contributors a successful lint workflow is required to pass. Check your code quality locally by running the commnand below and fixing it's recommendations.

```bash
./vendor/bin/sail bin duster lint --using=pint -v

# or if you have a Sail alias setup...
sail bin duster lint --using=pint -v
```

### Stopping the development environment

When you're done in the environment you can stop the containers using the command below.

```bash
./vendor/bin/sail down

# or if you have a Sail alias setup...
sail down
```
