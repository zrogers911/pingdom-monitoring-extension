# AppDynamics Pingdom Monitoring Extension

##Use Case
Pingdom ([https://www.pingdom.com/](https://www.pingdom.com/)) is a service that tracks website uptime, 
downtime, and performance. The Pingdom extension uses the REST API from Pingdom to retrieve key
metrics for your Pingdom Checks. It also retrieves other important data 
such as remaining Checks and remaining SMS credits.


##Installation

The monitor.xml file is used to execute the Java code that will start the monitoring extension. It contains
tags for your Pingdom credentials, as well as a tag where you can specify your own metric
path. If you specify the metric path, only a single tier will receive metrics from this
monitor.  

1.  Create a new directory in the \<machine agent home\>/monitors directory.
2.  Copy the contents in the 'dist' folder to the folder you created in
    step 1.
3.  In the monitor.xml file:
    1.  set the credentials to your Pingdom account
    2.  configure your own metric path (optional)

4.  Restart the Machine Agent.
5.  Look for the metrics in the Metric Browser at: "Custom Metrics|Pingdom Monitor" or your specified path.

##Files

Files/Folders Included:

|**Directory/File** | **Description**|
| ------------- |:-------------|
|bin |Contains class files|
|conf|Contains the monitor.xml|
|lib|Contains third-party project references|
|src|Contains source code to the Pingdom Monitor|
|dist|Contains the distribution package (monitor.xml, the lib directory, and pingdomMonitor.jar) |
|build.xml|Ant build script to package the project (required only if changing Java code)|


##XML Example
<table>
<th align = 'left'> Parameter </th>
<th align = 'left'> Description </th>
<tr>
<td>Username
</td>
<td>Pingdom username
</td>
</tr>
<tr>
<td>Password
</td>
<td>Pingdom password
</td>
</tr>
<tr>
<td>App-Key
</td>
<td>The Pingdom App-Key, found at [https://my.pingdom.com/account/appkeys](https://my.pingdom.com/account/appkeys)
</td>
</tr>
<tr>
<td>Metric-Path
</td>
<td>Optional: set your own metric path. The pattern is: Server | Component:(id or name) | Pingdom Monitor 
</td>
</tr>
</table>

~~~~

<monitor>
        <name>PingdomMonitor</name>
        <type>managed</type>
        <description>Reports key metrics from Pingdom using REST</description>
        <monitor-configuration></monitor-configuration>
        <monitor-run-task>
                <execution-style>continuous</execution-style>
                <name>Pingdom Monitor Run Task</name>
                <display-name>Pingdom Monitor Task</display-name>
                <description>Pingdom Monitor Task</description>
                <type>java</type>
                <java-task>
                        <classpath>pingdomMonitor.jar;lib/json-simple-1.1.1.jar;/lib/httpclient/commons-codec-1.6.jar;lib/httpclient/commons-logging-1.1.1.jar;lib/httpclient/fluent-hc-4.2.5.jar;lib/httpclient/httpclient-4.2.5.jar;lib/httpclient/httpclient-cache-4.2.5.jar; lib/httpclient/httpcore-4.2.4.jar;lib/httpclient/httpmime-4.2.5.jar</classpath>
                        <impl-class>com.appdynamics.monitors.pingdom.PingdomMonitor</impl-class>
                </java-task>
 
                <task-arguments>
                  <!-- CONFIGURE USER CREDENTIALS:
                       App-Key: you generate your application key inside the Pingdom control panel
                       (default value of App-Key is a non-working dummy, to show what the format looks like)
                  -->
                        <argument name="Username" is-required="true" default-value="Username"/>
                        <argument name="Password" is-required="true" default-value="Password"/>
                        <argument name="App-Key" is-required="true" default-value="zoent8w9cbt810rsdkweir23vcxb87zrt5541"/>
 
                        <!-- CONFIGURE METRIC PATH (OPTIONAL):
                       You can configure a metric path, such that only one tier is going to receive
                       metrics from this monitor. The pattern is: Server|Component:<id or name>|Pingdom Monitor
                       Default (if default-value="") is "Custom Metrics|Pingdom Monitor" under 
                       Application Infrastructure Performance in every tier
                  -->
                        <argument name="Metric-Path" is-required="false" default-value=""/>
                </task-arguments>
        </monitor-run-task>
</monitor>

~~~~

##Custom Dashboard example
The custom dashboard below contains a custom heading graphic, three monitors, and an iframe containing an 
external web site (on the right).


![](images/pingdom_01.png)


##Contributing

Always feel free to fork and contribute any changes directly via GitHub.


##Support

For any support questions, please contact ace@appdynamics.com.
