---
attachments: [Clipboard_2024-11-21-15-27-05.png, Clipboard_2024-11-21-15-27-16.png]
tags: [RFE Sections]
title: OpenSearch
created: '2024-11-19T15:33:17.787Z'
modified: '2024-11-22T09:49:11.853Z'
---

# OpenSearch

### Servers
- https://rdev1os2rfesrch2.aws-rfe-dev.copyright.com:9200
- https://rdev1os2rfesrchm2.aws-rfe-dev.copyright.com:9200
- https://rdev1os2rfesrch1.aws-rfe-dev.copyright.com:9200
- https://rdev1os2rfesrchm3.aws-rfe-dev.copyright.com:9200
- https://rdev1os2rfesrch3.aws-rfe-dev.copyright.com:9200

### EndPoints
- Mapping: /content23/_mapping
- Get information about one or more fields:
  https://rdev1os2rfesrch1.aws-rfe-dev.copyright.com:9200/content23/_mapping/field/pubDate
  GET content23/_mapping/field/pubDate

### TIPS
- **PubDate => None:** In database saved the value **0**, in Opensearch saved the value **1799-01-01T00:00:00**
- **Count results:** If you want to show the number of the results, you only need to add **"track_total_hits": true,** to the request.

#### Queries
<details>
  <summary>Get item by libraryDocumentId</summary>
  
```
{
  "query": {
    "bool": {
      "must": [
        {
          "range": {
            "libraryDocumentId": {
              "gte": 101705193,
              "lte": 101705193
            }
          }
        }
      ],
      "must_not": [],
      "should": []
    }
  },
  "from": 0,
  "size": 50,
  "sort": [],
  "aggs": {},
  "version": true
}
```
</details>

<details>
  <summary>Get all results order by pubDate ascending</summary>

  ```
  {
    "sort": [
      {
        "pubDate": {
          "order": "asc"
        }
      }
    ]
  }
  ```
</details>
<details>
  <summary>Get maximum and minimum value for one field</summary>

  ```
  {
    "size": 0, 
    "query": {
      "match_all": {}
    },
    "aggs": {
      "min": {
        "min": {
          "field": "pubDate"
        }
      },
      "max":{
        "max": {
          "field": "pubDate"
        }
      }
    }
  }
  ```
</details>
<details>
  <summary>Get item by libraryDocumentId on DB (**You should be check the relation on mapping between bbdd and OS**)</summary>

```
{
  "query": {
    "term": {
      "libraryDocumentId": {
        "value": "101705193"
      }
    }
  },
  "sort": [
    {
      "pubDate": {
        "order": "asc"
      }
    }
  ]
}
```
</details>
