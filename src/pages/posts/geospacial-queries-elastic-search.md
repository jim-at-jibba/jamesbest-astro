---
slug: "/geospacial-queries-in-elastic-search"
title: "Geospatial queries in Elasticsearch"
description: "Learn how to use a users location in your elastic search queries to only return the most relevent information"
pubDate: "2020-03-18"
hero: "/images/posts/elastic-search/elastic-search.jpg"
layout: "../../layouts/BlogPostLayout.astro"
tags: ["elasticsearch"]
---

## How we use location data provide region specific search results.

The Candide App is used across multiple countries, each with their own seasons and unique plants. This means that the way we store that data needs to reflect this and be easily searchable on a regionalised basis.

For most of our search needs, we lean on Elasticsearch. Where we felt it was important we have broken the indexes into regionalised domains (plants, problems etc). But in some cases, we felt that splitting the indexes was not the right thing to do. As our user base grows the need to regionalise the results of the indexes that are not split by region become ever greater. Being able to provide search results that are appropriate for you location provides a far better user experience.

## Setting out geo_point field mapping

For us to be able to make geospatial queries against out Elasticsearch index we need to correctly set up the field to be queried when creating our index. This is done by changing the type that is specified when setting the mappings for the index. The type in question is the _geo_point_ type. According to the [Elasticsearch documentation](https://www.elastic.co/guide/en/elasticsearch/reference/7.6/index.html), when setting fields to a `geo_point` types we can:

1. find geo-points within a bounding box, within a certain distance of a central point or a polygon
2. aggregate documents geographically by distance
3. integrate the distance into the relevance score
4. sort documents by distance

Now that we know some of the benefits of using geospatial queries, let look at the request that will set the _geo_point_ within our index' mappings. The snippet below will change the type of the _location_ field to be _geo_point_.

```json
  PUT my_index
  {
    "mappings": {
      "properties": {
        "location": {
          "type": "geo_point"
        }
      }
    }
  }
```

## Adding some data to our index

Now that we have set up our index correctly, we need to add some data. Geo-point fields can accept data in 5 ways. Each of these can be seen below. The one you choose will depend on the needs of your application. Take note of the format of the lat, lon, in some instances, the order is switched.

```json
PUT my_index/_doc/1
{
  "text": "Geo-point as an object",
  "location": {
    "lat": 41.12,
    "lon": -71.34
  }
}

PUT my_index/_doc/2
{
  "text": "Geo-point as a string",
  "location": "41.12,-71.34"
}

PUT my_index/_doc/3
{
  "text": "Geo-point as a geohash",
  "location": "drm3btev3e86"
}

PUT my_index/_doc/4
{
  "text": "Geo-point as an array",
  "location": [ -71.34, 41.12 ]
}

PUT my_index/_doc/5
{
  "text": "Geo-point as a WKT POINT primitive",
  "location" : "POINT (-71.34 41.12)"
}
```

## Querying

Now that we have all this lovely geo data being indexed. How can we query it?

We are going to cover 2 of the options for querying geo-point data, _geo_distance_ and _geo_bounding_box_.

### Filtering by distance

Filtering by distance will only return documents that occur within a specific distance from a geo-point.

```json
GET /my_index/_search
{
    "query": {
        "bool" : {
            "must" : {
                "match_all" : {}
            },
            "filter" : {
                "geo_distance" : {
                    "distance" : "200km",
                    "location" : {
                        "lat" : 40,
                        "lon" : -70
                    }
                }
            }
        }
    }
}
```

As with adding documents to our index, geo-points can be filtered in different representations of a geo-point. These can be seen [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-geo-distance-query.html#_accepted_formats).

### Filtering by a bounding box

Using a bounding box in our query allows us to filter our documents based on a bounding box. This could range from a bounding box containing a city to one containing a whole hemisphere. Either way the query looks like this:

```json
GET my_index/_search
{
    "query": {
        "bool" : {
            "must" : {
                "match_all" : {}
            },
            "filter" : {
                "geo_bounding_box" : {
                    "location" : {
                        "top_left" : {
                            "lat" : 40.73,
                            "lon" : -74.1
                        },
                        "bottom_right" : {
                            "lat" : 40.01,
                            "lon" : -71.12
                        }
                    }
                }
            }
        }
    }
}
```

As with adding documents to our index, geo-points can be filtered in different representations of a geo-point. These can be seen [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-geo-bounding-box-query.html#query-dsl-geo-bounding-box-query-accepted-formats).

The vertices of the bounding box can also be set to _top_right_ and _bottom_left_, as well as _topLeft_, _topRight_, _bottomLeft_ and _bottomRight_. You can also set the _top_, _bottom_, _left_ and _right_ separately.

## In conclusion

Need the ability to query shapes like squares and polygons? Check out [geo-shapes](https://www.elastic.co/guide/en/elasticsearch/reference/current/geo-shape.html) and use this [awesome tool](https://geojson.net) to generate your polygons

# Thanks for reading 🙏

If there is anything I have missed, or if there is a better way to do something then please let me know.

Check out our software focused podcast - [Salted Bytes](https://open.spotify.com/show/7IdlgpiDfYcOdCn57mPLvH?si=X1ArfHvqQXSOAfc1h7Y_Eg)
