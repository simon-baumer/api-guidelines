# Foreign Key Relations

## Link or Embed Foreign Key Relation

When a resource representation includes relation with another \(foreign\) resource, the relation **MUST** be expressed as a link relation or embed the related resource.

### Example

Use:

```javascript
{
  "_links": {
    "author": { "href": "/users/john" }
    ...
  }
  ...
}
```

or:

```javascript
{
  ...
  "_embedded": {
    "author": {
      "_links": { "self": "/users/john" },
      "name": "John Appleseed",
      "email": "john@apple.com"
    }
  }
}
```

instead:

```javascript
{
  ...
  "authorHref": "/users/john"
}
```

## Nest Foreign Key Relation

If a foreign object has another identifier, but URI or the foreign object isn't a resource, the object **MUST** be nested.

### Example

Use:

```javascript
{
  "author": {
    "id": "1234",
    "name": "John Appleseed",
    "email": "john@apple.com"    
  }
}
```

instead:

```javascript
{
  "authorId": "1234"
}
```

> NOTE: As a rule of thumb, in an HTTP message body, there SHOULD NOT be any field with trailing "\_id," "\_href," "\_url" etc. in its name.

