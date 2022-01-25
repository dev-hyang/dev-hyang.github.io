---
layout:     post
title:      2022-01-05-Intro to GraphQL
subtitle:   Introduction to GraphQL
date:       2022-01-05
author:     BY HY
header-img: img/post-bg-graphQL.png
catalog: true
tags:
    - GraphQL
---

## BackGround

### REST APIs vs GraphQL

REST APIs to query product information from server side. If the information are stored in a hierarchical structure, as below:

```json
[
	{
		"name": "BBQ restaurant",
		"rating": "A",
		"menu_URL": "https://xxx.restaurant.com/menu"
		...
	}
]

#somewhere in the resource store, menu_URL stores the menu info as below
{
    "breakfast": {},
    "launch": {},
    "dinner": {},
    "liquid": {},
    "Special_discounts": "https://xxx.special.discount.com/specials_today"
}
```

if we want to further retrieve the info from *menu_URL*, then we need to call another REST API, e.g.

`GET https://xxx.restaurant.com/menu` which could cause lots of api calls=labors in the client side. So 

RESTful APIs are optimized for servers, not clients. 

*** What if we want to put client first *** Backends for Frontends

### GraphQL is a specification.

But it is still a http request. The structure of a GraphQL is like below:

`POST https://yourhost.com/graphql`

e.g.

```json
# query parameter is like
{
	book(name: "Harry Porter with me")
	{
		name
		published_date
		author
	}
}

#response/return value will be like
{
    "data":{
        "book":{
            "name": "Harry Porter with me",
            "published_date": 01/09/2021,
            "author": King Rock
        }
    }
}
```



## Features of GraphQL

### GraphQL is typed

```json
# query parameter is like
{
	book(name: "Harry Porter with me")
	{
		name
		published_date
		author
	}
}

# the type is intepreted as below
type RootQuery{
	book(name: string) : Book
}

type Book{
	name: String!
	published_date: Date
	author: String
}

# if we want to return a list type
{
    books(category: fiction){
        name
        author
    }
}

type RootQuery{
    books(category: BookCategory) : [Book]!
}

enum BookCategory{
    Fiction
    Tale
    Science
    History
    Biography
}

type Book{
    name: String!
    author: String
}

```



### GraphQL is introspectable

Documentation and client generation are free.



### Multiple resources in one round trip

```json
{
	books(name:"Harry Porter", category:Fiction){
		published_date
		author
		recommendations:{
			recommendedBy
			recommendedDate
		}
	}
}
```



## Implement a GraphQL server

Pending



Mutation = HTTP POST/PUT/DELETE

Query = HTTP GET

### e.g1, How to define GraphQL types & schemas in C#



### FreQ1: How to debug in GraphQL error

1, Use `ToInputs` method to convert json format Variables to GraphQL Inputs type

if `ToInputs` is not supported directly in NewtonSoft.Json`JObject` type, we need to serialize and deserialize it. How?

```c#
//Pending solution
var inputs = query.Variables?.ToObject<Dictionary<string, object>>().ToInputs();
```

