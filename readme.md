# Fluree in Brief

Fluree is an immutable graph database that prioritises security, trust, provenance, privacy, and interoperability over traditional contemporary database functionality. Fluree can be run in a centralised, distributed, or decentralised fashion.

## Installation

Download latest stable: https://s3.amazonaws.com/fluree-releases-public/fluree-stable.zip

## Unzipe files and run the following commands inside the fluree-stable folder

`./fluree_start.sh`

Visit http://localhost:8090/ on browser

### Creation of a Ledger

`test/myexampleledger`

### Adding a collection

```
[
  {
    "_id": "_collection",
    "name": "person"
  },
  {
    "_id": "_collection",
    "name": "chat"
  },
  {
    "_id": "_collection",
    "name": "comment"
  },
  {
    "_id": "_collection",
    "name": "artist"
  },
  {
    "_id": "_collection",
    "name": "movie"
  }
]
```

### Adding Predicates

```
[
  {
    "_id": "_predicate",
    "name": "person/handle",
    "doc": "The person's unique handle",
    "unique": true,
    "type": "string"
  },
  {
    "_id": "_predicate",
    "name": "person/fullName",
    "doc": "The person's full name.",
    "type": "string",
    "index": true
  },
  {
    "_id": "_predicate",
    "name": "person/age",
    "doc": "The person's age in years",
    "type": "int",
    "index": true
  },
  {
    "_id": "_predicate",
    "name": "person/follows",
    "doc": "Any persons this subject follows",
    "type": "ref",
    "restrictCollection": "person"
  },
  {
    "_id": "_predicate",
    "name": "person/favNums",
    "doc": "The person's favorite numbers",
    "type": "int",
    "multi": true
  },
  {
    "_id": "_predicate",
    "name": "person/favArtists",
    "doc": "The person's favorite artists",
    "type": "ref",
    "restrictCollection": "artist",
    "multi": true
  },
  {
    "_id": "_predicate",
    "name": "person/favMovies",
    "doc": "The person's favorite movies",
    "type": "ref",
    "restrictCollection": "movie",
    "multi": true
  },
  {
    "_id": "_predicate",
    "name": "person/user",
    "type": "ref",
    "restrictCollection": "_user"
  },
  {
    "_id": "_predicate",
    "name": "chat/message",
    "doc": "A chat message",
    "type": "string",
    "fullText": true
  },
  {
    "_id": "_predicate",
    "name": "chat/person",
    "doc": "A reference to the person that created the message",
    "type": "ref",
    "restrictCollection": "person"
  },
  {
    "_id": "_predicate",
    "name": "chat/instant",
    "doc": "The instant in time when this chat happened.",
    "type": "instant",
    "index": true
  },
  {
    "_id": "_predicate",
    "name": "chat/comments",
    "doc": "A reference to comments about this message",
    "type": "ref",
    "component": true,
    "multi": true,
    "restrictCollection": "comment"
  },
  {
    "_id": "_predicate",
    "name": "comment/message",
    "doc": "A comment message.",
    "type": "string",
    "fullText": true
  },
  {
    "_id": "_predicate",
    "name": "comment/person",
    "doc": "A reference to the person that made the comment",
    "type": "ref",
    "restrictCollection": "person"
  },
  {
    "_id": "_predicate",
    "name": "artist/name",
    "type": "string",
    "unique": true
  },
  {
    "_id": "_predicate",
    "name": "movie/title",
    "type": "string",
    "fullText": true,
    "unique": true
  }
]
```

### Adding Data

```
[
  {
    "_id": "person$jdoe",
    "handle": "jdoe",
    "fullName": "Jane Doe",
    "age": 25,
    "favNums": [1223, 12, 98, 0, -2],
    "favArtists": ["artist$1", "artist$2", "artist$3"],
    "follows": "person$zsmith",
    "favMovies": ["movie$1", "movie$2", "movie$3"]
  },
  {
    "_id": "person$zsmith",
    "handle": "zsmith",
    "fullName": "Zach Smith",
    "age": 63,
    "favNums": [5, 645, 28, -1, 1223],
    "favArtists": ["artist$1"],
    "follows": "person$jdoe",
    "favMovies": ["movie$2", "movie$3"]
  },
  {
    "_id": "person$anguyen",
    "handle": "anguyen",
    "fullName": "Amy Nguyen",
    "age": 34,
    "favNums": [7, 98, 0, 2],
    "favArtists": ["artist$2", "artist$3"],
    "follows": "person$jdoe",
    "favMovies": ["movie$3"]
  },
  {
    "_id": "person$dsanchez",
    "handle": "dsanchez",
    "fullName": "Diana Sanchez",
    "age": 70,
    "favNums": [9, 1950],
    "favArtists": ["artist$2"],
    "follows": "person$anguyen",
    "favMovies": ["movie$1", "movie$2", "movie$3"]
  },
  {
    "_id": "chat",
    "message": "Hi! I'm chat from Jane.",
    "person": "person$jdoe",
    "instant": "#(- (now) 20000)",
    "comments": ["comment$zsmith", "comment$anguyen"]
  },
  {
    "_id": "chat",
    "message": "Hi! I'm a chat from Diana.",
    "person": "person$dsanchez",
    "instant": "#(- (now) 5000)",
    "comments": ["comment$zsmithagain", "comment$anguyenagain"]
  },
  {
    "_id": "chat",
    "message": "Hi! I'm a chat from Zach.",
    "person": "person$zsmith",
    "instant": "#(now)"
  },
  {
    "_id": "comment$zsmith",
    "message": "Zsmith is responding!",
    "person": "person$zsmith"
  },
  {
    "_id": "comment$anguyen",
    "message": "Hi Jane!",
    "person": "person$anguyen"
  },
  {
    "_id": "comment$zsmithagain",
    "message": "Welcome Diana!",
    "person": "person$zsmith"
  },
  {
    "_id": "comment$anguyenagain",
    "message": "Welcome Diana! This is Amy.",
    "person": "person$anguyen"
  },
  {
    "_id": "artist$1",
    "name": "Gustav Klimt"
  },
  {
    "_id": "artist$2",
    "name": "Augusta Savage"
  },
  {
    "_id": "artist$3",
    "name": "Jean-Michel Basquiat"
  },
  {
    "_id": "movie$1",
    "title": "The Shawshank Redemption"
  },
  {
    "_id": "movie$2",
    "title": "Hot Fuzz"
  },
  {
    "_id": "movie$3",
    "title": "Gran Torino"
  }
]
```

