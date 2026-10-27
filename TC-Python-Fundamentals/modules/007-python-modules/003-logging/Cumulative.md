# Cumulative for Logging

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:
- Understand the basics of the logging module and how to set up basic logging in Python

</details>


<details><summary>Description</summary>

# Introduction 

- The logging module allows you to configure logging for your application.
- The module is part of the base library, so all you need to do is import the module to get started.

```python
import logging
```

## Logging Module:
If all you need is to perform basic logging to the console, you can make use of the module directly. There are five logging levels:
- debug
- info
- warning
- error
- critical

Each level has an associated method you can call to print your log to the terminal. However, in most cases, you will want to set up some form of permanent log to keep track of what is happening in your app. The module provides a means to set up a basic configuration for your log files. Some of the primary configurations you will be concerned with are:
- **level**: what log events need to be persisted
- **filename**: where you want to save your logs
- **filemode**: how you want to save logs to your chosen file
- **format**: the form you want your log messages to take in your log file

While you can stick with using the root logger for all your logging purposes, it is usually more useful to create custom loggers for each module you are working in. This allows you to create more accurate log files since the log structure itself can tell you about whatever incident is being logged, not just the message of the log.

## Handlers
Sometimes you will want your logs to go to multiple locations (such as a file and the console, or to a remote repository, etc.). In these instances, you will want to create handlers: these are objects that handle sending logs to their respective destinations, and they hold the formatting information for the logs as well. 

## Formatters
If you need to format your logs differently, such as providing more detail for your permanent logs and more development-oriented logs to the terminal, you can create separate Formatters to indicate the structure the logs should take. These objects can be passed to your handlers to inform them how the logs should be formatted.

</details>
<details><summary>Real World Application</summary>

# Real World Application for Logging
Robust logging is an integral part of any business application, and the more complex your application or deployment is, the more important logging becomes. With robust logging, you have a single source of truth to query when things go wrong with the application. This becomes even more important if the application is part of a distributed system: if the application is working with data from multiple other sources, you need to be able to track down where the problem is coming from (is it the app itself, is it receiving bad data from another application, is it a problem on the client's end, etc.). Without logging, you would have to track down the application that is failing and hope you can access the console logs, which will be gone if the app crashes.

Beyond tracking application failures, logging also allows you to keep track of many other facets of your application, such as user activity, application metrics, and more.

</details>
<details><summary>Implementation</summary> 

# Implementation

## Configure Root Logger
Basic configuration
```python
# You need the logging module to configure your logger
import logging

# The level is set to Warning by default: if you want info or debug logs, you have to set the level lower.
logging.basicConfig(level=logging.DEBUG)

logging.debug('Hello, Debug!')
logging.info('Hello, Info!')
logging.warning('Hello, Warning!')
logging.error('Hello, Error!')
logging.critical('Hello, Critical!')
```
Creating permanent logs in a log file
```python
import logging

# The filename can either be a full path to the file (good for production environments)
# or it can be a relative path (from where you execute the file).
# Full path example: "/var/log/example/app.log"
logging.basicConfig(
 level=logging.DEBUG,  # sets the root logging level 
 filename='app.log',  # tells the root logger where to save the log file (relative path)
 filemode='a',  # tells the root logger to append the logs (not save over)
 format='%(name)s - %(levelname)s - %(message)s'  # tells the root logger how to format the logs
)

logging.debug('Hello, Debug!')
logging.info('Hello, Info!')
logging.warning('Hello, Warning!')
logging.error('Hello, Error!')
logging.critical('Hello, Critical!')
```
Creating a custom logger that sends logs to a file and the console
```python
import logging

# Note that we are skipping configuring the root logger.
# You could still configure a root logger if you want, but whatever configurations you set will
# be another location to which your logs are sent alongside your custom logger (in this case, it would cause
# three logs to be created: two from the custom logger, one from the root logger).

# If we don't provide a name here, the root logger will be used.
# __name__ is a special variable that references the name of the module in which the variable is referenced.
# or "__main__" if the module was executed directly. It is a convenient way to name your loggers and
# make it obvious where the logger lives in your code.
module_logger = logging.getLogger(__name__)

# We need two handlers: one to send logs to a file, and another to send logs to the console.
file_handler = logging.FileHandler('app.log')
console_handler = logging.StreamHandler()

# Since I don't want to see Debug info in the log file, I set the level to Info for this handler.
file_handler.setLevel(logging.INFO)

# We can specify different formats for the different handlers.
file_formatter = logging.Formatter('%(asctime)s [%(name)s] [%(levelname)s] [%(module)s:%(lineno)d] %(message)s')
console_formatter = logging.Formatter('%(asctime)s [%(levelname)s] %(message)s')

file_handler.setFormatter(file_formatter)
console_handler.setFormatter(console_formatter)

# Make sure to add the handlers to the logger.
module_logger.addHandler(file_handler)
module_logger.addHandler(console_handler)

# This will make the console handler print all logs to the console, but the file handler will still
# only print Info and above to the log file.
module_logger.setLevel(logging.DEBUG)

# The debug log will be excluded from the log file; everything else will go to both the console
# and the log file.
module_logger.debug('Hello, %s!', "Debug")  # note you can use a placeholder to pass values into your log messages (could pass a variable here).
module_logger.info('Hello, %s!', "Info")
module_logger.warning('Hello, %s!', "Warning")
module_logger.error('Hello, %s!', "Error")
module_logger.critical('Hello, %s!', "Critical")
```

</details>
<details><summary>Summary</summary> 

# Summary
- The logging module contains functions and properties to configure logging in your application.
- There are five basic logging levels:
 - debug
 - info
 - warning
 - error
 - critical
- The root logger can easily be configured with the `logging.basicConfig` method.
- Custom loggers can be created when you need unique logging configurations for your modules.
- Handlers can be used to specify where logs should be sent.
- Formatters can be used to specify how the logs should look when created.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
