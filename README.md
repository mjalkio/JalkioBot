# JalkioBot

The goal of this project is to create a personal assistant bot that can be used with [ChatSim](https://www.chatsim.com). ChatSim is a SIM card that gives unlimited international access to chat applications such as Messenger and WhatsApp. Since it does not allow you to use other applications, the goal of this app will be to use Messenger as an interface to access other services.

I have no official ties to ChatSim; I'm just a customer!

## Getting Started

Note: This guide is based on the [walk-through](https://developers.facebook.com/docs/messenger-platform/quickstart) provided by Facebook. I didn't feel that it led you through the process in a way that made sense, so I'm rewriting it here. However, some text will be copied directly.

### 1) Create a Facebook App and Page

Create a new [Facebook App](https://developers.facebook.com/quickstarts/?platform=web). Once you've created your App copy down the App Secret, which can be found on the App dashboard.

Next create a [Facebook Page](https://www.facebook.com/pages/create). There are lots of options and they confuse me, feel free to choose whatever makes the most sense to you!

Now go back to the App Dashboard and under Product Settings click "Add Product" and select "Messenger." In the Token Generation section, select your Page. A Page Access Token will be generated for you. Copy this Page Access Token.


### 2) Deploying to Heroku

Now you need to deploy your chatbot somewhere. Here I assume that you've already cloned the git repository and have it on your local machine. If you don't already have a [Heroku](https://www.heroku.com/) account make sure to create one. Then create a new app.

Go to the Settings tab for your app, and click "Reveal Config Vars." You need to add four configuration variables:
* `MESSENGER_APP_SECRET` - the App Secret you copied down earlier
* `MESSENGER_PAGE_ACCESS_TOKEN` - the Page Access Token you copied down earlier
* `MESSENGER_VALIDATION_TOKEN` - any string (you'll use it again later, so copy it down). Facebook uses my_voice_is_my_password_verify_me in their tutorial
* `SERVER_URL` - you can find this by scrolling down the page to the "Domains" section of the settings page

Now it's time to push your application to Heroku! You can find the Git URL in the "Info" section of the settings page. First we'll add that URL as a remote. In the root directory of your local repository type:

```
git remote add heroku YOUR_GIT_URL_HERE
```

Once you've done that you can deploy to Heroku at any time by typing:

```
git subtree push --prefix node heroku master
```

### 3) Setting Up Webhooks

Go back to the Facebook App dashboard. Navigate back to Messenger settings and in the Webhooks section, click "Setup Webhooks."

The callback URL is `SERVER_URL/webhook` (*not* the Git URL) and the Verify Token is `MESSENGER_VALIDATION_TOKEN` from earlier (not literally those strings, the values you put in your Heroku Settings). Select message_deliveries, messages, messaging_optins, and messaging_postbacks under Subscription Fields.

Finally, in the Webhooks section, you need to subscribe the webhook for the Facebook Page you created earlier (you will need to grant some permissions).

## Test Your Chatbot

If you've set up everything correctly you should be able to message your Page and have the text echoed back to you! Now it's time to hack up some amazing things!

## More Information

This project is forked from a sample project showcasing the Messenger Platform. You can go through the [walk-through](https://developers.facebook.com/docs/messenger-platform/quickstart) to understand this code in more detail. The [Complete Guide](https://developers.facebook.com/docs/messenger-platform/implementation) goes deeper into the features available.

Visit the [dev site](https://developers.facebook.com/docs/messenger-platform/) to find out more details about the Messenger Platform.
