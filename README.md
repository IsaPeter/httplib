# HTTPLib - Lightweight HTTP Request and Response Parser

## Overview

HTTPLib2 is a lightweight Python library for parsing, manipulating, and reconstructing raw HTTP requests and responses. It provides an easy way to analyze and modify HTTP requests for penetration testing, debugging, and automation.

## Features

- Parse raw HTTP requests and responses
- Modify headers, cookies, and authentication tokens
- Handle different Content-Type formats (application/json, multipart/form-data, application/x-www-form-urlencoded)
- Rebuild modified requests and responses
- Generate unique request and response IDs


## Installation

Clone the repository:

```bash
git clone https://github.com/IsaPeter/httplib.git
cd httplib
```

Use the library in your Python scripts:

```python
from httplib2 import HTTPRequest, HTTPResponse
```

## Usage


### Parsing an HTTP Request

```python
raw_request = """POST /login HTTP/1.1
Host: example.com
Content-Type: application/json
Content-Length: 48

{"username": "admin", "password": "password123"}"""

request = HTTPRequest(raw_request)
print(request.method)  # POST
print(request.path)    # /login
print(request.headers) # {'Host': 'example.com', 'Content-Type': 'application/json', 'Content-Length': '48'}
print(request.parsed_body) # {'username': 'admin', 'password': 'password123'}
```

### Modifying a Request

```python
request.set_custom_header("User-Agent", "CustomAgent/1.0")
request.set_bearer_token("my-secure-token")
print(request.rebuild_request())
```

### Handling Cookies

```python
request.set_cookie("session", "123456")
print(request.get_cookies())  # {'session': '123456'}
```

### Parsing an HTTP Response

```python
raw_response = """HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 27

{"message": "Success!"}"""

response = HTTPResponse(raw_response=raw_response)
print(response.status_code)  # 200
print(response.body)  # {"message": "Success!"}
```

### Rebuilding a Response

```python
modified_response = response.rebuild_response()
print(modified_response)
```

