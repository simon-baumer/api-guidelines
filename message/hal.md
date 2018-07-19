# HAL

The [`application/hal+json`](http://stateless.co/hal_specification.html) \(HAL\) **MUST** be used as the representation format of a resource.

## Introduction to HAL

> _HAL is a simple format that gives a consistent and easy way to hyperlink between resources in your API._

This document is an informal introduction to the HAL media type. For more details see [HAL - Hypertext Application Language Specification](http://stateless.co/hal_specification.html).

## Simple Document Example

The simplest Hal document looks like an empty JSON \(it is an empty JSON!\):

```javascript
{
}
```

A document representing a "Greeting" resource might look like:

```javascript
{
  "message": "Hello World!",
  "_links": {
    "self": {
      "href": "/greeting"
    }
  }
}
```

The field `_links` has a special meaning in HAL. It denotes a list of link relations - a pair of a relation identifier and a link \(URI\).

These link relations are used to express the relation of a resource with other resources.

In our case the "Greeting" resource isn't related to other resources but itself, hence the `self` relation pointing to the Greeting resource.

> NOTE: It is **customary** for every resource representation to include the `self` link relation.
>
> NOTE: The href **MUST** always be **relative path to the API root** \(e.g. without the host and scheme\).

## Relation Example

A more complex document example could be an "Order" resource that has a related resource "Author" \(a person who created the order. It might look like:

```javascript
{
  "_links": {
    "self": {
      "href": "/orders/1234"
    },
    "author": {
      "href": "/users/john"
    }
  },
  "orderNumber": 1234,
  "itemCount": 42,
  "status": "pending"
}
```

## Embedding Example

Let's assume there is an "Orders" resource which is a collection of all orders from different authors. There is the relation between the Orders resource and possibly many Order resources.

We could express this in the `_links` object using the `order` relation, but sometimes it is practical to "embed" \(entirely or partially\) related resources representations in the originating resource representation. For a scenario like this HAL offers the `_embedded` field.

The `_embedded` field's object just contains the related resources HAL representations:

```javascript
{
  "_links": {
    "self": { "href": "/orders" }
  },
  "_embedded": {
    "order": [
      {
        "_links": {
          "self": { "href": "/orders/1" }
        },
        "orderNumber": "1",
        "status": "pending"
      },
      {
        "_links": {
          "self": { "href": "/orders/2" }
        },
        "orderNumber": "2",
        "status": "cancelled"
      }      
    ]
  }
}
```

It is important to understand that embedded resource representation might be only **partial** and might also contain their own embedded resources.

The embedded resource representation should be used as a **convenience** function \(e.g. to reduce the initial number of calls needed at application launch\).

Where a full and up-to-date representation of a resource is needed the link relation should exercise the affordance \(e.g. `GET /orders/2`\).

#### Real-world Examples

Some APIs using HAL:

* [Amazon AppStream REST API](http://docs.aws.amazon.com/appstream/latest/developerguide/appstream-api-rest.html)
* [FoxyCart](https://wiki.foxycart.com/v/2.0/start)
* [Clarify.io](http://docs.clarify.io/overview/)
* [University of Oxford / Mobile Oxford](http://api.m.ox.ac.uk/browser/#/)

## Working with HAL

Refer to the [extensive list of libraries that work with HAL](https://github.com/mikekelly/hal_specification/wiki/Libraries).

### Spring Framework

Spring framework supports HAL out of the box. More info can be found in [Spring Documentation](https://spring.io/guides/gs/rest-hateoas/) and [examples](https://github.com/spring-guides/gs-rest-hateoas).

