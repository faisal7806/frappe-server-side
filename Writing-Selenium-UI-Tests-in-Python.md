1. Download ChromeDriver from here : [Link](https://sites.google.com/a/chromium.org/chromedriver/downloads)
2. Extract and move / copy the binary to `/usr/local/bin/` by running `sudo cp chromedriver /usr/local/bin/.`
3. Give it perms to execute by running `sudo chmod +x /usr/local/bin/chromedriver`
4. Create a test file in the tests folder
5. Frappe has a wrapper for the Selenium Driver that you can use. You can find the functions here  : [Link](https://github.com/frappe/frappe/blob/develop/frappe/utils/selenium_testdriver.py)

```
from frappe.utils.selenium_testdriver import TestDriver

def test():

    ''' Initialize the wrapper. This will automatically create 
        a driver object with the right settings for the site that
        you want to run this for '''

    frappe_wrapper = TestDriver()

   ''' You can access the Selenium Driver by accessing the "driver" attribute '''

    frappe_wrapper.driver.maximize_window()

```
6. Run `bench execute run-ui-tests --app [app-name]` to run tests for the app 
7. You can run a specific test by using `bench execute` as well 

    