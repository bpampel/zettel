---
title: github_pages_custom_domain
date: 2022-03-15 23:40
draft: false
tags: ["github", "dns", "website"]
---

# How to redirect a custom domain to github pages

Because I do not have a dedicated webspace to host my website, but do have a custom domain, I decided to simply redirect it to github pages.
That also has the benefit of using automatic deployment via github actions.
So the goal is to serve the website under `bpampel.github.io` but let it also be accessible via `bpampel.de`

To get the redirect working, you need to do two steps:

  1) set the correct A records for your domain
  2) tell github the domain it should serve the content for

Generally, changes to DNS records might take a while to have effect, so be patient.

## Setting A records

To set the a records, you need to access the DNS settings of your domain (often a web interface).
Then, you need to add the four A records given [on this website](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

In my case, I had no A records set previously. It might be a bit more complicated if you want to redirect only some subdomain.

I also set a CNAME record for `www.bpampel.de` to `bpampel.github.io`.

## Set github settings

On `github.com`, go to the repository hosting the website and access the *Settings*.
Under *Pages* you can set a custom domain, simply enter it here and click save (in my case `bpampel.de`).

It will take a bit until github has checked that your domain indeed links to github pages and it will then generate a SSL certificate, so your website can be served securely via HTTPS.
This might take a bit.

Due to caching, the changes might not be live directly. But after some time you should hopefully have a working redirect.
