elasticsearch-kibana-ansible-vagrant
====================================

notes

http://www.elasticsearch.org/blog/data-visualization-elasticsearch-aggregations/

http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/indices-delete-index.html

curl -XPOST "192.168.111.10:9200/nfl?pretty"

curl -XPUT "192.168.111.10:9200/nfl/2013/_mapping?pretty" -d @nfl_mapping.json

curl -XPOST "192.168.111.10:9200/nfl/2013/_bulk?pretty" --data-binary @nfl_2013.json

# random tweets

curl -XPUT 192.168.111.10:9200/_river/my_twitter_river/_meta -d '
{
    "type" : "twitter",
    "twitter" : {
        "oauth" : {
            "consumer_key" : "OitTLtBVkfKnkQokJkpwKQ",
            "consumer_secret" : "fJOjkDDD2lmTzBECqYZy522QcL7ysQefKj3R73Fgw",
            "access_token" : "2886-boqVzLIyLuV4WuWXJ0ssLUIhhxpYpOq1hibSvdnPywVvd",
            "access_token_secret" : "Kws81fYLYNlAn2cRZ5Ga3xkdesvXsKyahe1mkOAlW84kg"
        }
    },
    "index" : {
        "index" : "my_twitter_river",
        "type" : "status",
        "bulk_size" : 100,
        "flush_interval" : "5s"
    }
}
'

# remove twitter_river

curl -XDELETE http://localhost:9200/_river/my_twitter_river/

# keyword search

curl -XPUT 192.168.111.10:9200/_river/my_twitter_river/_meta -d '
{
    "type" : "twitter",
    "twitter" : {
        "oauth" : {
            "consumer_key" : "OitTLtBVkfKnkQokJkpwKQ",
            "consumer_secret" : "fJOjkDDD2lmTzBECqYZy522QcL7ysQefKj3R73Fgw",
            "access_token" : "2886-boqVzLIyLuV4WuWXJ0ssLUIhhxpYpOq1hibSvdnPywVvd",
            "access_token_secret" : "Kws81fYLYNlAn2cRZ5Ga3xkdesvXsKyahe1mkOAlW84kg"
        }
    },
    "index" : {
        "index" : "my_twitter_river",
        "type" : "status",
        "filter" : {
            "tracks" : "warbyparker"
        },
        "bulk_size" : 100,
        "flush_interval" : "5s"
    }
}
'

#  remove all indexes

curl -XDELETE http://localhost:9200/_all/

# track keywords

curl -XPUT 192.168.111.10:9200/_river/my_twitter_river/_meta -d '
{
    "type" : "twitter",
    "twitter" : {
        "oauth" : {
            "consumer_key" : "OitTLtBVkfKnkQokJkpwKQ",
            "consumer_secret" : "fJOjkDDD2lmTzBECqYZy522QcL7ysQefKj3R73Fgw",
            "access_token" : "2886-boqVzLIyLuV4WuWXJ0ssLUIhhxpYpOq1hibSvdnPywVvd",
            "access_token_secret" : "Kws81fYLYNlAn2cRZ5Ga3xkdesvXsKyahe1mkOAlW84kg"
        },
        "filter" : {
            "tracks" : ["RuinAChildrensBook", "RAWBrooklyn", "warbyparker", "warby"]
        }
    }
}
'
