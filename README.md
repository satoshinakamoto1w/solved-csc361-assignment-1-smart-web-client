Download Link: https://assignmentchef.com/product/solved-csc361-assignment-1-smart-web-client
<br>
7 The project is to build a tool at web client to collect information regarding a web server. The 8 purpose of this project is two fold:

<ul>

 <li>to provide students with hands-on experience with socket programming <strong>in Python</strong>,</li>

 <li>to help students understand the application-layer protocols HTTP/HTTPs. Note that HTTPs 11 is not a standalone protocol, but instead it is HTTP over Transport Layer Security (TLS). In 12 this assignment, your main focus is HTTP, not TLS.</li>

</ul>

<h1>13 2         Background</h1>

<h2>14 2.1           HTTP</h2>

<ul>

 <li>HTTP stands for Hyper Text Transfer Protocol and is used for communication among web servers.</li>

 <li>The web client initiates a conversation by opening a connection to a web server. Once a connec17 tion is set up, the client sends up an HTTP request. The server sends an HTTP response back to 18 the client. An HTTP request consists of two parts: a header and a body. Whether a body follows 19 a header or not is specified in the header.</li>

</ul>

20 Using <em>single-line header of HTTP request </em>as an example, the first line of any request header 21 should be:

<ul>

 <li>the method field: The method field can take on several different values, including GET, POST,</li>

 <li>HEAD, and so on.</li>

 <li>the URL field: It is the field to identify a network resource, e.g., “http://www.csc.uvic.ca/index.html”.</li>

 <li>the HTTP version field</li>

 <li>The response from a server also has two parts: a header and a body. The first line of a header 27 should be:</li>

 <li>the HTTP version field,</li>

 <li>the status code field,</li>

 <li>the phrase field.</li>

 <li>Two main status codes include 200 and 404. The status code 200 means that the request 32 succeeded and the information is returned in the response. The status code 404 means that the 33 requested document does not exist on this server. Two example response messages are: “<em>HTTP/1.0 </em>34 <em>404 Not Found</em><em>r</em><em>n</em><em>r</em><em>n</em>” and “<em>HTTP/1.0 200 OK</em><em>r</em><em>n</em><em>r</em><em>n data data data …</em>” Another two status 35 codes 505: “HTTP Version Not Supported”, and 302: “302 found” for URL redirection are also 36 useful for this assignment.</li>

</ul>

<h2>37 2.2           URI</h2>

38 URI stands for Uniform Resource Identifier and is also known as the combination of Uniform 39 Resource Locators (URL) and Uniform Resource Names (URN). It is a formatted string which 40 identifies a network resource. It generally has the format: <em>protocol://host[:port]/filepath</em>. When a 41 port is not specified, the default HTTP port number is 80, and the default HTTPS port number is 42 443.

<h2>43 2.3          Cookies</h2>

44 An HTTP cookie is a small piece of data that a server sends to the user’s web browser. The browser 45 may store it and send it back with the next request to the same server. Typically, it’s used to tell 46 if two requests came from the same browser keeping a user logged-in, for example. It remembers 47 stateful information for the stateless HTTP protocol. Cookies have many applications in web, such 48 as tracking, authentication, and web analytics. Due to this reason, cookies also cause many concerns 49 on security and privacy breach.

50 The textbook includes simple introduction on cookies. More detailed information could be 51 found at: <em>https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies</em>. Python includes dedi52 cated modules to handle Cookies: <em>https://docs.python.org/3/library/http.cookies.html</em>. Neverthe53 less, you are <strong>no allowed </strong>to use this package because it defeats the purpose of this assignment:

54            understanding the nuts and bolts of HTTP.

<h1>55 3          Project Description</h1>

56 You are required to build a smart web client tool, called <em>SmartClient</em>, in Python. <strong>Note that for </strong>57 <strong>consistence, program in other language will not be accepted!</strong>

58 Given the URL of a web server, your <em>SmartClient </em>needs to find out the following information 59 regarding the web server:

<ul>

 <li>1. whether or not the web server supports HTTPs,</li>

 <li>2. whether or not the web server supports http1.1</li>

 <li>3. whether or not the web server supports http2,</li>

 <li>4. the cookie name, the expire time (if any), and the domain name (in any) of cookies that 64 the web server will use.</li>

</ul>

65 Your program first accepts URI from stdin and parses it. Then it connects to a server, sends an 66 HTTP request, and receives an HTTP response. You should also implement a routine that prints 67 out the response from the server, marking the header and the body. When you finish the client, 68 you can try to connect to any HTTP server. For instance, type “www.uvic.ca” as the input to the 69 client program and see what response you get.

<ul>

 <li>As an <em>example </em>output, after you run your code with</li>

 <li>% python SmartClient.py www.uvic.ca</li>

 <li>Your <em>SmartClient </em>may output the received response from the server (<strong>optional</strong>), e.g.,</li>

 <li>—Request begin—</li>

 <li>GET http://www.uvic.ca/index.html HTTP/1.1</li>

 <li>Host: www.uvic.ca</li>

 <li>Connection: Keep-Alive</li>

