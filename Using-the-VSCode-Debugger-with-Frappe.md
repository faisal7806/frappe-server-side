You must have the python extension for VSCode for this to work. 

- Once you install it, go to "Open Configurations" from the "Debug" menu
- Add the below to the list : 
- Make sure your workspaceRoot (The folder that's opened in VSCode) is the apps folder
```
        {
            "name": "Frappe",
            "type": "python",
            "request": "launch",
            "stopOnEntry": false,
            "pythonPath": "${config:python.pythonPath}",
            "program": "${workspaceRoot}/frappe/debug.py",
            "cwd": "${workspaceRoot}",
            "debugOptions": [
                "WaitOnAbnormalExit",
                "WaitOnNormalExit",
                "RedirectOutput"
            ]
        },
```
 - Open VSCode Settings
 - Set the PythonPath Variable to the absolute path of python INSIDE the frappe-bench env. For example, mine looks like this : 
```
    "python.pythonPath": "/Users/vjfalk/frappe-develop/env/bin/python",
```
 - Create a file in the frappe folder called `debug.py`
 - In the file, add the below : 
```
import frappe.app

frappe.app.serve(port=<The port of your bench, usually 8000>, sites_path='<Absolute Path to the sites folder in your bench>')
```
 - Edit the Procfile inside your bench, and remove the line that starts with `bench serve`
 - Run `bench start` in the terminal
 - Start debugging process in VSCode and wait for output to say `Running on http://0.0.0...`
 - You should be able to debug your Frappe applications!