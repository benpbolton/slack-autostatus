# slack-autostatus
Automatically update Slack status emoji with your current Mac application/url


## TLDR;

Launch a plist that checks the frontmost app/webpage every 15s, associates it with an emoji, and sends it off via Slack's status API... optionally also set Slack away/auto presence when locked

## Installation (in three <del>easy</del> steps!)



### Step 1: Configure Slack (API and Emoji):

- First things first: ensure your Slack team has the perfect emoji for apps/sites you care about. Slack has
 [great instructions here](https://get.slack.help/hc/en-us/articles/206870177-Create-custom-emoji)
- Next, you're going to need a Slack user API token. <del>Go [here](https://api.slack.com/custom-integrations/legacy-tokens) and request one from your slack administrators.</del> **Alas; much has changed in the Slack world, and they now want you to create a Slack app with a user scope**. That's a bit beyond this humble readme, but suffice it to say that you can create an 'internal' Slack app with the following [User Token Scope](https://api.slack.com/scopes?filter=user): `users.profile:write`. Once installed to your workspace, it will generate a 'User OAuth Token' (`xoxp-...`) to use.

_ps. Keep this token secret - though the scope is limited to your account, it can post status updates as you!!_



### Step 2: Get the slack-autostatus script:

Whether you fork/clone, copy/paste, or hand-type, you'll want a copy of this script locally on your Mac.

You might:

```
curl -o /usr/local/bin/slack-autostatus https://raw.githubusercontent.com/benpbolton/slack-autostatus/master/slack-autostatus

chmod +x /usr/local/bin/slack-autostatus
```

... but regardless of your approach, you'll want the file to be executable

_ps. Edit **this** file to add/remove applications/urls/emoji/etc_


### Step 3: Edit the launchd (plist) file:

Steady yourself: this is the final step

- curl down the sample plist file:

```
curl -o ~/Library/LaunchAgents/slack-autostatus.plist https://raw.githubusercontent.com/benpbolton/slack-autostatus/master/slack-autostatus.plist
```

- Make the following two (or three) edits to the file:
  - Change `PUT_IT_HERE!!!` to your Slack user token from above
  - (If needed) Change `/usr/local/bin/slack-autostatus` to the location you saved the slack-autostatus script
  - If you want the script to **also** update your slack presence (away/auto) based on whether your laptop is locked:
      + uncomment the `SET_PRESENCE` environmental variable
      + in a terminal, install the Quartz dependency with a `pip install pyobjc-framework-Quartz` (or `pip3` if you're using Python 3)

- Load the plist up:

```
launchctl load -w ~/Library/LaunchAgents/slack-autostatus.plist
```

- :tada:

![Sample Emoji](/essential-repository-asset.png "Turns out, I am using Slack")
