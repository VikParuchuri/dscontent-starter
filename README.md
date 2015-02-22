Overview
-----------------

Starter content for [Dataquest](www.dataquest.io).

How to use
-----------------

Fork this repo to start working on your own content.

Structure
------------------

This repo contains two mission folders, `1` and `2`.  The first has examples and comments embedded that explain the various sections.  The second is an example of a real mission.

Each folder has one *mission outline* (a .yaml file), and potentially some *resource files*, which are used in the coding exercises in that outline.

Adding content
-----------------

* Make a new folder, with a number one higher than the highest existing folder number.  This is a *mission folder*.  The name is the *mission number*.  The number has to be unique.
* In that folder, make a file called `{MISSION_NUMBER}.yaml`.  This is a *mission outline*.  {MISSION_NUMBER} should be the same number as the folder name.
* Develop the outline.
    * Read through the outline to see how content is structured.  The top section is the metadata, and every section below is a screen, starting with the first, then the second, and so on.  The section separator is 4 or more dashes (----).
    * Mission metadata fields:
        * `name` -- Name of the mission (user visible)
        * `description` -- Description of mission (user visible)
        * `author` -- The first and last name of the person who made the mission (user visible)
        * `prerequisites` -- List of integers (mission numbers) that are prerequisites.
        * `language` -- programming language used (only python support now)
        * `premium` -- True/False indicating whether or not mission is premium content.
        * `under_construction` -- True/False indicating whether mission is being built, or is done.
        * `file_list` -- list of files you want to reference in the mission.  These files should be in `missions/data/resources`.  Don't specify a path, just a filename.
        * `mission_number` -- the number of the mission.  This should be the same as the folder name and the start of the outline name.
        * `demo` -- whether or not the mission is a demo with a few screens instead of a whole mission.
        * `imports` -- code to run before computing the variable sets.
        * `vars` -- code for the variable sets.
    * Screen fields:
        * `name` -- Name of screen (user visible)
        * `type` -- Screen type, currently `video` or `code`.
        * See the files for the rest of the fields.
* Put any .csv, .txt, or .db files you want to access in the mission into the *mission folder*.
    * You can refer to these in your solvers by name -- you don't need a path.
    * If you need a different file type, contact vik@dataquest.io.

Removing content
-------------------

To remove content, just delete the folders you don't want.  Make sure that *mission numbers* are all unique.

The sections.json file
--------------------

The `sections.json` file is useful if you're running a dataquest server locally and want to add new content.  If you aren't, it's safe to ignore this file.