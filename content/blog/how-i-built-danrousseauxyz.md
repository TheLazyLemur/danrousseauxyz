---
Title: How I Built danrousseauxyz
Tag: Web Development
PostedAt: Sep 12 2020
Summary: A tutorial on how to build a website like this one with Hugo,Tailwind CSS and self host it on your own VPS with Digital Ocean and Caddy webserver
---

## How Have I Built This?
Tools :

    Blazor Server
    Tailwind CSS
    Strapi CMS
    Caddy Web Server
    Docker
    Digital Ocean

### The Rundown

The front-end website is built using Blazor Server with Server prerendering enabled. For the blog section of this website I used Strapi CMS to quickly put together a powerful API. All styling is done using Tailwind CSS. Tailwind CSS is a utility first CSS library which has really changed the way I work with CSS, and I will never go back.

For hosting I used a combination of Docker hosted on a Digital Ocean VPS I then put the exposed port behind a Caddy reverse proxy so that it makes it easier to get https quickly up and running. Caddy is by far my favorite web server to work with because of how simple it is to get up and running, and how much it does for you.

In the next section of this article I will do a step by step guide on how to setup this exact setup and show you how all these pieces fir together to make for an enjoyable and easy development environment.

## The Tutorial
### Step 1 : Build Blazor Application

This tutorial is performed on Ubuntu Linux 20.04. First we need to have .NET installed, this process will vary depending on what OS you are using, as mentioned I am using Ubuntu 20.04. Follow the relative guide for your OS to get .NET installed

Once you have .NET installed create a new directory and cd into it

```
mkdir MyApp
cd MyApp
```

Then create your Blazor Server Application

```
dotnet new blazorserver
```

Great! Yout have now created your first Blazor App you can now run it with :

```
dotnet watch run
```

Note that putting watch before run makes it so that when you make changes to a file your Blazor app will automatically recompile.

### Step 2 : Setup Strapi

Now you have a few ways you can handle installing and setting up Strapi. See the installation guide for more information, but we will be using Docker. Again here you will of course need Docker installed so follow the relative guide for your OS to get Docker installed for everything to work as expeced you should also follow the Docker post installations steps found here if you are on a Linux based system.

Once that is completed, in the root of your Blazor application create a new file called docker-compose.yml

```
touch docker-compose.yml
```

Now open that file and add the following code :

```
    version: '3'
    services:
    strapi:
        image: strapi/strapi
        volumes:
        - ./app:/srv/app
        ports:
        - '1337:1337'
```

You can now do a docker-compose up and navigate to your browser and visit localhost:1337 to see you instance of strapi running.
