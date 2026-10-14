# What is Gobuster?
A wordlist-based enumeration tool used to discover web paths, DNS subdomains, and virtual hosts.

## Choose the mode

| Mode | Use it to find | Main target input |
|---|---|---|
| `dir` | Web directories and files | Base URL with `-u` |
| `dns` | DNS subdomains | Domain with `-d` |
| `vhost` | Websites selected by the HTTP `Host` header | URL/IP with `-u` |

Remember: `dns` makes DNS queries; `vhost` sends HTTP requests with candidate hostnames. Their results do not have to match.

## Commands

### 1. Directory and file enumeration
```bash
gobuster dir -u http://TARGET/ -w /path/to/wordlist.txt
```

Useful options:
- `-x php,txt,js` — test file extensions.
- `-r` — follow redirects.
- `-c "NAME=VALUE"` — send a cookie.
- `-H "Header: value"` — add an HTTP header.
- `-s 200,204,301,302,403` — show selected status codes.
- `-b 404` — exclude a status code.
- `-o results.txt` — save output.

If you find a directory, scan it separately; `dir` is not recursive by default.

### 2. DNS subdomain enumeration
```bash
gobuster dns -d example.com -w /path/to/subdomains.txt
```

Useful options:
- `-i` — show resolved IP addresses.
- `--show-cname` — show CNAME records (Canonical Name records, which point one domain name to another domain name).
- `-r 8.8.8.8` — use a specified DNS resolver (check local help for exact syntax).

A discovered DNS name does not automatically mean a website is reachable or vulnerable.

### 3. Virtual host enumeration
```bash
gobuster vhost -u http://TARGET_IP \
  --domain example.com \
  -w /path/to/subdomains.txt \
  --append-domain \
  --exclude-length 250-320
```

Useful options:
- `--domain example.com` — domain suffix for candidate hostnames.
- `--append-domain` — turns a word like `blog` into `blog.example.com`.
- `--exclude-length 250-320` — ignore responses with body lengths in this range.
- `-r` — follow redirects.
- `-m GET` — set the HTTP method.

Use `--exclude-length` only after checking the server's default response. A filter can hide valid results.

## Common options

| Option | Meaning |
|---|---|
| `-u` | Target URL |
| `-d` | Domain for DNS mode |
| `-w` | Wordlist path |
| `-t 20` | Number of concurrent threads |
| `--delay 500ms` | Delay between requests per thread |
| `-o file.txt` | Save output |
| `--debug` | Troubleshoot unexpected behavior |
| `--help` | Show available options |

Check options for your installed version:
```bash
gobuster --help
gobuster dir --help
gobuster dns --help
gobuster vhost --help
```
