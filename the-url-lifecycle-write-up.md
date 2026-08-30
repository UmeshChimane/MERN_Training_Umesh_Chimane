# What happens when I type https://www.google.com and press Enter?

When I type `https://www.google.com` in the browser and press Enter, many things happen in a very short time. The browser first needs to find the server, create a secure connection, send the request, receive the response, and then display the webpage.

## 1. DNS lookup

First, the browser needs to know which IP address belongs to `www.google.com`. It checks information that may already be available in the browser or operating system cache. If the IP address is not available, a DNS lookup is performed.

The DNS server converts the domain name `www.google.com` into an IP address. Now the browser knows where it needs to connect.

If DNS fails, the browser cannot find the server's IP address. In that case, the connection cannot continue and the website will not load. The browser normally shows a DNS or "site can't be reached" type of error.

## 2. TCP connection


After getting the IP address, the browser establishes a TCP connection with the server. TCP uses a three-way handshake:

`SYN → SYN-ACK → ACK`

This makes sure that both sides are ready to communicate and that the connection is established before sending the actual application data.

## 3. TLS handshake

our URL starts with: https://

The S means the communication should be secure.

So now the browser and server perform a TLS handshake.

Because the URL starts with `https`, the communication needs to be encrypted using TLS.

During the TLS handshake, the server provides its TLS certificate. The browser checks whether the certificate is valid, trusted, and matches the website. The browser and server then agree on the cryptographic details needed to create a secure connection.

After this process, data sent between the browser and server is encrypted.

## 4. HTTP request and response

Now the browser can send an HTTP request over the secure connection. A simplified request would look something like:

`GET / HTTP/1.1`

The server receives the request and sends back an HTTP response. The response contains a status code, headers, and usually the HTML content of the page.

For example, a successful request normally returns a `200 OK` response.

Sometimes the server can return a `301 Moved Permanently` response instead. This means the requested URL has been permanently moved to another URL. The browser reads the `Location` header and makes another request to the new URL.

## 5. HTML parsing

After receiving the HTML, the browser starts parsing it. It converts the HTML into a structure called the DOM (Document Object Model).

While parsing the HTML, the browser can find other resources such as CSS files, JavaScript files, images, fonts, and other resources. These resources may require additional network requests.

The CSS is parsed into the CSSOM (CSS Object Model), while JavaScript can modify the DOM and affect how the page behaves.

## 6. Rendering the page

Finally, the browser combines the DOM and CSS information to decide what should appear on the screen.

It creates the render tree, calculates the position and size of elements during layout, and then paints the pixels. The browser may also use compositing to efficiently put different parts of the page together.

After these steps, I can see and interact with the Google webpage.

### Simple flow

`URL → DNS → IP address → TCP → TLS → HTTP → HTML → DOM/CSSOM → Layout → Paint → Screen`

