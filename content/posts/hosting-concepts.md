---
title: "demystifying web hosting"
date: 2026-04-03T12:00:00+05:30
draft: false
---

When you first start building full-stack applications or AI automations, the hardest part isn't writing the code. It is figuring out how to get that code onto the internet.

Between GitHub Pages, AWS, Firebase, domains, and DNS, it can feel like a tangled web. This post breaks down the core mechanics of how the internet actually works using simple analogies.

## 1. the phonebook: how the internet finds your site

When a user types your domain, for example `stoicfeats.com`, into their browser, the internet does not magically know to go to GitHub.

Think of your domain like a person's name in a phonebook.

1. **The registrar:** when you buy a domain from GoDaddy, Namecheap, or similar services, that company acts as your master phonebook, holding a ledger called DNS records.
2. **The lookup:** the browser asks the registrar, "Where does stoicfeats.com live?"
3. **The IP address:** the registrar looks at a specific A record and tells the browser the physical location of that website.
4. **The connection:** the browser travels directly to that IP address, knocks on the digital door, and asks for the files.

## 2. subdomains vs. subfolders

If you have multiple projects, you have to decide how to link them to your domain.

### the subfolder, for example `stoicfeats.com/project1`

Imagine your overarching domain is the street address to a physical building. A subfolder like `/project1` is simply a specific room inside that exact same building.

If your main website is hosted on GitHub Pages, any folder you create must also live on GitHub Pages. You cannot tell the internet to look inside the GitHub building for a room that actually exists on an AWS server 5,000 miles away.

### the subdomain, for example `n8n.stoicfeats.com`

A subdomain is completely different. When you create a subdomain, you are splitting your plot of land and building a totally separate house next door.

You tell the internet phonebook: "If someone types stoicfeats.com, send them to GitHub. But if they type n8n.stoicfeats.com, completely ignore GitHub and send them to my AWS server."

Subdomains make it easy to host dozens of apps on different platforms under one unified brand name.

## 3. storage units vs. kitchens

If you want to host an app in a subfolder like `stoicfeats.com/project1`, it depends on what kind of server the app needs. There are two broad categories:

### github pages is a "storage unit" for static hosting

GitHub Pages only has the physical ability to serve flat text files such as HTML, CSS, and static images. It is a storage unit. People can walk inside and look at the paintings you hung on the wall.

If your project is a basic HTML/CSS portfolio site, you can place it in a folder in your repo and `stoicfeats.com/project1` will work perfectly.

### aws, n8n, and next.js are "kitchens" for compute hosting

Advanced automations like n8n and robust APIs like Next.js server functions are living things. They need to actively crunch numbers, process AI data, talk to databases, and consume Node.js memory.

GitHub Pages does not have the processors to cook data. If you try to drop an n8n Docker container into a GitHub folder, nothing will happen because there is no compute power to turn it on.

### the solution for advanced apps

If your app requires a kitchen to cook data:

- **For backend automations:** rent an AWS EC2 or DigitalOcean box.
- **For frontend apps:** deploy to platforms like Vercel or Firebase.

Vercel acts as a massive kitchen that automatically builds and runs Next.js code, which is why the industry prefers it over GitHub Pages for advanced web apps.