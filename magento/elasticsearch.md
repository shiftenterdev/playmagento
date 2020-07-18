## Installation
> For proper installation please follow the following steps for Elasticsearch installation.
```bash
$ sudo apt-get install default-jre
$ java -version
$ wget -qO – https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add –
$ sudo apt-get install apt-transport-https
$ echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list
$ sudo apt-get update
$ sudo apt-get install elasticsearch
$ sudo /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-icu
$ sudo /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-phonetic
$ sudo -i service elasticsearch start
$ sudo vi /etc/elasticsearch/jvm.options
# Deleting 2 lines Xms4g and Xmx4g
$ sudo vi /etc/elasticsearch/elasticsearch.yml
# Adding the code "indices.query.bool.max_clause_count: 10024" on the bottom of the page.
$ curl -XGET 'http://localhost:9200/_cat/health?v&pretty'
```