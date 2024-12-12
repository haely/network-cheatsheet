# Parsing Log Files and Other Common Python Questions

## Parsing Log Files

**Sample Log Line (`example.logs`)**

```
27.59.104.166 - - [04/Oct/2019:21:15:54 +0000] "GET /users/login HTTP/1.1" 200 41716 "-" "okhttp/3.12.1"
```

**Nginx Default Access Log Pattern**

```
IP_ADDRESS - - [DATETIME] "METHOD /users/login HTTP/1.1" STATUS_CODE BYTES_SENT "-" "USER_AGENT"
```

**Q1. Get the number of logs per minute for different status codes.**

```python
def analyze_logs(log_file_path):
  """
  Analyzes log files to count occurrences of different status codes per minute.

  Args:
    log_file_path: Path to the log file.

  Returns:
    A dictionary where keys are timestamps (minute) and values are dictionaries 
    containing status code counts and total count for that minute.
  """

  parsed_data = {}

  with open(log_file_path, "r") as file:
    for line in file:
      try:
        parts = line.split()
        time = parts[3][1:17]  # Extract timestamp up to the minute
        status_code = parts[8]

        if time not in parsed_data:
          parsed_data[time] = {"count": 0} 
        parsed_data[time]["count"] += 1

        if status_code not in parsed_data[time]:
          parsed_data[time][status_code] = 0
        parsed_data[time][status_code] += 1

      except IndexError:
        print(f"Skipping malformed log line: {line}")

  return parsed_data

if __name__ == "__main__":
  log_file_path = "example.logs"
  result = analyze_logs(log_file_path)
  for time, data in result.items():
    print(f"{time}: {data}")
```

**Explanation:**

1. **`analyze_logs(log_file_path)` function:** Encapsulates the logic for better organization and reusability.
2. **Error Handling:** Includes a `try-except` block to handle potential `IndexError` for malformed log lines.
3. **Efficient Parsing:** Uses `line.split()` for efficient parsing of space-delimited log lines.
4. **Clear Output:**  Prints the parsed data in a readable format.

---

##  Working with Log Files

1. **Open the log file:** Use `with open(log_file_path, 'r') as file:` to open the file in read mode, ensuring it's automatically closed.
2. **Parse more than one line:** Iterate through the file line by line using `for line in file:`.
3. **Export parsed data to a text file:**
   ```python
   with open(export_file_path, "w") as outfile:
       for item in parsed_data:
           outfile.write(str(item) + "\n") 
   ```
4. **Turn a block of code into a function:**  Define a function with parameters for flexibility (as shown in `analyze_logs` above).
5. **Match regex into already parsed data:**
   ```python
   import re
   regex = r'pattern' 
   for item in parsed_data:
       match = re.search(regex, item)
       if match:
           # Process the match
   ```

---

## Example (Combining Concepts 1-4)

```python
import re
from datetime import datetime

def parse_log_file(log_file_path, export_file_path, regex):
    """
    Parses a log file, extracts data based on a regex, and exports it to a text file.

    Args:
      log_file_path: Path to the log file.
      export_file_path: Path to the output file.
      regex: Regular expression to match and extract data.
    """

    with open(log_file_path, "r") as file:
        match_list = []
        for line in file:
            for match in re.finditer(regex, line, re.S):
                match_text = match.group()
                match_list.append(match_text)

    with open(export_file_path, "w") as outfile:
        outfile.write("EXPORTED DATA:\n")
        for item in set(match_list):  # Remove duplicates
            outfile.write(item + "\n")

if __name__ == '__main__':
    log_file_path = r"C:\ios logs\sfbios.log"
    timestamp = datetime.now().strftime("%Y-%m-%d_%H-%M-%S")
    export_file_path = rf"C:\ios logs\filtered_output_{timestamp}.txt"
    regex = r'(<property name="(.*?)">(.*?)<\/propert>)'

    parse_log_file(log_file_path, export_file_path, regex)
```


---

## Working with APIs

**Basic API Request**

```python
import requests

response = requests.get("[http://api.open-notify.org/astros.json](http://api.open-notify.org/astros.json)")
print(response.status_code)
print(response.json())
```

**Pretty Printing JSON**

```python
import json

def jprint(obj):
    """Pretty prints a JSON object."""
    text = json.dumps(obj, sort_keys=True, indent=4)
    print(text)

jprint(response.json())
```

**Handling Paginated API Responses**

```python
import requests

session = requests.Session()

def get_jobs():
    url = "[https://api.angel.co/1/tags/1664/jobs](https://api.angel.co/1/tags/1664/jobs)" 
    first_page = session.get(url).json()
    yield first_page
    num_pages = first_page['last_page']

    for page in range(2, num_pages + 1):
        next_page = session.get(url, params={'page': page}).json()
        yield next_page

for page in get_jobs():
    # Process each page of data
    print(page) 
```

**Scraping Data with `requests` and `lxml`**

```python
import requests
from lxml import html

URL_PATTERN = "[http://www.wiseowl.co.uk/videos/default-](http://www.wiseowl.co.uk/videos/default-){}.htm"

with requests.Session() as session:
    page_number = 1
    while True:
        response = session.get(URL_PATTERN.format(page_number))
        if response.status_code == 404:
            break

        print(f"Processing page number {page_number}..")

        tree = html.fromstring(response.text)
        for video_link in tree.xpath('//p[@class="woVideoListDefaultSeriesTitle"]//a'):
            title = video_link.text
            link = video_link.attrib['href']
            print(title, link)

        page_number += 1
```

---

## Directory Traversal

```python
import os

def traverse_directory(root_dir):
    """
    Traverses a directory tree and prints directory and file names.
    """
    for dir_name, subdir_list, file_list in os.walk(root_dir):
        print(f'Found directory: {dir_name}')
        for fname in file_list:
            print(f'\t{fname}')

if __name__ == '__main__':
    root_dir = '.'
    traverse_directory(root_dir)
```

---

## Writing to CSV

**List to CSV**

```python
import csv

# Field names
fields = ['Name', 'Branch', 'Year', 'CGPA'] 

# Data rows
rows = [ 
    ['Nikhil', 'COE', '2', '9.0'],
    ['Sanchit', 'COE', '2', '9.1'],
    # ... more rows
]

with open('student_data.csv', 'w', newline='') as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(fields)  # Write header row
    writer.writerows(rows)   # Write data rows
```

**Dictionary to CSV**

```python
import csv

field_names = ['No', 'Company', 'Car Model']

cars = [
    {'No': 1, 'Company': 'Ferrari', 'Car Model': '488 GTB'},
    {'No': 2, 'Company': 'Porsche', 'Car Model': '918 Spyder'},
    # ... more cars
]

with open('cars.csv', 'w', newline='') as csvfile:
    writer = csv.DictWriter(csvfile, fieldnames=field_names)
    writer.writeheader()
    writer.writerows(cars)
```

**Key changes from my txt file:**

* **Code readability:** Improved formatting, variable names, and comments.
* **Efficiency:**  Used more efficient techniques for parsing and processing data.
* **Organization:**  Structured the code into logical sections with clear headings.
* **Completeness:**  Expanded explanations and provided more complete examples.
* **Best practices:**  Followed Python best practices for file handling, error handling, and code style.
