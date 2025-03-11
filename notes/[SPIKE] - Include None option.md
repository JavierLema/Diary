---
tags: [__JIRA Tickets]
title: '[SPIKE] - Include None option'
created: '2024-11-20T10:43:55.650Z'
modified: '2025-02-13T08:17:31.365Z'
---

# [SPIKE] - Include None option 
## RFE-18066 - Filters tab - How to Include "None" option in publication date filter field

**Final document**
https://docs.google.com/document/d/1PEMhN0WjyNaa70VdhwM0uvh397V2imJ_AW5cCXe34rM/edit?tab=t.0

<details>
  <summary>Guión</summary>

  **Affected Areas:** Qué áreas están afectadas y por que. Primero se debe centrar el tiro en las SL que es lo que piden y después lo demás.
  **Other areas:** añadir opción al filtro si se quiere y areas directamente afectadas.

  **Backend** 
    - Hay que modificar la forma de atacar OS. 
    - OS no registra null values para este campo en el índice de la forma en que está definida, lírica y apéndice con el JSON

  **Cómo afrontarlo, cómo se haría?**
    - Propuesta: yo creo que la mejor opción es esta por esto por esto,...
    - Alternativa: Kirill si es viable y sino

  **Story breakdown:**
    - Opción 1: necesitariamos estás historias. (SL y backend 1 y luego las demás)
    - Opción 2: si es viable.

</details>

### Affected files
- vl/VLShared/library/LibrarySearchBase.cs **Add none option in the shared libraries**
- vl/vlib/Services/search/RFESearchOptions.cs **Add none option in advanced search**
- vl/vlib/Services/search/RFESearchFilters.cs **Add none option in refine search**
- vl/vlib/library/mylibrary.aspx.cs **No needed to change because this is a old design**
- vl/VLShared/search/ContentSearchParams.cs **Get description to saved searches**
- vl/VLShared/library/LibraryDocument.cs **RestAPI**
- vl/VLShared/search/UserSavedSearch.cs **RestAPI**
- vl/vlib/library/mylibrary/MyLibraryGeneralFilters.cs **Modify JSON model to React app**
- vl/VLShared/Elastic/ElasticHelper.cs **Give OpenSearch support to the new option**


### SQL
<details>
  <summary>SQL Script to filter valid/invalid pubDates</summary>

  ```
  select top 100 LibraryDocumentId as Id, PublicationDate as pubDate, * from librarydocument 
  -- where publicationDate = 0
  where PublicationDate <  19780000 and PublicationDate > 0 and PublicationDate < 3000000 
  -- where ISDATE(PublicationDate) = 0
  order by CreatedTime desc
  ```
</details>

#### OpenSearch query to have a relationship with DatabaseItem
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

```
{
  "query": {
    "query_string": {
      "query": "libraryDocumentId:101705193"
    }
  },
  "size": 10,
  "from": 0,
  "sort": []
}
```
</details>

#### Opensearch query:
<details>
  <summary>query_string => Total results: **1043778**</summary>

  ```
  {
      "query": {
        "query_string": {
          "query": "pubDate: \"1799-01-01T00:00:00\""
        }
      },
      "size": 100,
      "track_total_hits": true,
      "from": 0,
      "sort": []
    }
  ```
</details>

<details>
  <summary>query match => Total results: **1043778**</summary>

  ```
  {
    "query": {
      "match": {
        "pubDate": {
          "query": "1799-01-01T00:00:00"
        }
      }
    },
    "track_total_hits": true,
    "size": 100,
    "from": 0,
    "sort": []
  }
  ```
</details>

#### OpenSearch Queries captured on RFE 

<details>
  <summary>Search by term "aspirin" and with pubDate none => Query (exact) Total results: **59 results**</summary>

