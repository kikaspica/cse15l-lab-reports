# Lab Report 3
## Part 1 - Bugs
Bug Chosen: issue with `reverse()` method

**1. Failure-inducing input as a JUnit test**
```
  @Test
  public void testReverse3() {
    int[] input = {3, 4, 1};
    assertArrayEquals(new int[] {1, 4, 3}, ArrayExamples.reversed(input));
  }
```
**2. Input that *doesn't* induce failure as a JUnit test**
```
  @Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }
```
**3. Symptom**
![Bug symptom](lab3Images/lab3JUnit.png)

**4. Bug: Before & After**

  Before:
  ```
  static int[] reversed(int[] arr) {
      int[] newArray = new int[arr.length];
      for(int i = 0; i < arr.length; i += 1) {
        arr[i] = newArray[arr.length - i - 1];
      }
      return arr;
  }
  ```
  After:
  ```
  static int[] reversed(int[] arr) {
      int[] newArray = new int[arr.length];
      for(int i = 0; i < arr.length; i += 1) {
        newArray[i] = arr[arr.length - i - 1];
      }
      return newArray;
  }
  ```
**5. Fix description**

This fix addresses the issue because in the old code, it was re-assigning the indexes in `arr` to values in `newArray`. However, all the indexes in `newArray` have no values in them, so the method was originally clearing out `arr` and returning it. The fix changes this by assigning values from `arr` to `newArray` backwards and returns `newArray`. 

## Part 2 - Researching Commands
**Command chosen:** `find`

(Source for all: https://linuxize.com/post/how-to-find-files-in-linux-using-the-command-line/)

**1. `-name` option**
```
   kyang@Kellys-MacBook-Air technical % find ./ -name "Media"
   .//government/Media
```
   Here, the command is finding a file named "Media" and returns the directory `Media` in the `./government` directory, which is useful for when you remember the name of a file, but not where it is.
```
   kyang@Kellys-MacBook-Air technical % find ./911report -name "*.txt" 
  ./911report/chapter-13.4.txt
  ./911report/chapter-13.5.txt
  ./911report/chapter-13.1.txt
  ./911report/chapter-13.2.txt
  ./911report/chapter-13.3.txt
  ./911report/chapter-3.txt
  ./911report/chapter-2.txt
  ./911report/chapter-1.txt
  ./911report/chapter-5.txt
  ./911report/chapter-6.txt
  ./911report/chapter-7.txt
  ./911report/chapter-9.txt
  ./911report/chapter-8.txt
  ./911report/preface.txt
  ./911report/chapter-12.txt
  ./911report/chapter-10.txt
  ./911report/chapter-11.txt
```
   Here, the command is looking for files with the extension `.txt` in the `./911report` directory, which is useful when you're looking for a specific file extension.

**2. `-type` option**
```
kyang@Kellys-MacBook-Air technical % find . -type d
.
./government
./government/About_LSC
./government/Env_Prot_Agen
./government/Alcohol_Problems
./government/Gen_Account_Office
./government/Post_Rate_Comm
./government/Media
./plos
./biomed
./911report
```
  Here, the command is looking for all directories in `./technical`, which is helpful when you want to see ONLY all the directories from your home directory.

```
kyang@Kellys-MacBook-Air technical % find ./government/Alcohol_Problems -type f
./government/Alcohol_Problems/Session2-PDF.txt
./government/Alcohol_Problems/Session3-PDF.txt
./government/Alcohol_Problems/DraftRecom-PDF.txt
./government/Alcohol_Problems/Session4-PDF.txt
```
  Here, the command is looking for all regular files in `./government/Alcohol_Problems`, which is useful when looking for only files, but not directories and other file types. 
  
**3. `-size` option**
```
kyang@Kellys-MacBook-Air technical % find ./plos -size -35k -size +34k
./plos/pmed.0020182.txt
./plos/pmed.0020045.txt
./plos/pmed.0010036.txt
```
  Here, the command is looking for files less than 35kb in size, but greater than 34kb in `./plos`. This is useful for looking for files within a certain size.

```
kyang@Kellys-MacBook-Air technical % find . -size -1k
.
./government
./government/About_LSC
./government/Env_Prot_Agen
./government/Alcohol_Problems
./government/Post_Rate_Comm
./plos/pmed.0020191.txt
./plos/pmed.0020226.txt
./911report
```
  Here, the command is looking for files with a size less than 1kb. This is useful for looking for files that are under a size cap. 
  
**4. `-mtime` option**
```
kyang@Kellys-MacBook-Air technical % find . -type d -mtime 0
.
./government
./government/About_LSC
./government/Env_Prot_Agen
./government/Alcohol_Problems
./government/Gen_Account_Office
./government/Post_Rate_Comm
./government/Media
./plos
./biomed
./911report
```
  Here, the command is looking for all directories that have been modified today, which are all of them. This is useful for finding a file you remember editing recently.

```
kyang@Kellys-MacBook-Air technical % find ./government/Alcohol_Problems -type f -mtime 0
./government/Alcohol_Problems/Session2-PDF.txt
./government/Alcohol_Problems/Session3-PDF.txt
./government/Alcohol_Problems/DraftRecom-PDF.txt
./government/Alcohol_Problems/Session4-PDF.txt
```
  Here, the command is looking for all regular files in `./government/Alcohol_Problems` that have been modified, which are all of them unfortunately. This would be useful if some files were modified later while some were modified recently. 
