# CSE 15L Lab Report 5 - Putting It All Together

Yang Hu  
3/7/2024  

### Part 1 - Debugging Scenario
1. Edstem Post  
## How to solve this bug in my grade.sh?  #321
Anonymous                                   182  
5 days ago in Lab REports                              VIEWS  
  
I got this result when I was running an implementation of ListExamples.java in `grade.sh`. Why is program stuck and no output is printed?    
![Image](bug.png)  
This is my file and directory structure:  
```
- list-examples-grader
    - lib  
      - hamcrest-core-1.3.jar  
      - junit-4.13.2.jar  
    - grading area  
    - student-submission
    - grade.sh
    - TestListExamples.java`
```

The contents of `grade.sh` before fixing the bug:  
```
CPATH='.;./lib/hamcrest-core-1.3.jar;./lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

find student-submission -type f -exec mv '{}' student-submission ';'
if [ ! -f "student-submission/ListExamples.java" ]
then
    echo "Error: ListExamples.java not found in the student submission. Please check your file name."
    exit 1
fi

cp -r lib grading-area/
cp student-submission/ListExamples.java grading-area/
cp TestListExamples.java grading-area/

cd grading-area
javac -cp $CPATH TestListExamples.java ListExamples.java
if [ $? -ne 0 ]; 
then
    echo "Error: Compilation failed. You got a 0 because of this. "
    exit 1
fi

echo "No Error: Compilation successful."


java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > junit-output.txt
lastline=$(tail -n 1)
tests=$(echo $lastline | grep 'Tests run: [0-9]+' | awk '{print $NF}')
failures=$(echo $lastline | awk '{print $NF}')
successes=$((tests - failures))

echo $lastline
echo $tests
echo $failures
echo "Your score is $successes / $tests"
```
The contents of `TestListExamples.java` before fixing the bug:  
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {

  @Test
  public void testFilter() {
      // Create a sample list
      List<String> inputList = Arrays.asList("apple", "banana", "moon", "star", "sun");

      // Create a StringChecker that checks for the word "moon"
      StringChecker isMoonChecker = new IsMoon();

      // Apply the filter method
      List<String> filteredList = ListExamples.filter(inputList, isMoonChecker);

      // Verify that only "moon" is included in the filtered list
      assertEquals(1, filteredList.size());
      assertTrue(filteredList.contains("moon"));
  }

  @Test
  public void testMerge() {
      // Create two sorted lists
      List<String> list1 = Arrays.asList("apple", "banana", "cherry");
      List<String> list2 = Arrays.asList("banana", "grape", "orange");

      // Apply the merge method
      List<String> mergedList = ListExamples.merge(list1, list2);

      // Verify that the merged list is sorted
      assertEquals(Arrays.asList("apple", "banana", "banana", "cherry", "grape", "orange"), mergedList);
  }
}
```
The full command line (or lines) I ran to trigger the bug:  
`bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected`  
My speculation would be that the JUnit test `TestListExamples.java` is not running correctly.  
Thank you!  

Comment ···  

### 1 Answer  
Yang Hu <span style="font-size:0.5">STAFF</span>  
2 hours ago  

You can start to debug this by inserting print statements in your java and bash script, especially around the output of the test!  
In bash scripts, `cat` and `echo` commands might be helpful.  

     Anonymous  
     1h  
     Now I totally get it - it was because my grep command to get $lastline was empty.  
     There are always two empty lines in the output of JUnit tests.  
     I fixed it by grabbing the line with "Test run:".  
     I edited the 34th line of `grade.sh` to `lastline=$(grep "Tests run:" "junit-output.txt")`. The fiexed `grade.sh` is shown below.  
     I also added a if-then around the final output because when all tests passed, there is no "Test run:" line in the file.  

  ![Image](bug-fixed.png) 

     Thank you very much!  
       
     Reply ···  

      

### Part 2 - Reflection  
 The most useful thing I learnt in the second half of this quarter is Java Debugger. It provides a good way to look into the buggy part of your code and to find out where your code went wrong.  
 The other thing that really helps is the practice on bash scripts. Using Bash (or the Process class in Java) gives a very flxible way to inspect and modify a file system. It was cool.



