## New Features Planned for Version 1.8

### New directory structure

The entire application (including the webnotes server-side library) will be stored in the app folder. This will be kept separate from the www folder for better security. Also all models will have a "path" instead of module that will store its model definition.

When the app will by synced, all the model definitions will be stored in an index table for easy loading, default controllers (js / py) and views will be stored in the same folder by default or as defined in the __init__.py file of that folder.

The old forced directory structure will be abandoned.

### MVC style namespaces:

Retire the earlier DOM based namespace to MVC style

### Refactor code:

Test Driven Refactoring of namespaces, and higher object orientation

### Tighter database integration:

Delegate Foreign keys, authentication, etc to database

### Separation of model and views:

Separate .model files and .view files

### Multiple views, controllers per model:

Ability to select controller based on a model attribute

### RESTful HTTP:

Use HTTP GET, PUT, POST and DELETE to manage interaction

### Refactor client side structure:

Re-design client side view management. Keep the api as much as possible similar to the server-side. Use more ready made plugins, HTML5 and other frameworks

### Lazy loading of libraries:

Improve page loading speed by lazy loading of libraries