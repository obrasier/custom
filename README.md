Add the following lines to /edx/app/edx_ansible/server-vars.yml

cd /edx/app/edx_ansible

```yml
cat server-vars.yml 

edxapp_use_custom_theme: true
edxapp_theme_name: 'cloudgenius'
edxapp_theme_source_repo: 'https://github.com/beacloudgenius/cloudgenius.git'
edxapp_theme_version: 'HEAD'
```

	sudo chown edx-ansible:edx-ansible server-vars.yml 

Make sure to keep file permissions for server-vars.yml assigned to edx-ansible:edx-ansible

	sudo chmod edx-ansible:edx-ansible /edx/app/edx_ansible/server-vars.yml
	
Compile assets manually

To compile javascript and css outside of the update script run the following commands:

	sudo -H -u edxapp bash
	source /edx/app/edxapp/edxapp_env
	cd /edx/app/edxapp/edx-platform
	paver update_assets cms --settings=aws
	paver update_assets lms --settings=aws


Re-run the provisioning scripts:

    sudo /edx/bin/update edx-platform release    

read more https://github.com/edx/edx-platform/wiki/Stanford-Theming 



If you use a custom theme like cloudgenius, you will need to copy the static_templates directory like this:

sudo cp /edx/app/edxapp/edx-platform/lms/templates/static_templates /edx/app/edxapp/themes/cloudgenius/templates

THEN, you will need to append "theme-" to the name of every file within the static_templates directory like this:

sudo mv about.html theme-about.html

This should resolve the "THERE HAS BEEN A 500 ERROR ON THE XXX SERVERS" error on the navigation links.


Overview
========

![Alt text](/default_theme_screenshot.jpg?raw=true "Open edX Default Theme Screenshot")

Theme Authoring
===============
To customize your theme:
- Fork this repository.
- Clone it into the theme directory next to your edx-platform directory and rename the theme directory to your new theme's name.
- Upload your own image assets.
- Edit the .scss file in static/sass/ and rename the file with your theme's name.
- Edit the lms.envs.json file in edx-platform and set 'USE_CUSTOM_THEME' to true, and 'THEME_NAME' to your theme's name.