```
{
  "track_total_hits": true,
  "from": 0,
  "highlight": {
    "fields": {
      "title.en": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets": true
        }
      },
      "title.ja": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets": true
        }
      },
      "abstract.en": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets": true
        }
      },
      "abstract.ja": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets": true
        }
      },
      "fulltext.en": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets_terms": true
        }
      },
      "fulltext.ja": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets_terms": true
        }
      },
      "doctext.en": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets_terms": true
        }
      },
      "doctext.ja": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets_terms": true
        }
      }
    },
    "fragment_size": 2147483647,
    "number_of_fragments": 1
  },
  "query": {
    "bool": {
      "filter": [
        {
          "bool": {
            "must": [
              {
                "bool": {
                  "should": [
                    {
                      "bool": {
                        "must": [
                          {
                            "term": {
                              "libraryId": {
                                "value": 0
                              }
                            }
                          },
                          {
                            "term": {
                              "ownerId": {
                                "value": 1098530
                              }
                            }
                          },
                          {
                            "term": {
                              "docType": {
                                "value": "libraryDocument"
                              }
                            }
                          }
                        ]
                      }
                    },
                    {
                      "bool": {
                        "must": [
                          {
                            "terms": {
                              "libraryId": [
                                38671,
                                39449,
                                41812,
                                46640,
                                47669,
                                48678,
                                55009,
                                55638,
                                64427,
                                68165,
                                69616,
                                70058,
                                75695,
                                75873,
                                76155
                              ]
                            }
                          },
                          {
                            "term": {
                              "docType": {
                                "value": "libraryDocument"
                              }
                            }
                          }
                        ]
                      }
                    },
                    {
                      "bool": {
                        "must": [
                          {
                            "term": {
                              "clientId": {
                                "value": 0
                              }
                            }
                          },
                          {
                            "term": {
                              "docType": {
                                "value": "content"
                              }
                            }
                          }
                        ]
                      }
                    }
                  ]
                }
              },
              {
                "match": {
                  "pubDate": {
                    "operator": "and",
                    "query": "1799",
                    "boost": 0
                  }
                }
              }
            ]
          }
        }
      ],
      "must": [
        {
          "bool": {
            "should": [
              {
                "match": {
                  "title.en": {
                    "operator": "and",
                    "query": "aspirin",
                    "boost": 2000
                  }
                }
              },
              {
                "match": {
                  "title.ja": {
                    "operator": "and",
                    "query": "aspirin",
                    "boost": 1
                  }
                }
              },
              {
                "match_phrase": {
                  "altTitles.en": {
                    "query": "aspirin",
                    "slop": 99,
                    "boost": 2000
                  }
                }
              },
              {
                "match_phrase": {
                  "altTitles.ja": {
                    "query": "aspirin",
                    "slop": 99,
                    "boost": 1
                  }
                }
              }
            ]
          }
        }
      ]
    }
  },
  "size": 100,
  "sort": [
    {
      "_score": {
        "order": "desc"
      }
    },
    {
      "contentId": {
        "order": "asc"
      }
    }
  ],
  "_source": {
    "includes": [
      "docType",
      "contentId",
      "parentId",
      "titleSort",
      "libraryDocumentId",
      "libraryId",
      "relatedItems.relatedItemId",
      "relatedItems.relatedItemType",
      "relatedItems.libraryDocumentId"
    ]
  },
  "terminate_after": 1000000,
  "timeout": "20s",
  "track_scores": true,
  "track_total_hits": true
}
```
</sumary>
</details>

<details>
  <summary>Search by term "aspirin" and with pubDate none => Range lte (less than or equal) Total results: **59 results**</summary>

