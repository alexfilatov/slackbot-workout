# slackbot-workout
A fun hack that gets Slackbot to force your teammates to work out!

<img src = "https://ctrlla-blog.s3.amazonaws.com/2015/Jun/Screen_Shot_2015_06_10_at_5_57_55_PM-1433984292189.png" width = 500>


# Instructions

1. Clone the repo and navigate into the directory in your terminal.

    `$ git clone git@github.com:brandonshin/slackbot-workout.git`

2. In the **[Slack API Page](https://api.slack.com/docs/oauth-test-tokens)**, register yourself an auth token for your team. You should see this. Take note of the token, e.g. `xoxp-2751727432-4028172038-5281317294-3c46b1`. This is your **SLACK_USER_TOKEN_STRING**

    <img src="http://i.imgur.com/RZqDRbL.png" width = 500>

3. In the **Slackbot [Remote control Page](https://slack.com/apps/A0F81R8ET-slackbot)**. Register an integration by clicking Add Configuration & then you should see this. __Make sure you grab just the token out of the url__, e.g. `AizJbQ24l38ai4DlQD9yFELb`. This is your **SLACK_URL_TOKEN_STRING**

    <img src="https://ctrlla-blog.s3.amazonaws.com/2015/Jun/Screen_Shot_2015_06_03_at_8_44_00_AM-1433557565175.png" width = 500>

4. Save your SLACK_USER_TOKEN_STRING and SLACK_URL_TOKEN_STRING as environmental variables in your terminal.

    `$ export SLACK_USER_TOKEN_STRING=YOURUSERTOKEN`

    `$ export SLACK_URL_TOKEN_STRING=YOURURLTOKEN`

    If you need help with this, try adapting the first 5 steps of the guide to [edit your .bash_profile](http://natelandau.com/my-mac-osx-bash_profile/)

5. Set up channel and customize configurations

    Open `default.json` and set `teamDomain` (ex: ctrlla) `channelName` (ex: general) and `channelId` (ex: B22D35YMS). Save the file as `config.json` in the same directory. Set any other configurations as you like.

    If you don't know the channel Id, fetch it using

    `$ python fetchChannelId.py channelname`

6. If you haven't set up pip for python, go in your terminal and run.
`$ sudo easy_install pip`

7. While in the project directory, run

    `$ sudo pip install -r requirements.txt`

    `$ python slackbotExercise.py`

Run the script to start the workouts and hit ctrl+c to stop the script. Hope you have fun with it!

# Install on Heroku

1. [Install Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)

    `brew tap heroku/brew && brew install heroku`

2. Login to Heroku

    `heroku login`
    
3. Create Heroku app

    `heroku create`
    
    As a result you'll get smth like that:
    
    ```
     Creating app... done, stack is heroku-18
     https://floating-dragon-42.heroku.com/ |
     https://git.heroku.com/floating-dragon-42.git
    ```
   
   Where `floating-dragon-42` will be your Heroku app name
    
4. Set up all environment variables needed for the Slack bot in the Heroku app settings, e.g.:

    `heroku config:set --app floating-dragon-42 SLACK_USER_TOKEN_STRING=YOURUSERTOKEN SLACK_URL_TOKEN_STRING
    =YOURURLTOKEN`
    
    You can also configure `teamDomain`, `channelName` and `channelId` via environment variables, e.g.:
    
    `heroku config:set --app floating-dragon-42 SLACK_TEAM_DOMAIN=ctrlla SLACK_CHANNEL_NAME=channelName
     SLACK_CHANNEL_ID=channelId`

5. Deploy to heroku

    `git push heroku master`        

6. Scale the app dyno

    `heroku ps:scale bot=1`

7. In case you need to check logs 

    `heroku logs --tail`

Heroku CLI commands: https://devcenter.heroku.com/articles/heroku-cli-commands
