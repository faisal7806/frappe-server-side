# Caching Records in Browser

Use localStorage to store documents in the browser and periodically refresh updates from the server.
#Hard problem, from my skimming. different browsers, different ways. docs.google.com uses it on chrome for sure though.

## Design

- On the server, every-time a doc is updated, it must be logged in the cache logger and must get a unique number
- Only parent and readable docs to be logged

## Implementation

### Client

Client will have a DocumentStore that will expose the cache API:

Return a doclist of the given doc, either from local or server:

    wn.docstore.get(dt, dn) - synchronous ajax call

Check the server for updates:

    wn.docstore.refresh()

Clear a particular item from the docstore:

    wn.docstore.clear(dt, dn)

Load a from server:
 
   wn.docstore.load(dt, dn)

Version:

    wn.docstore.version

### Server

The server must log updates (modifications to existing docs):

    webnotes.model.update_log.log(dt ,dn)

Keep a version number:

    webnotes.model.update_log.get_updates('update_version')

returns a list of updates [[dt, dn], [dt1, dn1], ..]

Handle requests from the client 

### Implemetation

1. implement `wn.docstore` on client side
2. implement `webnotes.model.update_log` on server side

### Pulling from db

When the git version is changed, there can be 2 options - either all (doctypes) can be re-loaded, or we need to maintain a list of doctypes that have been changed from the last version.

This can be kept in versions-local.db (timestamps). If the timestamps of the txt files have been changed, when merge-local is called, it will also log all timestamp changes in doctype (txt) files

This needs to be done in "all" databases in a multi-tenant system. - or there needs to be a push mechanism for multi-tenant system based