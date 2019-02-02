Redmine Git Mirror plugin
==================

Adds ability to clone and fetch remote git repositories to redmine.

## Key Features
* Easy install (just clone to redmine plugins folder)
* Webhooks integration (gitlab and custom)
* Works well with enabled autofetch changesets setting and in mix with other scm types  
* Automatic deletes unreachable commits

# Install

    cd [redmine-root]/plugins
    git clone https://github.com/linniksa/redmine_git_mirror

Restart redmine, and enable `Git Mirror` scm type at `redmine.site/settings?tab=repositories`

## Accessing private repositories

At this moment only ssh access with redmine user ssh key is supported. 

# Fetching changes

This plugin supports 2 ways of fetching changes, via cronjob or via hooks.
You can use only one or both of them together.

## Cronjob

Run ```./bin/rails runner "Repository::GitMirror.fetch"```, for example: 

    5,20,35,50 * * * * cd /usr/src/redmine && ./bin/rails runner "Repository::GitMirror.fetch"  -e production >> log/cron_rake.log 2>&1

## Hooks

Hooks is preferred way because you can immediately see changes of you repository.

To enable hooks you should go to `redmine.site/settings?tab=repositories` and enable WS support:

![Enable ws support](docs/img/redmine-ws.png)

### GitLab integration

You can setup per-project or system wide hook, for both variants use 
* `redmine.site/sys/git_mirror/gitlab` as `URL`
* key from `Repository management WS API key` as `Secret Token`

###### For system wide setup

Go to `gitlab.site/admin/hooks`, and select only `Repository update events` trigger.

###### For per-project setup

Go to `gitlab.site/user/project/settings/integrations`, and select only `Push` and `Tags` events

