# RTView Splunk Integration

Learn how to integrate RTView Data from different data sources (EMSMon, BWMon, HostMon) in Splunk with the following examples. 

## System Requirements

* RTView 
* Splunk Enterprise
* Splunk REST Add-on 
* Java

## Useful Links

* Download Splunk: http://www.splunk.com
* Download Splunk REST Add-on: https://splunkbase.splunk.com/app/1546/release/1.4/agree/
* Download RTView: http://sl.com/evaluation-request/
* Download Java: http://www.oracle.com/technetwork/java/javase/downloads/index.html


## Setup

### Install REST add-on for Splunk

In order to query the RTView dataserver from splunk, download the REST add-on for Splunk. 

Install the add-on by selecting "Manage Apps" from the "App" menu in the upper left corner of your browser window. In the Apps window, click the "Install app from file" button, use the "Browse..." button to set the path to the downloaded file, and click "Upload".


### Update Python Script

After the REST interface is installed, you'll need to update a python script to handle the specific json format returned by queries to the RTView dataserver. Edit "<SplunkHome>/etc/apps/rest_ta/bin/responsehandlers.py" and include the slEventHandler. A copy of this script is included in the 'samples' directory of this repository.   

We'll use this class when configuring connections to REST-ful endpoints in the examples. 

### Ingest RTView Metrics to Splunk

Given a working dataserver and Splunk with the REST add-on, we can now configure a connection to pull data into Splunk. Click the "Settings" menu item in the splunk browser interface and select "Data inputs", then click on the "add new" action for the REST type. Configure the connection fields with the following values:

Endpoint URL: http://<dataserver url:port>/hostbase_rtvquery/cache/HostStats/current
HTTP Method: GET
URL Arguments: fmt=json
Response Type: json
Response Handler: slRtvEventHandler
Request Timeout: 10
Backoff Time: 60
Polling Interval: 30
Set sourcetype: Manual
Source type: rtv_emsinfo

Save these settings, and then go to the "App: Search & Reporting" screen and click the "Data Summary" button. On the "Data Summary" pop-up, the "Sourcetypes(*)" tab should now show that data for a new source type "rtv_emsinfo" is available.

## RTView Splunk Examples

For each example listed here, the corresponding data, queries and reports are included in this repository for you to play with. 

### Search Queries

A few search queries are included for you to try in the Splunk Search & Reporting app. Here we have included examples to query RTView host monitor and RTView EMS monitor. You can connect to other RTView data servers to run similar queries. 

Search Query Files: 

search_query_emsmon
search_query_hostbase_trendchart
search_query_hostbase
search_query_emsmon_trendchart

### Reports

A couple of PDF reports exported from Splunk is included in the 'reports' directory for your reference.

Reports: 

ems_server_info_-_report-2016-03-31
timechart_consumer_count-2016-03-31

### Data

Sample data files are included for your reference. This is to show how the data will look like when you retrieve metrics from RTView data server using the REST add-on from Splunk. 

Data Files: 
data_bw_engine_info
data_ems_server_info

## For More Details on this Sample

RTView Blog: http://sl.com/wp-content/uploads/2016/01/tech-note-rtview-In-splunk-dashboards.pdf
 