</ul>

77

<ul>

 <li>—Request end—</li>

 <li>HTTP request sent, awaiting response…</li>

</ul>

80

<ul>

 <li>—Response header —</li>

 <li>HTTP/1.1 200 OK</li>

 <li>Date: Tue, 02 Jan 2018 22:42:27 GMT</li>

 <li>Expires: Thu, 19 Nov 1981 08:52:00 GMT</li>

 <li>Cache-Control: no-store, no-cache, must-revalidate, post-check=0, pre-check=0</li>

 <li>Pragma: no-cache</li>

 <li>Set-Cookie: SESSID_UV_128004=VD3vOJhqL3YUbmaZSTJre1; path=/; domain=www.uvic.ca</li>

 <li>Set-Cookie: uvic_bar=deleted; expires=Thu, 01-Jan-1970 00:00:01 GMT; Max-Age=0; path=/; dom</li>

 <li>Keep-Alive: timeout=5, max=100</li>

 <li>Connection: close</li>

 <li>Content-Type: text/html; charset=UTF-8</li>

 <li>Set-Cookie: www_def=2548525198.20480.0000; path=/</li>

 <li>Set-Cookie: TS01a564a5=0183e07534a2511a2dcd274bee873845d67a2c07b7074587c948f80a42c427b1f7ea 94 Set-Cookie: TS01c8da3c=0183e075346a73ab4544c7b9ba9d7fa022c07af441fc6214c4960d6a9d0db2896; p 95 Set-Cookie: TS014bf86f=0183e075347c174a4754aeb42d669781e0fafb1f43d3eb2783b1354159a9ad8d81f7</li>

</ul>

96

<ul>

 <li>— Response body —</li>

 <li>Body Body …. (the actual content)</li>

</ul>

99

<ul>

 <li>Note that some lines in above output were truncated.</li>

 <li>Your code might need to send multiple requests in order to find out the required information. 102 Your code should output the final results (<strong>mandatory</strong>), for example:</li>

 <li>website: www.uvic.ca</li>

 <li>Supports of HTTPS: yes</li>

 <li>Supports http1.1: yes 106 3. Supports http2: no 107 4. List of Cookies:</li>

 <li>cookie name: SESSID_UV_128004, domain name: www.uvic.ca</li>

 <li>cookie name: uvic_bar, expires time: Thu, 01-Jan-1970 00:00:01 GMT; domain name: .uvic.ca</li>

 <li>cookie name: www_def,</li>

 <li>cookie name: TS01a564a5</li>

 <li>cookie name: TS01c8da3c, domain name: www.uvic.ca</li>

 <li>cookie name: TS014bf86f, domain name: .uvic.ca</li>

</ul>

<h2>114 3.1          Other Notes</h2>

115 1. Regarding other printout: Anything not specified in Assignment 1 is optional. For example, 116 you can decide whether or not to print out the IP address, port number, and so on. When 117 TAs test your code, if your code works fine without any problem, you are fine even if you 118 do not print out anything not required in Assignment 1. Nevertheless, if your code does not 119 work, TAs will not spend time to figure out what is wrong and you get a zero mark on the 120 required function (Refer to the table in Section 5 of Assignment 1). In this case, if your code 121 includes some printout to show intermediate results, TAs will have an idea on how far you 122 have achieved and give you some partial mark based on their own judgement.

123 2. Regarding readme file. Readme file is important. Without it TAs will not know how to 124 compile your code and how to run your code. It would waste our time to deal with your 125 complaint if TAs cannot run your code and give you a zero.

126 3. For more information on HTTP, HTML, URI, etc., please refer to http://www.w3.org. It is 127 the home page of W3 Consortium and you will find many useful links to subjects related to 128 the World Wide Web.

<h1>129 4        Schedule</h1>

<ul>

 <li>In order to help you finish this programming assignment successfully, the schedule of this assignment</li>

 <li>has been synchronized with both the lectures and the tutorials/ labs. Before the final deadline, there 132 are three tutorial sessions to help you finish the assignment. A schedule is listed as follows:</li>

</ul>

<table width="552">

 <tbody>

  <tr>

   <td width="66">Session</td>

   <td width="301">Tutorial</td>

   <td width="185">Milestones</td>

  </tr>

  <tr>

   <td width="66">Tut 1</td>

   <td width="301">P1 spec go-through, design hints, python</td>

   <td width="185">design and code skeleton</td>

  </tr>

  <tr>

   <td width="66">Tut 2</td>

   <td width="301">socket programming and testing</td>

   <td width="185">alpha code done</td>

  </tr>

  <tr>

   <td width="66">Tut 3</td>

   <td width="301">socket programming and last-minute help</td>

   <td width="185">beta code done</td>

  </tr>

 </tbody>

</table>


