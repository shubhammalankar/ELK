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
   d. To start the elastic enter the command in CMD.
   ```
   elasticsearch.bat
   ```  
   e. Elastic search will run on default port 9200
   f. Enter the URL in your browser - `localhost:9200`
4. Start Kibana:  
   a. Open CMD in the bin loaction of kibana folder  
   b. Uncomment `elasticsearch.hosts: ["http://localhost:9200"]` in the path `F:\kibana-8.17.0-windows-x86_64\kibana-8.17.0\config\kibana.yml`  
   c. Change the path to - `cd .\kibana-8.17.0\bin\`  
   d. To start kibana enter the command in the CMD  
   ```
   kibana.bat
   ```  
   e. Kibana will run on default port 5601  
   f. Enter the URL in your browser - `localhost:5601'  
6. Start Log stash:  
   a. create a file by name - `logstash.conf` in `.\logstash\bin` and enter below code in it  
   ```
   input {
       file {
           path => "F:/ELKDemoProject/elk-stack.log"
           start_position => "beginning"
           sincedb_path => "NUL" # Ensures the file is reprocessed every time Logstash starts
       }
   }
   
   output {
       stdout {
           codec => rubydebug
       }
       # sending properly parsed log events to elasticsearch
       elasticsearch {
           hosts => ["localhost:9200"]
           index => "logstash-demo"
       }
   }
   ```
   b. Change the path to - `.\logstash-8.17.0\bin` and run the command 
   ```
   logstash -f bin\logstash.conf
   ```  
   c. Then it will read the complete log and send all the data to elastic search.  
   d. To verify the indices -  
      -Open the URL `localhost:9200/_cat/indices`  
      -You can open the index file in "http://localhost:9200/logstash-demo/_search"  
      -Here we can only view `logstash-demo` index named files in kibana console   
6. Creating a dashboard in Kibana
  

 
