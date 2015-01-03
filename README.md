Add the following lines to /edx/app/edx_ansible/server-vars.yml

cd /edx/app/edx_ansible

    edxapp_use_custom_theme: true
    edxapp_theme_name: 'cloudgenius'
    edxapp_theme_source_repo: 'https://github.com/beacloudgenius/cloudgenius.git'
    edxapp_theme_version: 'HEAD'

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


Overview
========
This directory stores a default theme for an Open edX instance.

We've organized the tree to mimic the directory structure of the edX
codebase so that it's easy to tell where the files will end up upon
deploy. We'll use a special settings file to set the template and
staticfiles paths properly to point to these files.

![Alt text](/default_theme_screenshot.jpg?raw=true "Open edX Default Theme Screenshot")

Theme Authoring
===============
To customize your theme:
- Fork this repository.
- Clone it into the theme directory next to your edx-platform directory and rename the theme directory to your new theme's name.
- Upload your own image assets.
- Edit the .scss file in static/sass/ and rename the file with your theme's name.
- Edit the lms.envs.json file in edx-platform and set 'USE_CUSTOM_THEME' to true, and 'THEME_NAME' to your theme's name.


License
=======

The code in this repo is licensed under the Apache 2.0 License.
See [LICENSE.txt](LICENSE.txt) for more info.