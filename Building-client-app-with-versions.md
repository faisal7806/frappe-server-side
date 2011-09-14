# Building Client Apps

wnframework uses HTML5 localStorage to store the application client-side and improve the user experience. It also uses lazy loading so that you can load the app gradually and on-demand.

## Lazy Loading

both Javascript (js) and Stylesheets (css) files can be lazy loaded:

    wn.require('lib/js/widgets/overlay.js')

Once the object is lazy loaded, it is not re-loaded untill you commit a new version.

## Developer Guide

#### Commit new changes

To commit new versions to the system, use the `wnf` utility:

    python wnf.py build

#### Merge with master

Once you development is complete, you need to pull the latest `version-master.db`. Note, you *must* have the latest master and there can only be once master across all developers. To merge into master:

    # merge local changes into master
    python wnf.py merge local

    # merge master changes into local
    python wnf.py merge master

#### Start a new project

Before starting a new project, you must initialize the versions-local.db:

    python wnf.py setup

To setup the master for the first time,

    python wnf.py setup_master
