# Formalization

This file contains all the formatting rules and suggestions that must be followed throughout the entire _Zettelkasten_.
### No hierarchy filesystem
All markdown files are stored non-hierarchically; we keep them all in the same directory and link them according to their topics (either by the use of [[#linked notes]] or [[#tagged notes]])
### Each note has its own ID
Since all markdown files are stored in the same directory, it's essential that each file has a unique name. Therefore, each file must have an ID. This ID consists of the following information:
- Year
- Month
- Day
- Hour
- Minute
Following the format `YYMMDDHHmm`.
For instance `2505050138` will be the ID for a note that will be create right now at the moment of writing. That means this new note I want to create will have that ID as a prefix; imagine something like `2505050138_best-openai-models.md`.
### Rigorous note naming
Not only each note name needs to be prefixed with its ID but also it has to follow some other rules such as:
- An underscore has to separate the note's ID and its literal name.
- Spaces in its literal name has to be represented with hyphen characters.
- No uppercase letters are allowed.
- Forget about any other language more than English
- Ampersand symbol and Greek alphabet is completely allowed, however those are the only accepted ones — a part of underscore, hyphens and numbers (the use of ampersand is specially good to simplify long filenames).
### Atomized notes
To keep everything organized, it's essential that the concept of a single idea translates into a single note. This doesn't mean you can't develop or build upon your ideas; in fact, they'll all relate to each other without having to navigate a messy filesystem, allowing you to easily and accurately extract relevant topics.
### Types of notes
In a Zettelkasten notes system — at least in its classical form, we have three different types of notes:
1. **Fleeting** — Consists of temporally nature notes. Floating concepts and ideas to be developed in the future.
2. **Literature** — Notes about ideas and concepts extracted from external sources rather than you own imagination. Imagine articles, books, videos and similar resources.
3. **Permanent** — Ideas already consolidated and developed to be kept and perhaps update them in long-term future.

In order to know whatever is the nature of the note we are currently at, just notice one of their tags at the end of the file, you will see a set of words prefixed with a `#` and between all of them there might be `fleeting`, `literature` or `permanent` (or there should be). More details at [[@tags]].

In addition to this main types of notes, other useful type of notes are `moc` notes, or hub notes. These kind of notes allows you to interconnect a set of related ideas in separate notes to organize information and keep it accessible. You will notice `moc` notes doesn't have an ID but instead are prefixed with `moc_`. ^859958
### Tagged notes
To relate all the notes to each other, we'll use note tagging as a classification mechanism. Except in a few cases, we'll typically reference a specific set of tags at the end of the file by writing `#tag_name_here`.
Every time we are about to take notes regard to some new topic, it's quite important to register its tag into the [[@tags]] file. This file contains a list of all available tags in the Zettelkasten and is the decision point when starting to investigate a new topic from the whole notes.
### Linked notes
Although the note tags system allows us to classify different topics are treat regard to one note, you can also create a direct link between two particular notes by making use of the syntax `[[2505050227_my-other-note-name.md]]`. Is quite common to find a lot of direct links to other notes within `moc` notes (see [[#^859958]]).
### Markdown Attachments
Perhaps the current markdown note we're writing references external files (mostly images). All files without the `.md` extension (any file that isn't markdown), and therefore markdown attachments, should be stored in the `./media` directory.
### Notes Language
Just as happens with the filenames, the only allowed language in this whole Zettelkasten is English.