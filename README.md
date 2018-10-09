http://cloud.spring.io/spring-cloud-dataflow/

# Installation
## Launch local server
java -jar spring-cloud-dataflow-server-local-1.2.3.RELEASE.jar

## Install kafka
brew install kafka
### Launch kafka
zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties & kafka-server-start /usr/local/etc/kafka/server.properties

## Install Redis
Download https://redis.io/download

## Compile
````
cd redis-XX/
make
````
## Launch
```
./src/redis-server
```

# Launch Dashboard
## Dashboard link
http://localhost:9393/dashboard

## Import applications (source/sink/processor)
Apps -> Bulk import 
http://bit.ly/Bacon-RELEASE-stream-applications-kafka-10-maven


# Example project (Twitter analytics)
https://github.com/spring-cloud/spring-cloud-dataflow-samples/tree/master/analytics/twitter-analytics

## Make twitter API keys and Token 
https://apps.twitter.com

```
(1) dataflow:>stream create tweets --definition "twitterstream --consumerKey=<CONSUMER_KEY> --consumerSecret=<CONSUMER_SECRET> --accessToken=<ACCESS_TOKEN> --accessTokenSecret=<ACCESS_TOKEN_SECRET> | log"
Created new stream 'tweets'

(2) dataflow:>stream create tweetlang  --definition ":tweets.twitterstream > field-value-counter --fieldName=lang --name=language" --deploy
Created and deployed new stream 'tweetlang'

(3) dataflow:>stream create tagcount --definition ":tweets.twitterstream > field-value-counter --fieldName=entities.hashtags.text --name=hashtags" --deploy
Created and deployed new stream 'tagcount'

(4) dataflow:>stream deploy tweets
Deployed stream 'tweets'
```

## Visualization
* For real-time updates on language tags, select:
Metric Type as __Field-Value-Counters__
Stream as __language__
Visualization as __Bubble-Chart__ or __Pie-Chart__

* For real-time updates on hashtags tags, select:
Metric Type as __Field-Value-Counters__
Stream as __hashtags__
Visualization as __Bubble-Chart__ or __Pie-Char__
