# Nobox Deployment Process

We use the [Forge](https://forge.laravel.com/) server management service to help us automate and manage server droplets hosted on [Digital Ocean](https://digitalocean.com).

This guide assumes there exists a GitHub repository with a Laravel application.

## Create Server

On Forge's index page, there is a form to create a server droplet. You don't need to login to DG for anything. Forge's use of their API makes everything automated.

### Credentials

Select the credentials to the server service to create the server on. We currently only host on DG droplets, so select that.

### Name

Choose a name to indentify the server with. This name is only relevant inside the Forge service. It's not used anywhere else. Nevertheless, choose names that are self describing about what the contents of the server are about.

### Server Size

This choice comes down to what the intentions are for the server. If it's hosting sites that rely on heavy DB data or media (videos, photos) manipulation, and/or will have heavy spikes of traffic like promotions with email blasts and heavy media traffic, it's recommended to use at least the `2GB RAM` option.

For smaller, mostly static sites, `1GB RAM` should be enough.

It isn't recommended to use `512 MB` option, even when it's the cheapest and most tempting, if the deployment process depends on `npm`.

### Region

This option is mostly irrelevant other than to allow networking between droplets for load balancing, etc. If communication between droplets is desired, then make sure both are in the same location. 

Because most of our client's are LatAm based, the closest the droplet is to it the better. In DG's case, the default `New York 3` is the best option.

### Database Name (Optional)

The first database created by Forge will have this name. This name is then one used on the corresponding app's environment variable. The default `forge` is fine.

### Provision As Load Balancer

Choose this option if the created droplet will only act as a server redirection hub to route traffic under heavy load conditions. A load balancer can be `512 MB`. [Learn more](https://laracasts.com/discuss/channels/forge/scaling-with-laravel-and-forge?page=2)

### Install HHVM & Hack

We don't use either of these. Learn more about [HHVM](http://hhvm.com/) and [Hack](http://hacklang.org/)

### Install MariaDB

This option is checked by default. [MariaDB](https://mariadb.org/) is a drop-in replacement of MySQL is most regards, with fixes and performance improvements.

For most scenarios this will work fine, but it's important to know the difference and be concious of their distinctions if any issues should arise.

### Enable Backups

If the server droplet will contain production sites, this should be enabled so in the case of any catastrophic errors, the droplet can be rolled back to a stable state. This process is done through DG, not Forge.

## New Site

After submitting, Forge will go through the process of creating it on DG, and provisioning the droplet with the latest Ubuntu LS version, PHP7, Nginx, etc. After the progress indicator is done you can go into the new server and start creating sites.

By default, there's a `default` site created by Forge. It's recommended to delete this placeholder site before starting to add our own.

### Root domain

Enter the domain for your site. Specifying the `www.` subdomain isn't necessary, as Forge creates a redirect for it to the `www.`-less site automatically.

On ther other hand, enter the subdomain if desired, like for example `dev.` sites, or if creating sites inside root domains like `.nbxapps` if a dedicated domain is overkill.

### Web Directory

This is the root directory for the site that should be web accessible. For Laravel apps, this would be the `public` directory, which is the default. Change this if setting up an app that has a different web directory.

## Install Repository

### Provider

GitHub as default is probably right, but who knows. Change this if necessary.

### Repository

Write the name of the repo, like `Nobox/TestSite`.

### Branch

Leave the `master` default if you're creating a production site, which is the convention we follow. Change this to whatever branch you want to clone if needed.

### Install Composer Dependencies

It's recommended to uncheck this default option and install the dependencies with the deploy script after the environment variables are set and ready. Some dependencies rely on these variables to work, otherwise they crap out with critical errors and stop the creation of the site completely.

## SSH

You can SSH into the server through any terminal by adding your computer's SSH key to the allowed keys list in the `SSH Keys` tab on the `Server Details` page. Once you add it, the server will allow you to connect. Creating the SSH key itself is beyond scope, but [GitHub](https://help.github.com/articles/generating-an-ssh-key/) has a great guide to follow along.

Once you get to the step of copying the key to your clipboard, add it to the server through Forge.

Once it's set, open your terminal and run something like:

`ssh forge@103.192.14.19 -p`

The IP address should be the server's IP address. This command will then prompt you for a password, which is the `sudo` password provided by Forge's email after the server finished provisioning.

## Database

Once you have your SSH access setup, if the site requires a database then it needs to be created on the server. Forge doesn't have an interface to do this so it must be done through SSH.

```
mysqld -u forge -p 
```

This command will prompt you for the **database** password, and will open an interactive console instance of mysql.

```
create database example_database;
```

The semi-colon is important as it instructs mysql that it's the end of the command. An output of `Query OK, 1 row affected (0.00 sec)` should indicate the database was created. You can query to see them with the `show databases;` query.

## Environment

This tab allows you to edit the server's `.env` file for production use without having to manually edit it through SSH on a terminal. By default this file is empty. [Learn more](https://laravel.com/docs/5.2/configuration#environment-configuration)

Set the site's environment variables with the correct values for the new site like:

`VARIABLE=value`

Some crucial ones are:

#### APP_ENV

Set to `production` for production sites, `staging` for dev sites and unfinished projects. 

#### APP_DEBUG

If `true`, error messages and stack trace will be displayed fully on the site when they occur. Set to `false` on production sites because users shouldn't see this.

#### APP_KEY

Set to a 32 character string. Any less or if this var is missing and the app will throw a critical error. It's kind of important.

### DB settings

Set `DB_HOST` to `localhost` if the database is on the same server as the site. Very rarely will it be outside, but if so set it to the IP address of the other server.

`DB_DATABASE` should contain the name of the database for this site, created on this server.

`DB_USERNAME` and `DB_PASSWORD` are self explanatory. Set to the server's credentials sent by Forge on an email when the server finished provisioning. Note: Do not confuse the database access password with the server's `sudo` password.

### CACHE_DRIVER

The default value of `file` is fine, but it's recommended to use the faster `memcached` which is already configured to just work on Laravel apps. This eats `RAM` though, so keep an eye on memory consumption.

## Deployment Script

The yellow `Edit Deploy Script` button will allow you to specificy the commands the server will run on every deployment run. You edit this any way you deem necessary for the site's needs. It can contain the commands to pull from the git repo, install composer dependencies, install npm and bower dependencies, build the front-end with `gulp`, etc.

## SSL Certificates

Thanks to Forge, adding HTTPS to our sites is easy and free with [Let's Encrypt](https://letsencrypt.org/) support. Steps to add SSL certificates from other paid sources are outside the scope of this guide, but should be self-explanatory through Forge's comments and interface.

### Let's Encrypt

Press the `Let's Encrypt (Beta)` button and it will automatically show you the domains to which we will create SSL certificates for.

Press the `Obtain` button and it will automatically obtain and add them to the bottom `Current Certificates` list. When it's finished, click the lock icon to activate the certificate.

If you now visit the site through HTTP it should redirect to HTTPS automatically.

## Troubleshooting

Common problems and errors that we've encountered after this process and their possible solutions:

### 'Whoops! Something went wrong' screen

Because production apps usually have debugging disabled, the site will not display any meaningful error messages. Either enable debugging temporarily to see the errors (make sure site isn't receiving traffic if you do this), or you can access the site through SSH and go through the logs yourself. There are also error logging apps like [Rollbar](https://rollbar.com/) to make this easier.

Things to double check:

* Environment variables, including the encryption key. Laravel throws a critical error if this variable is not set. The key must be 32 characters long. Use Artisan's `php artisan key:generate` command to do this automatically (assuming the `.env` file exists).

* Make sure the database has been created on the server. Query mysql with `show databases;` to see all databases.

* DB access credentials. Make sure username and password are correct with no typos.


