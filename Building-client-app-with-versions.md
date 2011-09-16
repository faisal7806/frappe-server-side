# Building Client Apps

wnframework uses HTML5 localStorage to store the application client-side and improve the user experience. It also uses lazy loading so that you can load the app gradually and on-demand.

## Concepts

All the js/css files are sent only once to the client (browser). If there are changes, the client maintains a version number and will supply the version number on refresh. If the version is shifted, the client will get a list of changed files that it needs to reload (on demand).

The version info is stored in the file `versions-local.db`

#### Merging with global changes

The `versions-local.db` is not a part of the repository as the developer might make many changes. So when the changes are to be committed, the have to be merged with the `versions-master.db`. This works both ways. When a new version is pulled, the changes have to merged from the master to local.

## Developer Guide

#### Get the latest changes

After getting the latest changes, the latest version info (versions-master.db) must be merged with the local (versions-local.db). So after pulling the latest changes from the git repository, run:

    python lib/wnf.py merge-local

#### Commit new changes

To commit new changes (in js/css files) to the version control, use the `wnf` utility:

    python lib/wnf.py build

#### Merge with master

Once you development is complete, you need to pull the latest `version-master.db`. Note, you *must* have the latest master and there can only be once master across all developers. To merge into master:

    python lib/wnf.py merge

#### Start a new project

Before starting a new project, you must initialize the versions-local.db:

    python lib/wnf.py setup

To setup the master for the first time,

    python lib/wnf.py setup master

## Lazy Loading

both Javascript (js) and Stylesheets (css) files can be lazy loaded:

    wn.require('lib/js/widgets/overlay.js')

Once the object is lazy loaded, it is not re-loaded untill you commit a new version.
    python wnf.py setup_master
