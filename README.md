This write up continues my learning journey of the Splunk platform. In this lab, I will be learning about dashboards and reports. 

Objectives:
1)Learn why you need to organize data in Splunk
2)How to create dashboards to visualize information
3)Turning SOC use cases into alerts


The main reason that Splunk includes dashboards to help organize the overwhelming amount of data that gets forwarded and indexed into Splunk.

In SPL languange, index=* appears to be a wild card command that will return a large group of data. When I put in the command, I also set it to "all time" so it returns all of the data that is historically available. The search shows the event and time of the event. This includes the username, timestamp,source IP address and the destination IP address in a pretty easy to understand format. The downside to this, however, is that this is a lot of events (over 35,000!), so it isn't wise to include data from "all time". This also causes performance issues within Splunk due to the sheer amount of data within the search. 


Creatubg Reports for Recurring Searches 

From time to time, security teams will need to run a timed report, which is simply a report that runs at a certain time, usually every 5 to 10 minutes or every few hours. This is neccessary in settings such as a SOC environment where there are multiple shifts, which not only helps increase the search head's load and processing time and reduce error, but will reduce the possibility of errors and inefficiency. 

Right now, I am creating a report by running a search to see the number of hosts sending logs in the Splunk instance. The search resulted in three hosts which are a network-server, web-server and a vpn_server. This is nice, but the objective of this report is to show the number of users who are using the VPN. So, I ran the the host=vpn_server | stats count by Username command. This command simply shows that you are looking for hosts that have contacted the VPN server and you are looking for all of the usernames of the individuals who have connected to the VPN server. I saved the report now and I can view it.


Creating Dashboards for Summerized Results 

Now, the lab tasks me with creating my own report from the network-server logs. It wants to know what is the highest number of times any port is used in the network connections. I mimicked the SPL command from my previous search, but instead I changed it to pull a report that lists the ports used in a network connection and their count. The command for this is host=network-server | stats count by port. It wants me to search for the highest number of times any port was used in the network. Once I generated the report, I clicked on the events tab (25,000 events) and scrolls down to the "interesting fields" section and selected the "ports" section. The highest number of times a port has been hit is 5.

I am not learning to create a dashboard in the lab. Dashboards are incredibly useful as it provides us with quick information about the data present in Splunk. They give a brief overview of the most important data and can give us a smaller area to focus on, such spike and drops in data sources, which can show a surge in failed login attempts. I navigated over to the dashboards tab and selected "Create New Dashboard". Once I finished naming the dashboard, setting permissions and setting the format, I created a new dashboard where I added the report from before where Isearch for the names of VPN users. Once I finished that up, I opted to give the report a bar graph look. It shows me that Emma has logged in the least amount of times and the dashboard is complete!

Learning Note: Splunk dashboards use the data from the reports to build the visualizations. 


Alerting on High Priority Events 


