Project Type Categories
 - Generative
   - The content is "generated"
     - art, text, sound, other
     - external library
       - the generative procedures are built with or depend on some library/cdn
     - built-in
       - everything needed to generate the content exists natively in the program

 - Static
   - The content is essentially hard-coded
     - remote source
       - data is being pulled from an external url 
     - local source
       - the data exists locally 
         - data is an external file (still local)
         - data is hardcoded into the program

 - Serving
   - requires a server
     - python
       - running in cloud
       - running via tunnel
     - external API
       - custom cloudflare worker
       - other API
   - does not require a server
   - can be used with/without