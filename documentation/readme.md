# Overview
When surfacing data from systems of record, one of the concerns designers and developers need to address is the potential of retrieving an enormous number of results in a single load session. This requires significant processing power on both the client and server sides and network traffic, and can degrade the overall data consumption and experience.

There are different approaches to address this concern, but one of the most widely used is the concept of pagination. Pagination is a term commonly used to describe the process of a sequential division of the contents (fetched data) into separate pages. This relieves the pressure on both sides of communication and its channel.

In most cases, systems of record (databases) offer out-of-the-box features to enable pagination — in this post this will be referred to as “simple pagination.” However, that’s not always the case, since APIs can choreograph calls to each other to collect and combine results that provides a paged result set to the consumers. It’s often up to application designers and developers to come up with a suitable solution.

## Single/simple pagination
Simple pagination describes the technique and support of systems of record to provide paginated results without too much additional logic or complex implementation. Databases (relational or NoSQL/Cache) are great examples of systems of records that support simple pagination by allowing developers to write commands to query paginated data. They require  an OFFSET and a LIMIT, which determine where to start from and the maximum number of rows to be fetched. 

Some APIs allow consumers to provide an OFFSET and a LIMIT for the purpose of getting paginated payloads, either by using query parameters or headers as part of the HTTP request. Another option is limiting the number of records per page at an API level — so that instead of consumers specifying an OFFSET and a LIMIT, they only specify what page they want to get. While this approach is less flexible on the consumer side, it increases the levels of control on the API side.

## Composite/complex pagination 
Composite or complex pagination describes an approach and a technique implemented in Anypoint Platform to allow Mule applications to consolidate data from two or more different (paged) result-sets. This provides a simple pagination experience, where the server is responsible for keeping track of the appropriate OFFSET and LIMIT to the different data sources. From an API consumer’s perspective, there is only one data-set.

Though there are many options, the goal is to give consumers the experience of paginating results as if this was coming from a single result set while leveraging what is available out-of-the-box in Mule. By leveraging ObjectStore and some DataWeave code, we can build a logic that maintains the OFFSET and LIMIT to each data-set source while merging them into a single result-set.

## How to use
Import the fragment in your API and add in main raml file or in a library:

```
traits:
  paginated: !include exchange_modules/[YOUR ORGANIAZTION]/trait-pageable/[FRAGMENT VERSION]/pageable.raml
```

## Reference
[api-pagination-patterns](https://blogs.mulesoft.com/dev/design-dev/api-pagination-patterns/)