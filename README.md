# ELK
ELK first project
Steps to install the ELK Stack:

1. Download ELK stack softwares from there website. Unzip it all of them.
2. Start Elastic search:  
   a. Open CMD in the bin location of Elastic folder
   b. Change `xpack.security.enabled: true` to `xpack.security.enabled: false` in `\elasticsearch-8.17.0\config\elasticsearch.yml`     
   c. Change the path to
   `
   cd .\elasticsearch-8.17.0\bin\
   `  
   To start the elastic enter the command in CMD.
   ```
   elasticsearch.bat
   ```  
   d. Elastic search will run on default port 9200
   e. Enter the URL in your browser - `localhost:9200`
4. Start Kibana:  
   a. Open CMD in the bin loaction of kibana folder
   b. Uncomment `elasticsearch.hosts: ["http://localhost:9200"]` in the path `F:\kibana-8.17.0-windows-x86_64\kibana-8.17.0\config\kibana.yml`  
   c. Change the path to - `cd .\kibana-8.17.0\bin\`
   To start kibana enter the command in the CMD  
   '''
   kibana.bat
   '''  
   d. Kibana will run on default port 5601
   e. Enter the URL in your browser - `localhost:5601'
6. Start Log stash:
   a. create a file by name - logstash.conf in logstash/bin path and enter below codoe in it
```
input {
    file {
        path => "F:/ELKDemoProject/elk-stack.log"
        start_position => "beginning"
    }
}

output {
    stdout {
        codec => rubydebug
    }
    # sending properly parsed log events to elasticsearch
    elasticsearch {
        hosts => ["localhost:9200"]
    }
}
```
  b. Open CMD to logstash bin location - "F:\logstash-8.17.0-windows-x86_64\logstash-8.17.0\bin" and run the command "logstash -f bin\logstash.conf"
  c. Then it will read the complete log and send all the data to elastic search

5. To verify the indices -
  Open the URL localhost:9200/_cat/indices > here we can only view ".ds-logs-generic-default-2024.12.22-000001" index named files in kibana console
  You can open the index file in "http://localhost:9200/.ds-logs-generic-default-2024.12.22-000001/_search"
6. Creating a dashboard in Kibana
  

 
