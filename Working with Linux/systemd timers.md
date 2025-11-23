# Understanding systemd Timers

Systemd timers are the modern replacement for cron and provide a more
powerful, reliable and fully integrated scheduling system on Linux.

------------------------------------------------------------------------
 
## 1. What Are systemd Timers?

A systemd timer is a scheduling unit that defines when a corresponding
systemd service should run.\
Timers are managed by the systemd init system and provide far more
control and reliability than traditional cron jobs.

A timer file typically lives here:

    /etc/systemd/system/example.timer

------------------------------------------------------------------------

## 2. Benefits of systemd Timers

### Logging with journald

All timer-triggered service output is automatically captured by
`journald`, making debugging simple and centralised.

### Dependency Handling

Timers can declare dependencies so that services only run when the
system is in the correct state.

### Service Supervision

If the service that a timer triggers fails, systemd can automatically
restart, stop, isolate or escalate depending on the configuration.

### Resource Limits

You can apply resource restrictions such as: - CPU quotas\
- Memory limits\
- IO throttling

Using systemd's cgroup integration.

### Restart Limits

Systemd can enforce rate limiting and prevent runaway services from
endlessly restarting.

### Extremely Reliable

Since timers integrate directly with systemd, they avoid many of the
timing issues and race conditions that cron can experience, especially
during reboots or downtime.

------------------------------------------------------------------------

## 3. What Does a systemd Timer Do?

A systemd timer defines:

-   When a service should run\
-   How often it should run\
-   Whether it should persist across reboots\
-   How it behaves if the system was offline when the scheduled time
    passed\
-   What triggers activate the service (time-based, event-based or
    monotonic)

The timer does **not** run the job itself --- it **activates** a
corresponding `.service` unit that performs the actual work.

------------------------------------------------------------------------

## Summary

-   systemd timers replace cron with more reliability and flexibility.\
-   They live in `/etc/systemd/system/*.timer`.\
-   Timers trigger services based on schedules and conditions.\
-   They include full logging, dependency control, supervision, resource
    limiting and fail-safes.
