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
Logstash 2.4 --- (rubrikfilter_pre5.conf)
Logstash 5.0.2-1 --- (rubrikfilter_5.conf)

Please use the correct Verion identified file for the logstash version as there are differences in the required logstash plugins and logstash syntax.

###Required Filters
Rubrik filter leverages the standard included filters with Logstash. Additionally, the Assured DP Rubrik Syslog filter requires the community maintained logstash-filter-elapsed.

## Contributing
1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## History
2016-NOV-29: Initial creation : aeva_assured

## Credits
aeva_assured

## License
]]></content>
  <tabTrigger>readme</tabTrigger>
</snippet>