###

# Fluree Query

## Basic Query

### Select Key

The select-array can include any combination of the items in any order. A "\*"
,Predicate Names: Namespaced or Not
,A map, crawling the graph.
,Reversely-referenced Predicates
or A map with sub-select options

### From key

A from key is used where your select options are applied to the field.

```json
{
  "select": ["*", { "chat/_person": ["*", { "_as": "chperson" }] }],
  "from": [87960930223082, ["person/handle", "jdoe"]]
}
```

### Where Key

Where clauses are a simple way to apply very basic filters to a query

```json
{
  "select": ["chat/message", "chat/instant"],
  "where": "chat/person = 351843720888322 OR chat/instant > 1517437000000"
}
```

## Analytical Query

Analytical query is used to answer more complicated questions about the data.

```json
{
  "select": ["?nums", "(avg ?nums)"],
  "where": [["?person", "person/favNums", "?nums"]]
}
```

### Where key

#### Three Tuple

You define the values for one or two portions of a three-tuple when you include it in your where-array. Nulls or variables make up the sections you don't define.

#### Four Tuple

Four tuples are identical to three tuples with the exception that four tuples give a data source for the subject, predicate, and object patterns.

#### Two Tuple Variable Binding

Bind a variable to a value, including an aggregate value that has been computed. These variables can be utilised in the where-array items that follow.

```json
{
  "select": "?person",
  "where": [
    ["?handle", "jdoe"],
    ["?person", "person/handle", "?handle"]
  ]
}
```

#### Binding map

Serves the same function as a two-tuple variable binding, except the syntax is different.

#### Optional map

Like, three-tuples, looks for flakes (pieces of data) that match a provided pattern. However, when joining the results of this map with the queries existing resultset, will simply bind null if there is no match (a left outer join).

#### Union map

The two parts of a union map are outer joined.

#### Filter map

Filters the results up to that point in the query.

```json
{
  "select": ["?handle", "?num"],
  "where": [
    ["?person", "person/handle", "?handle"],
    ["?person", "person/favNums", "?num"],
    { "filter": ["(> 10 ?num)", "(= \"jdoe\" ?handle)"] }
  ]
}
```

### Prefixes key

If we wish to query across many Fluree ledgers, we may use the prefixes map to indicate the ledger.

```json
{
  "prefixes": {
    "ftest": "fluree/test"
  },
  "select": "?nums",
  "where": [
    ["$fdb4", ["person/handle", "zsmith"], "person/favNums", "?nums"],
    ["ftest", ["person/handle", "zsmith"], "person/favNums", "?nums"]
  ]
}
```

### Vars key

used to subsitute value in given query

```json
{
  "select": "?handle",
  "where": [["?person", "person/handle", "?handle"]],
  "vars": {
    "?handle": "dsanchez"
  }
}
```

## Block Query

this query is used to select all flakes from a block or a selection of blocks.

```json
{
  "block": [3],
  "prettyPrint": true
}
```

## Advanced Query

```json
{
  "select": [
    "handle",
    { "comment/_person": ["*", { "_as": "comment", "_limit": 1 }] }
  ],
  "from": "person"
}
```

# Fluree Basic Transactions

## Update Data

```json
[
  {
    "_id": ["person/handle", "dsanchez"],
    "age": 71
  }
]
```

update using subject id

```json
[
  {
    "_id": 351843720888324,
    "age": 71
  }
]
```

## Upsert Data

you can upsert data in fluree if you have unique predicate marked

```json
[
  {
    "_id": ["_predicate/name", "person/handle"],
    "upsert": true
  }
]
```

## Delete Data

### Delete a subject

```json
[
  {
    "_id": ["person/handle", "zsmith"],
    "_action": "delete"
  }
]
```

### Delete a predicate

```json
[
  {
    "_id": ["person/handle", "jdoe"],
    "age": null
  }
]
```
