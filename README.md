# WordPress Skeleton

This is simply a skeleton repo for a WordPress site. Use it to jump-start your WordPress site repos, or fork it and customize it to your own liking!

## Assumptions

* WordPress as a Git submodule in `/wp/`
* Custom content directory in `/content/` (cleaner, and also because it can't be in `/wp/`)
* `wp-config.php` in the root (because it can't be in `/wp/`)
* All writable directories are symlinked to similarly named locations under `/shared/`.

## Installation

0. Prerequisites
	* Install [vagrant](https://www.vagrantup.com/)
	* Install [VirtualBox](https://www.virtualbox.org/)
1. Run `vagrant up` on the root directory
2. Add `192.168.33.10 dev.my-project.com` in /etc/hosts
3. Install Wordpress
	1. Install Wordpress going to http://dev.my-project.com/wp/wp-admin/install.php
	2. Follow the steps
	3. Connect to http://dev.my-project.com/wp/wp-login.php
	4. Go to http://dev.my-project.com/wp/wp-admin/options-general.php
	5. Remove the trailing wp in "Site Address (URL)" and save
5. Done, you can access to http://dev.my-project.com!

To change the URL of the project (dev.my-project.com):

* Update all `dev.my-project.com` in [provision/vhosts/dev.my-project.com.conf](/provision/vhosts/dev.my-project.com.conf)
* Update the name in [Vagrantfile](/Vagrantfile)
* Change `192.168.33.10 dev.my-project.com` in /etc/hosts

## Questions & Answers

**Q:** Will you accept pull requests?  
**A:** Maybe — if I think the change is useful. I primarily made this for my own use, and thought people might find it useful. If you want to take it in a different direction and make your own customized skeleton, then just maintain your own fork.

**Q:** Why the `/shared/` symlink stuff for uploads?  
**A:** For local development, create `/shared/` (it is ignored by Git), and have the files live there. For production, have your deploy script (Capistrano is my choice) look for symlinks pointing to `/shared/` and repoint them to some outside-the-repo location (like an NFS shared directory or something). This gives you separation between Git-managed code and uploaded files.

**Q:** What version of WordPress does this track?  
**A:** The latest stable release. Send a pull request if I fall behind.

**Q:** What's the deal with `local-config.php`?  
**A:** It is for local development, which might have different MySQL credentials or do things like enable query saving or debug mode. This file is ignored by Git, so it doesn't accidentally get checked in. If the file does not exist (which it shouldn't, in production), then WordPress will used the DB credentials defined in `wp-config.php`.

**Q:** What is `memcached.php`?  
**A:** This is for people using memcached as an object cache backend. It should be something like: `<?php return array( "server01:11211", "server02:11211" ); ?>`. Programattic generation of this file is recommended.

**Q:** Does this support WordPress in multisite mode?  
**A:** Yes, as of WordPress v3.5 which was released in December, 2012.
