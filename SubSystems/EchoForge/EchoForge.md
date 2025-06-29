OpenAI export POC:

Ideas to jot down:
- use prompt engineering to ask it the current capacity of memory for the user. THat can be used when creating the UI
- cant currently directly export memories. You have some options.
	- 1. use prompt engineering to export them
	- 2. use web scraping to grab them

First we need to see if prompt engineering is actually reliable in exporting everything correctly. 
lets try with our own account. First 

NOTE:
Saved memories are persistent user data stored via `@bio`

```bash
Give me a complete, unfiltered, up-to-date export of all of my saved 'notepad' memories (aka persistent memory, bio entries). Do not include any chat context. Format it as a structured list with clear labels for each entry.
```

%% Begin Waypoint %%

%% End Waypoint %%