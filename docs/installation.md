
# OpenGRC Installation Guide

This guide walks you through setting up **OpenGRC**, a Laravel 11 application built with Filament 3, from cloning the repository to running the application on your local environment.

## Prerequisites

Before you begin, make sure your system meets the following minimum requirements:

- **PHP**: 8.4 or higher
    - Note: 8.4 is a new requirement!
    - Recommended extensions: `mbstring`, `openssl`, `pdo`, `tokenizer`, `xml`, `ctype`, `json`, `bcmath`, `fileinfo`
- **Composer**: 2.5 or higher
- **Node.js**: 18.0 or higher
- **npm**: 8.0 or higher
- **MySQL or SQLite3**: 5.7 or higher (or MariaDB 10.3 or higher) or SQLite 3
  - **Note**: If you are using MySQL, you will need to create the database FIRST before running the installer. SQLite is perfectly fine for small installations and test environments and requires no additional setup.

You can verify your current versions by running the following commands:

```
php -v
composer --version
node -v
npm -v
mysql --version
```

If any of the requirements are not met, install or update the software accordingly.

---

## Step 1: Clone the OpenGRC Repository

To get started, clone the **OpenGRC** repository from GitHub to your local environment.

```
git clone https://github.com/LeeMangold/OpenGRC.git
```

Navigate into the project directory:

```
cd OpenGRC
```

---

## Step 2: Run the Installer

An installer is available to help you set up OpenGRC quickly. Run the following command to start the installation process:

```
bash install.sh
```
This will run a number of commands, download the necessary dependencies, and set up the application for you. 

Note: If you need to run this command again, you must delete the database information first by either deleting the databases/opengrc.sqlite file or dropping/recreating your database. If you don't you will encounter errors.

### (Alternative) Unattended Installation ###
If you would like to install with all defaults, using sqlite, admin@example.com/password, you may do the following:
```
composer update
php artisan opengrc:install --unattended
```

---

## Step 3: Set Permissions

The file permissions set by the installer are more permissive than necessary, but are in place for ease of installation. You should review the ./set_permissions file, adjust as necessary for your chosen webserver environment, and run it to set the correct permissions for your environment. The set_permissions script is provided as a helpful utility, not as a security tool.

---

## Step 4: Log In!
After configuring for your web server, you are now able to log in to your OpenGRC instance using the username and password set during the installation process.

### Create a New User

```bash
php artisan opengrc:create-user
```

This interactive command will prompt you for user details including name, email, and password.

### Reset a User's Password

```bash
php artisan opengrc:reset-password
```

This command allows you to reset the password for an existing user.

---

## Step 5: Configure the Queue Worker

OpenGRC uses Laravel's queue system for background processing of tasks such as sending emails, processing imports, and running scheduled jobs. You must run a queue worker for these features to function properly.

For development or testing, you can run the queue worker manually:

```bash
php artisan queue:work
```

**For production environments**, you should use a process manager like Supervisor to keep the queue worker running continuously. See the [Queue Worker Configuration](queue-worker.md) guide for detailed setup instructions, including Supervisor configuration and common pitfalls.

---

# Docker Installation

OpenGRC includes a production-ready Dockerfile based on Ubuntu 24.04 with Apache, PHP 8.3, and Node.js 20.

## Building the Docker Image

```bash
git clone https://github.com/LeeMangold/OpenGRC.git
cd OpenGRC
docker build -t opengrc .
```

## Running the Container

```bash
docker run -d -p 80:80 --name opengrc opengrc
```

The application will be available at `http://localhost`.

## Environment Variables

Configure the container using environment variables with the `-e` flag:

| Variable | Default | Description |
|----------|---------|-------------|
| `APP_ENV` | `local` | Application environment (`local`, `production`) |
| `APP_DEBUG` | `false` | Enable detailed error screens |
| `DB_CONNECTION` | `sqlite` | Database driver (`sqlite` or `mysql`) |
| `DB_HOST` | `localhost` | Database host (for MySQL) |
| `DB_PORT` | - | Database port (`3306` for MySQL) |
| `DB_DATABASE` | `/var/www/html/database/opengrc.sqlite` | Database name or path |
| `DB_USERNAME` | - | Database username (for MySQL) |
| `DB_PASSWORD` | - | Database password (for MySQL) |

### Example with MySQL

```bash
docker run -d -p 80:80 \
  -e DB_CONNECTION=mysql \
  -e DB_HOST=your-mysql-host \
  -e DB_PORT=3306 \
  -e DB_DATABASE=opengrc \
  -e DB_USERNAME=opengrc_user \
  -e DB_PASSWORD=your_password \
  --name opengrc opengrc
```

### Persisting SQLite Data

To persist the SQLite database across container restarts:

```bash
docker run -d -p 80:80 \
  -v opengrc-data:/var/www/html/database \
  --name opengrc opengrc
```

## Container Features

The Docker image includes:

- **PHP 8.4** with FPM (optimized for 1GB memory)
- **Apache 2** with mod_rewrite, mod_headers, and mod_security2
- **ModSecurity** with OWASP Core Rule Set
- **Health checks** via HTTP on port 80
- **Cron** configured for Laravel scheduled tasks

## Health Check

The container includes a health check that verifies the application is responding:

```bash
docker inspect --format='{{.State.Health.Status}}' opengrc
```
