# Lab Report 5
## Part 1 - Debugging Scenario
### Original Post
When I run my grade.sh, I get this error. 

Command Ran: `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-lab3`
![Original bug](lab5Images/bug.png) 

Here is my file and directory structure:

![File Structure](lab5Images/structure.png) 

My `grade.sh` file is written as such (BEFORE DEBUG):
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

# Step 2 -- Check that the student code contains ListExamples.java
if [[ -f student-submission/ListExamples.java ]]; then
    echo "File Existed"
else
    echo "ListExamples.java does not exist"
    echo "Grade: 0"
    exit 1
fi

# Step 3 -- Put all the relevant files in the grading-area directory
cp student-submission/ListExamples.java TestListExamples.java grading-area
cp -r lib grading-area

# Step 4 -- Compile the java files and check that they compiled successfully
cd grading-area
javac -cp $CPATH ListExamples.java TestListExamples.java

echo "This is the exit code of javac (previous command): $?."


# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests

if [ $? -ne 0 ] 
then
    echo "Compilation error!"
    exit 1
fi


echo "Program complied successfully"


java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > junit-output.txt

outputLast=$(cat junit-output.txt | tail -n 2 | head -n 1)
tests=$(echo $outputLast | awk -F'[, ]' '{print $3}')
fail=$(echo $outputLast | awk -F'[, ]' '{print $6}')
success=$((tests - fail))
score=$((success/tests))

echo $outputLast
echo "Score: $score%"
```

And my code for `TestListExamples.java` is as follows (BEFORE DEBUG):
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
  public void testSimpleFilter() {
    StringChecker checker = new IsMoon();
    List<String> input = Arrays.asList("hello", "MOON", "hey", "moonnnn");
    List<String> expected = Arrays.asList("MOON");
    assertEquals(expected, ListExamples.filter(input, checker));
  }
}
```
The student submission I used to run with `grade.sh` should be passing this test and it should have a score of 100%.

### TA Response
Hello! Looking at the error message you're getting, it seems the problem is in lines 52 and 53 where you declare your `success` and `score` variables. Try using `echo` around those two lines to see the values of the variables you're using in those lines. One of the variables you're using might not be initialized.
