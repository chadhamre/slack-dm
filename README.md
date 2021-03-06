# slack-dm

A Python utility to bulk DM users in a Slack workspace by calling the Slack API via HTML requests.

## Prerequisites

This script uses **Python 3** due to its calling of the `print()` method. The script also uses the Python libraries `time` and `requests` to set timeouts and perform HTML GET requests. Run `pip install` as necessary.

To run the script, you'll need a file `users` with the usernames you wish to DM on a separate line, starting at line 1. You can do this by calling the `users.list` method from the Slack API. A simple way to manually generate a `users` file can be done as follows.

## Usage

### Generating a `users` file

1. Visit [https://api.slack.com/custom-integrations/legacy-tokens](https://api.slack.com/custom-integrations/legacy-tokens) to provision a _legacy token_ for the script. Copy and save the token somewhere. 

2. Run `curl https://slack.com/api/users.list?token=$TOKEN&pretty=1 -o users`, replacing `$TOKEN` with the token from step 1 to write the output of the HTML request to a file `users`.

3. Using **vim** or your preferred regex utility, remove all lines from the file except those containing the `"NAME":` attribute, then truncate the remaining lines such that only the username is kept without any enclosing double quotes. In **vim**, you would run:
	```
	:%s/^\([^\"]*\"name\"\: \"\)/
	:%s/",[.]*$/
	```
	This leaves a file with one username per line. Edit the list as necessary such that it contains only usernames of the people to whom messages will be sent.
	Of course, you can do this manually if you're a masochist. Or you can edit `slack-dm.py` so that it does this automatically (if you do, pull request it please!). 

### Editing and running `slack-dm.py`

1. On line 6, intialise `token` as a string containing the legacy token.

2. On line 8, edit the list `msgs` to contain any number of messages to be sent. 

	**NOTE:** All messages must be formatted with percent-encoding, ie. all spaces and non-alphanumeric symbols need to be escaped with a percent code.

3. On line 13, initialise `user` as the sending user's (your) username.

4. On line 19, change the sleep variable as necessary.

5. Run `python3 slack-dm.py`. 

6. ???

7. Profit.
