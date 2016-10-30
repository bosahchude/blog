---
layout: post
title: Setup GitHub Pages on an Apex Domain Without Breaking Emails.
date: 2016-10-25
category: reporting
comments: True
tags: github, email
---

GitHub pages are a life saver when you want to escape the current hell of Content Management Systems. Most website can be easily made into a static website. Search functionality is the only thing lacking in most static websites but there are some workarounds for that.

Whether you choose to run [Jekyll](http://jekyllrb.com/), [Hyde](http://hyde.github.io/) or you just want to drop plain old html
files onto your sever. GitHub Pages is a free way to deploy your site.

GitHub recommends you use a subdomain not an apex domain. So if your site is `example.com` it's recommended you create a subdomain like `blog.example.com`. If you choose to still go ahead and work with a apex domain name, you would have alter your ALIAS records.

According to GitHub, using an apex domain has the following drawbacks:

* No access to the Content Deliver Network.
* You would need to manually update the IP addresses if GitHub servers migrate.
* Your emails might get broken when you tamper with ALIAS records.

This blog post demonstrates a workaround for you to host your GitHub Pages
site on an apex domain such that visiting `example.com` takes you directly to your website and your emails don't get broken.

Basically, here are solutions to the three listed drawbacks of using an apex domain stated above. Just follow the following steps:

## Step 1: Add the site name to your repository.
This is best achieved with the special `www` subdomain. It's most likely that
this subdomain was created automatically when you created your domain mane.

You can add it to the repository it two different ways:

1. Create a file named CNAME. The file should contain a single line which indicates
the subdomain the repository points to without the http prefix. Example `www.example.com`

2. The second way (the officially recommended way) is to add your site's
name under setting tab of your repo. This automatically creates the CNAME file and
commits it to your repository.

## Step 2: Configure the CNAME records

Since we used a subdomain, we only need to configure the CNAME records of the
domain that we are using. You can do this by hopping on to your webhosting interface. You should note that some webhost might require special tools to
edit the details of special subdomains like the `www` one.

On cpanel, you would need the *Advanced DNS Zone Editor* not the *Simple DNS Zone Editor* to alter the DNS details of the `www` subdomain.

You would have to replace the current CNAME record with *username*.github.io
where *username* is your actual GitHub username.

This method removes the need to hardcode IP addresses. Thus, you wouldn't get burnt
if the GitHub serves moves to a new location.

Run the following [dig](https://www.isc.org/downloads/) command to confirm your changes

    dig www.example.com +nostats +nocomments +nocmd

Your results should look similar to this

![Dig Command]({{site.baseurl}}/assets/images/dig.jpg)

Do note that DNS changes typically take up to 24 hours to fully propagate and take effect.

## Step 3: Add Permanent Redirects

After the previous step, if someone visits your site at `www.example.com` they would see your GitHub pages sites but if they visit your site at `example.com` they would not get taken to your GitHub pages site.

You can fix this by adding permanent redirects from `example.com` to `www.example.com`

The redirects should also be done on you webhost's backend. Ensure the following
rules are enforced with the redirects.

1. Enable wildcard redirects so that example.com/about.html redirects to www.example.com/about.html

2. Do NOT enable the option to force redirects of the www subdomain. This might trigger an endless loop.

3. Ensure that the redirects are permanent not temporary so you don't get punished by search engines.


## Step 4: Check to ensure email is still working.

After waiting for the DNS changes to take effect, you should check to see if your
email system is broken. This can be done by sending out and receiving emails then
verifying if they are sent or received.

A more technical way to get this done is to run an email trace through your webhost. If you've followed this guide word-for-word, everything should be in order.

## Summary
Configure the `www` subdomain of your website to point to GitHub and redirect the apex domain to it. This way, you don't tamper with your ALIAS records hence little chance of a breaking emails.
