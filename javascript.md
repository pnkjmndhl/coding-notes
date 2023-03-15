### javascript promise and await
- promise
  - the promise object repesents the eventual completion or failure or an asynchronous operation and it's resulting value 


### debugging javascript in chrome
- sprinkling `console.log` is not efficient

#### inspect elements
- console
- sources
  - contains all the files for running the webpage
  - you can pause the code on certain lines (clicking the line number in the file in sources) and you can see the value of variables at that specific time (in the Local tab)
  - you can resume script execution if the values of variabels are okay

![image](imgs/chrome_debugging.jpg)

#### open dev tools (`Ctrl + Shift + J`)
-  sources panel
   -  this is where you debug javascript
   -  file navigator pane 
      -  inspect the file that it uses
      -  clicking on the file, you can see the contents of the file
   - javasdript debugging pane
     - event listener breakpoints
       - eg mouse -> click, the script excution stops at the first like code after any mouse click
     - resume script execution `F8`, resumes and continues the execution of script