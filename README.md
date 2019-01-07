# Chrome-Up! Launcher

Chrome-Up! is a chrome startup script that launches Chrome on MacOS in "private browsing" mode with all forms of caching aggressively disabled. A bash script that runs from the command line, it can create new directories for user files so settings, extensions, bookmarks, and so forth can be "namespaced" for virtual separation. The script also launches Chrome with the appropriate command line parameters to aggressively disable caching, making it ideal for web development work.

## Installation (MacOS)

Chrome-Up! requires Chrome to be installed on your Mac. The `chrome` script itself is simply a text file; a "bash" shell script that will kick off the Chrome browser for you using "private browsing" (the so-called "Incognito mode") with a variety of other command line options pre-configured to aggressively disable the browser cache.

After downloading the `chrome` script, place it somewhere in your `$PATH` and make sure the file is executable:

```
sudo cp chrome /usr/local/bin
sudo chmod 755 /usr/local/bin/chrome
```

## Configure `default` (Optional)

If you do not specify the optional directory name command line parameter, the script will use the directory name "default" for you. That way, you can run the `chrome` Chrome-Up! script (without the optional directory name command line parameter) and get your default settings and bookmarks for routine browsing, but with the added cache-clearing and "private browsing" mode benefits. 

Using the MacOS Terminal app, create a `.chrome` directory within your home directory:

```
cd ~
mkdir .chrome
```

Next, link the Chrome application default directory to `default`:

```
cd ~/.chrome
ln -s "/Users/${USER}/Library/Application Support/Google/Chrome" default
```

## Usage

Chrome-Up! commands Chrome to use the `~/.chrome` directory to store user data. If you do not manually create the needed directories, the script will create them for you.

Using the MacOS Terminal app, type `chrome` to launch:

```
chrome [directory name]
```

The script accepts a single, optional command line parameter, which is a "directory name" that you would like to use. The script creates this directory within `~/.chrome` and stores user data files there. For the sanity of your file system, use single-word, all lowercase profile names; for example:

```
chrome dev
chrome gmail
chrome school
chrome shopping
```

You can even namespace your Chrome-Up! directory; for example:

```
chrome dev/projectx
chrome dev/projecty
```

Note that each "directory namespace" has its own set of bookmarks, too, so `chrome dev` can house your bookmarks, cookies, history, extensions, and so forth ("browser settings") needed for your development work; `chrome school` can house your browser settings needed for your school work; and so on. It's like virtualization for your browser, and it works great.

This is a powerful tool for privacy, by the way. Because every time you launch Chrome in a new directory namespace, Chrome has no way of seeing the bookmarks, cookies, history, extensions, and so forth as used by the other namespaces since it cannot see into those other directories. So besides development work, using the Chrome launcher can increase your privacy and security, too.

## Uninstall

If it sucks, you can get rid of Chrome-Up! by simply deleting the `.chrome` directory:

```
rm -fR ~/.chrome
```

## Caveats

1. The `HTTP-REFERER` header should be disabled in development as a security measure when developing web applications to prevent sensitive information disclosure, especially the domain names of local development and staging environments. However, this will cause some web apps that, against best practices, actually use `HTTP-REFERER` headers for authorization or other such things. Poorly engineered eCommerce sites are particularly vulnerable to this; and some sites will even fire off CSRF ([cross-site request forgery](https://en.wikipedia.org/wiki/Cross-site_request_forgery)) errors when you attempt to use these sites when Chrome is using the `--no-referrers` command line switch (as with this script). In those cases, I recommend launching Chrome in the usual way (i.e., using MacOS to start Chrome from Launchpad) and then conducting these browsing activities from there.

2. If you uninstall and remove `~/.chrome`, all bookmarks, cookies, history, extensions, and so forth for all Chrome profiles stored there will be destroyed. Back things up if there's anything important there.
