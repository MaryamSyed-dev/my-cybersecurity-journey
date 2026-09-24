# OSI Model

## Layer 7 — Application Layer
The Application Layer is the top layer of the OSI model, where applications 
interact with network services. It uses protocols such as HTTP, HTTPS, FTP, 
SMTP, and DNS for different types of communication.

Example: When we enter www.facebook.com in a browser, the browser uses HTTPS 
to communicate securely with Facebook's server, which commonly listens on 
port 443. The application creates the request, while the Transport Layer adds 
the source and destination ports. The client normally uses a temporary source 
port, while the server receives the request on destination port 443. The 
server processes the request and sends a response back to the client's 
corresponding port, allowing the page to load. If the server or service is 
unavailable, or the response doesn't arrive within the timeout period, the 
browser may show a connection or timeout error.

### Protocols & Port Numbers
| Protocol | Port Number |
|----------|-------------|
| HTTP     | 80          |
| HTTPS    | 443         |
| FTP      | 21          |
| SSH      | 22          |
| DNS      | 53          |
| SMTP     | 25          |

*Note: These are common/well-known ports I've learned and can identify with 
their corresponding protocols.*

## Layer 6 — Presentation Layer
The Presentation Layer is responsible for preparing data before it's sent to 
the lower layers — formatting, encrypting, and compressing it when necessary.

**As Sender:** Data comes from the Application Layer → Presentation Layer 
translates/formats → encrypts → compresses → passes to lower layers.

**As Receiver:** Data comes from lower layers → Presentation Layer 
decompresses → decrypts → translates/formats back → passes to Application 
Layer, where the app/browser displays the original message.

**Easy way to remember:**
- Sender → Translation → Encryption → Compression
- Receiver → Decompression → Decryption → Translation

## Layer 5 — Session Layer
*(in progress)*

## Notes to self
- Continue with Session, Transport, Network, Data Link, Physical layers