# Webdav for Zotero with Docker

Note: You have to set up a server such as Nginx or Apach to handle a request. 
Since this webdav setting is for http, users will send a request to a port 80, 
and the server should pass a request to port 8080 in the host OS, then that request is again
passed to the port 80 in the Docker guest OS.


### References
- [Expand Zotero's capacity using webdav on one's own server (JPN)](https://akitoshiblogsite.com/docker-zotero-webdav/)

