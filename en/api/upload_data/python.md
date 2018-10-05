# PYTHON

SDK for the work Corezoid.com

https://github.com/MaxBondar/Corezoid

This module helps you sending and modifying tasks to Corezoid processes.

```PYTHON
from Corezoid import Corezoid

# Insert Corezoid Process credentials
# Learn more about credentials: https://doc.corezoid.com/en/interface/access_management.html
API_KEY    = '<INSERT API KEY>' 
API_SECRET = '<INSERT API SECRET>'
PROCESS_ID = '<INSERT PROCESS ID>'

# Initialize Corezoid SDK
c = Corezoid(API_KEY, API_SECRET, PROCESS_ID)

# There are 2 methods available: send and modify tasks.
# Learn more about Corezoid API: https://doc.corezoid.com/en/api/upload_data/

# Send a new task to Corezoid process
def send_task(ref, data):
    # ref: string. Can be a custom value. By default it's a timestamp. 
    # data: JSON. Must be a JSON object.

    c.create_task(ref, data)

# Modify an existing task by ref at Corezoid process
def modify_task(ref, data):
    # ref: string. Can be a custom value. By default it's a timestamp. 
    # data: JSON. Must be a JSON object.

    c.modify_task(ref, data)
```