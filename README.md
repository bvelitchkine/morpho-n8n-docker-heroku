# Overview

This is a [Heroku](https://heroku.com/)-focused container implementation of [n8n](https://n8n.io/). I forked it from [n8n-heroku](https://github.com/n8n-io/n8n-heroku) to make it work with docker.

# Purpose

I needed to have the n8n config in a repo somewhere to be able to force-rebuild it on heroku and have the latest version of n8n. This project was instantiated for the sole purpose of having n8n latest updates.

# On first deploy

## Steps

1. Create a new heroku app
2. Set the config vars (cf. below)
3. Clone this GitHub project on your machine
4. Login to heroku on your machine
   ```bash
   heroku login
   ```
5. Add the heroku as a remote to your local project
   > You'll end up with two remotes: one that is this github repo, another that's the heroku one.
   ```bash
   git remote -a morpho-n8n
   ```
6. Deploy the app
   ```bash
   git push heroku main
   ```
7. Go back to the heroku dashboard to set the `WEBHOOK_URL` var (cf. below)

## Environment variables

```plaintext
DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED=false
EXECUTIONS_DATA_MAX_AGE=48
EXECUTIONS_DATA_PRUNE=true
EXECUTIONS_DATA_PRUNE_MAX_COUNT=10000
EXECUTIONS_DATA_SAVE_MANUAL_EXECUTIONS=none
EXECUTIONS_DATA_SAVE_ON_ERROR=all
EXECUTIONS_DATA_SAVE_ON_SUCCESS=none
EXECUTIONS_PROCESS=main
GENERIC_TIMEZONE=Europe/Paris
GITHUB_AUTO_DEPLOY=false
N8N_DISABLE_PRODUCTION_WEBHOOKS=true
N8N_ENCRYPTION_KEY=**a secure key**
WEBHOOK_URL=**You'll only know it after the first deploy**
```

You'll have some extra environment variables set automatically by heroku.

# To update n8n

Simply run these commands on your local machine:

```bash
git commit --allow-empty -m "updating n8n"
git push heroku main
```

You'll force re-build the app and pull the latest n8n version.

> No worries, workflows, executions and credentials are all persisted in the postgres database add-on of the heroku project ;)
