# Implementation Recommendations

Adhering to local IT best practices will help your GeoBlacklight install get up and running with optimal support from your IT staff. Below are some discussion points worth discussing locally as you move your GBL application to production:

### Uptime and Performance Monitoring

Your local IT staff should implement uptime and performance monitoring for your production GeoBlacklight application.

Systemd for process / uptime management and Nagios/Zabbix/CloudWatch for alerting are common tools. Third party options like AppSignal and UptimeRobot can help, too.

### Log Rolling

You will need to schedule your application logs to periodically rotate to maintain the size of these files. The `logrotate` utility can be very helpful here.

### Useful Cron Tasks

A few cronjobs will help keep your database lean. These examples use the popular [whenever](https://github.com/javan/whenever) rubygem.

##### Delete Old Searches

```ruby
# Clean up recent anonymous search records
every :day, at: '2:30am', roles: [:app] do
  rake 'blacklight:delete_old_searches[7]'
end
```

##### Delete Old Guest Users

```ruby
# Cleans up anonymous user accounts created by search sessions
every :day, at: '1:30am', roles: [:app] do
  rake 'devise_guests:delete_old_guest_users[2]'
end
```
