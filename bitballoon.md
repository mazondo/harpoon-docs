# BitBalloon Support
We've recently added support for deploying to BitBalloon using harpoon

## Getting Started
Just run the command as normal:

```
harpoon init
```

and edit your `harpoon.json` file as needed.  Here's an example file for BitBalloon

```json
{
  "name" : "bitballoon-app",
  "hosting" : "bitballoon",
  "auth_namespace" : "main",
  "hosting_options" : {
    "primary_domain" : "yourdomain.com"
  },
  "directory" : "dist"
}

```

run `harpoon setup` to create your app, and `harpoon doctor` to confirm you're raedy to go

## Authentication
The first time you run a harpoon command, you'll be asked for your BitBalloon access_token.  To generate a token, just go to https://www.bitballoon.com/applications and generate a new Personal Access Token

## Using an existing BitBalloon site
If you're app is already deployed to bitballoon, just make sure that the `name` of your app in your `harpoon.json` file matches the name of your bitballoon app.  If it does, you can begin managing your deploys using harpoon.

## Running the commands
All of the harpoon commands are configured to work for BitBalloon, this includes:

* `harpoon setup` - Sets up your deploys with BitBalloon
* `harpoon doctor` - Confirms your setup is ready to go
* `harpoon deploy` - Deploys the current site
* `harpoon list` - Lists previous versions of the site available for rollback
* `harpoon rollback {{version}}` - Rolls back to a previous version of your site
