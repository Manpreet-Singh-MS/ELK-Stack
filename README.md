#ELK Stack

sudo apt-get update
sudo apt install openjdk-8-jdk
sudo apt-get install nginx

wget-q0 - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list

sudo apt-get update 
sudo apt install elasticsearch 
sudo apt install kibana 
sudo apt install logstash 
sudo apt install filebeat

    beat
        filebeat
	metricbeat
	heartbeat
	winlogbeat
	networkbeat
	auditbeat

Configuration ELK Stack

nano /etc/elasticsearch/elasticsearch.yml > 

Uncomment the below fields 

cluster.name : my-application
node.name : node-1
path.date : /var/lib/elasticsearch
path.logs : /var/log/elasticsearch
network.host : localhost
http.port : 9200

after modifying the above yaml file

sudo systemctl start elasticsearch
sudo systemctl status elasticsearch

curl localhost:9200


sudo nano /etc/kibana/kibana.yml >
server.port : 5601
server.host : "localhost"

sudo systemctl status kibana
sudo systemctl start kibana


Accessing Kibana with Nginx

sudo apt install apache2-utils -y
sudo htpasswd -c /etc/nginx/htpasswd.users kibana > enter the password
sudo nano/etc/nginx/htpasswd.users
sudo mv /etc/nginx/sites-available/default /etc/nginx/sites-available/new-default
sudo nano /etc/nginx/sites-available/default

server {
listen 80;
server name <AWS EC2 ip address>;
auth basic "Restricted Access";
auth_basic_user_file /etc/nginx/htpasswd.users;
I
location / {
proxy_pass http://localhost: 5601;
proxy_http version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection 'upgrade';
proxy_set_header Host $host;
proxy_cache_bypass $http_upgrade;
}

sudo system restart nginx
sudo systemctl status nginx

File beat commands

sudo filebeat modules list > list all modules for data collection
sudo filebeat modules enable system
sudo filebeat modules list -> System is now show in enabled Category
sudo nano /etc/filebeat/modules.d/system.yml -> edit the system.yml

syslog:
var.paths : ["/var/log/syslog*"] -> collects all system logs

authorization logs:
var.paths : ["/var/log/auth.log*"]

sudo systemctl stop filebeat
sudo systemctl start filebeat

Select StackManagement ->  Index Management -> Index Patterns -> Create index Pattern -> define index pattern -> configure setting @timestamp

Visualization -> Create visualization -> select any random visualization from the list -> choose a source.

Download custom dashboard

sudo filebeat setup -e -> command to download new dashboard related to filebeat


