---
title: REST vs. SOAP
tags: [sampleTagDuke, sampleTag2Duke]
keywords: testDuke, retestDuke, etcDuke
last_updated: "June 30, 2016"
summary: "Writing sample contrasting My Company's REST and SOAP APIs"
sidebar: dukedocs_sidebar
permalink: /duke_rest_vs_soap/
---

## My Company's Web Service APIs

My Company's web service APIs allow you to add our features to your web application.
  
From a client perspective, our APIs differ mostly in terms of the messaging formats used 
for requests and responses. Our web services are designed based on SOAP (a W3C standard 
called "Simple Object Application Protocol" until SOAP v1.2) and REST (Representational 
State Transfer) principles. 

Both SOAP and REST are for exchanging information over a distributed network environment, 
such as the Internet. They are platform-independent and language-independent. SOAP and 
REST support messaging over HTTP, the application protocol that our web services use. 
This means that the language you use to create your web application must be able to 
exchange data over HTTP. Most can.

### Which API should you use?

It depends. Here are some considerations:

#### URIs vs. XML
The verbosity of a message affects bandwidth and therefore performance, especially 
in mobile devices. It can also impact general ease of use, particularly for requests 
(your standard CRUD -- create, read, update, delete -- operations). 

REST (or RESTful) API messages (particularly requests) are generally shorter than their 
SOAP counterparts because they use HTTP methods (like GET and POST) in URIs to retrieve 
and manipulate resources. Each URI is a representation of an object. So to retrieve the 
profile of a user object, your web application might send an HTTP request 
for that resource through URIs like these:

*  `http://www.abcd.com/user/12345`
*  `http://www.abcd.com/user/12345?first=some&last=body` 

The first example might retrieve a full set of data associated with a given user ID, such 
as `12345`. The second URI, which is parameterized, might retrieve a subset of the data 
associated with that ID, such as the first and last name of the user (`"some body"`). 
Unlike REST, SOAP requires an XML-based construct for messaging operations. For example, 
the XML for retrieving data on user `12345` through the SOAP API might look something 
like this:

~~~ 
<soapenv:Envelope 
 xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" 
 xmlns:v1="http://abcd.com/v1">
   <soapenv:Header/>
   <soapenv:Body>
      <v1:getUser>
         <id>12345</id>
      </v1:getUser>
   </soapenv:Body>
</soapenv:Envelope>
~~~

Notice that the `getUser` request represented here is wrapped in a SOAP envelope that 
is formatted in XML, as required by the SOAP standard. As you can see, elements that make 
up that envelope are responsible for much of the verbosity of SOAP messages.

### The WSDL
A SOAP web service provides a well-defined interface in the form of a WSDL (Web Services 
Description Language) file that serves as a "contract" between the sender and receiver of 
messages. To gain access to that interface (and to complex data types it references 
through an XML schema, or XSD), you need the URI to the WSDL file (for example, 
`http://abcd.company.com:8080/ws/v1/abcdservice?wsdl`). 

The WSDL is machine-readable, so Java tools like `wsimport` can use it to generate a set of 
stub classes (and source files) for each method in the API. Other examples include SoapUI 
(which reads the WSDL to generate XML that you can use directly to test methods in the 
API), Suds for Python, and so on.

Our RESTful web services lack a counterpart to the WSDL we use for SOAP. To understand 
the interface to both types of web services, you can use our API documentation and code 
examples.

### Response formats

Our RESTful API reponses use a JSON format. A simple example might look like this:

~~~
{  "user": 
   {    
      "id": 12345,
      "first": "some",  
      "last": "body", 
      "other": "some other user property"
   }
}
~~~

Our SOAP API responses use an XML format like this one:

~~~
<S:Envelope 
 xmlns:S="http://schemas.xmlsoap.org/soap/envelope/">
   <S:Body>
      <ns2:getUserResponse 
       xmlns:ns2="http://abcd.company.com/v1">
          <return>
             <id>12345</id>
             <first>some</first>
             <last>body</last>
             <other>some other property</other>
          </return>
      </ns2:getUserResponse>
   </S:Body>
</S:Envelope>
~~~

The different messaging formats affect how you go about making requests and handling 
responses. For example, a Java web application might use the latest stable version of 
HttpClient API for URIs. It might use a library such as GSON to convert a Java object 
to a JSON string or to convert a JSON response string to a Java object. For Python, 
a web application might use a library such as `urllib`. Other open source libraries and 
tools are available for most languages, whether you are dealing with URIs, JSON, or XML. 
