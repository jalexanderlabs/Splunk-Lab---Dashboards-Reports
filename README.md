This write-up continues my learning journey with the Splunk platform. In this lab, I focused on dashboards and reports.

Objectives:
Learn why organizing data in Splunk is important.
Understand how to create dashboards to visualize information.
Turn SOC use cases into alerts.
Organizing Data in Splunk

Splunk includes dashboards to help manage the overwhelming amount of data that is forwarded and indexed. This allows for better data organization and quicker insights.

In SPL language, the command index=* acts as a wildcard, returning a broad set of data. I set the time range to "All Time" to retrieve all historical data. The search results displayed events along with timestamps, usernames, source IP addresses, and destination IP addresses in a clear format. However, this approach is inefficient because it returns over 35,000 events, which can cause performance issues. It’s generally not advisable to search across "All Time" due to the sheer volume of data.


Creating Reports for Recurring Searches

Security teams often need to run scheduled reports at regular intervals—typically every 5 to 10 minutes or every few hours. This is especially important in a SOC environment, where multiple shifts rely on timely data. Automating these reports helps improve search head performance, reduce errors, and increase efficiency.

Currently, I am creating a report to see how many hosts are sending logs to the Splunk instance. The search returned three hosts: a network server, a web server, and a VPN server. While this is useful, the goal of this report is to track VPN user activity. I refined the search using the command:
host=vpn_server | stats count by Username
This command looks for all usernames that have connected to the VPN server. I saved the report and can now view it as needed.


Creating Dashboards for Summarized Results

Next, the lab tasked me with creating a report from the network server logs to identify the most frequently used ports in network connections. Using a similar SPL command, I modified it to list the ports and their counts:
host=network-server | stats count by port
After generating the report, I reviewed 25,000 events and navigated to the "Interesting Fields" section to analyze port usage. The most frequently used port was hit five times.

Now, I am learning how to create dashboards. Dashboards are incredibly useful because they provide quick insights and focus areas, such as spikes or drops in data sources. For example, they can highlight surges in failed login attempts.

I navigated to the Dashboards tab and selected Create New Dashboard. After naming the dashboard, setting permissions, and choosing the format, I added the VPN user report. I opted for a bar graph visualization, which revealed that Emma had the fewest logins. The dashboard is now complete.

Learning Note: Splunk dashboards use data from reports to build visualizations.


Alerting on High-Priority Events

I also learned how to set up alerts. First, I ran a search and selected Save As > Alert. In a previous section, Sarah had the highest VPN connection count, so I created an alert specifically for her. The search command was:
index=summary extracted_host=vpn_server Username=Sarah

I configured the alert to run every hour and trigger if Sarah logs in five or more times. The alert settings ensure I am notified when the threshold is met.

Conclusion
I learned how to organize data in Splunk by creating reports and uploading data into them. These reports can run on a schedule and be visualized through dashboards for better readability. Additionally, I configured alerts to notify me when specific conditions are met, keeping me updated in real time.

