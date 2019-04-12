# Adding a Doc to Desk Module

Lets see how we can add a DocType link in a Module Grouping section.


## 1. Create a desk.py file

In your `app->module->config` folder, create a desk.py file.

## 2. Add a get_data function
Create a `get_data` function which will return mapping between doctype links and module grouping.

```
from __future__ import unicode_literals
from frappe import _


def get_data():
    return [
        {        }
    ]
```

## 3. Return doctype mapping with the module grouping

For Example you want to map a custom **Meeting** doctype in the **Tools** module in the desk. The JSON mapping would look something like this:

```
    {
            "label": _("Tools"),
            "icon": "octicon octicon-briefcase",
            "items": [
                {
                    "type": "doctype",
                    "name": "Meeting",
                    "label": _("Meeting"),
                    "description": _("Arrange meetings within Organisation"),
                    "onboard": 1,
                    }
            ]
        }
``` 
## 4. Example

Finally the `desk.py` of your app would look something like: 

```
from __future__ import unicode_literals
from frappe import _


def get_data():
    return [
        {
            "label": _("Tools"),
            "icon": "octicon octicon-briefcase",
            "items": [
                {
                    "type": "doctype",
                    "name": "Meeting",
                    "label": _("Meeting"),
                    "description": _("Arrange meetings within Organisation"),
                    "onboard": 1,
                    }
            ]
        }
    ]
```

# Using the Calendar View

Let's see how we can use the Calendar view to the mark your documents with regards to date field on the calendar view.


## 1. Create a Calender View JS File

In you doctype folder (App->Module->Doctype->Doctype folder->) create a .js file with suffix `_calendar.js`. For example the name of your doctype is **Meeting**, create a file `meeting_calendar.js`. 

## 2. Calender View Settings

Now start enterting the calendar settings:

```
frappe.views.calendar["Meeting"] = {
        field_map: {},
        options:{},
	get_events_method: ""
}
```
where: 

- field_map: is the mapping between the settings fields of the calendar component and the fields returned from the API method as a dictionary. Example start in calendar view component if to me mapped with 'from_time' for key coming from API method, map the field as {start:from_time}.
- options: Display Options for the Calendar view component.
- get_events_method: Server side method to be invoked. Generally it should be whitelisted API method written in the module of your appication.

## 3. Example

An Example code for the putting the meeting docs on the calendar view. 

```
frappe.views.calendar["Meeting"] = {
        field_map: {
            "start": "start",
            "end": "end",
            "id": "name",
            "title": "title",
            "allDay": "all_day"
        },
	get_events_method: "meeting.api.get_meetings"
}
```

For API code refer [Frappe Meeting App Example Code here](https://github.com/frappe/meeting).

# Assigning status indicator colors in the list view

Lets take an example how we can assign indicator colors in list view for different status values of a document.

Consider for example, **Meeting** doctype has following status values:

1. Planned
2. Invitation Sent
3. In Progress
4. Completed
5. Cancelled

Lets see how we can assign different colors in the list view for these statuses. 

## 1. Create a list view JS file
Similar to calendar view discussed above, create a meeting_list.js file.

## 2. Add List view setting for indicator

Now let the listview setting have the indicator option:


```
frappe.listview_settings['Meeting'] = {
    get_indicator: function(doc) {
        return [status, color];
        }
};
```
## 3. Example

Lets see an example mapping of the indicator color and the document status:

```
frappe.listview_settings['Meeting'] = {
    add_fields: ["status"],
    get_indicator: function(doc) {
        return [__(doc.status), {
            "Planned": "blue",
            "Invitation Sent": "orange",
            "In Progress": "red",
            "Completed": "green",
            "Cancelled": "darkgrey"
            }[doc.status]];
        }
};
```