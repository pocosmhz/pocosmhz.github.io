---
layout: single
status: publish
title: DuckDNS in two minutes
tags: []
comments: true
author: manuel_molina
author_profile: true
categories: []
published: true
excerpt_separator: <!--more-->
---
I recently changed my fiber provider to [Fibergy](https://fibergy.net/), for the connection I have in my hometown.

After requesting them to be taken out of [CG-NAT](https://en.wikipedia.org/wiki/Carrier-grade_NAT) pool, I went to the admin interface of my router. I wanted to configure a dynamic DNS provider.
<!--more-->
Long time ago (even before they were [bought by Oracle](https://www.wired.com/2016/11/oracle-just-bought-dyn-company-brought-internet/)) I had an account with [DynDNS](https://account.dyn.com/), but not anymore. Too much expense for doing some tests now and then.
 always liked to interact with people through public forums like those on [NNTP](https://en.wikipedia.org/wiki/Network_News_Transfer_Protocol).

I really wanted one that was inexpensive. [YDNS](https://ydns.io/) looked like a good fit. However, the list of providers accepted by the Huawei EG8145V5 router is limited, and the tests were not working.

<figure class="align-left">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2022-08-25-duckdns-in-two-minutes/duck_icon.png"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/2022-08-25-duckdns-in-two-minutes/duck_icon.png" alt="duck"></a>
  <figcaption>DuckDNS logo</figcaption>
</figure> 
I discovered [DuckDNS](https://ydns.io/) and it has been the chosen one. The process was very straightforward:

1. You go to their website and log in with either [Persona](https://persona.io/), Twitter, GitHub or Google SSO credentials. A new token is generated for you, tied to that identity.
2. You're offered the option to create up to five domains. As you create them, automatically your current browsing IP address will be assigned as the current value.
3. Then you go to their [install](https://www.duckdns.org/install.jsp) tab and select both your OS, router or API standard you want to use, together with your domain, from a drop-down menu. That way you'll be shown the different API calls you have to perform, with token credentials included.
4. You take those credentials (I used DynDNS), and place them in your router. You're done.