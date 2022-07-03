# To download docker image
docker-compose up -d


# To make a ensure everithing is done correctly

curl -XGET https://localhost:9200 -u 'admin:admin' --insecure

curl -XGET https://localhost:9200/_cat/nodes?v -u 'admin:admin' --insecure

curl -XGET https://localhost:9200/_cat/plugins?v -u 'admin:admin' --insecure

# To open OpenSearch Dashboards

http://localhost:5601

# Add data

# Answer questions below

## Data analytics task (Ecommerce data)

- Find top-10 most common first name of the customers from Birmingham

![](./screenshoots/top10Birmingham_Kibana.png)
![](./screenshoots/top10Birmingham_query.png)

``` console
GET opensearch_dashboards_sample_data_ecommerce/_search
{
  "query": {
    "bool": {
      "filter": [
        {"term": {
          "geoip.city_name": "Birmingham"
        }}
      ]
    }
  }, 
  "aggs": {
    "user_agg": {
      "terms": {
        "field": "customer_first_name.keyword",
        "size": 10
        }
      }
    }
}
```


- What is the busiest day for women buying products cheaper than 75$
- How many products were bought in the last 3 days from Great Britain?
- Standard deviation visualisation of the price with ability to filter by country


## Data analytics task (Flights data)

- Total distance in miles travelled by all flights
- Median price of the flight from Japan, US and Italy
- Top-10 most delayed destination airports
- Geo map visualisation based on the number of flights from and to the airport

## Data analytics task (Logs data)

- Top 5 tags in logs in which contains request to deliver css files
- What is sum of all RAM for Windows machines that have requests from 6am to 12pm
- Find total number of logs with IP in range from 176.0.0.0 to 179.255.255.254