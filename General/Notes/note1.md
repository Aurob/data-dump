data-dump:
	password protect web portal at dump.garden?
	fix action to dump contents in Wasabi

data-lake:
	add directory-level metadata
	add manual summary/tagging
	organize all scripts into category directories
	  - apply directory and file-level summaries
	web portal
	  - for uploading data
	  - maybe a full Drive-like interface for upload/update/delete
	setup book catalog pipelin
	make a task/todo system with reminders
    add pipeline for the AI conversation extracts for chatgpt/claude/gemini
sdf.org:
	fix home page
	think about ways to use the email
other:
	Web link Spaced Repetition system
	  - put all links into a srs like Anki
	  - consider auto-creating cards for links
	    - LLM-based summary/tags
	Revisit GBA dev/emulation

Finish Espedair Street
Keep reading game-sense and wgcbp and free/style
read more and think about matrix (protocol)


Project
 - Use an S3-compatible storage bucket to hold files
   - upload project files from desktop/laptop/cloud
   - create a metadata file/db to track each file and directory
   - use this metadata to populate other sub-projects

Sub-projects
 - Staging Interface
   - Need some kind of UI to be able to manage the metadata of the lake
     - not the underlying files, but just the metadata
     - So that I can modify entries, add/remove them, create new ones
     - maybe use it for running pipelines, even the jupyterlabs UI might work
 - URL Summarizing/Tagging
   - includes: Any file with a url as a title/key or has urls in the content
   - create metadata for each link as if it were a file
     - create metadata for summary and tag separatly and link to the link metadata
   - use ai to create summaries and lists of tags for a given url
   - add other metadata properties like read/unread for tracking articles or stories I want to read
 - TODO tracker
   - includes: files with certain flags in the title or in the content
     - Similar to the links, find instances of certain flags like '#TODO' or similar
       and create metadata entries in the lake with the todo statement/task
     - create a system to then track these todos and put them into something like
       https://jrnl.sh/ or todo.txt
     - connect this system to some kind of notification system either via email or push systems (gotify)
     - some kind of UI to easily track the todo items, possibly even something like trello or slack to be
       able to manage (create/update/delete) todos, ideally grouping and like status/priority/points stuff
 - Reminder
   - similar to the TODO tracker where certain flags will add a reminder to the system
   - maybe could just merge the 2 into one pipeline
 - Spaced-Repitition
   - I want to be able to create "cards" in an SRS system
   - AI generated, but maybe have a way to create custom ones directly
   - Could utilize the link metadata summaries to instruct an AI to generate content from them
   - maybe use the deep-research models from oai and google
 - Prompts
   - Allow for any number of files/metadata to be passed to an AI model
     - the content will be used as the prompt, the output will be stored in the lake and linked to the original prompt(s)/metdata(s)


make a webpage to list all the links/bookmarks that you both visit regularly(reddit, x, youtube), sites you don't visit too often but may have personal data to add to the lake (are.na, letterboxd, AI, other), and sites I want to retain for reading or for reference or any other reason.
use the site as llike a landing page for both ease of access of common sites, but also to remember sites I may have not visited in awhile and to have a place to see all the sites I've bookmarked but have not visited.
add an identifier to see whi h sites I use to populate the lake.
add a backend feature to track when I access a link so that I can sort the links by those I haven't visited or haven't in awhile.
add a link for the data sites that will take me to a display of all that data in the lake.