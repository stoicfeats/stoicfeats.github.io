---
title: "how dns works"
date: 2025-10-25T11:31:21+05:30
draft: false
---

DNS, or domain name system, acts as the internet's phonebook. it converts easy-to-remember names like www.google.com into numerical IP addresses like 142.250.183.132 that computers use to communicate.

## why DNS exists

computers communicate using IP addresses, not words. you could enter an IP directly into your browser to reach a site, but memorizing numbers for every website is impractical. DNS solves this by mapping human-friendly domain names to machine-readable IP addresses.

## step 1: you enter a website name

you open your browser and type:

```
https://www.google.com
```

your computer must now find the IP address for www.google.com before connecting to the server.

## step 2: checking local cache

your computer first checks if it already knows the IP address. this process is called DNS caching.

cache locations checked in order:

1. browser cache: remembers recent visits.
2. operating system cache: stores results for minutes or hours.
3. hosts file: a local file acting as a manual phonebook.

example hosts file entry:

```
127.0.0.1   localhost
142.250.183.132  www.google.com
```

if the IP is found here, the process ends and connection begins. if not, it proceeds to the next step.

## step 3: asking the DNS resolver

your computer sends a query to a DNS resolver, which finds IP addresses.

common resolvers:

- google: 8.8.8.8
- cloudflare: 1.1.1.1
- ISP-provided (automatic)

the query is like asking: "what is the IP for www.google.com?"

this uses UDP port 53 (or TCP for large responses) and travels through your router and ISP to the resolver.

## step 4: resolver checks its cache

the resolver checks its own cache, which stores millions of lookups.

if found, it returns the IP immediately. if not, it starts recursive resolution.

## step 5: recursive resolution

the resolver queries servers in sequence:

### a) root DNS servers
there are 13 logical root servers worldwide (with mirrors).

query: "who handles .com domains?"

response: directs to .com TLD nameservers.

### b) TLD (top-level domain) servers
managed by organizations like verisign for .com.

query: "who handles google.com?"

response: provides google's authoritative nameservers, such as ns1.google.com and ns2.google.com.

### c) authoritative DNS server
google's servers hold the final records.

query: "what is the IP for www.google.com?"

response: "142.250.183.132" with TTL of 300 seconds.

TTL means the result can be cached for 300 seconds.

### d) resolver returns the answer
the resolver sends the IP back to your computer:

```
www.google.com → 142.250.183.132
```

## step 6: caching the result

the IP is cached in:

- the resolver
- your operating system
- your browser

for the TTL duration, future requests use the cache without full lookup.

## step 7: browser connects

with the IP, the browser proceeds to TCP connection, TLS handshake, HTTP request, and page loading. DNS only locates the server; it does not transfer data.

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

## example DNS packet

query to resolver:

```
query:
  type: A (IPv4 address)
  name: www.google.com
```

response:

```
answer:
  name: www.google.com
  type: A
  TTL: 300
  address: 142.250.183.132
```

## additional technical details

- UDP is default for speed; TCP used if response exceeds 512 bytes (e.g., with DNSSEC).
- TTL values range from minutes to days.
- reverse DNS converts IP to domain, used in email and logging.
- CNAME records alias one domain to another.

example:

```
www.example.com → CNAME → example.com → A → 192.0.2.1
```

- DNSSEC adds signatures to verify response authenticity.
