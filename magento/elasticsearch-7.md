## Installation
> Install elasticsearch `v7.x`
```bash
# Linux
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-linux-x86_64.tar.gz
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-linux-x86_64.tar.gz.sha512
shasum -a 512 -c elasticsearch-7.8.1-linux-x86_64.tar.gz.sha512 
tar -xzf elasticsearch-7.8.1-linux-x86_64.tar.gz
cd elasticsearch-7.8.1/ 

# Mac
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-darwin-x86_64.tar.gz
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-darwin-x86_64.tar.gz.sha512
shasum -a 512 -c elasticsearch-7.8.1-darwin-x86_64.tar.gz.sha512 
tar -xzf elasticsearch-7.8.1-darwin-x86_64.tar.gz
cd elasticsearch-7.8.1/ 
```

> Running as deamon
```bash
$ ./bin/elasticsearch -d -p pid
$ pkill -F pid
```