# Alerts

Alerts are notifications sent by the system when the components that run in the production environment are not functioning as expected. Whenever a critical error (e.g., Out Of Memory error) occurs, the component logs an error and notifies the members of your organization with admin rights via an email. This email contains a link to the [**Observability**](../observability/observability-overview.md) tab of the component where the metrics and logs applicable to the time interval in which the error occurred are highlighted. The system collects and sends alerts to admin users every five minutes. 


## Types of alert email notifications

When an alert occurs for the first time during the alerting interval, the system sends an alert email immediately. When there are multiple occurrences of the same type of alert for a particular component, the system suppresses the alerts for 15 minutes and generates a single email that specifies the event count to denote how many such errors occurred during an alerting interval.

## Types of alerts

### Out of Memory alert

If the Kubernetes pod that runs your component goes out of memory, it restarts immediately. However, during that interval, the service becomes unavailable and the requests that it was processing at the time can become erroneous.
Due to this, the out-of-memory error can be very adverse for your component. Therefore, when an out-of-memory error occurs, the admin members of the organization that owns the component receive an alert email similar to the sample given below.


![Out of Memory alert email](../assets/img/alerting/oom-email.png){.cInlineImage-full}

This email contains details about your component and the number of times this event occurred within the alert monitoring period.
You can check the logs and the memory usage during that time interval by clicking **Check in Portal**. This takes you to the Observability view of that particular component. You can also contact WSO2 for support via the **Contact us** link provided at the bottom of the alert email.

#### How to troubleshoot Out of Memory error in the Observability view

When you click the Check in Portal button you will be redirected to the Observe page of the component in the Choreo console.

![OOM Troubleshooting](../assets/img/alerting/oom-troubleshooting.png){.cInlineImage-full}

The item marked  **1** in the above image shows the time bin where the Out of Memory error that occurred is highlighted and the other logs that occurred during that time are displayed within the scrollable Logs column. It also contains the count of such logs.

![Log bins](../assets/img/alerting/log-bins.png){.cInlineImage-half}

Item **2** is the one-hour time range around the point of time at which the error occurred (i.e. error time +/- 30mins). In the **Diagnostic View** tab, this  time range is further divided into 5 similar sized time bins. In this scenario, the size of each bin is 12 minutes. These 12-minute bins are shown by **3**.

![Diagnostic view](../assets/img/alerting/diagnostic-view-values.png){.cInlineImage-half}

When you hover over the graph, you can view the memory usage. You can note that it has increased steadily during the time interval and reached the maximum value. This causes the application to log the out-of-memory error and restart.

Select custom time range

If you want to change the automatically selected time interval (i.e., one hour) for debugging purposes, do as follows:

1. Click the drop-down bar for time selection (marked in the image below).

    ![Custom Time range](../assets/img/alerting/custom-time-range.png){.cInlineImage-half}

2. Specify the time range for which you want to view logs in the **Diagnostics View** tab by entering the required times in the **From** and **To** fields.

3. Click **Apply**.

![Custom Time range](../assets/img/alerting/custom-time-range.png){.cInlineImage-half}

Then you can select the **Custom** option, this will automatically add the time range that is already given by the alert email. You can modify them to see the **Diagnostic View** for that  specific time range.

For more information on how to use the Observability view for root cause analysis, see [Root Cause Analysis](../observability/root-cause-analysis.md).

### Application Error alert

This alert is triggered when you use the **“log:printError()”** function in your component and the component logs an error via that. Such errors indicate that your component is unable to function as designed, and therefore you are notified via an email so that you can troubleshoot them. The following is a sample of such a notification email. 

![Application Error email](../assets/img/alerting/application-error-email.png){.cInlineImage-full}

This email provides details about the component. You can click **Check in Portal** to open the Observability view in the Choreo Console for this component. You can also get support from WSO2 via the **Contact us** link provided in the email.

![Application Error email](../assets/img/alerting/application-error-email.png){.cInlineImage-full}

#### How to troubleshoot Application error in the Observability view

Once you click on the **Check in Portal** link you will be redirected to the observe page of the component in the Choreo console

![Application Error Troubleshooting](../assets/img/alerting/application-error-troubleshooting.png){.cInlineImage-full}

This will open the **Throughput and Latency** view and automatically select the request that caused this error log. This is shown in **1**, it will show you the throughput and latency of the particular request. The color of the graph will tell you whether that request is successful or an error. You can also see the status of the request; its latency and status code indicated in a green colored circle in **4**. You will also see the error log that triggered the alert email in **2**. The time range used to highlight the relevant error log is indicated in **3**.  But you can scroll up and down and get more logs within the time range specified in **5**. You can also diagnose further by changing the selected time ranges. See the (**Selecting custom time ranges**) section above.