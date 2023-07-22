# error_checker_in_log_files
# Error Log Analyzer

This Python script is a simple error log analyzer that helps you search for specific errors in a log file and save the results to a separate log file.

## Usage

To use this script, follow the steps below:

1. Make sure you have Python 3 installed on your system.

2. Download the `error_log_analyzer.py` script to your computer.

3. Open a terminal or command prompt and navigate to the directory where the `error_log_analyzer.py` file is located.

4. Run the script with the following command:


Replace `<path_to_log_file>` with the path to the log file you want to analyze.

5. The script will prompt you to enter the error you want to search for in the log file.

6. The script will then search for all occurrences of the specified error in the log file and print them to the console.

7. Additionally, the script will create a new log file named `errors_found.log` in your home directory and save all the found errors in that file.

## Code Explanation

The code consists of two main functions:

### 1. `error_search(log_file)`

This function takes the path to a log file as input and prompts the user to enter the error they want to search for. It then reads the log file, searches for the specified error (case-insensitive), and returns a list of all matching log entries.

### 2. `file_output(returned_errors)`

This function takes the list of returned errors from the previous function and writes them to a new log file named `errors_found.log` in the user's home directory.

### Main Execution

The script checks if it is being run as the main module using the `if __name__ == "__main__":` block. If so, it retrieves the log file path from the command-line arguments and calls the `error_search()` function to find the matching errors. Then, it calls the `file_output()` function to save the errors to the `errors_found.log` file.

## Example

Suppose you have a log file named `application.log` containing various log entries. To search for the error "connection timeout" in this file and save the results, follow these steps:

1. Open a terminal or command prompt.

2. Navigate to the directory where the `error_log_analyzer.py` script is located.

3. Run the script with the following command:


4. The script will prompt you to enter the error you want to search for. Type "connection timeout" and press Enter.

5. The script will display all occurrences of the "connection timeout" error found in the log file.

6. A new file named `errors_found.log` will be created in your home directory, containing the same errors found in the log file.

Feel free to use and modify this script to suit your specific needs. Happy log analysis!

---

### Code: `error_log_analyzer.py`

```python
#!/usr/bin/env python3
import sys
import os
import re

def error_search(log_file):
error = input("What is the error? ")
returned_errors = []
with open(log_file, mode='r', encoding='UTF-8') as file:
 for log in file.readlines():
   error_patterns = ["error"]
   for i in range(len(error.split(' '))):
     error_patterns.append(r"{}".format(error.split(' ')[i].lower()))
   if all(re.search(error_pattern, log.lower()) for error_pattern in error_patterns):
     returned_errors.append(log)
 file.close()
return returned_errors

def file_output(returned_errors):
with open(os.path.expanduser('~') + '/data/errors_found.log', 'w') as file:
 for error in returned_errors:
   file.write(error)
 file.close()

if __name__ == "__main__":
log_file = sys.argv[1]
returned_errors = error_search(log_file)
file_output(returned_errors)
sys.exit(0)
