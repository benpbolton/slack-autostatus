# slack-autostatus
Automatically update Slack status (emoji) with your current Mac application/url


## TLDR;

Launch a plist that checks the frontmost app/webpage every 15s, associates it with an emoji, and sends it off via Slack's status API...

## Installation:

### Slack (API and Emoji):

- First things first: ensure your Slack team has the perfect emoji for apps/sites you care about. Slack has
 [great instructions here](https://get.slack.help/hc/en-us/articles/206870177-Create-custom-emoji)
- Next, you're going to need a personal slack API token. Go [here](https://api.slack.com/custom-integrations/legacy-tokens) and request one from your slack administrators. 

_ps. Keep this token secret - though the scope is limited to your account, it can read/post/etc as you!!_

### The slack-autostatus script:

Whether you fork/clone, copy/paste, or hand-type, you'll want a copy of this script locally on your Mac. 

You might:

```
curl -o /usr/local/bin/slack-autostatus https://raw.githubusercontent.com/benpbolton/slack-autostatus/master/slack-autostatus

chmod +x /usr/local/bin/slack-autostatus
```

... but regardless of your approach, you'll want the file to be executable

### The launchd (plist) file:

Steady yourself: this is the final step

- curl down the sample list file:

```
curl -o ~/Library/LaunchAgents/slack-autostatus.plist https://raw.githubusercontent.com/benpbolton/slack-autostatus/master/slack-autostatus.plist
```

- Make the following two edits to the file:
  - Change `PUT_IT_HERE!!!` to your Slack legacy/testing token from above
  - (If needed) Change `/usr/local/bin/slack-autostatus` to the location of the slack-autostatus script

- Load the plist up:

```
launchctl load ~/Library/LaunchAgents/slack-autostatus.plist
```

- :tada:



