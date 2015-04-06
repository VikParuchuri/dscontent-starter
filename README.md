Overview
-----------------

Starter content for [Dataquest](www.dataquest.io).

How to use
-----------------

## Authoring content

Fork this repo to start working on your own content.

After you've forked it:

* Clone your fork locally (`git clone YOUR_FORK_URL`)
    * `cd dscontent-starter` to move into the folder.
* Install the python packages in requirements.txt. (`pip install -r requirements.txt`)
    * This should ideally happen in a virtualenv, but it's not strictly needed.
    * Dataquest uses python 3, and that is the version you should use.  We're exploring python 2 support for the future.
    * If the install fails, you may need to install numpy before installing the rest of the requirements (`pip install numpy==1.9.1`)
* Run ipython notebook (`ipython notebook`).
* In your web browser, navigate to `127.0.0.1:8888`.
    * Open `Mission1.ipynb` and `Mission2.ipynb`.
    * Look through the structure of the notebooks.
* Either make your own notebook in the same directory, or edit the existing ones to make new content.
* Put any files you need to open in the missions into the root of the directory (same level as the notebooks).

### Linking the repo

To upload content, first visit [Dataquest](https://www.dataquest.io) and make an account.  Once you have an account:

* Visit the [course creator](https://dataquest.io/creator/github_link) and link your github account.
    * You'll be redirected to the github site, where you'll need to login.
* Link the repo you forked to dataquest on [this](https://dataquest.io/creator/github_link) page.
* Now, you can sync and test missions.

### Uploading content

After you linked your repo, you can upload and test content.

* Commit your local repo changes and push them to github.
    * `git add .`
    * `git commit -m "Added more content"`
    * `git push origin master`
* Now, run `dqauthor sync` -- this will let you pick the repo to sync, and then will pull the changes over to dataquest.
    * If this fails, your notebooks may not be structured properly.  Look at the error messages and retry.
* Run `dqauthor test` to test your mission to see if everything works properly.
    * If you see any errors, fix them before publishing.
* If you want to see how your missions look, or publish them live, visit [the sync page](https://dataquest.io/creator/sync_missions).


Structure of missions
------------------

This repo contains two mission files, `Mission1.ipynb` and `Mission2.ipynb`.  The first has examples and comments embedded that explain the various sections.  The second is an example of a real mission.

## Mission format

### Mission format

Each mission file is composed of multiple ipython notebook cells.  The first cell contains mission metadata, and should be a markdown cell.  The very first line contains extended metadata fields that shouldn't be normally displayed.  These fields are wrapped in an html comment, so they don't show up in the notebook.  Ensure that your metadata also looks like this: `<!-- mission_number=1 file_list=['test.txt', 'crime_rates.csv', 'titanic_survival.csv'] mode="multiscreen" -->`.

Extended metadata fields:

* `mission_number` -- a locally unique id indicating the number of the mission.  Once set, this shouldn't be changed.
* `prerequisites` -- List of integers (mission numbers) that are prerequisites.
* `language` -- programming language used (only python support now)
* `premium` -- True/False indicating whether or not mission is premium content.
* `under_construction` -- True/False indicating whether mission is being built, or is done.
* `file_list` -- list of files you want to reference in the mission.  These files should be in the root directory (where the notebooks are).  Don't specify a path, just a filename.
* `mode` -- either `singlescreen` for a scrolling interface, or `multiscreen` for an interface where each screen is shown separately.

After the extended metadata, three lines tell us the name of the mission, the description, and the author.  The name line starts with `#`, and the other two start with `##`.  Here's an example:

```
<!-- mission_number=1 file_list=['test.txt', 'crime_rates.csv', 'titanic_survival.csv'] mode="multiscreen" -->

# New Mission
## This is a new mission.  Edit these fields to customize the display.
### Author Name Here
```

### Screen format

After the mission cell, we get to screens.  Screen can either be code screens, or video screens.  

Screens all start with a markdown cell.  The first line of the markdown cell should be extended metadata.  It should look like this: `<!-- type="code" -->`.

Extended metadata fields:

* `type` -- `code` or `video`.

After the extended metadata, the next line should be the name of the screen, preceded by `#`.  Example:

```
<!-- type="code" -->

# Intro Code
```

If you have a video screen, you're almost done.  Just add a link to the video below the name:

```
<!-- type="video" -->

# Intro

http://youtu.be/kDDiR7TDGw0
```

If you have a code screen, after the name should come a few lines introducing the screen, and providing any needed background.

```
<!-- type="code" -->

# Intro Code

This is where the text that goes in the left panel of the code screen is written.

This text is used to introduce the screen, and describe any background
information needed.
```

If you want students to provide an answer, you'll need to add the `## Instructions` and `## Hint` sections after this.

```
<!-- type="code" -->

# Intro Code

This is where the text that goes in the left panel of the code screen is written.

## Instructions

Assign `20` to the variable `c`.

## Hint

Check that `c` is defined.
```

Code screens also have a code component.  You'll need to make another cell after your markdown cell, which should be a code cell.

This cell has a few sections:
* `Initial` -- any code you want to run before the submitted code.  This will not be visible to learners.
* `Display` -- the code that is first displayed to someone seeing the screen.
* `Answer` -- the code for the answer.
* `Check vars` -- variables that should be checked for in the submitted solution.  The values will be compared between the `answer` code and the submitted code.
* `Check val` -- code output that should be checked for in the student solution (only one of `check vars` or `check val` is needed).
* `Check code run` -- this should be used very rarely, but you can define a function to check the correctness of a submission if you need to.  `Check vars` should be defined if this is provided.  Any variables in `check vars` will be passed to this code at runtime.

Here's a sample code cell:

```
## Initial

import pandas
    
## Display

import numpy as np

## Answer

a = 50

## Check vars

['a']

```

The only required field is `Display`.  If you provide an `Answer`, then you must provide either `Check vars` or `Check val`.

Each mission can have as many screens as you want.

Caveats!
--------------------

We're always iterating dataquest to make it easier to develop content for, but there are a few important caveats for now:

* Instances of custom classes can't be passed between screens in singlescreen mode.
    * You'll need to use the "Initial" section to recreate the instance in subsequent screens.
* Custom classes can't be checked for correctness.  There isn't a workaround to this right now.
* The "Initial" section is carred to subsequent screens.  This means that you don't need to keep adding the same code to the initial section.
* In "multiscreen" mode, each screen (aside from the Initial section) is self-contained, and won't receive variables from previous screens.
    * Thus, something that works in ipython notebook may not work in multiscreen mode.
* The only available packages are the ones in requirements.txt.
    * We're working on support for custom packages and versions.
* Files shouldn't be larger than ~2MB -- any larger makes the execution take too long, and reduces student experience.

Generated yaml files
---------------------

Running `dqauthor generate .` will generate yaml files from any notebooks in the current directory.  Dataquest uses yaml as its internal file format, so this is a needed step before importing missions into dataquest.

Running the command will make a folder called `missions` (if it doesn't exist already), and make a separate folder inside for each mission.  Each mission folder will have a `.yaml` file containing its definition, as well as any resource files needed for the mission.

This is automatically done when syncing, so you don't need to run it yourself, but it can be a good debugging check to make sure your missions are structured properly.


Removing content
-------------------

To remove content, first delete the notebooks you don't want.  Make sure that *mission numbers* are all unique.

Then, delete any generated mission folders in `mission` for those notebooks.

The sections.json file
--------------------

The `sections.json` file is useful if you're running a dataquest server locally and want to add new content.  If you aren't, it's safe to ignore this file for now.

Eventually, this will be used to create courses that are sequences of lessons.