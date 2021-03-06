logHibernateStats
=================

### Summary
A simple plugin to log Hibernate statistics on controller actions.

### Configuration and Usage
Just add
```
logHibernateStats.enabled = 'ALWAYS'// From ALWAYS, ALLOWED, NEVER
```
to the environments you want to track statistics for, then in your config set:
```
info    'grails.app.filters.controller.ControllerFilters' // or debug
```
You should now be seeing output like:
```
INFO  controller.ControllerFilters  -
############## Hibernate Stats ##############
Action:                     /controller/actionName

Transaction Count:          2
Flush Count:                1
Prepared Statement Count:   2

Total time:                 500 ms
#############################################
```
after each request.  If you set the logging to 'debug', you will also see:
```
DEBUG  controller.ControllerFilters  -
### Start logging for action: controller/actionName ###
```
at the start of each action (useful if logSql is enabled too).

If instead you'd like to target only specific actions, you can set
```
logHibernateStats.enabled = 'ALLOWED'
```
and instead append the parameter '_logHibernateStats=true' to your request.  This will isolate the logging to just that request.

It is recommended to keep the plugin enabled value at 'NEVER' by default, and setting it to 'ALLOWED' or 'ALWAYS' when debugging in development.

### Caveats
* This plugin heavily assumes that no other place in the code is clearing/using Hibernate statistics.
* If there are background services interacting with Hibernate, or if multiple requests are sent in succession, the statistics may not be accurate.

### Credits
Plugin created by Igor Shults.

Inspired by a post on Hibernate logging by Himanshu Seth: http://www.intelligrape.com/blog/2011/11/07/grails-find-number-of-queries-executed-for-a-particular-request/

