---
layout: post
title: "Setting up Heroku to use your custom domain"
date: 2012-04-30 22:08
comments: true
categories: 
- Development
---

In this post I'll explain how to:

* Setup your heroku app to use your own custom domain
* Redirect requests from yourdomain.com to www.yourdomain.com and why it's important

#Heroku and Custom Domains#

You just wrote your new social network for hamsters called Hamsterville and have successfully pushed it to Heroku where it sits at www.hamsterville.heroku.com. All's good but except for the long url so you go and buy hamsterville.com from a site such as GoDaddy with the intent to use that instead.

<!-- more -->

## Specify your domains in your heroku app ##
First you'll need to tell Heroku about this new domain. So in your console, in your apps directory run

```
heroku domains:add www.hamsterville.com 
```

and it will link it to your app. You can multiple domains (and we will do later).

At any time you can view the domains you have added to a particular app by running

```
heroku domains
```

Similiary if you wish to remove a domain ( perhaps because you mistyped it when adding it) run

```
heroku domains:remove www.hamsterrrrrville.com 
```

## Configure DNS servers ##
Next you have to configure the DNS servers. Thankfully due to a free Heroku add on this is a lot simpler than it sounds.

Zerigo DNS kindly provide a free service in the form of a free heroku add-on to make  setup easier. To start using it you simply need to run in your console

```
heroku addons:add zerigo_dns:basic
```

After you need to go to your domain registrar where you bought the custom domain - in this case GoDaddy.com.- Log into your account and go to management options for your custom domain and configure it to use Zerigos servers. Simple replace with the following Zerigo server addresses

```
a.ns.zerigo.net
b.ns.zerigo.net
c.ns.zerigo.net
d.ns.zerigo.net
e.ns.zerigo.net
```

Once saved you can verify all is well by running in your console ( Unix based systems only )

```
dig ns yourdomain.com  
```

where you should see the above 5 addresses in the long output. HOWEVER you may have to wait a while ( several minutes, couple of hours or even a whole day) before the changes you made come into effect. 

Now you can access hamsterville by typing 

www.hamsterville.com into your address bar. All done? Not quite.

#Redirecting hamsterville.com to www.hamsterville.com#

All's great typing www.hamsterville.com but if you try the "naked domain" version in your browser i.e. just hamsterville.com you will notice that the request will fail. 

What you want to happen when a user goes to hamsterville.com is for the user to be redirected to www.hamsterville.com automatically. 

To do so first you need to tell heroku about your naked domain with the command we ran above

```
heroku domains:add hamsterville.com
```

running 

```
heroku domains 
```

should show both hamsterville.com and www.hamsterville.com

Second you need to tell Zerigo to do this redirection 

To access zerigos settings 
* login to your account on the heroku website. 
* click on "My Apps" i.e. hamsterville 
* click on "Add-ons" in the top right selecting "Zerigo-DNS" and then "Configure"

You'll be logged automatically into Zerigo's dashboard.

Now to redirect
* Under the Hosts tab click add
* Leave the first field for host empty.
* Under the Type dropdown select 'redirect'
* In 'Data' enter the full www domain name i.e. http://www.hamsterville.com 
* Save.

Now users can access your hamster social network from either hamsterville.com or www.hamsterville.com

# Notes #

Can't I do this the other way round? Can't I make hamsterville.com point to my app and make www.hamsterville.com redirect to it?

According to Heroku that isn't such a good idea. You want the www version to be the big daddy here. You can read more about that and why here 

https://devcenter.heroku.com/articles/avoiding-naked-domains-dns-arecords

Why don't I just make both domains point to the app instead of all this linking malarky?

For SEO reasons you shouldn't do this. Search engines would treat both domains as two different websites despite there only being one. And if they think they're two different websites then they will come to the wrong conclusion that your content is being duplicated. Duplicating content was an old school way to game the search engine system so rules have been put in place to penalize such behaviour. Thus your website would be bansished into the lower ranks of search results. 











