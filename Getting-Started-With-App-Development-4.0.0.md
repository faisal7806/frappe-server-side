### Introduction

1. App applications are Python modules
1. Installation will by via `setuptools`
1. Apps communicate to base framework and other apps via `hooks.txt`
1. Important: DocType names and module names must be unique throughout all apps! So please check existing names before creating new apps / modules / doctypes

## Setting up the Environment

1. Setup a `virtualenv`.
1. Create your `bench` folder - which will contain the sites and apps.
1. In bench, you can create a separate folder for each app repository.
1. In bench, create a `sites` folder. This is where sites will exist.
1. Install `webnotes` and `erpnext`. For develop mode, checkout repositories in `bench` and run `python setup.py develop` in each app.
1. In create `sites/apps.txt` for list of globally installable apps.
1. For executing command line `webnotes` the working directory must be `sites`

Final Directory structure should be:

```
- bench
  + webnotes
  + erpnext
  - sites
    apps.txt
    languages.txt
    + assets
    + site1
    + site2
```

## Creating a New App

1. Add setup.py
1. Add MANIFEST.IN
1. Add README
1. Create app folder
1. Add `[app]/__init__.py`
1. Add `[app]/hooks.txt`
1. Add `[app]/modules.txt`. List of modules in the app in code format (lowercase and no spaces)
1. Add `[app]/desktop.json`. List of desktop icons for the app.

### Installing for Development

`python setup.py develop`

### Hooks

Hooks are events that are called from `webnotes` or any application. Hooks.txt is a simple key value pair, with multiple values possible per key. Hooks could be values or routes to a function name depending on what the caller will do. There is no standard for a caller.

#### Application Name and Description

- `app_name`
- `app_description`
- `app_publisher`
- `app_color`
- `app_icons`

#### Installation

- `before_install` (method)
- `after_install` (method)

#### Build Includes

There are two javascript / css builds, one for the website and one for the application interface.

#### Scheduler

To run scheduled events, add scheduler hooks

### `desktop.json`

Sample:

```
{
	"Calendar": {
		"color": "#2980b9", 
		"icon": "icon-calendar", 
		"label": "Calendar", 
		"link": "Calendar/Event", 
		"type": "view"
	}, 
}
```

## Create a Module

An app is broken up into modules. Module name must be unique across applications.

1. Add list of modules in `[app]/modules.txt`
1. Create a Module Def record (from the UI)

#### Creating a DocType

1. Create a new DocType (New > DocType)
1. When you save, a folder will be created in the module with the document (`.txt`) file and a basic controller.