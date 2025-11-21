Current note taking setup:
 - Git repo via vscode.dev
 - handwritten notes
 - google task reminders on my phone

Ideas:
 A. use sr.ht pastes
 B. sync google task (if possible)
 C. setup scanning auto-sync 
 D. git repo with more automations

Current:
 - I currently have 3 main purposes for "note taking"
    1. simple notes similar to what I'm doing now
    2. reminders
        - things I actually want "pushed" to me to catch my attention and remind myself about
        - currently only done via google tasks on my phone
    3. bookmarks
        - webpage links
        - or even just simple lists like movie/show/books without any link

Goal:
 - I like using a git repo as my central "dump"
 - but I don't think I really like using github for it
   - I could use sr.ht but still basically the same as its a third-party
 - I could self-host the repo on my server and then maybe sync it with an S3 bucket
   - Though this does add complexity, using a git site really simplifies

 - I do like being able to just go to vscode.dev and instantly be able to start adding notes
   - but also that requires logging in, I'd like an even quicker method
   - thought I'd have to be careful that it isn't public, so I'd still need some kind of auth setup
     - thus a single repo in github really simplifies it

 - Using github requires that I commit and push for every single addition
   - I would have to write a custom app to bypass that

 - Maybe the current setup I have for notes is fine, but reminders still needs work
 - How would I want to be "reminded"?
   - push notifications
     - phone
     - computer (laptop/desktop)
       - desktop notifications
       - browser notifications
     - email
     - print
     

Maybe do another restructuring of the dump repo
 - Lists
   - this is where I'll put my bookmark links and general non-link lists
 - Reminders
   - anything in this section will go into the reminder system
     - might need a way to specify timing/frequency
       - and potentially a way to auto-update the note when I want to remove the reminder but maybe not the actual content
 - General
   - everything else, ie just general notes

   