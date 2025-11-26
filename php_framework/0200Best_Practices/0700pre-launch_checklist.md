# Pre-Launch Checklist


Here's a little checklist that you can run through before launching your next big Trongate web app.

## Check 1


When you launch your web app, make sure your main config file (`config.php`) does *not* have 'ENV' set to 'dev'. The recommendation is to change the ENV setting to 'live' or 'production' or *any* word that is not 'DEV' or 'dev'.

> [!CAUTION]
> Never launch a Trongate web app with the environment set to 'dev'.


## Check 2


Change the password to your admin panels to something that is difficult or impossible to guess.

> [!CAUTION]
> The admin panels that are produced by the Trongate Desktop App all have a default username of 'admin' and a default password of 'admin'. So, it's really important to make sure you don't have 'admin' as your password.


## Check 3


Improve your site security by hiding your main admin login URL.

## Check 4


Make sure your `BASE_URL` is set to the full base URL that corresponds with your live website homepage. For example, 'https://trongate.io/'.

## Check 5


Make sure your `database.php` file contains database settings that relate to *your* live database and not your localhost.

## Check 6


Make sure your `site_owner.php` file contains values that relate to the person or organisation who *own* the site.

## Check 7


Don't forget to set up at least one live email account and run some two-way tests to make sure you're able to send and receive emails. The mechanics of setting up email accounts is beyond the scope of this documentation. However, it's always a good idea to talk to your web hosts and see if they have any recommendations that might prove to be helpful.

## Check 8


And finally... when you're testing a live website for the first time, it's a very good idea to use a different computer from the one that you built on. If that's not possible then **switch off the PHP engine on your localhost**. One of the most common mistakes developers make when they launch is they leave 'localhost' paths in their code. Switching off localhost makes those kinds of mistakes very easy to spot.

## BONUS CHECK


Most of the people who visit your website will probably be using mobile devices. So, be sure to test your site on a mobile device such as a smartphone.

> [!CAUTION]
> If you use GIT, be extra careful to avoid uploading a commit that contains your live website settings. Every day, websites get hacked because of developers accidentally uploading passwords and other credentials to GitHub.


> [!TIP]
> **Best Practices**
>
> **Git users** - for maximum security, it is recommended to have your entire `config` directory declared in your `.gitignore` file. Furthermore, when uploading your config files, it's a good practice to use a basic FTP application like Filezilla. The uploading of site settings is safest when it is handled manually and beyond the reach of third-party software or websites. When it comes to uploading config files and other sensitive data, *think old school.* That means no GIT. No exotic third-party software. Just basic, simple FTP software.


