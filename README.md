## Progressive profiling update user profile app

This is a simple node app that works along with Auth0 redirect rules to progressivly ask and update user's profile

## Bit of context

First, head over to Auth0 documentation to learn about [Progressive Profiling](https://auth0.com/docs/users/concepts/overview-progressive-profiling)

Second, if you are not yet familiar with Auth0's powerful extensibility feature called Rules, then head over to [Rules](https://auth0.com/docs/rules) documentation and especially relevant to the topic of progressive profiling, checkout [redirect rules](https://auth0.com/docs/rules/guides/redirect).

Finally, checkout redirect rules example [here](https://github.com/auth0/rules/tree/master/redirect-rules/progressive-profiling) that shows how to put all of these concepts together to implement progressive profiling.

## Just tell me how to make it work

Set up redirect rules as specified in the redirect rules example [here](https://github.com/auth0/rules/tree/master/redirect-rules/progressive-profiling#auth0-setup) **Note: You will get `UPDATE_PROFILE_WEBSITE_URL` value later once you have deployed this `progressive-profile-demo` webapp**

Now, this simple node webapp is just a replacement of `update-profile-website` webtask implemented [here](https://github.com/auth0/rules/blob/master/redirect-rules/progressive-profiling/update-profile-website.js).

1. clone this repo
2. host this webapp with your choice of server platform that supports nodejs platform (I'll explain below how to set it up with heroku)
3. setup environment variables with same names as webtask secrets mentioned [here](https://github.com/auth0/rules/tree/master/redirect-rules/progressive-profiling#secrets)
4. make sure you install all the dependencies specified in `package.json`
5. fire up the server. This should give you a public url of this app that you need to use as a value for `UPDATE_PROFILE_WEBSITE_URL`

## Step by step guide to set this app with Heroku

**Pre-requisites: You have heroku account and you have already [installed Heroku command line interface](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)** Oh and Heroku CLI needs `git` so there is that. 


1. Login to Heroku by running `heroku login` command in your OS terminal
2. Clone this repo by running `git clone git@github.com:ashishdasnurkar/update-profile-website.git`
3. Change into repo directory by running `cd update-profile-website`
4. Now create a Heroku app by running `heroku create`. This will give a random name to your app and set up a git repo within Heroku where you can push the app source code.
5. Push the app source code to Heroku to deploy it by running `git push heroku master`. This will install all required dependencied on Heroku in order to run the app and once successful, it will spit out the live url for your app. This is the url that you should use for `UPDATE_PROFILE_WEBSITE_URL` value in step#5 mentioned in earlier section
6. To complete the setup all you need to do now is to setup the required environment variables mentioned in step #4 above. You can do so by using Heroku CLI `heroku config:set AUTH0_DOMAIN=YOUR_TENANT_DOMAIN`.  Here `YOUR_TENANT_DOMAIN` refers to <YOUR_TENANT>.auth0.com or if you are using custom domain then <YOUR_CUSTOM_DOMAIN>

## How do I test if everything is working?

Make sure you understand [how the example works](https://github.com/auth0/rules/tree/master/redirect-rules/progressive-profiling#how-it-works)

Now, login to your own app (not this one. Or if you are just testing then download one of Auth0 quickstarts) and signup with a new user email & password. After successful signup you should be redirected to this app where you will be prompted to enter your First Name and Family Name. Once you submit the form, the entered first name and family name should be saved in user profile > user metadata (confirm this by going to auth0 dashboard & looking up user profile). The saving/updating user profile is done by `continue-from-update-profile-website` [rule](https://github.com/auth0/rules/blob/master/redirect-rules/progressive-profiling/continue-from-update-profile-website.js)

On third login, you will be presented to enter your date of birth. One you submit the form, the entereed DOB should be saved in user profile > user metadata (confirm this by going to auth0 dashboard & looking up user profile).

## What if I can't get it to work?

[Open an issue](https://github.com/ashishdasnurkar/update-profile-website/issues) or reach out to the friendly [Auth0 Community](https://community.auth0.com/) for help.