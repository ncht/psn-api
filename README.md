# PSN API

This is a python wrapper for the PSN API.

**Read the [wiki](https://github.com/ncht/psn-api/wiki)** and previous issues before opening a new one! Maybe your issue is already answered.

## How to get refresh token

Sony now is using reCaptcha. There is no way to do this authentication via the Script at this time. So we have worked around the authentication issue by doing the following.

1. From the PSN Website or App or Console Enable 2 Step Verification
2. Go to [https://auth.api.sonyentertainmentnetwork.com/login.jsp](https://auth.api.sonyentertainmentnetwork.com/login.jsp) Enter your credentials, Solve the reCaptcha, and when you get the `ENTER Verification Code` screen take a look at the URL in your browser. Collect the following ID: `ticket_uuid=b7aeb485-xxxx-4ec2-zzzz-0f23bcee5bc5&layout_type=......` **DO NOT ENTER THE VERIFICATION CODE**
3. From the API

```python
auth = Auth('YOUR EMAIL', 'YOUR PASSWORD', b7aeb485-xxxx-4ec2-zzzz-0f23bcee5bc5, 'verification_code_you_got_on_your_phone)

tokens = auth.get_tokens()

print(tokens)
```

4. Save the `refresh` and `npsso` values from the output

5. From now on you can authenticate (Refresh your tokens) instead of re-authenticating every time.

Like this:

```python
new_token_pair = Auth.GrabNewTokens(refresh_token)

tokens = {
    "oauth": new_token_pair[0],
    "refresh": new_token_pair[1],
    "npsso": npsso # saved above!
}

friend = Friend(tokens)
friend_list = friend.my_friends()
```

## Features
- Login to PSN
- Get user information
- View and manage your friends list
- Manage and send messages through PSN

## TODO
- View trophies and trophies for a specific game
- Create, manage and view communities

## Legal

This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by PlayStation or any of its affiliates or subsidiaries. This is an independent and unofficial API. Use at your own risk.
