# DevOps Assignment

I set up automated Telegram chatbot messaging in response to push events to this repository using Github Actions. Whenever some files are pushed into or changed in the repository, the actions described in a YAML file (tmessage.yml) in the folder `.github/workflows` will be executed. The expected message from the bot is as follows:

> **Good day, ias-9! There was a push event in ias-9/DevOps_Assignment.**

The steps I took to complete this job were as follows:

1. Create a new Github repository

2. Create a Telegram bot by messaging [@BotFather](https://web.telegram.org/#/im?p=@BotFather), typing in `/newbot` and following the instructions

![BotFather starts](https://github.com/ias-9/DevOps_Assignment/blob/master/images/BotFather.JPG)
*BotFather starts*

![Creating a new bot](https://github.com/ias-9/DevOps_Assignment/blob/master/images/BotFather2.JPG)
*Creating a new bot*

3. Start the newly created bot by pressing on the link sent by @BotFather

![Starting the new bot](https://github.com/ias-9/DevOps_Assignment/blob/master/images/send_noti_bot.JPG)
*Starting the new bot*

4. Create a YAML file in the folder `.github/workflows` containing instructions for Github actions to send message through the bot. The instructions are as follows:
```yml
name: telegram message
on: [push]
jobs:
  
    build:
      name: Build
      runs-on: ubuntu-latest
      steps:
      - uses: actions/checkout@master
      - name: send custom message with args
        uses: appleboy/telegram-action@master
        with:
          to: ${{ secrets.TELEGRAM_TO }}
          token: ${{ secrets.TELEGRAM_TOKEN }}
          args: The ${{ github.event_name }} event triggered first step.
```
5. Change the `args:` in the last line to `message:` and modify the message to my liking. 

![Changing args to message](https://github.com/ias-9/DevOps_Assignment/blob/master/images/updated%20yml.JPG)
*Changing the message*

6. Set up secrets for `TELEGRAM_TO` and `TELEGRAM_TOKEN` so that Github Actions can access these values to use the bot and send message to my number. The token `TELEGRAM_TOKEN` is provided by @BotFather and the chat ID `TELEGRAM_TO` can be seen from https://api.telegram.org/bot/getUpdates by pasting the bot token between `/bot` and `/getUpdates`.

![Setting up secrets](https://github.com/ias-9/DevOps_Assignment/blob/master/images/Secrets.JPG)
*Setting up Secrets*

7. Push a file into the repository to try out this function and check for completion in the **Actions** tab above and in the Telegram chat with the bot

![Telegram Chat](https://github.com/ias-9/DevOps_Assignment/blob/master/images/send_noti_bot2.JPG)
*Message from the bot*

In conclusion, creating the Telegram bot and then making the YAML file comes first before pushing files to test Github Actions.

