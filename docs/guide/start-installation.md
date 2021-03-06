Installing Yii
==============

There are two ways to install Yii:

* Using [Composer](http://getcomposer.org/);
* Downloading an archive file from [yiiframework.com](http://www.yiiframework.com/download/).

The first approach is highly recommended, as it allows you to automatically install updates


Installing via Composer
-----------------------

The recommended way to install Yii is to use the [Composer](http://getcomposer.org/) package manager. If you do not already
have Composer installed, you may download it from [http://getcomposer.org/](http://getcomposer.org/), or run the following command to download and install it:

```
curl -s http://getcomposer.org/installer | php
```

(It is strongly recommended to perform a [global Composer installation](https://getcomposer.org/doc/00-intro.md#globally)).

For problems with, or more information on, installing Composer, see the official Composer guide:

* [Linux](http://getcomposer.org/doc/00-intro.md#installation-nix)
* [Windows](http://getcomposer.org/doc/00-intro.md#installation-windows)

With Composer installed, you can create a new Yii site using one of Yii's ready-to-use application templates. Based on your needs, choosing the right template can help bootstrap your project.

Currently, there are two Yii application templates available:

- [Basic Application Template](https://github.com/yiisoft/yii2-app-basic), a basic frontend application template
- [Advanced Application Template](https://github.com/yiisoft/yii2-app-advanced), consisting of a frontend, a backend, console resources, common (shared code), and support for environments

For template installation instructions, see the above linked pages.
To read more about the ideas behind these application templates and the proposed usage,
refer to the [basic application template](apps-basic.md) and [advanced application template](apps-advanced.md) documents.

If you do not want to use a template, rather starting from scratch, you'll find information in the [creating your own application structure](apps-own.md) document. This approach is only recommended for advanced users.


Installing from zip
-------------------

Installation from a zip file involves two steps:

   1. Downloading an application template from [yiiframework.com](http://www.yiiframework.com/download/).
   2. Unpacking the downloaded file.

If you only want the Yii Framework files you can download a zip file directly from [github](https://github.com/yiisoft/yii2-framework/releases).
To create your application you might want to follow the steps described in [creating your own application structure](apps-own.md).
This is only recommended for advanced users.

> Tip: The Yii framework itself does not need to be installed under a web-accessible directory (in fact, it should not be).
A Yii application has one entry script, which is usually the only file that absolutely must be
exposed to web users (i.e., placed within the web directory). Other PHP scripts, including those
in the Yii Framework, should be protected from web access to prevent possible exploitation by hackers.


Requirements
------------

Yii 2 requires PHP 5.4.0 or higher. Yii has been tested with the [Apache HTTP server](http://httpd.apache.org/) and
[Nginx HTTP server](http://nginx.org/) on both Windows and Linux.
Yii may also be usable on other web servers and platforms, provided that PHP 5.4 or higher is present.

After installing Yii, you may want to verify that your server satisfies
Yii's requirements. You can do so by running the requirement checker
script in a web browser or from the command line.

If you have installed a Yii application template via the downloaded zip file or Composer, you'll find a `requirements.php` file in the
base directory of your application.

In order to run this script on the command line use the following command (after navigating to the directory where `requirements.php` can be found):

```
php requirements.php
```

In order to run this script in your browser, you must make sure it's within a web directory, and then
access `http://hostname/path/to/yii-app/requirements.php` in your browser.

> Note: This section is under development.

The basic Yii application template is a perfect fit for small projects or when you're just learning the framework.

The basic application template includes four pages: a homepage, an about page, a contact page, and a login page.
The contact page displays a contact form that users can fill in to submit their inquiries to the webmaster. Assuming the site has access to a mail server and that the administrator's email address is entered in the configuration file, the contact form will work. The same goes for the login page, which allows users to be authenticated before accessing privileged content.

Installation
------------

Installation of the framework requires [Composer](http://getcomposer.org/). If you do not have Composer on your system yet, you may download it from
[http://getcomposer.org/](http://getcomposer.org/), or run the following command on Linux/Unix/MacOS:

~~~
curl -s http://getcomposer.org/installer | php
~~~

You can then create a basic Yii application using the following :

~~~
php composer.phar create-project --prefer-dist --stability=dev yiisoft/yii2-app-basic /path/to/yii-application
~~~

Now set document root directory of your Web server to /path/to/yii-application/web and you should be able to access the application using the URL `http://localhost/`.

Directory structure
-------------------

The basic application does not divide application directories much. Here's the basic structure:

- `assets` - application asset files.
  - `AppAsset.php` - definition of application assets such as CSS, JavaScript etc. Check [Managing assets](assets.md) for
    details.
- `commands` - console controllers.
- `config` - configuration.
- `controllers` - web controllers.
- `models` - application models.
- `runtime` - logs, states, file cache.
- `views` - view templates.
- `web` - webroot.

Root directory contains a set of files.

- `.gitignore` contains a list of directories ignored by git version system. If you need something never get to your source
code repository, add it there.
- `codeception.yml` - Codeception config.
- `composer.json` - Composer config described in detail below.
- `LICENSE.md` - license info. Put your project license there. Especially when opensourcing.
- `README.md` - basic info about installing template. Consider replacing it with information about your project and its
  installation.
- `requirements.php` - Yii requirements checker.
- `yii` - console application bootstrap.
- `yii.bat` - same for Windows.


### config

This directory contains configuration files:

- `console.php` - console application configuration.
- `params.php` - common application parameters.
- `web.php` - web application configuration.
- `web-test.php` - web application configuration used when running functional tests.

All these files are returning arrays used to configure corresponding application properties. Check
[Configuration](configuration.md) guide section for details.

### views

Views directory contains templates your application is using. In the basic template there are:

```
layouts
    main.php
site
    about.php
    contact.php
    error.php
    index.php
    login.php
```

`layouts` contains HTML layouts i.e. page markup except content: doctype, head section, main menu, footer etc.
The rest are typically controller views. By convention these are located in subdirectories matching controller id. For
`SiteController` views are under `site`. Names of the views themselves are typically match controller action names.
Partials are often named starting with underscore.

### web

Directory is a webroot. Typically a webserver is pointed into it.

```
assets
css
index.php
index-test.php
```

`assets` contains published asset files such as CSS, JavaScript etc. Publishing process is automatic so you don't need
to do anything with this directory other than making sure Yii has enough permissions to write to it.

`css` contains plain CSS files and is useful for global CSS that isn't going to be compressed or merged by assets manager.

`index.php` is the main web application bootstrap and is the central entry point for it. `index-test.php` is the entry
point for functional testing.

Configuring Composer
--------------------

After application template is installed it's a good idea to adjust default `composer.json` that can be found in the root
directory:

```json
{
    "name": "yiisoft/yii2-app-basic",
    "description": "Yii 2 Basic Application Template",
    "keywords": ["yii", "framework", "basic", "application template"],
    "homepage": "http://www.yiiframework.com/",
    "type": "project",
    "license": "BSD-3-Clause",
    "support": {
        "issues": "https://github.com/yiisoft/yii2/issues?state=open",
        "forum": "http://www.yiiframework.com/forum/",
        "wiki": "http://www.yiiframework.com/wiki/",
        "irc": "irc://irc.freenode.net/yii",
        "source": "https://github.com/yiisoft/yii2"
    },
    "minimum-stability": "dev",
    "require": {
        "php": ">=5.4.0",
        "yiisoft/yii2": "*",
        "yiisoft/yii2-swiftmailer": "*",
        "yiisoft/yii2-bootstrap": "*",
        "yiisoft/yii2-debug": "*",
        "yiisoft/yii2-gii": "*"
    },
    "scripts": {
        "post-create-project-cmd": [
            "yii\\composer\\Installer::setPermission"
        ]
    },
    "extra": {
        "writable": [
            "runtime",
            "web/assets"
        ],
        "executable": [
            "yii"
        ]
    }
}
```

First we're updating basic information. Change `name`, `description`, `keywords`, `homepage` and `support` to match
your project.

Now the interesting part. You can add more packages your application needs to `require` section.
All these packages are coming from [packagist.org](https://packagist.org/) so feel free to browse the website for useful code.

After your `composer.json` is changed you can run `php composer.phar update --prefer-dist`, wait till packages are downloaded and
installed and then just use them. Autoloading of classes will be handled automatically.
