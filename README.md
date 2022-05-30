# Make sure there is a files folder.
```
cd web/sites/default
mkdir files
mkdir files/private
mkdir files/tmp
cd ..
cd umami
mkdir files
mkdir files/private
mkdir files/tmp
```
# Add symlink to the local config file:
```
cd web/sites/default
ln -sf ../../../.ddev/local-settings/demo/settings.php
ln -sf ../../../.ddev/local-settings/demo/settings.env.php
ln -sf ../../../.ddev/local-settings/demo/settings.local.php
ln -sf ../../../.ddev/local-settings/demo/local.development.services.yml
cd ..
cd umami
ln -sf ../../../.ddev/local-settings/umami/settings.php
ln -sf ../../../.ddev/local-settings/umami/settings.env.php
ln -sf ../../../.ddev/local-settings/umami/settings.local.php
ln -sf ../../../.ddev/local-settings/umami/local.development.services.yml
```
# Requirements
## Install ddev locally
```
brew install drud/ddev/ddev
```
## Install mutagen locally
This might not be required because ddev will install it for you if needed. If not, then you can run the following command.
```
brew install mutagen-io/mutagen/mutagen
```
# Start project
```
ddev start
```
# Import DB locally
Export a database file at the following formats:
```
database.sql | database.sql.gz
```
Import DB into ddev when it is up:
--target-db=db is the default so you can omit that parameter in the command
```
ddev import-db --src=_resources/db/ddev-demo.sql.gz
```

# DB Management
DB can be accessed using phpMyAdmin
```
ddev launch -p
```
# Some commands that will help you

Start environment.
```
ddev start
```
Stop environment.
```
ddev stop
```
Start over the containers, and reload their configuration.
```
ddev restart
```
Remove all persistent data from a project, similar to prune
```
ddev remove projectname --remove-data -O
```
Delete all project information (including database) for an existing project
```
ddev delete
```
Check logs for the docker containers.
```
ddev logs -s [container_name]
```
Run a shell at the PHP container(default), other containers
```
ddev ssh -s [container_name]
```
To launch the website
```
ddev launch
```
# Drupal sync, core update, modules update
We have the update command in all ddev projects that handles the actions needed to update the instance when changing branches for example.
It will run composer install, and all the drush commands to get the DB up to speed and imports of new configuration changes.
## Drupal sync
```
ddev update
```
## Drupal core update
Before running the core update it will do the drupal sync so you are always up to speed.
```
ddev update --core
```
## Drupal module update
Before running the module update it will do the drupal sync so you are always up to speed.
```
ddev update --module [modulename]
```
# Mutagen
By default this project is set with mutagen. If you need to alter configuration, for example turn off mutagen create a file called config.local.yaml and add this line:
```
mutagen_enabled: false
```
# Xdebug
Set xdebug on
```
ddev xdebug on
```
Set xdebug off
```
ddev xdebug off
```
# SOLR
SOLR configuration has been moved inside .ddev folder, that will be mounted in the solr cores created in ddev.
Check .ddev/solr-demo and .ddev/solr-umami
