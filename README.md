# violinist-drupal-demo

This repo is what was in use in the demo and description in the blogpost [https://orkjern.com/updating-drupal-core-automatically-demo](https://orkjern.com/updating-drupal-core-automatically-demo)

## Travis set-up

Look at the file [.travis.yml](https://github.com/eiriksm/violinist-drupal-demo/blob/master/.travis.yml)

## Mergify set-up

First sign up, and then look at the file [.mergify.yml](https://github.com/eiriksm/violinist-drupal-demo/blob/master/.mergify.yml)

## Codeship setup

This project uses the following settings for codeship:

- Test commands: None (we are running tests with Travis)
- Deploy: Type "custom script".

The script is very crude, and you probably want to change at least the part where we log in as root. But for this demo it looks like this (xxx.xxx.xxx.xxx is the IP address of the server it was deployed to):

```bash
ssh root@xxx.xxx.xxx.xxx "cd /var/www/html && git pull && composer install && drush updb -y && drush cim -y && drush cr && drush cron"
```

The reason we run cron after, is to make sure the update status is updated (for demo purposes). You probably want to remove this for your setup.
