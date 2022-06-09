# ELK with Filebeat for WSO2 products

## The way it works
- logs -> filebeat -> logstash -> elasticsearch <- kibana

## Usage

### Set up the ELK with Filebeat
1. Install Docker & Docker-compose install 
2. Clone this repository.
3. Enter the logs files path in the docker-compose.yaml in order to mount
   
   `e.g., <WOS2 product home>/repository/logs`
   
   ```
   filebeat:
    user: root
    container_name: filebeat
    image: docker.elastic.co/beats/filebeat:7.5.0
    links:
      - logstash:logstash
    depends_on:
      - logstash
    volumes:
      - /var/run/docker.sock:/host_docker/docker.sock
      - /var/lib/docker:/host_docker/var/lib/docker
      - <path to log files>:/usr/share/filebeat/logs
      - ./filebeat.yml:/usr/share/filebeat/filebeat.yml
   ```
4. Docker-compose up command
    ```
    docker-compose up -d
    ```
   
### Useful links
- https://grokdebug.herokuapp.com/
- https://logz.io/blog/logstash-grok/

