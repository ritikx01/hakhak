1. Scan using automated scanner
2. WP plugin update confusion. https://hackerone.com/reports/1364851
	```
	tl;dr
	Website is using a custom wp plugin
	Plugin is not in https://plugins.svn.wordpress.org/tf-elementor
	Attacker registers a plugin with same name on Wordpress svn and bumps the version
	Website gets update notification
	As soon as they update, attacker backdoor plugin is installed in the website
	```