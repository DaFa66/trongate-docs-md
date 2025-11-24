# API Terminology Explained


Before moving forward, let's clarify some important terminology.

## Endpoint


The word 'endpoint' means a URL (i.e., a website address) that has been designed to accept and process HTTP requests. Strictly speaking, an endpoint could be URL that loads up a webpage - perhaps with pictures, JavaScript and HTML. Or, an endpoint could simply return text-based data - perhaps in the form of XML, JSON or comma separated values (CSV format).

## HTTP


HTTP stands for Hypertext Transfer Protocol and is the dominant method of communication by which information is sent across the internet.

## HTTP Request


An 'HTTP request' is a packet of data that has been transmitted to an endpoint. Different types of HTTP request include (but are not limited to):


- GET
- POST
- PUT
- DELETE

## HTTP Response


An 'HTTP response' is a server's response to an inbound HTTP request. Typically, a server's response will contain (but not be limited to) two key parameters.


- **an HTTP response status code** - check [this webpage](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) for details.
- **an HTTP response body **- which is a body of text that can be read by a browser and translated into entities like; HTML pages, JSON objects, XML documents and more.

## In-Built API Endpoint


An **in-built** API endpoint is the phrase we'll be using, in the Trongate documentation, to refer to an endpoint that comes shipped with all installations of the Trongate framework. In other words, it's an assortment of endpoints that have already been coded into the framework and you can start using them immediately. Trongate's in-built endpoints assist with executing common database related tasks such as create, read, update and delete.

## Custom API Endpoint


A **custom** API endpoint is a bespoke endpoint that has been custom built - by a developer - to serve a particular purpose. Custom endpoints are, by definition, *not included* with the Trongate framework.

