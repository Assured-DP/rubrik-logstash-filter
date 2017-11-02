# rubrik-logstash-filter
Rubrik-logstash-filter provides a quick and easy filter to convert the output of a Rubrik Syslog into the base components to be searched upon by ElasticSearch. 
## Installation
Installation of the rubrik-logstash-filter is completed by placing the rubrikfilter.conf file into your logstash config folder. Typically this folder is located at: 
>/etc/logstash/conf.d/

Alternatively, filter can be applied by executing logstash from the working directory and referencing the configuration file.

>bin/logstash -f rubrikfilter.conf

## Usage
Edit the rubrikfilter.conf file to update the input IP address of your logstash instance. 
Edit the rubrikfilter.conf file to output to the hostname of your ElasticSearch Cluster
Place the rubrikfilter.conf file with changes into the logstash config folder

###Compatibility
####Tested Logstash Versions:

Logstash 2.4 --- *rubrikfilter_pre5.conf*
```
uses pre version 5.0 ruby formatting of event['<eventname>']
```

Logstash 5.0.2-1 --- *rubrikfilter_5.conf*
```
updated for event.get / event.set v5+ requirements
```

Please use the correct version identified file for the logstash version as there are differences in the required logstash plugins and logstash syntax. This filter is not designed to be used alongside a larger filter set in the same instance of logstash. The intent is that it is deployed in its own instance. A future design plan is to create a version that will run in conjunction with other designed filters

####Rubrik Versions
Tested Versions 3.2.3-534, 3.0.0-DA3-53, Version 3.0.0-DA5-89

###Required Filters
Rubrik filter leverages the standard included filters with Logstash. Additionally, the Assured DP Rubrik Syslog filter requires the community maintained [logstash-filter-elapsed](https://github.com/logstash-plugins/logstash-filter-elapsed).

###Known Issues
Issue 001: Fileset Completed backups do not calculate elapsed time due to syslog variations
Issue 002: Elapsed plugin only allows for a limited amount of time between events. Long running events will fail to show duration and any event where the initiating event is lost or was not captured will cause the calculation to fail.

###Output Fields
|Field | Type | Description|
|---: |:---:| ---|
|ls_vs | number | syslog version|
|ls_ts | timestamp | logstash ingest timestamp|
|host | IP Address | Source IP transmitting to Logstash|
|port | number | source port|
|syslog5424_pri | number | syslog5424 type tagging|
|syslog5424_ver | number | syslog5424 version number|
|syslog5424_ts | timestamp | syslog5424 event timestamp synced to the logstash timestamp|
|syslog5424_host | hostname | hostname of transmitting rubrik|
|syslog5424_app | string | syslog application name - Always Rubrik in this case|
|syslog_severity_code | number | syslog severity code number|
|syslog_facility_code | number | syslog facility code|
|syslog_facility | string | syslog notification level|
|syslog_severity | string | syslog severity level|
|mdc | string | mdc number reported|
|eventtype | string | task type |
|uuid | UUID | Backup Target UUID|
|rubriknodeid | string | rubrik node ID number|
|eventId | UUID | individual event UUID - part of a task|
|eventSeriesId | UUID | task UUID - combination of tasks|
|objectId | UUID | UUID of backup target|
|status | string | current status of event|
|description | string | plain text of event objective|
|dbname | string | name of DB being backed up when relevant|
|bkptarget | string | name of target backup VM or server|
|snapshotname | string | name of snapshot created for event |
|snapshotduration | number | time to take snapshot in seconds|
|vmtools_vs | string | version of vmtools for incompatible vmtools discovered|
|vCenterIP | IP Address | IP Address of vCenter when relevant |
|vCentername | hostname | hostname of vCenter when relevant|
|ingestdata | bytes | amount of data ingested in bytes when reported|
|tags | array | list of all tags discovered while reviewing|
|elapsed_time | number | total event duration in seconds from Queued to Completed |
|taskduration | number | event duration from creating to completed in seconds|
|queueduration | number | time spent in queue before a task begins|
|syslog5424_sd | string | syslog parse with combined troubleshooting data|
|syslog5424_msg | string | full syslog message summary|
|message | string | copy of complete syslog message text|
|rbkuser | string | local user performing action in an audit event|
|auditevent | string | action being performed during an audit event |

## History
2017-SEP-26: Corrected for Audit Trails and validated against 3.2.3 : aeva_assured
2016-NOV-29: Initial creation : aeva_assured

## Credits
[aeva_assured](https://github.com/aeva-assured)

## License
