# Introduction 

- The logging module allows you to configure logging for your application
- the module is part of the base library, so all you need to do is import the module to get started

```python
import logging
```

## Logging Module:
If all you need is to perform basic logging to the console you can make use of the module directly. There are five logging levels:
- debug
- info
- warning
- error
- critical

each level has an associated method you can call to print your log to the terminal. However, in most cases you will want to set up some form of permanent log to keep track of what is happening in your app. The module provides a means to set up a basic configuration for your log files. Some of the primary configurations you will be concerned with are:
- **level**: what log events need to be persisted
- **filename**: where you want to save your logs
- **filemode**: how you want to save logs to your chosen file
- **format**: the form you want your log messages to take in your log file

While you can stick with using the root logger for all your logging purposes it is usually more useful to create custom loggers for each module you are working in. This allows you to create more accurate log files since the log structure itself can tell you about whatever incident is being logged, not just the message of the log.

## Handlers
Sometimes you will want your logs to go to multiple locations (such as a file and the console, or to a remote repository, etc.). In these instances you will want to create handlers: these are objects that handle sending logs to their respective destinations, and they hold the formatting information for the logs as well. 

## Formatters
If you need to format your logs differently, such as providing more detail to your permanent logs and more development-oriented logs to the terminal, you can create separate Formatters to indicate the form the logs should take. These objects can be passed to your handlers to tell them how the logs should be formed.