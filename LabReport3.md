# Lab Report 3
---

Part 1
---

Failure-inducing input:
``` 
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 1,2,3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 1,2,3 }, input1);
	}
```

Successful input:
```
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
```
The symptom:
With the failure-inducing input:
![image](Failed_JUnit.jpg)

With the successful input:
![image](Successful_JUnitTest.jpg)


Part 2
---

