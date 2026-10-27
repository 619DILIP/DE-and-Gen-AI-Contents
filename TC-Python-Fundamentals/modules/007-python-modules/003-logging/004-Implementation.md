# Implementation

## Configure Root Logger
basic configuration
```python
# you need the logging module to configure your logger
import logging

# the level is set to Warning by default: if you want info or debug logs you have to set the level lower
logging.basicConfig(level=logging.DEBUG)

logging.debug('Hello, Debug!')
logging.info('Hello, Info!')
logging.warning('Hello, Warning!')
logging.error('Hello, Error!')
logging.critical('Hello, Critical!')
```
creating permanent logs in a log file
```python
import logging

# the filename can either be a full path to the file (good for production environment)
# or it can be a relative path (from where you execute the file)
# Full path example: "/var/log/example/app.log"
logging.basicConfig(
    level=logging.DEBUG, # sets the root logging level 
    filename='app.log', # tells the root logger where to save the log file (relative path)
    filemode='a', # tells the root logger to append the logs (not save over)
    format='%(name)s - %(levelname)s - %(message)s' # tells the root logger how to format the logs
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

# note that we are skipping configuring the root logger
# You could still configure a root logger if you want, but whatever configurations you set will
# be another location your logs are sent to alongside your custom logger (in this case it would cause
# three logs to be created: two from the custom logger, one from the root logger)

# if we don't provide a name here the root logger will be used
# __name__ is a special variable that references the name of the module the variable is referenced in
# or "__main__" if the module was executed directly. It is a convenient way to name your loggers and
# make it obvious where the logger lives in your code
module_logger = logging.getLogger(__name__)

# we need two handlers, one to send logs to a file, another to send logs to the console
file_handler = logging.FileHandler('app.log')
console_handler = logging.StreamHandler()

# Since I don't want to see Debug info in the log file I set the level to Info for this handler
file_handler.setLevel(logging.INFO)

# We can specify different formats for the different handlers
file_formatter = logging.Formatter('%(asctime)s [%(name)s] [%(levelname)s] [%(module)s:%(lineno)d] %(message)s')
console_formatter = logging.Formatter('%(asctime)s [%(levelname)s] %(message)s')

file_handler.setFormatter(file_formatter)
console_handler.setFormatter(console_formatter)

# make sure to add the handlers to the logger
module_logger.addHandler(file_handler)
module_logger.addHandler(console_handler)

# this will make the console handler print all logs to the console, but the file handler will still
# only print Info and above to the log file
module_logger.setLevel(logging.DEBUG)


# the debug log will be excluded from the log file, everything else will go to both the console
# and the log file
module_logger.debug('Hello, %s!', "Debug") # note you can use a placeholder to pass values into your log messages (could pass a variable here)
module_logger.info('Hello, %s!', "Info")
module_logger.warning('Hello, %s!', "Warning")
module_logger.error('Hello, %s!', "Error")
module_logger.critical('Hello, %s!', "Critical")
```