```
{
  "track_total_hits": true,
  "from": 0,
  "highlight": {
    "fields": {
      "title.en": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets": true
        }
      },
      "title.ja": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets": true
        }
      },
      "abstract.en": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets": true
        }
      },
      "abstract.ja": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets": true
        }
      },
      "fulltext.en": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets_terms": true
        }
      },
      "fulltext.ja": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets_terms": true
        }
      },
      "doctext.en": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets_terms": true
        }
      },
      "doctext.ja": {
        "type": "experimental-rfe",
        "options": {
          "hit_source": "postings",
          "return_offsets_terms": true
        }
      }
    },
    "fragment_size": 2147483647,
    "number_of_fragments": 1
  },
  "query": {
    "bool": {
      "filter": [
        {
          "bool": {
            "must": [
              {
                "bool": {
                  "should": [
                    {
                      "bool": {
                        "must": [
                          {
                            "term": {
                              "libraryId": {
                                "value": 0
                              }
                            }
                          },
                          {
                            "term": {
                              "ownerId": {
                                "value": 1098530
                              }
                            }
                          },
                          {
                            "term": {
                              "docType": {
                                "value": "libraryDocument"
                              }
                            }
                          }
                        ]
                      }
                    },
                    {
                      "bool": {
                        "must": [
                          {
                            "terms": {
                              "libraryId": [
                                38671,
                                39449,
                                41812,
                                46640,
                                47669,
                                48678,
                                55009,
                                55638,
                                64427,
                                68165,
                                69616,
                                70058,
                                75695,
                                75873,
                                76155
                              ]
                            }
                          },
                          {
                            "term": {
                              "docType": {
                                "value": "libraryDocument"
                              }
                            }
                          }
                        ]
                      }
                    },
                    {
                      "bool": {
                        "must": [
                          {
                            "term": {
                              "clientId": {
                                "value": 0
                              }
                            }
                          },
                          {
                            "term": {
                              "docType": {
                                "value": "content"
                              }
                            }
                          }
                        ]
                      }
                    }
                  ]
                }
              },
              {
                "range": {
                  "pubYear": {
                    "lte": 1799,
                    "boost": 0
                  }
                }
              }
            ]
          }
        }
      ],
      "must": [
        {
          "bool": {
            "should": [
              {
                "match": {
                  "title.en": {
                    "operator": "and",
                    "query": "concerta",
                    "boost": 2000
                  }
                }
              },
              {
                "match": {
                  "title.ja": {
                    "operator": "and",
                    "query": "concerta",
                    "boost": 1
                  }
                }
              },
              {
                "match_phrase": {
                  "altTitles.en": {
                    "query": "concerta",
                    "slop": 99,
                    "boost": 2000
                  }
                }
              },
              {
                "match_phrase": {
                  "altTitles.ja": {
                    "query": "concerta",
                    "slop": 99,
                    "boost": 1
                  }
                }
              }
            ]
          }
        }
      ]
    }
  },
  "size": 100,
  "sort": [
    {
      "_score": {
        "order": "desc"
      }
    },
    {
      "contentId": {
        "order": "asc"
      }
    }
  ],
  "_source": {
    "includes": [
      "docType",
      "contentId",
      "parentId",
      "titleSort",
      "libraryDocumentId",
      "libraryId",
      "relatedItems.relatedItemId",
      "relatedItems.relatedItemType",
      "relatedItems.libraryDocumentId",
      "pubDate"
    ]
  },
  "terminate_after": 1000000,
  "timeout": "20s",
  "track_scores": true
}
```

</details>

#### Affectec areas: REST API

<details>
  <summary>REST API</summary>

  - vl\RFERestAPI\Requests\BasicSearchRequest.cs
  This class contains the enum to **SearchPubDateRange**, to support NONE option we need to add a new enum value and investigate all usings
  Class definition: 
  ```public class BasicSearchRequest : SearchRequestBase
      public SearchPubDateRange? DateRange { get; set; } = SearchPubDateRange.ALL;
  ```
  This class has childs:
  - SemanticSearchRequest : BasicSearchRequest
  - (CiteIt) WordPluginSearchRequest : BasicSearchRequest
  - (CiteIt) WordSearchRequest : BasicSearchRequest


</details>

