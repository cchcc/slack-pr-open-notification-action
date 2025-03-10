# Slack Pull Request Open Notification
Use GitHub Actions to notify Slack that a pull request has been opened.

![example](https://raw.githubusercontent.com/jun3453/slack-pr-open-notification-action/images/example.png)

## Usage
Add the following YAML to your new GitHub Actions workflow:

```yaml
name: Slack Pull Request Open Notification

on:
  pull_request:
    types: [opened, reopened]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Notify slack pr open
      env: 
        SLACK_WEBHOOK_URL : ${{ secrets.SLACK_WEBHOOK_URL }}
        SLACK_CHANNEL : 
        SLACK_USER_NAME : 
        PULL_REQUEST_NUMBER : ${{ github.event.pull_request.number }}
        PULL_REQUEST_TITLE : ${{ github.event.pull_request.title }}
        PULL_REQUEST_AUTHOR_NAME : ${{ github.event.pull_request.user.login }}
        PULL_REQUEST_AUTHOR_ICON_URL : ${{ github.event.pull_request.user.avatar_url }}
        PULL_REQUEST_URL : ${{ github.event.pull_request.html_url }}
        PULL_REQUEST_BODY : ${{ github.event.pull_request.body }}
        PULL_REQUEST_COMPARE_BRANCH_OWNER: ${{ github.event.pull_request.head.repo.owner.login }}
        PULL_REQUEST_COMPARE_BRANCH_NAME : ${{ github.event.pull_request.head.ref }}
        PULL_REQUEST_BASE_BRANCH_OWNER: ${{ github.event.pull_request.base.repo.owner.login }}
        PULL_REQUEST_BASE_BRANCH_NAME : ${{ github.event.pull_request.base.ref }}
        IS_SEND_HERE_MENTION : true
        MAKE_PRETTY : false
        MAKE_COMPACT : false
        IS_PR_FROM_FORK: false
        SEND_USER_ID_MENTIONS : ABCDE12345,AAABBBCCCC
        SEND_GROUP_ID_MENTIONS : GROUPIDDDD,GGGGROUPID
      uses: jun3453/slack-pr-open-notification-action@v1.3.0
```

### Arguments
#### SLACK_WEBHOOK_URL
The incoming Slack webhook URL. Create a repository secret named 'SLACK_WEBHOOK_URL' and paste the URL as the value.

#### PULL_REQUEST_*
See the following URL: https://developer.github.com/v3/pulls/.

#### IS_SEND_HERE_MENTION
**boolean (DEFAULT: true)**  
Whether to include the '@here' Slack mention when sending a message.

#### MAKE_PRETTY
**boolean (DEFAULT: false)**  
Pretty prints the information. Adds a "See Pull Request" button.

![make_pretty](https://raw.githubusercontent.com/jun3453/slack-pr-open-notification-action/images/make_pretty.png)

#### MAKE_COMPACT
**boolean (DEFAULT: false)**  
Smaller visual footprint.

![make_compact](https://raw.githubusercontent.com/jun3453/slack-pr-open-notification-action/images/make_compact.png)

#### IS_PR_FROM_FORK
**boolean (DEFAULT: false)**  
Whether notifications should support PRs from forks. By default, only the branch name is listed when sending a message.  
If set to 'true', it will add the branch owner in front of the branch name ('owner:branch' vs 'branch'). If this option is used, you may need to enable fork pull request workflows under your repository's Actions settings.

![make_compact and is_pr_fork](https://raw.githubusercontent.com/jun3453/slack-pr-open-notification-action/images/make_compact_fork.png)

#### SEND_USER_ID_MENTIONS
**string (Optional)**
Throw mentions to a specific user.
Enter your Slack user ID separated by commas.
Please google how to find out your user ID.

#### SEND_GROUP_ID_MENTIONS
**string (Optional)**  
Throw mentions to a specific group.
Enter your Slack group ID separated by commas.
Please google how to find out your group ID.