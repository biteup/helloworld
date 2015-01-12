# Backend Design

Database
--------

Because our models may change rapidly in the early stages of development, MongoDB looks to be a fine choice.
Flexibility and minimal relationships (simple relationships between models, if any) are the main factors to choosing NoSQL over SQL.

Cron Jobs
---------

At times, we may need to relegate some time-based tasks off from the main application, and into smaller manageable cron jobs.
Examples include sending an email to users every start of the month.

If needed, we can write crons with python, given the excellent python package, [python-crontab](https://pypi.python.org/pypi/python-crontab)
The ease of writing programs in Python should make cron management fun!

Main Application
----------------

After deliberating between Go and Python, we decided that Go would be the language of our main backend application.
Why? Because trying new technologies should be encouraged!

Also, given the strong support around Go (see http://gophercasts.io for instance), I think we would have fun building a backend web application with Go and Martini.

