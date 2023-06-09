# Understanding RESTFul services with Windows Communication Foundation (WCF) and Oracle HR Schema

What Are RESTful Web Services?
REST stands for Representational State Transfer is an architectural style rather than a prescribed way of building Web services, some of the most important aspects of the REST environment are:

HTTP or HTTPS may be used as the transfer protocol.
URLs including query strings are used to address resources.
Representation formats supported range from HTML and XML to JSON and ATOM.
A Simple and intuitive programming interface is achieved by using HTTP verbs and status codes.
Statelessness in the interaction between clients and services.
REST is not concerned with the definition of messages and the design of methods, the key point here is that REST describes a stateless, hierarchical scheme for representing resources and business objects over a network. The main components of this model are: resources and actions. The action of the resource is determined by four main HTTP verbs: GET, PUT, DELETE and POST, and the action which can affect those resources are mainly CRUD (Create, Read, Update and Delete) methods, the success of the action is found by the HTTP status code.

The REST model relies on the application that accesses the data sending the appropriate HTTP verb as part of the request used to access the data.

GET is used exclusively to retrieve data and, therefore, the result can also be buffered.
POST is used to add new records.
PUT is used to add or change a resource.
DELETE is used for delete resources.
The data can be returned in a number of formats, but for portability the most common formats include XML (POX) and JSON.
WCF and REST
The REST architecture is becoming increasingly common, and WCF provides attributes, methods, and types with which you can build and access REST Web Services quickly and easily.

WebHttpBinding: An binding that uses the HTTP transport and text message encoder.
WebBehavior: This is an endpoint behavior that will modify the dispatch layer on all operations on a contract. The modifications cause messages to be dispatched to methods on your service based on URIs and HTTP verbs.
WebServiceHost: This is a ServiceHost-derived class that simplifies the configuration of a web-based service.
WebOperationContext: This is a new context object, which contains the state of the incoming request and ongoing response, and simplifies coding against HTTP using WCF.
WebGetAttribute/WebInvokeAttribute: Operation behaviors that are applied as attributes on a ServiceContract's methods. WebGetAttribute is for GET verb and WebInvokeAttribute is for all the other verbs. It also tells the dispatcher how to match the methods to URIs and how to parse the URI into method parameters.
The following table shows the properties of both WebGetAttribute and WebInvokeAttribute.
Method	The HTTP verb the method should respond to.
UriTemplate	The definition of the URI the CLR method should respond to.
RequestFormat	Enumeration that specifies the format for deserializing the request (Xml or Json).
ResponseFormat	Enumeration that specifies the format for serializing the response (Xml or Json).
BodyStyle	Enumeration that specifies whether the request and the response data should be wrapped in an element with the same name as the CLR method name. Bare is typically used with RESTful services.
The essential components to construct a REST Service with WFC can be found in System.ServiceModel.Web assembly. However, the most important part of the process is designing the schema that you will use to provide access to the resources exposed by the service. So the main idea behind REST is to design your URIs in a way that makes logical sense based on your resource set. The URIs should, if possible, make sense to the application that consumes the data.

Depending on the volume of data in the database, a query might retrieve a large number of items, therefore, it makes sense to provide additional query parameters that a user can specify to limit the number of items returned.

Implementing a simple RESTful Service Example with WCF and Oracle.
In this example, we will develop a WCF RESTful service by using Oracle HR Sample Schema, ODP.NET, ADO.NET and Visual Studio 2015. You can learn about the HR Schema in this post, I have written to introduce you to this schema. The following illustration shows the components in the Employee service that I have written for this post.

Fig 1. Components of our Employee RESTFul service.



Step 1:Write the POCO object.

Fig 2. Employee entity class.



Step 2: Write the following utility class.

Fig 3. Utility class.



Step 3: Write the following helper class adding the Oracle Data Provider for .NET.

Fig 4. DAC data access class.



Step 4:Define and write the service contract.

Fig 5. Service contract interface.



Step 5: Write the service implementation class.

Fig 6. Service implementation class.



Step 6: Write the following Employee.svc file. Use the WebServiceHost class, the WebServiceHost class inherits from ServiceHost and automatically assigns the correct binding and behavior to your endpoint. You no longer need to be concerned about the content of your configuration file.

Fig 7. EmployeeService.svc File.



Step 7: Write the configuration file and store the connection string for the Oracle HR schema.

Fig 8. Configuration File.



In this example a GET at http://localhost/WcfRest/EmployeeService.svc/Employees shows all the employees in the HR database.
Fig 9. Running the example, querying all the employees.



Here a GET at http://localhost/WcfRest/EmployeeService.svc/102 show only one employee with the ID 102.
Fig 10. Querying only one employee.



Also, a GET at http://localhost/WcfRest/EmployeeService.svc/110 show the employee with the ID 110.
Fig 11. Querying another employee.



Download example source code.
