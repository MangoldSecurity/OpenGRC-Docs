# Queue Worker Configuration

OpenGRC uses Laravel's queue system for background processing of tasks such as:

- Sending email notifications
- Processing data imports
- Generating reports
- Running AI analysis tasks
- Scheduled maintenance jobs

A queue worker must be running continuously for these features to work properly.

## Quick Start

For development or testing, run the queue worker manually:

```bash
php artisan queue:work
```

This command will process jobs until you stop it with `Ctrl+C`. For production environments, continue reading to set up Supervisor.

---

## Production Setup with Supervisor

[Supervisor](http://supervisord.org/) is a process control system that ensures your queue worker stays running, automatically restarting it if it crashes or if your server reboots.

### Installing Supervisor

**Ubuntu/Debian:**

```bash
sudo apt-get update
sudo apt-get install supervisor
```

**CentOS/RHEL:**

```bash
sudo yum install epel-release
sudo yum install supervisor
```

**Fedora:**

```bash
sudo dnf install supervisor
```

### Creating the Supervisor Configuration

Create a new configuration file for the OpenGRC queue worker:

```bash
sudo nano /etc/supervisor/conf.d/opengrc-worker.conf
```

Add the following configuration (adjust paths as needed):

```ini
[program:opengrc-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /var/www/html/OpenGRC/artisan queue:work --sleep=3 --tries=3 --max-time=3600
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
user=www-data
numprocs=1
redirect_stderr=true
stdout_logfile=/var/www/html/OpenGRC/storage/logs/worker.log
stopwaitsecs=3600
```

### Configuration Options Explained

| Option | Description |
|--------|-------------|
| `process_name` | Names each process instance (useful with multiple workers) |
| `command` | The artisan command to run |
| `user` | **Critical**: The user that runs the worker (see below) |
| `numprocs` | Number of worker processes to run |
| `autostart` | Start automatically when Supervisor starts |
| `autorestart` | Restart if the process exits |
| `stdout_logfile` | Where to write worker output |
| `stopwaitsecs` | Time to wait for graceful shutdown |

### Queue Work Options

| Flag | Description |
|------|-------------|
| `--sleep=3` | Seconds to wait before polling for new jobs when empty |
| `--tries=3` | Number of times to attempt a job before marking it failed |
| `--max-time=3600` | Maximum seconds a worker should run before restarting (prevents memory leaks) |
| `--queue=high,default` | Process specific queues in priority order |

### Starting the Worker

After creating the configuration, update Supervisor and start the worker:

```bash
sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl start opengrc-worker:*
```

### Monitoring the Worker

Check worker status:

```bash
sudo supervisorctl status opengrc-worker:*
```

View worker logs:

```bash
tail -f /var/www/html/OpenGRC/storage/logs/worker.log
```

---

## The User Permission Problem

One of the most common issues with queue workers is running them as the wrong user. This causes file permission errors that can be difficult to diagnose.

### The Problem

When the queue worker runs as a different user than your web server, files created by the worker will be owned by that user. This leads to:

- **Cache files** that the web server can't read or write
- **Log files** that become inaccessible
- **Uploaded files** with incorrect permissions
- **Session files** that cause authentication issues

### Example Scenario

Your web server runs as `www-data`, but you start the queue worker as `root` or your personal user account:

```bash
# DON'T DO THIS in production
php artisan queue:work
```

Now any files the worker creates (logs, cache, etc.) are owned by root/your user, and the web server can't access them.

### The Solution

**Always run the queue worker as the same user as your web server.**

#### Method 1: Supervisor Configuration (Recommended)

Set the `user` directive in your Supervisor config:

```ini
user=www-data
```

#### Method 2: Using sudo -u

If running manually or in scripts:

```bash
sudo -u www-data php artisan queue:work
```

#### Method 3: Using su

```bash
su -s /bin/bash -c "php artisan queue:work" www-data
```

### Finding Your Web Server User

**Apache:**

```bash
ps aux | grep apache
# or
ps aux | grep httpd
```

**Nginx with PHP-FPM:**

```bash
ps aux | grep php-fpm
# Check the pool configuration
cat /etc/php/8.2/fpm/pool.d/www.conf | grep "^user"
```

Common web server users by distribution:

| Distribution | Typical User |
|--------------|--------------|
| Ubuntu/Debian | `www-data` |
| CentOS/RHEL | `apache` or `nginx` |
| Alpine | `nginx` or `nobody` |

---

## Common Pitfalls and Solutions

### 1. Worker Not Processing Jobs

**Symptom:** Jobs stay in the queue and never process.

**Solutions:**

- Verify the worker is running: `sudo supervisorctl status`
- Check the queue connection in `.env` matches your setup
- Ensure the `QUEUE_CONNECTION` is not set to `sync`

### 2. "Permission denied" Errors

**Symptom:** Worker logs show permission errors for cache, logs, or storage.

**Solutions:**

- Ensure the worker runs as the web server user
- Fix existing permissions:

```bash
sudo chown -R www-data:www-data storage bootstrap/cache
sudo chmod -R 775 storage bootstrap/cache
```

### 3. Jobs Failing Silently

**Symptom:** Jobs disappear but nothing happens.

**Solutions:**

- Check the `failed_jobs` table in your database
- Review logs in `storage/logs/laravel.log`
- Increase the `--tries` value for debugging

### 4. Memory Issues

**Symptom:** Worker crashes or becomes unresponsive over time.

**Solutions:**

- Use `--max-time=3600` to restart workers periodically
- Use `--max-jobs=1000` to restart after processing a set number of jobs
- Monitor memory usage and adjust PHP's `memory_limit`

### 5. Worker Not Restarting After Deploy

**Symptom:** Code changes aren't reflected in job processing.

**Solution:** Restart workers after each deployment:

```bash
php artisan queue:restart
```

Add this to your deployment script. Workers check for this signal between jobs.

---

## Deployment Best Practices

Include these commands in your deployment process:

```bash
# Clear and rebuild caches
php artisan config:cache
php artisan route:cache
php artisan view:cache

# Signal workers to restart gracefully
php artisan queue:restart
```

The `queue:restart` command tells workers to exit after their current job completes. Supervisor will then start fresh workers with the new code.

---

## Multiple Queue Workers

For high-traffic installations, you may want multiple workers:

```ini
[program:opengrc-worker]
numprocs=4
process_name=%(program_name)s_%(process_num)02d
```

This runs 4 worker processes. Adjust based on your server resources and job volume.

### Priority Queues

If you have jobs of varying priority, configure workers for specific queues:

```ini
[program:opengrc-worker-high]
command=php /var/www/html/OpenGRC/artisan queue:work --queue=high,default
numprocs=2

[program:opengrc-worker-low]
command=php /var/www/html/OpenGRC/artisan queue:work --queue=low
numprocs=1
```

---

## Troubleshooting

### Checking Queue Status

View pending jobs:

```bash
php artisan queue:monitor
```

View failed jobs:

```bash
php artisan queue:failed
```

Retry failed jobs:

```bash
php artisan queue:retry all
```

### Clearing the Queue

To clear all pending jobs (use with caution):

```bash
php artisan queue:clear
```

### Testing the Queue

Verify your queue is working:

```bash
# Process a single job and exit
php artisan queue:work --once

# Process jobs with verbose output
php artisan queue:work -v
```
