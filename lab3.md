# Lab Report 3
## Part 1 - Bugs
Bug Chosen: issue with `reverse()` method
1. Failure-inducing input as a JUnit test
```
  @Test
  public void testReverse3() {
    int[] input = {3, 4, 1};
    assertArrayEquals(new int[] {1, 4, 3}, ArrayExamples.reversed(input));
  }
```
2. Input that *doesn't* induce failure as a JUnit test
```
  @Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }
```
3. Symptom

4. Bug: Before & After

**Before:**
```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
}
```
**After:**
```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
}
```
