# **Lab Report 2**
### **Debugging step #1**
Github Diff:

![diff1](pics2/1.png)

[Failure-Inducing Input](https://github.com/atorshizi/cse15l-lab-reports/blame/main/failed%20test%201.md)

Symptom:

![diff1](pics2/1b.png)

In this case, the symptom was an exception thrown when attempting to run the file which is not what we expected since the links from the file were never printed. Looking at the test file, we can see that the failure-inducing input had an extra line of text that was not a markdown link and thus, when, in line 14, the program was searching for the next open brackets after the very last one, it could not find any so it was returning -1. When in the next lines, it tries to search for the next closed brackets, the integer -1 is given as an arguemnt which prompts it to seach for the next closed bracket from the begining of the file, and thus, everytime it gets to the end of the markdown file, it starts over causing an infinite loop and eventually prompts the exception seen as the symptom when it runs out of memory to use. The bug in this case was a missing block of code to exit the while loop which would prevent further searching if no open bracket is found. This bug (missing condition), allows the infinite loop and the exception (the symptom) to occur when the test file has a non-link text at the end (failure-inducing input).

### **Debugging step #2**
Github Diff:

![diff1](pics2/2.png)

[Failure-Inducing Input](https://github.com/atorshizi/cse15l-lab-reports/blame/main/failed%20test%202.md)

Symptom:

![diff1](pics2/2b.png)

This failure-inducing input contains some text that is not a link but has an open bracket in it. This causes the program to search for the next closed bracket which it cannot find since there are no links afterwards, and it returns -1. This causes a similar issue as the first part where -1 is given as an argument for the next method which prompts it to begin from the start of the file every time it gets to that point, causing an infinite loop which eventually means java runs out of memory and throws the exception shown. In this case, the bug is the missing block of code that prevents further seraching if there is no more closed brackets which allows the infinite loop and thus the out of memory error (the symptom) to occur when the test file (the failure-inducing input) has one open bracket and no closing ones at the end. To err on the side of caution, we added blocks of code to prevent any infinite loops from happening if there is no open or closed brackets or parenthesis.

### **Debugging step #2**
Github Diff:

![diff1](pics2/3.png)

[Failure-Inducing Input](https://github.com/atorshizi/cse15l-lab-reports/blame/main/failed%20test%203.md)

Symptom:

![diff1](pics2/3b.png)

Here, the failure-inducing input is the test file that contains an image in markdown, which is very similar to a link since the name of the image is between brackets and the link is between parenthesis. The symptom was that the link to the picture from the failure-inducing input was being added to the arrayList and printed out as if it was a link since it is formated the same as a link when it is not actually a link. The bug, in this case, was a missing block of code to differentiate between the pictures (which ends in .jpg) and the other links in the test file. Once the bug was resolved (the extra block of code was added), the program did not add the picture link to arrayList and the test file was no longer causing a failure in the program. 
