# Logging



## Python Logging and Log Files

Python logging provides a structured way to record events and messages within your application. These messages are typically written to log files, but can also be directed to other destinations. Here's a breakdown of the concepts:

**Logging:**

- **Purpose:**  Logging allows you to track the execution of your program, pinpoint errors, analyze application behavior, and gain insights into user interactions.
- Benefits:
  - **Debugging:** Logs provide a detailed trail of what happened during program execution, aiding in identifying the source of errors.
  - **Monitoring:** Logs help you understand how your application behaves under different conditions and identify potential issues before they become critical.
  - **Auditing:** Logs can be used to track user activity and maintain an audit trail for security purposes.

**Log Files:**

- **Destination:** Log messages are typically written to text files, although they can also be sent to network sockets, email, or other destinations.

- Content:

   Log files contain information about the logged messages,

   including:

  - **Level:** The severity level of the message (debug, info, warning, error, critical).
  - **Timestamp:** The date and time the message was logged.
  - **Logger Name:** The name of the module or component that generated the message.
  - **Message:** The actual content of the message you logged.

- Benefits:

  - **Centralized Monitoring:** Logs provide a centralized location to track application activity from a single source.
  - **Persistence:** Logged information persists even after the program terminates, allowing for historical analysis.
  - **Customization:** You can configure logging to capture specific types of information relevant to your needs.



​	More information at: https://docs.python.org/3/howto/logging.html



## Logging Levels

The logging levels in Python's `logging` module define the severity of a message. They are used to categorize log messages and control which ones get recorded based on their importance. Here's a breakdown of the levels and their typical uses:

- **DEBUG (10):** These are detailed, low-level messages intended for diagnosing issues during development. They might include variable values, function calls, or internal program flow. You'd typically only enable DEBUG logging when actively debugging a specific problem.
- **INFO (20):** Informational messages that confirm expected behavior. These are useful for tracking the general progress of your application and monitoring its state. Examples include successful logins, database connections established, or configuration settings loaded.
- **WARNING (30):** These indicate potential problems or unexpected conditions. WARNING messages don't necessarily mean there's a critical issue, but they deserve attention. Examples include low disk space, invalid user input, or resource limitations.
- **ERROR (40):** These indicate serious errors that may have prevented the application from performing some functionality.  They typically require intervention to fix. Examples include failing to connect to a database, encountering unexpected exceptions, or data validation errors.
- **CRITICAL (50):** Critical messages indicate a severe error that likely caused the application to crash or become unusable. These are high-priority issues requiring immediate attention. Examples include critical system failures, data corruption, or security breaches.

Here's a general guideline for choosing the appropriate level:

- Use DEBUG for detailed troubleshooting information.
- Use INFO for normal application events.
- Use WARNING for potential issues that may become problems later.
- Use ERROR for serious errors that prevent functionality.
- Use CRITICAL for system crashes or unrecoverable situations.

By effectively using logging levels, you can create a log file that is informative and helps you identify and fix problems efficiently.



## Run Mode

In Python, there's no specific "run mode" required to create log files using the `logging` module.  Your program can generate log files as long as the logging configuration is set up and the program runs to execute the logging statements.

Here's why:

- The `logging` module operates within your Python program itself. It doesn't rely on external factors like a development environment or specific execution mode.
- As long as your program reaches the lines of code where you call logging methods (like `debug`, `info`, etc.), corresponding log messages will be generated based on your configuration.
- This configuration typically happens using `basicConfig` or a more advanced logging configuration file. This setup defines where the logs go (often a file) and the level of detail captured (debug, info, etc.).

Therefore, you can create log files regardless of whether you're running your program from the command line, within an IDE, or even embedded within another application. As long as the program executes the logging statements, logs will be generated based on your configuration.



```{note}
VSCode seems to be the exception.  The Log file will only create  when ran from the debug mode. 
```

## Lecture Code



```python
'''
Programmer: James Goudy
Logging lecture code

NOTE: for the log file to run in VSCODE,
 the program needs to run in logging mode

If the program runs from the command prompt,
it will create the log files
'''


import logging
logger = logging.getLogger(__name__)

def setupLogging():
    # setup logging file with force=True to overwrite existing handlers
    logging.basicConfig(filename='myLogfile.log',
                        level=logging.DEBUG,
                        format='%(asctime)s:%(levelname)s:%(message)s',
                        force=True)


def levelMessages():

    # demo logging messages
    logger.debug("A debug message")
    logger.info("An info message")
    logger.warning("An warning message")
    logger.error("An error message")
    logger.critical("A critical message")


def example1():

    num1 = 10
    num2 = 0
    ans = 0

    try:
        ans = num1 / num2
    except Exception as err:
        logger.critical(err)

def example2():

    for i in range(10):
        logger.info("i = " + str(i))

def main():
    setupLogging()

    levelMessages()

    example1()

    example2()

    print("bye")

main()

'''
Output:
2024-07-23 18:42:39,485:DEBUG:A debug message
2024-07-23 18:42:39,487:INFO:An info message
2024-07-23 18:42:39,487:WARNING:An warning message
2024-07-23 18:42:39,488:ERROR:An error message
2024-07-23 18:42:39,488:CRITICAL:A critical message
2024-07-23 18:42:39,488:CRITICAL:division by zero
2024-07-23 18:42:39,488:INFO:i = 0
2024-07-23 18:42:39,488:INFO:i = 1
2024-07-23 18:42:39,488:INFO:i = 2
2024-07-23 18:42:39,489:INFO:i = 3
2024-07-23 18:42:39,489:INFO:i = 4
2024-07-23 18:42:39,489:INFO:i = 5
2024-07-23 18:42:39,489:INFO:i = 6
2024-07-23 18:42:39,489:INFO:i = 7
2024-07-23 18:42:39,489:INFO:i = 8
2024-07-23 18:42:39,490:INFO:i = 9
'''
```

