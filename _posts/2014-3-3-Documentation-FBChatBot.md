---
layout: post
title: Test Documentation
---

Facebook realtime callback endpoint

# Facebook realtime callback endpoint

Facebook will call this endpoint when there is a change in user's feed/likes or if there is a new message for DeCirc page

- Copy `fbrealtime-apache.conf` to `/etc/apache/sites-available` and enable it

- Put SSL certificates in `/usr/local/sslcert/`

- Check https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps for deploying

- Facebook will call these url's: `https://feed.decirc.com/fbrealtime` and `https://feed.decirc.com/messenger`


### Setup/Change realtime subscriptions in facebook:

```bash
curl -XPOST 'https://graph.facebook.com/732254010188683/subscriptions' -d 'access_token=732254010188683|liUKDnHIHjVmeg2ctKFVutScxqI&callback_url=http%3A//test.decirc.com%3A5000/fbrealtime&object=user&verify_token=8830413dee096b33785d502684a8875f&fields=feed,likes'
```

### Set Greeting Text

```bash
curl -X POST -H "Content-Type: application/json" -d '{
  "setting_type":"greeting",
  "greeting":{
    "text":"Hi, hope you are doing well! We have got some great new games, music and movies that you may like.  What can I get for you?"
  }
}' "https://graph.facebook.com/v2.6/me/thread_settings?access_token=<page_access_token>"
```

### Explaination: 

```bash
access_token=appAccessToken&callback_url=callback_server_url_encoded&object=user&verify_token=verify_token&fields=feed,likes
```

verify_token in the above request is `fb_realtime_verify_token` value in `FBRealtimeCallback/configuration.ini`

### Test if the server is working:

```bash
https://feed.decirc.com/fbrealtime?hub.mode=subscribe&hub.challenge=testing&hub.verify_token=8830413dee096b33785d502684a8875f
```

### Add this url in facebook developer settings for an app

##### FB Realtime edge for portal user's likes and feed

- Go to `DeCirc` app in FB and click `Webhooks` (https://developers.facebook.com/apps/621166884630730/webhooks/)
- Enter `Callback URL` as `https://feed.decirc.com/fbrealtime` and enter `fb_realtime_verify_token` in `FBRealtimeCallback/configuration.ini` as `Verify Token`
- Enter `feed, likes` in `Fields`
- Facebook will verify this and start pushing realtime data

##### FB Realtime edge for Messenger

- Go to `Social Store` app in FB and click `Webhooks` (https://developers.facebook.com/apps/806491129480662/webhooks/)`
- Enter `Callback URL` as `https://feed.decirc.com/messenger` and enter `fb_realtime_verify_token` in `FBRealtimeCallback/configuration.ini` as `Verify Token`
- Enter `message_deliveries, messages, messaging_optins, messaging_postbacks` in `Fields`
- Facebook will verify this and start pushing messages data
