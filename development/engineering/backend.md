# Backend Design

Database
--------

Because our models may change rapidly in the early stages of development, MongoDB looks to be a fine choice.
Flexibility and minimal relationships (simple relationships between models, if any) are the main factors to choosing NoSQL over SQL.

Cron Jobs
---------

At times, we may need to relegate some time-based tasks off from the main application, and into smaller manageable cron jobs.
Examples include sending an email to users every start of the month.

For us, Node JS seem to be a good fit, given that these jobs seem very much event-driven. We currently maintain all cron-related scripts over at [Runningman repository](http://github.com/gobbl/runningman) (built with Node JS)

Main Application
----------------

After deliberating between Go and Python, while using Go to build something would be educational and really cool, I have better understanding of Python compared to Go. Hence, for faster production, we decided to use Python, and in particular the Falcon framework. You can find the main backend API server [here](http://github.com/gobbl/snakebite).

