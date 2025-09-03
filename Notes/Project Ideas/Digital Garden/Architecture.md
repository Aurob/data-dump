## Data Store:

1. Notion
    1. This will be my main tool for note writing
    2. Make everything public by default
        1. or at least visible to the API connection
    3. Use Python API to make a custom wrapper around the Notion API
        1. Group everything into a parent → child hierarchy
        2. Might need to write a custom scraper because trying to rebuild a notion page is a pita.
2. Git (GitHub)
    1. Will be used more as a personal journal
    2. Private repo
    3. Just like for Notion, use Python to make an API wrapper to list the contents of the repo
        1. Implement an oauth step so only I can view it on the web after logging in
            1. maybe consider using Cloudflare authentication
                1. I may need to add [https://rau.wiki](https://rau.wiki) to Cloudflare, otherwise I’ll have to use [https://rau.dev/login](https://rau.dev/login) for auth, which may cause cross-site cookie issues
        2. allow for some kind of tagging system so I can make certain files public without logging in
3. Cloudflare R2
    1. I will use R2 like a CDN. I’ll store code libraries, config files, general data dumps, etc..
        1. A kind of data lake meant to be used for the [[Digital Garden]] project and any adjacent project it spawns

## Interface:

1. Notion
    1. Web
    2. Mobile App (any platform)
2. Git
    1. GitJournal (Android)
        1. Any app that connects to a git repo and acts as a journal/note taking app
    2. Custom Web UI
        1. HTML/JS Front-end
        2. Python API back-end
    3. CLI