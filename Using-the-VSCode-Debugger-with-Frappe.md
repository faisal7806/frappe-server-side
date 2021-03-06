You must have the python extension for VSCode for this to work. 

- Once you install it, go to "Open Configurations" from the "Run" menu
- Select "Python" > "Python File" (You may have to open a python file to have the "Python" option appear
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
            "console": "integratedTerminal",
            "redirectOutput": true
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
 - Edit `frappe/app.py`, in the `run_simple` method, change `use_reloader` to `False` 
 - Edit your `/etc/hosts` and add an entry for the site(s) you want to debug (do this on host machine if using Remote Development Extensions for developing inside a VM)
 - Run `bench start` in the terminal
 - Start debugging process in VSCode and wait for output to say `Running on http://0.0.0...`
 - Open your site by accessing it from your browser with the hostname you have set
 - If you see output in the "Debug Console" of VSCode, it's working!
 - DEBUG! 💃 