# CSE 15L Lab Report 5 - Putting It All Together

Yang Hu  
3/7/2024  

### Part 1 - Debugging Scenario
1. Edstem Post  
## How to solve this bug in my grade.sh?  #321
Anonymous                                   182  
5 days ago in Lab REports                              VIEWS  
  
I got this result when I was running a correct implementation of ListExamples.java in `grade.sh`. Why is the score not correct?    
![Image](bug.png)  
My speculation would be that the test is not running correctly. 
Thank you!  

Comment ···  

### 1 Answer  
Yang Hu <span style="font-size:0.5">STAFF</span>  
2 hours ago  

You can start to debug this by inserting print statements in your java and bash script, especially around the output of the test!  

     Anonymous  
     1h  
     Thank you very much!  
  
     Reply ···  
2. Set up  
file structure:  
  - list-examples-grader
    - lib  
      - hamcrest-core-1.3.jar  
      - junit-4.13.2.jar  
    - grading area  
    - student-submission
    - grade.sh
    - TestListExamples.java
      

### Part 2 - Reflection  
 The most useful thing I learnt in the second half of this quarter is Java Debugger. It provides a good way to look into the buggy part of your code and to find out where your code went wrong.  
 The other thing that really helps is the practice on bash scripts. Using Bash (or the Process class in Java) gives a very flxible way to inspect and modify a file system. It was cool.



