---
created: 2024-07-30T09:22
updated: 2024-08-22T08:59
---
# What is a servlet? 
A [[java]] class that extends server functionalities, **handling requests and generating responses** from [[web client]]. Servlets are used to create [[dynamic web pages]] and are part of the [[Java Servlet API]], providing [[interfaces]] and classes for writing servlets. [[interface-java]]


### How does a servlet work?
1. Client requests: when a web client sends a request to the [[server]], the server forwards this request to the servlet
2. Processing the request: The servlet processes the request. It could mean reading data sent by the client, interacting with a [[database]], performing some business logic, etc. 
3. Generating a response: after processing the request, the servlet generates a response. It could be an HTML page, JSON, XML, etc
4. Sending the response: the servlet sends the response back to the web client which displays it to the user. 
#### Key Points:
- [[Server-side]]
- [[HTTP Protocol]] 
- Lifecycle: managed by the [[web container]] (like Apache Tomcat), which includes initialization, handling request, and termination 

#### Basic example: 
```java
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

//server forwards the request to the appropriate servlet that extends HttpServlet
public class HelloWorldServlet extends HttpServlet { 
	//the servlet's doGet or doPost method receives an HttpServletRequest object containing details about the request
	// The servlet processes the request
	@Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) 
	    //read from request here
	    //write to response
		    //error handling
            throws ServletException, IOException {
        //The HttpServletResponse object is used to set the reponses content type and headers
        response.setContentType("text/html");
        //The servlet gets a PrintWriter from the HttpServletResponse object and writes the response body to send back to the client
        PrintWriter out = response.getWriter();
        out.println("<html><body>");
        out.println("<h1>Hello, World!</h1>");
        out.println("</body></html>");
    }
}
```

#### Explanation of each class:
- `java.io.IOException` 
	- Purpose: This exception is thrown to indicate that an Input/Output operation has failed or been interrupted
	- Usage in Servlets: When performing I/O operations such as reading from or writing to a file or network connection, this exception handles errors.
- `java.io.PrintWriter` 
	- Purpose: This class is used to write formatted text to a character-output stream
	- Usage in Servlets: used to send character text to the client. It provides methods to write strings, characters, and other data types in a formatted manner. 
- `javax.servlet.ServletException`
	- Purpose: This exception is a general exception a servlet can throw when it encounters difficulty. It encapsulates any issues that occur during the servlets processing
	- Usage in Servlets: It is through to indicate a servlet-specific error, such as issues with request or response handling, and is part of the servlets error-handling mechanism. 
- `javax.servlet.http.HttpServlet`
	- Purpose: The base class for creating HTTP servlets. Provides methods to handle various HTTP methods (GET, POST, etc)
	- Usage in Servlets: By extending `HttpServlet`, your servlet can override methods like `doGet` and `doPost` to define hoe to handle HTTP GET and POST requests.
- `javax.servlet.http.HttpServletRequest`
	- Purpose: This [[interfaces | interface]] provides methods to access information about the HTTP request, such as request parameters, headers, and body. 
	- Usage in Servlets: the `HttpServletRequest` object is passed to the servlet's `doGet` or `doPost` method. It allows the servlet to read data sent by the client, such as form inputs or query parameters. 
- `javax.servlet.http.HttpServletResponse` 
	- Purpose: This [[interfaces | interface]] provides methods to create and sent the HTTP response to the client, including setting the response headers, status codes, and the response body.
	- Usage in Servlets: The `HttpServletResponse` object is passed to the servlets `doGet` or `doPost` method. It allows the servlet to send data back to the client, such as HTML content, JSON data, or redirect instructions. 