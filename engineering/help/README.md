# Setting up Scheduled Jobs on Mac OS X

## TL;DR

If you are familiar with setting up scheduled jobs via crons (i.e., crontabs) on *nix-based machines, you may have realized that Mac OS X discourages crontab but encourages [launchd](https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/ScheduledJobs.html) instead.

Skip to the Setup section below to see how to configure scheduled jobs right away on you Mac instead.

## Why

On Apple's developer pages, it argues that cron jobsare not run should the computer falls asleep (in sleep mode). Damn these computers! However, `launchd` jobs are sure to run the moment the computer wakes up once again! Of course, if the computer is completely shut down, we can only pray :(

![wtf](http://i1.kym-cdn.com/entries/icons/original/000/004/592/my-brain-is-full-of-fuck.jpg)

If you really must, you can still set up scheduled tasks via crontab on Mac. Please see the [stackoverflow question here](http://stackoverflow.com/questions/15395479/using-cron-on-mac-osx-mountain-lion) and the [cron wiki page](http://en.wikipedia.org/wiki/Cron#Examples) in general.


## Setup

There exists a great [tutorial here](http://alvinalexander.com/mac-os-x/launchd-plist-examples-startinterval-startcalendarinterval) by Alvin Alexander.

However, let's discuss a quick introduction of how launchd works.

Firstly, launchd is a daemon on Mac OS X that simply runs tasks as requested by the user. What tasks the daemon should run is controlled by what launchctl (i think it probably means lanuch control?) lists as jobs.

In short, you may not speak to launchd but only to its boy: the launchctl

If you don't believe me, try running ```$ launchd``` on your terminal.


So how do we assign a job to launchctl? Also, how do we tell launchctl to run it at say, every 3:00pm of Monday?

Attached in this directory is the file [com.slack.benri.slackbot.plist](com.slack.benri.slackbot.plist). Take a look at the file. Looks like a XML file, doesn't it? It is! 

Why is the extension `.plist` then? Basically, the `.plist` is to mean **process list**. It is basically a task script that launchctl reads and executes accordingly.

When we need to ensure that launchd daemon runs this task, we simple run the command: ```$ launchctl load com.slack.benri.slackbot.plist```. To check that this process list is loaded, we can do a ```$ launchctl list | grep benri``` to check all process lists with names containing `benri`. We should see this task listed!

Take a closer look at the full name of the task. It reads `com.slack.benri.slackbot`. Why did it give the task that name? The magic is in the [om.slack.benri.slackbot.plist](om.slack.benri.slackbot.plist) file. Take a look at the `<key>Label</key><string>com.slack.benri.slackbot</string>` tag. This is what we label this process list as. 

To set up the frequency or interval, simply change the values inside the `<key>SetCalenderInterval</key>` tag. Here, we are asking the daemon to run this task on 19:00 hours (7:00 PM) every Wednesdays.

```
<key>StartCalenderInterval</key>
<dict>
	<key>Hour</key>
	<integer>19</integer>
	<key>Minute</key>
	<integer>0</integer>
	<key>Weekday</key>
	<integer>3</integer>
</dict>
```

What commands to run then? Take a look at the following snippet of the file:

```
<key>ProgramArguments</key>
  <array>
    <string>bash</string>
    <string>slackbot.sh</string>
  </array>
```

What this says is : run this following command : `bash slackbot.sh`

Note that for every space in the terminal command, we need to treat them as separate `&lt;string&gt;` elements then.
You can peer inside the [slackbot.sh](slackbot.sh) file to see what exactly the script is trying to execute!

That's all for now! Hope this is beneficial!
