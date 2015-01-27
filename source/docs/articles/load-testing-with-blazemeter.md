#Load Testing with Blazemeter


Your site is loaded with content and is almost ready to go live. You know what it can do, but how will it perform in the wild? Load testing will expose slow page loads, heavy transactions, PHP errors, and database errors. At Pantheon, we make sure every Enterprise site is load tested before going live, and we recently began using [Blazemeter](http://blazemeter.com) to run the tests. This guide will explain why we load test, show you how we do it, and give advice for recognizing and resolving errors you may experience. 

##Performance Hits

While we recommend keeping Drupal’s Watchdog enabled to log important events, if your site is throwing errors, the database for your application will quickly grow and eventually stretch its limits. At the extreme end, this can slow down the application and even cause the site to timeout and crash. Even a single error or warning logged will slow down performance, so be sure to regularly review the dblog and fix any errors. 

##Strategy and Planning 

In order to configure your load test, you’ll need to calculate concurrent users, which are the number of users on the site at the same time. There are a couple of approaches depending on the metrics:   

**Convert visits per hour to concurrent users**

concurrent_users = (hourly_visits * time_on_site) / 3600  

Example: If you have 1,000 visits per hour, and each visitor stays on the average 3 minutes (180 seconds) on your site, that means you would have (1000 * 180) / 3600 = 50 concurrent users.  

**Convert visits per month to concurrent users:**

concurrent_users = (monthly_visits * time_on_site) / (3600 * 24 * 30)

##Current vs. Estimated Metrics

If the site is live elsewhere and you have current traffic metrics, great! If not you can estimate traffic numbers and patterns once the site goes live. Your best bet is to run the load test with more concurrent users than you expect. For sites with historical traffic spikes, test based on those patterns to make sure your site will handle the load.

Aside from concurrent users, you’ll want to map out user behavior and time spent on the site. 


##Running a Test

First, [install the Chrome plugin](https://chrome.google.com/webstore/detail/blazemeter-the-load-testi/mbopgmdnpcbohhpnfglgohlbhfongabi?hl=en) on your Chrome browser. Next, navigate to the site you'd like to test and click the Blazemeter icon to open settings and begin recording. You'll have several configuration options: 

- Record/Follow Me: Select **Record**    
- Name of the test: Name your test configuration in a brief, client-specific way, such as "Marked Private Authenticated" or "Marked Private Anon"    
- Concurrency: The number calculated according to client provided metrics  
- Load Origin: Dependent on project and traffic as outlined by client   
- User Agent: Default  
- Filter Pattern: The default filter pattern will be set to include http://*/* and https://*/* You'll want to designate the top level domain.   
Example: http://live-sitename.gotpantheon.io/) and add an asterisk at the end so it looks like http://live-sitename.gotpantheon.io/* so that all pages on the top level domain are captured.  
- Advanced Options: Select **Record only Top Level Requests** and **Disable Browser Cache**

Here is an example of what these settings would look like if we were to test our own site:  

![The Blazemeter settings window](/docs/assets/images/blazemeter-settings.png)

##Recording a Test

1. Click the red record button in the plugin window.
2. Navigate through the user scenario. When finished, click the Blazemeter icon and click **Stop**. 
3. Select **Edit recording** to review the script. 
4. Next, select **Export to Jmeter**, designated as the file extension .jmx. This will begin an automatic download of the .jmx file which you will need to rename before executing the test. 

**Note:** If you will be testing authenticated users, download JMeter to your local machine, and upload the .jmx file generated with the Blazemeter plugin. 

##Executing a Test

Log in to your [Blazemeter account](https://a.blazemeter.com/user), select **Add JMeter Test**, and upload the .jmx file. Set the following options for load scenario properties and save when finished:  

- Location: Virtual traffic origin, dependent on client provided metrics  
- Ramp Up: How quickly the test will activate users, shown in seconds. The preset (300s) is usually fine.  
- Iterations: This is set to infinity by default and will allow the user behavior to loop and finish out the test.  
- Duration: Somewhere between 15-30 minutes.  

Once you've saved your load test scenario, click on the tests icon to select the test you want to run, and click Start Test (play icon).   

##Review and Share the Results

Results are graphed, along with any error messages, response times, and so forth. All tests are shared in "Sessions". To share public links with the client in the load test report, click the share button, turn sharing on and then copy the link. 


Now that you’ve run your load test, you can review the results on BlazeMeter and see a summary of users, throughput, errors, response times, and bandwidth. You can also access an aggregate report of load times on each page and a list of errors generated. 

The report is a nice high-level overview of site performance, but you’ll want more details for the full picture. New Relic (which you can enable through the Pantheon Site Dashboard) will provide more information on slow transactions and appserver response times for both web and non-web transactions. 

Depending on the application you’re running, you can also access error and slow logs. Drupal can log these to the database with [DBlog](https://api.drupal.org/api/drupal/modules!dblog!dblog.module/7) (though be sure to prune these regularly as they can bloat the database and slow your site down). Wordpress has plugins like Debug Bar, SQL Monitor, P3, and Debug Queries.


##Resolve Errors and Performance Hits

The errors and performance hits you discover will each will have a different solution. We recommend doing a search of the error message and reading solutions posted by others, or post your own issue and see if anyone else has an answer. Additionally, if a specific module or plugin is slow, check the issue queue to see if the problem is known and if a patch is available.

Outside of error messages, the most common performance hit comes from poorly configured (or non-existent) caching. While you may already know about anonymous page caching, you can also greatly boost performance with backend caching (Redis) and by caching individual components on the site, such as views, panels, and blocks. 

##Example Stats of Performance Benefits


