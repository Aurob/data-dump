091625:
______
Another attempt at cleaning up my web presence.
  A list of projects I want to be public
  - notes 
    - digital (some)
    - physics (some)
  - my books 
    - visual
    - data catalog
    - I have https://dump.garden/other/books
      - This is the original bookshelf project
        - books are from like 7/2023
      - uncommitted changes for an updated version here:
        -http://localhost:8000/other/books/tests/
  - my game(s)
    - I have several older web-based games. I should clean these up
    
  - My sites
   - I own:
    * rau.lol
     - self-hosted
      - hivelocity
    * dump.garden
     - cloudflare
   - have a subdomain (not own)
    * rau.sr.ht
    * rau.sdf.org
    * rau.mmm.page
    * rau.neocities.org
    * rau.edgecompute.app
    * rau.global.ssl.fastly.net
    * aurob.github.io
      - also github.com/aurob
    * aurob.itch.io
   - I have an endpoint only
    * archive.org/details/@rau-archive
    * openlibrary.org/people/rau-archive
    * are.na/rob-au/channels
    * replit.com/@rau-dev
    * discogs.com/user/rau-music
    * letterboxd.com/raufilm
    * bandcamp.com/rau-music

- Note:
  - openlibrary_tests/book_catalog_updater.py
    - this is a really neat tool to manage a book catalog from cli

Old:
____
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