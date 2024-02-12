# CSE 15L Lab Report 3 - Bugs and Commands

Yang Hu\\
2/8/2024

### Part 1 - Bugs

Here I will take the bug in `reverseInPlace` method in `ArrayExamples.java` from Lab 4 activities.\\
1. failure-inducing input for the buggy program
```
  @Test
  public void testReverseInPlace2() {
    int[] input = {1,2,3};
    int[] expected = {3,2,1};
    ArrayExamples.reverseInPlace(input);
    assertArrayEquals(expected, input);
  }
```

2. input that doesn't induce a failure 
```
public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input = {1};
    ArrayExamples.reverseInPlace(input);
    assertArrayEquals(new int[]{1}, input);
	}
```

3. the symptom 


4. the bug

### Part 2 - Researching Commands
The options of command `grep` :

