---
title: Web Services API Reference
keywords: testDuke, retestDuke, etcDuke
last_updated: June 28th, 2016
summary: "Sanitized excerpts from a SOAP API reference"
sidebar: dukedocs_sidebar
permalink: /duke_api_ref/
---

### Overview

The CodeChecker API allows you to create, delete, retrieve, and modify various objects 
(such as users, user groups, and so on) in the CodeChecker database. Many of these objects 
are also editable through the configuration screens within the CodeChecker UI and through 
various CodeChecker commands. For example, you can create users and user groups through
the API or through the configuration UI (see the [User Guide](../placeholder)), and you 
can manage defect data through the `cc-manage` command (see the 
[Command Reference](../placeholder)). 

### Audience

This reference assumes that you are familiar with common 
[CodeChecker terms](#glossary) and that you have these skills:

* Knowledge of web services and WSDL files

* An understanding of SOAP

* An understanding of XML

* Knowledge of a language that supports SOAP bindings

  Examples: Perl, Python, C/C++, Java, C#

### Getting Started

To get started with the API:

 1. [Download](#downloading) the WSDL file for the CodeChecker service. 

 2. [Run](#running) the sample application.

 3. Create scripts or a web application for the API requests and responses you need 
    to handle.

    Your scripts require a SOAP library (for example, SOAP::Lite with Perl or suds 
    with Python).

**Tip:** You can familiarize yourself with methods in the API by using SOAP directly,
for example, with [SoapUI](https://www.soapui.org/). To practice using SOAP to generate 
API requests, view responses, and troubleshoot your scripts, see our 
[developer forum posting](../placeholder) on this topic.

Note that method documentation in this API reference provides examples of SOAP-based 
requests and responses. For example, see the sample SOAP requests and responses to 
[createUser()](#createUser).

#### Downloading the WSDL file {#downloading}

SOAP includes XML descriptions of the message format and transport protocols, which are 
available from the server in WSDL (Web Services Description Language) file here:

`http://<domain>:<port>/path/to/<latest_api_version>/config_service?wsdl`

For example: `http://mycompany.domain:8080/ws/v2/config_service?wsdl`

Though you need to use the API version that is associated with your installation, you can 
find WSDLs for additional versions of the API at the following URL:

`http://mycompany.domain:8080/ws`

For version information and changes to the API, see [API History](../placeholder). 

#### Running the Sample Application {#running}

The API includes a sample client application that is especially useful in demonstrating 
how to authenticate messages that your application sends to the server. You can also use 
it as a starting point in developing your own applications.

The sample application simply generates a request for all users and returns a user 
list. It is located within your CodeCheck installation directory (`<install_dir>`).

To run the sample web Services client application:

1. Meet prerequisites:

   * JDK 1.8 is installed on your system, and its `bin` directory is in your path.
   * You know the URI (`<server-address>:<server-port>`) of the CodeChecker UI and 
     the administrator password.
   * The CodeChecker UI is running.

2. Extract the sample from `api_example.zip`, a file within the 
   CodeChecker installation directory. 

   * On Linux:

     ```
     <install_dir>/doc/en/api/example/api_example.zip
     ```

   * On Windows:
   
     ```
     <install_dir>\doc\en\api\example\api_example.zip
     ```
     
3. Go to the extracted folder named `api_example`.

4. On Linux, change permissions of `runme.sh` script so that it is executable:

   `> chmod +x runme.sh`

5. Compile and run the application from `api_example`:

   On Linux:
   `> ./runme.sh <server-address>:<server-port> <admin-password>`
   
   On Windows:
   `> runme.bat <server-address>:<server-port> <admin-password>`
   
   Example:

   ```
       $ ./runme.sh 10.9.9.999:8080 myadminpassword
       compiling...
       mkdir: classes: File exists
       running...
       Total number of records:4
       myuser
       test
       admin
   ```

**Note:**
In CodeChecker, Windows paths are converted to lowercase characters, and separators 
are converted to forward slash characters (`/`).

### Config Service {#configService}
	
API for performing CodeChecker configurations.

#### Method: createUser {#createUser}

Create a CodeChecker user. 

**Parameters: createUser**

| Name             | Description                | Type   |
|------------------+----------------------------+--------|
| email            | Email address of the user. | string |
| firstName        | First name of the user.    | string |
| lastName         | Last name of the user.     | string |
| username         | User name of the user.     | string |

```
<!-- SAMPLE SOAP REQUEST: createUser() -->
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:v2="http://mycompany.com">
   <soapenv:Header/>
   <soapenv:Body>
      <vX:createUser>
         <userSpec>
            <email>rbg@mycompany.com</email>
            <firstName>Ruth</firstName>
            <lastName>Ginsburg</lastName>
            <userName>ruthie</userName>
         </userSpec>
      </vX:createUser>
   </soapenv:Body>
</soapenv:Envelope>
```

```
<!-- SAMPLE SOAP RESPONSE: createUserResponse() -->
<S:Envelope xmlns:S="http://schemas.xmlsoap.org/soap/envelope/">
   <S:Body>
      <ns2:createUserResponse xmlns:ns2="http://mycompany.com/v2"/>
   </S:Body>
</S:Envelope>
```

#### Method: createWidget

Create a [widget](#widget). You can do a lot of cool things with widgets. You will need
to use your imagination. This is just a dummy entry for this writing sample.

**Parameters: createWidget** {#createWidget}

| Name             | Description                            | Type          |
|------------------+----------------------------------------+---------------|
| properties       | Cool properties for widgets.           | [widgetDataObj](#widgetDataObject) |

#### Data object: widgetDataObject {#widgetDataObject}

**Parameters: widgetDataObj**

| Name        | Description                                                   | Type    |
|-------------+---------------------------------------------------------------+---------|
| name        | User-specified name for the widget.                           | string  |
| cool        | Some cool property. See [Cool Constants](#cool).              | string  |
| showInUI    | Display widget in the CodeChecker UI (`true`) or not (`false`)| boolean |

```
<!-- SAMPLE1 SOAP REQUEST: createWidget() for STRING type Widget -->
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:v2="http://mycompany.com">
   <soapenv:Header/>
   <soapenv:Body>
      <vX:createWidget>
         <widgetSpec>
            <name>myWidget</widgetName>
            <cool>cool1</cool>
            <cool>cool2</cool>
            <cool>cool3</cool>
            <cool>cool4</cool>
            <showInUI>true</showInUI>
         </widgetSpec>
      </vX:createWidget>
   </soapenv:Body>
</soapenv:Envelope>
```

```
<!-- SAMPLE1 SOAP RESPONSE: createWidgetResponse() -->
<S:Envelope xmlns:S="http://schemas.xmlsoap.org/soap/envelope/">
   <S:Body>
      <ns2:createWidgetResponse xmlns:ns2="http://mycompany.com/v2"/>
   </S:Body>
</S:Envelope>
```
 
### Types and Constants {#typesConstants}
	
Enumerations and string-based values that are valid for specified fields and parameters.

#### Role Type  (roleTypeDataObj.type) {#roleTypeDataObj}

| Role Type  | Description                        |
|------------+------------------------------------|
| group      | Role that is assigned to a group.  |
| user       | Role that is assigned to a user.   |

#### Cool Constants {#cool}

| Some Type   | Description                       |
|-------------+-----------------------------------|
| cool1       | Description of property cool1.    |
| cool2       | Description of property cool2.    |
| cool3       | Description of property cool4.    |
| cool4       | Description of property cool4.    |
	
### Error Codes {#errorCodes}
	
Descriptions of error codes returned for invalid web service requests.

SOAP Example (Error 1001 to an `updateUser()` request):

```
<S:Envelope xmlns:S="http://schemas.xmlsoap.org/soap/envelope/">
   <S:Body>
      <S:Fault xmlns:ns4="http://www.w3.org/2003/05/soap-envelope">
         <faultcode>S:Server</faultcode>
         <faultstring>User not found.</faultstring>
         <detail>
            <ns2:Fault xmlns:ns2="http://ws.company.com/v1">
               <errorCode>1001</errorCode>
               <message>User not found.</message>
            </ns2:Fault>
         </detail>
      </S:Fault>
   </S:Body>
</S:Envelope>
```

Authentication errors produce a error message without an error code. Example:

```
<S:Envelope xmlns:S="http://schemas.xmlsoap.org/soap/envelope/">
   <S:Body>
      <S:Fault xmlns:ns4="http://www.w3.org/2003/05/soap-envelope">
         <faultcode>S:Server</faultcode>
         <faultstring>User authentication failed.</faultstring>
      </S:Fault>
   </S:Body>
</S:Envelope>
```

**Error Codes**

 | Error Code | Description                 |
 |------------+-----------------------------|
 | 1001       | User not found.             |
 | 1003       | Group not found.            |
 | 1004       | Password must not be empty. |
 | 1005       | Another error message here. |
 | 1006       | Another error message here. |
 

{% include glossary.md %}
