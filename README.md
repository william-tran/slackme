# slackme

Hey slackers, tired of staring at your terminal to wait for a long running command to finish? Or forgetting to check that it finished, and wasting precious cycle time? Slack better, with slackme.

## Installation

1. Create a private channel for yourself, and then create an [Incoming Webhook](https://api.slack.com/incoming-webhooks) Slack integration that points to your private channel.
2. Set the webhook url in an environment variable called `SLACKME_INCOMING_WEBHOOK_URL`, eg in your .bash_profile:

```
export SLACKME_INCOMING_WEBHOOK_URL=https://hooks.slack.com/services/XXXX/YYYY/ZZZZ
```
3. add the [slackme script](/slackme) to your `PATH`

## Usage

It's a bit like `nohup some-command with args & `. `slackme` will trap SIGHUP and run the command in the background, so no need to `&` at the end, e.g.:

```
$ slackme ./gradlew runSomeReallyLongTests
saving output of ./gradlew runSomeReallyLongTests to /tmp/slackme.12345.tmp
```  

Contol is given back immediately. You can watch the output of your command via the temp file. When the command is finished, you'll get a slack message in your private channel!

>Hey @channel, command
>```
>./gradlew runSomeReallyLongTests
>```
>exited with status code 1.
>
> Output saved to /tmp/slackme.12345.tmp, here are the last 3500 bytes:
>```
>...
>fail!
>fail!
>fail!
>
>BUILD FAILED
>
>Total time: 30 mins 14.638 secs
>Stopped 1 compiler daemon(s).
>Received result Failure[value=org.gradle.initialization.Reported...
>```

The including more than 3500 bytes of output seems to cause Slack to not `pre` format the output. 

## License

[MIT License](/LICENSE)

