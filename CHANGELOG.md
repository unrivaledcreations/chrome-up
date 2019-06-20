# Changes

**2019-06-20:**

* Added `-n` and `--new` command line arguments, which are _required_ when creating a new profile directory namespace for a Google Chrome user data directory
* Added `-r` and `--referrer` command line arguments, which optionally removes the `--no-referrers` startup option for Google Chrome (necessary when accessing certain poorly engineered logon pages and web apps)
* Added `-h` and `--help` command line arguments, which shows brief usage instructions
* Script aborts (and shows usage instructions) if any unrecognized command line argument is found
* Prevents creating a new profile directory for Google Chrome if `-n` or `--new` is not specified
* Prevents creating a new profile directory for Google Chrome if it detects that the directory already exists, even if `-n` or `--new` is specified
* Allow Google Chrome to be optionally launched without the `--no-referrers` command line argument (to allow access to certain poorly engineered logon pages and web apps) 
* Added "CHANGELOG.md"
* Added "TODO.md"
* Updated the "usage" instructions
* Updated the "README.md" documentation
