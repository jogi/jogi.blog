---
author: Vashishtha Jogi
categories:
  - How To
date: 2016-05-19T05:35:00.000Z
description: >-
  The instructions on Heroku [Custom Domains](https://devcenter.heroku.com/articles/custom-domains) are good but not comprehensive enough for Godaddy.
draft: false
slug: how-to-add-custom-domain-to-heroku-godaddy-version
tags:
  - how-to
  - heroku
  - domain
title: "How to add custom domain to Heroku [GoDaddy\_version]"
---

The instructions on Heroku [Custom Domains](https://devcenter.heroku.com/articles/custom-domains) are good but not comprehensive enough for Godaddy. Here are the instructions on how to add a custom domain (which is registered with Godaddy) to a heroku app:

- Add the full custom domain www.example.com to Heroku app using -
```
$ heroku domains:add www.example.com
```
- Log in to your Account Manager.
- Next to Domains, click Launch.
- Change the www CNAME entry for your domain to point to `your-herokuapp.herokuapp.com`.

That’s it. This will redirect all the requests to www.example.com to your-herokuapp.herokuapp.com. Now to setup naked domain redirection i.e. example.com to www.example.com which in turn redirects to your herokuapp, follow the below steps:

1. Log in to your Account Manager.
2. Next to Domains, click Launch.
3. Select the domain name you want to forward.
4. Click Forward, and then select Forward Domain.
5. Select http:// or https:// depending on your server settings.
6. In the Forward to field, enter the URL you want to forward your domain name to.
7. To automatically update your nameservers to accommodate your forwarding changes, select Update my DNS setting to support this change.
8. Click OK.

All set! Wasn’t that easy?
