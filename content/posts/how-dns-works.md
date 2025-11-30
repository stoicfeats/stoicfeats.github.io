---
title: "how dns works"
date: 2025-10-25T11:31:21+05:30
draft: false
---

DNS, or Domain Name System, acts as the internet's phonebook. It converts easy-to-remember names like www.google.com into numerical IP addresses like 142.250.183.132 that computers use to communicate.

## Why DNS Exists

Computers communicate using IP addresses, not words. You could enter an IP directly into your browser to reach a site, but memorizing numbers for every website is impractical. DNS solves this by mapping human-friendly domain names to machine-readable IP addresses.

## Step 1: You Enter a Website Name

You open your browser and type:

```
https://www.google.com
```

Your computer must now find the IP address for www.google.com before connecting to the server.

## Step 2: Checking Local Cache

Your computer first checks if it already knows the IP address. This process is called DNS caching.

Cache locations checked in order:

1. Browser cache: Remembers recent visits.
2. Operating system cache: Stores results for minutes or hours.
3. Hosts file: A local file acting as a manual phonebook.

Example hosts file entry:

```
127.0.0.1   localhost
142.250.183.132  www.google.com
```

If the IP is found here, the process ends and connection begins. If not, it proceeds to the next step.

## Step 3: Asking the DNS Resolver

Your computer sends a query to a DNS resolver, which finds IP addresses.

Common resolvers:

- Google: 8.8.8.8
- Cloudflare: 1.1.1.1
- ISP-provided (automatic)

The query is like asking: "What is the IP for www.google.com?"

This uses UDP port 53 (or TCP for large responses) and travels through your router and ISP to the resolver.

## Step 4: Resolver Checks Its Cache

The resolver checks its own cache, which stores millions of lookups.

If found, it returns the IP immediately. If not, it starts recursive resolution.

## Step 5: Recursive Resolution

The resolver queries servers in sequence:

### a) Root DNS Servers
There are 13 logical root servers worldwide (with mirrors).

Query: "Who handles .com domains?"

Response: Directs to .com TLD nameservers.

### b) TLD (Top-Level Domain) Servers
Managed by organizations like Verisign for .com.

Query: "Who handles google.com?"

Response: Provides Google's authoritative nameservers, such as ns1.google.com and ns2.google.com.

### c) Authoritative DNS Server
Google's servers hold the final records.

Query: "What is the IP for www.google.com?"

Response: "142.250.183.132" with TTL of 300 seconds.

TTL means the result can be cached for 300 seconds.

### d) Resolver Returns the Answer
The resolver sends the IP back to your computer:

```
www.google.com → 142.250.183.132
```

## Step 6: Caching the Result

The IP is cached in:

- The resolver
- Your operating system
- Your browser

For the TTL duration, future requests use the cache without full lookup.

## Step 7: Browser Connects

With the IP, the browser proceeds to TCP connection, TLS handshake, HTTP request, and page loading. DNS only locates the server; it does not transfer data.

## DNS Workflow Summary

```
You type "www.google.com"
↓
Check browser cache
↓
Check OS cache / hosts file
↓
Ask DNS Resolver (e.g., 1.1.1.1)
↓
Resolver checks cache
↓
If not found → ask Root server
↓
Root: "Ask .com TLD"
↓
TLD: "Ask google.com’s authoritative server"
↓
Authoritative: "Here’s the IP → 142.250.183.132"
↓
Resolver caches and returns IP
↓
Your PC caches and connects to 142.250.183.132
```

## Example DNS Packet

Query to resolver:

```
Query:
  Type: A (IPv4 Address)
  Name: www.google.com
```

Response:

```
Answer:
  Name: www.google.com
  Type: A
  TTL: 300
  Address: 142.250.183.132
```

## Additional Technical Details

- UDP is default for speed; TCP used if response exceeds 512 bytes (e.g., with DNSSEC).
- TTL values range from minutes to days.
- Reverse DNS converts IP to domain, used in email and logging.
- CNAME records alias one domain to another.

Example:

```
www.example.com → CNAME → example.com → A → 192.0.2.1
```

- DNSSEC adds signatures to verify response authenticity.
