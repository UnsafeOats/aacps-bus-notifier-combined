# AACPS Bus Notifier

This is a combined repo for my two separate iterations of creating a notification system to text me when my son's bus isn't running for the day.  Both the codebase in the `python/` folder and the `rust/` folder do generally the same thing and are completely independent of one another, this is just a repo to combine them both for easy testing and deployment.

Anne Arundel County Public Schools is an absolute trash heap for anything IT related (although the schools are pretty good), so currently the county just sends a text message to every parent at the school when a single bus from the school won't be running that day.  Parents are then responsible for opening up the website and searching for their bus number to see if the alert is for them or not.

**It's so absolutely stupid.**

To fix my personal experience with the crappy bus performance this year & last year, I created these notification systems.  First one was implemented in Python and was then reimplemented in Rust as a way to learn Rust.  The Rust implementation is *not quite* done yet, but it's close and what is done works phenomenally.

Both implementations generally work the same way:
  1) Pull the current bus outage table from the [AACPS website](https://busstops.aacps.org/public/BusRouteIssues.aspx)
  2) Parse the table and collect necessary information into a simple set/HashSet containing all outage events
  3) Compare the current outage information with the previously collected outage information and send out text messages to all parents for each bus that has had a change in status

The current differences in implementation are:
  **Python** - Currently checks the bus outage site at specifically scheduled times throughout the day
  **Rust** - Checks the bus outage site every 5 mins for more responsive notifications
