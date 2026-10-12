# cURL – HTTP Requests

## 1. What is cURL?
`curl` is a command-line tool used to send HTTP requests and inspect server responses without a browser.

## 2. Basic GET Request

```bash
curl http://TARGET/
```

- Sends a `GET` request to retrieve a resource.
- Displays the response body, such as HTML.

## 3. Sending POST Requests

```bash
curl -X POST -d "username=user&password=user" http://TARGET/post.php
```

- `-X POST`: Specifies the HTTP method.
- `-d`: Sends data in the request body using URL-encoded form format by default.
- Useful for testing login forms and other form submissions.

Send additional form fields:

```bash
curl -X POST -d "username=user&password=user&submit=Login" http://TARGET/post.php
```

Display response headers and body:

```bash
curl -i -X POST -d "username=user&password=user" http://TARGET/post.php
```

- `-i`: Includes HTTP response headers.
- Check status codes, `Set-Cookie`, and `Location` headers.

## 4. Cookies and Sessions

Save cookies received from the server:

```bash
curl -c cookies.txt -d "username=admin&password=admin" http://TARGET/session.php
```

Reuse saved cookies:

```bash
curl -b cookies.txt http://TARGET/session.php
```

- `-c`: Saves cookies to a file.
- `-b`: Sends cookies with the request.
- `PHPSESSID` is a common PHP session cookie.

**Important:** Receiving a `Set-Cookie` header does not necessarily mean login succeeded. Verify the response and session behavior.

## 5. Automating Login Attempts (Bash)

Create `passwords.txt`:

```text
admin123
password
letmein
secretpass
secret
```

Create `loop.sh`:

```bash
#!/bin/bash

for pass in $(cat passwords.txt); do
  echo "Trying password: $pass"

  response=$(curl -s -X POST \
    -d "username=admin&password=$pass" \
    http://TARGET/bruteforce.php)

  if echo "$response" | grep -q "Welcome"; then
    echo "[+] Password found: $pass"
    break
  fi
done
```

Run the script:

```bash
chmod +x loop.sh
./loop.sh
```

- `-s`: Silent mode; hides the progress meter.
- `$(cat passwords.txt)`: Reads the candidate passwords.
- `grep -q`: Checks for a success indicator without printing matches.
- `break`: Stops the loop when the indicator is found.

**Limitation:** The script depends on the response containing `Welcome`. A different success message, redirects, CSRF tokens, or session requirements may need additional handling.

## 6. Custom User-Agent

Some applications inspect the `User-Agent` request header.

Send a custom User-Agent:

```bash
curl -A "internalcomputer" http://TARGET/ua_check.php
```

Compare responses:

```bash
curl -i http://TARGET/ua_check.php
curl -i -A "internalcomputer" http://TARGET/ua_check.php
```

- `-A`: Sets the `User-Agent` header.
- Useful for testing User-Agent-based filtering.
- Changing the header can bypass a simple check, but does not bypass stronger authentication or authorization controls.
## Most Important cURL Options

| Option | Function |
|---|---|
| `-X` | Specifies the HTTP method, such as GET or POST. |
| `-d` | Sends data in the request body. |
| `-i` | Displays response headers and body. |
| `-v` | Shows detailed request and connection information. |
| `-H` | Adds a custom HTTP header. |
| `-b` | Sends cookies with the request. |
| `-c` | Saves received cookies to a file. |
| `-A` | Sets the User-Agent header. |

### Examples

```bash
# Display response headers and body
curl -i http://TARGET/

# Send a POST request
curl -X POST -d "username=admin&password=123" http://TARGET/login.php

# Add a custom HTTP header
curl -H "Content-Type: application/json" http://TARGET/api/

# Send cookies from a file
curl -b cookies.txt http://TARGET/

# Save received cookies to a file
curl -c cookies.txt http://TARGET/

# Set a custom User-Agent
curl -A "Mozilla/5.0" http://TARGET/

# Display detailed connection information
curl -v http://TARGET/
```


