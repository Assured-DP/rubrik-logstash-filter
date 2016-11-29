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
Tested Logstash Versions:

Logstash 2.4 --- *rubrikfilter_pre5.conf*
```
uses pre version 5.0 ruby formatting of event['<eventname>']
```

Logstash 5.0.2-1 --- *rubrikfilter_5.conf*
```
updated for event.get / event.set v5+ requirements
```

Please use the correct version identified file for the logstash version as there are differences in the required logstash plugins and logstash syntax. This filter is not designed to be used alongside a larger filter set in the same instance of logstash. The intent is that it is deployed in its own instance. A future design plan is to create a version that will run in conjunction with other designed filters

###Required Filters
Rubrik filter leverages the standard included filters with Logstash. Additionally, the Assured DP Rubrik Syslog filter requires the community maintained [logstash-filter-elapsed](https://github.com/logstash-plugins/logstash-filter-elapsed).

###Known Issues
Issue 001: Fileset Completed backups do not calculate elapsed time due to syslog variations

###Output Fields
Field | Type | Description
---: |:---:| ---
ls_vs | number | syslog version
ls_ts | timestamp | logstash ingest timestamp


## History
2016-NOV-29: Initial creation : aeva_assured

## Credits
[aeva_assured](https://github.com/aeva-assured)

## License
