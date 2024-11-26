This write up continues my learning journey of the Splunk platform. In this lab, I will be learning about dashboards and reports. 

Objectives:
1)Learn why you need to organize data in Splunk
2)How to create dashboards to visualize information
3)Turning SOC use cases into alerts


The main reason that Splunk includes dashboards to help organize the overwhelming amount of data that gets forwarded and indexed into Splunk.

In SPL languange, index=* appears to be a wild card command that will return a large group of data. When I put in the command, I also set it to "all time" so it returns all of the data that is historically available. The search shows the event and time of the event. This includes the username, timestamp,source IP address and the destination IP address in a pretty easy to understand format. The downside to this, however, is that this is a lot of events (over 35,000!), so it isn't wise to include data from "all time". This also causes performance issues within Splunk due to the sheer amount of data within the search. 

From time to time, security teams will need to run a timed report, which is simply a report that runs at a certain time, usually every 5 to 10 minutes. This is neccessary in settings such as a SOC environment where there are multiple shifts, which not only helps increase the search head's load and processing time and reduce error, but will reduce the possibility of errors and inefficiency. 

Right now, I am creating a report by running a search to see the number of hosts sending logs in the Splunk instance. The search resulted in three hosts which are a network-server, web-server and a vpn_server. This is nice, but the objective of this report is to show the number of users who are using the VPN. So i have to run the host=vpn_server | stats count by Username command
