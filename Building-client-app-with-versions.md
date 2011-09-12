# Building Client Apps

wnframework uses HTML5 localStorage to store the application client-side and improve the user experience. It also uses lazy loading so that you can load the app gradually and on-demand.

## Lazy Loading

both Javascript (js) and Stylesheets (css) files can be lazy loaded:

    wn.require('lib/js/widgets/overlay.js')

Once the object is lazy loaded, it is not re-loaded untill you commit a new version.

## Committing new versions

To commit new versions to the system, use the `wnf` utility:

    ./wnf add path/to/myfile
    ..
    ./wnf commit

To search and commit:

    ./wnf commit -a

To find changes:

    ./wnf diff

Once you development is complete, you need to pull the latest `version-master.db`. Note, you *must* have the latest master and there can only be once master across all developers. To merge into master:

    ./wnf merge master

This will merge the master version db both ways (new commits from elsewhere will also be pulled)

To reset version control (sends a signal to the client, to clear localStorage):

    ./wnf version reset