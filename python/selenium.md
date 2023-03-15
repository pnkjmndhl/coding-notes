### Automating web browsing with selenium
```py
from selenium import webdriver
driver = webdriver.Chrome()
driver.get(Url)
```
- get the *xpath* using the selenium browser -> inspect element
- entering values and clicking a button
```py
# entering values in a msg box
messageField = driver.find_element_by_xpath(*xpath*) # use the xpath copied from the selenium browser
messageField.send_keys("Hello World")
# clicking a button
showMessageButton = driver.find_element_by_xpath(*xpath*)
showMessageButton.click()
```
- dragging and dropping (practice using [dhtmlgoodies](http://dhtmlgoodies.com))

```py
from selenium.webdriver.common.action_chains import ActionChains

source = driver.find_element_by_xpath(*xpath*)
destination = driver.find_element_by_xpath(*xpath*)
actions = ActionChains(driver)
actions.drag_and_drop(source,destination).perform()
```

- wait functions
- explicit and implicit wait
```py
from selenium.webdriver.common.by import By
from selenium.webdriver.suppoert.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10) # throws an exception after 10 seconds
launchEarthButton = wait.until(EC.element_to_be_clickable((By.XPATH, *xpath*)))
launchEarthButton.click()
```