# Chrome-Up! Launcher

Chrome-Up! is a chrome startup script that launches Chrome on MacOS in "private browsing" mode with all forms of caching and tracking aggressively disabled. As a bash script that runs from the command line, it can create new directories for user files so settings, extensions, bookmarks, and so forth can be "namespaced" for virtual separation. This is ideal for web development work (e.g., keeps your development browsing separate from your personal browsing), but it's also terrific for keeping your privacy by separating your "interests" into namespaces.

## Getting Started

### Requirements

Chrome-Up! requires Chrome to be installed on your Mac.

###  Installation (MacOS only)

The `chrome` script itself is simply a text file; a "bash" shell script that will kick off the Chrome browser for you using "private browsing" (the so-called "Incognito mode") with a variety of other command line arguments pre-configured to aggressively disable the browser cache and enforce privacy settings.

After downloading the `chrome` script, place it somewhere in your `$PATH` and make sure the file is executable:

```
sudo cp chrome /usr/local/bin
sudo chmod 755 /usr/local/bin/chrome
```

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

Using the MacOS Terminal app, type `chrome` to launch.

Chrome-Up! commands Chrome to use the `~/.chrome/default` directory to store your Chrome profile. If you provide a "profile directory" name on the command line, the script will create a new user profile for you (if you provide the `-n` or `--new` command line arguments). For example: `chrome shopping -n` creates a new directory (named `~/.chrome/shopping`) and uses that directory to store your "shopping"-related bookmarks, settings, tracking cookies, etc. (Once you've created this profile, you can access it in the future using simply the `chrome shopping` command.)

If you do not specify the optional directory name command line argument, the script will use the directory name "default" for you. That way, you can run the `chrome` Chrome-Up! script (without the optional directory name command line argument) and get your default settings and bookmarks for routine browsing, but with the added cache-clearing and "private browsing" mode benefits. 

Here are some examples:

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

Note that each "directory namespace" has its own set of bookmarks, too, so `chrome dev/projectx` can house your bookmarks, cookies, history, extensions, and so forth ("browser settings") needed for your development work; `chrome school` can house your browser settings needed for your school work; and so on.

This is a powerful tool for privacy, by the way. Because every time you launch Chrome in a new directory namespace, Chrome has no way of seeing the bookmarks, cookies, history, extensions, and so forth as used by the other namespaces since it cannot see into those other directories. So besides development work, using the Chrome launcher can increase your privacy and security, too.

## Uninstall

If it sucks, you can get rid of Chrome-Up! by simply deleting the `.chrome` directory:

```
rm -fR ~/.chrome
```

Then, remove the `chrome` script from `/usr/local/bin` (or wherever you stored it):

```
sudo rm /usr/local/bin/chrome
```

## Caveats

1. The `HTTP-REFERER` header is disabled by default as a security measure. When developing web applications, disabled referrers prevent sensitive information disclosure, which is especially useful in development and staging environments. However, this will cause some web apps that, against best practices, actually use `HTTP-REFERER` headers for authorization or other such things. Poorly engineered eCommerce sites are particularly vulnerable to this; and some sites will even fire off CSRF ([cross-site request forgery](https://en.wikipedia.org/wiki/Cross-site_request_forgery)) errors when you attempt to use these sites when Chrome is using the `--no-referrers` command line argument. In those cases, launch Chrome Up! using the `-r` or `--referrer` command line arguments.

2. If you uninstall and remove `~/.chrome`, all bookmarks, cookies, history, extensions, and so forth for all Chrome profiles stored there will be destroyed. Back things up if there's anything important there. Removing these directories will not affect Google Sync, so if you use that, your Google profile will remain intact in the cloud.
