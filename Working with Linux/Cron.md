# Cron -- Traditional Linux Scheduler

Cron is a classic scheduling tool in Linux that allows commands and
scripts to be executed automatically at specified times and intervals.
It has been widely used for decades for simple, recurring jobs such as
backups, cleanups and reporting.

Modern systems increasingly replace complex cron setups with **systemd
timers**, which offer more reliability, logging and dependency handling.
However, cron is still important to understand as a fundamental Linux
concept.

------------------------------------------------------------------------

## 1. What Is Cron?

Cron is a time-based job scheduler in Unix-like operating systems.

Key points: - It runs in the background and executes commands at
specified times. - It is ideal for simple repetitive jobs (e.g., daily
backups, log rotation). - It uses a text-based configuration format
called a **crontab**.

The system-wide crontab file typically lives at:

    /etc/crontab

Users can also have their own crontab files, managed via the `crontab`
command.

------------------------------------------------------------------------

## 2. Limitations of Cron

While cron is simple and widely supported, it has several weaknesses
compared to systemd timers:

-   **No dependency handling**\
    Cron does not understand service dependencies or system boot stages.
    It simply runs commands at specific times.

-   **No logging or service supervision by default**\
    Output is not automatically captured by a central logging system.\
    If a job fails, there is no built-in restart policy or supervision.

-   **Not ideal for complex workflows**\
    Cron is fine for straightforward tasks, but complex jobs with
    multiple steps, dependencies, or error-handling requirements can
    become unreliable or hard to manage.

Because of these limitations, **systemd timers** are preferred for more
advanced or critical scheduled tasks.

------------------------------------------------------------------------

## 3. Basic Cron Syntax

A cron job is defined using a specific time format followed by the
command to run:

    # ┌ minute (0 - 59)
    # │ ┌ hour (0 - 23)
    # │ │ ┌ day of month (1 - 31)
    # │ │ │ ┌ month (1 - 12)
    # │ │ │ │ ┌ day of week (0 - 7) (Sunday is 0 or 7)
    # │ │ │ │ │
    # * * * * *  command-to-execute

### Example

    0 2 * * * /usr/local/bin/backup.sh

This means:

-   Minute: `0`\
-   Hour: `2` (02:00 / 2 AM)\
-   Day of month: `*` (every day)\
-   Month: `*` (every month)\
-   Day of week: `*` (every day of the week)

So this job runs:

> `/usr/local/bin/backup.sh` at **02:00 every day**

------------------------------------------------------------------------

## 4. When To Use Cron vs systemd Timers

Use cron when: - You need a **simple**, repeating scheduled job. - You
are working on systems that **do not use systemd**. - Logging and
dependency handling can be managed manually.

Prefer systemd timers when: - You need **reliable** scheduling with
logging and monitoring. - Jobs depend on specific services or boot
stages. - You want integration with journald and systemd's service
supervision.

------------------------------------------------------------------------

## Summary

-   Cron is the traditional Linux scheduler for recurring jobs.
-   It is simple and text-based but lacks dependency handling, logging
    and supervision by default.
-   For complex, critical or production-grade scheduling, systemd timers
    are generally a better choice.