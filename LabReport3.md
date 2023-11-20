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
__The symptom:__  

__With the failure-inducing input__
![image](Failed_JUnit.jpg)

__With the successful input:__  
![image](Successful_JUnitTest.jpg)

__The bug:__  

__Before:__  
```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

__After:__  
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      int holder = arr[i];
      arr[i] = arr[arr.length - i - 1];
      //we need to swap 
      arr[arr.length - i - 1] = holder;
    }
  }
```

Part 2: Researching "find"
---

Sources:   
https://man7.org/linux/man-pages/man1/find.1.html   
https://www.youtube.com/watch?v=KCVaNb_zOuw&ab_channel=CoreySchafer

___"-name"___:   
**Example 1:**   
```
$ find -name "*.java"
./DocSearchServer.java
./Server.java
./TestDocSearch.java

```

**Example 2:**   
```
$ find -name "*.txt"
./biomed-sizes.txt
./find-results.txt
./grep-results.txt
./plos-sizes.txt

```   

The "-name" allows us to search for certain words in the name of the file. Above you can see the command and the resulting outputs right below each command.   

___"-type"___:   
**Example 1:**   
```
$ find -type d
.
./.git
./.git/hooks
./.git/info
./.git/logs
./.git/logs/refs
./.git/logs/refs/heads
./.git/logs/refs/remotes
./.git/logs/refs/remotes/origin
./.git/objects
./.git/objects/info
./.git/objects/pack
./.git/refs
./.git/refs/heads
./.git/refs/remotes
./.git/refs/remotes/origin
./.git/refs/tags


```

**Example 2:**   
```
$ find -type f
./.git/config
./.git/description
./.git/HEAD
./.git/hooks/applypatch-msg.sample
./.git/hooks/commit-msg.sample
./.git/hooks/fsmonitor-watchman.sample
./.git/hooks/post-update.sample
./.git/hooks/pre-applypatch.sample
./.git/hooks/pre-commit.sample
./.git/hooks/pre-merge-commit.sample
./.git/hooks/pre-push.sample
./.git/hooks/pre-rebase.sample
./.git/hooks/pre-receive.sample
./.git/hooks/prepare-commit-msg.sample
./.git/hooks/push-to-checkout.sample
./.git/hooks/update.sample
./.git/index
./.git/info/exclude
./.git/logs/HEAD
./.git/logs/refs/heads/main
./.git/logs/refs/remotes/origin/HEAD
./.git/objects/pack/pack-f83b5301734bdfa3e9958e8f4887d80e5c1a51f9.idx
./.git/objects/pack/pack-f83b5301734bdfa3e9958e8f4887d80e5c1a51f9.pack
./.git/packed-refs
./.git/refs/heads/main
./.git/refs/remotes/origin/HEAD
./biomed-sizes.txt
./count-txts.sh
./DocSearchServer.java
./Failed_JUnit.jpg
./find-results.txt
./grep-results.txt
./LabReport3.md
./plos-sizes.txt
./README.md
./Server.java
./Successful_JUnitTest.jpg
./TestDocSearch.java

```   

"-type" helps us find what we're looking for on a large scale-- you follow up with what you're looking for specfically after the "-type" like above. We use "-type d" to find all directories and "-type f" to find all the files. You can even use fancy commands to find files that were edited within x amount of time.

___"-size"___:   
**Example 1:**   
```
$ find -size +1M

```

**Example 2:**   
```
$ find -size -1M
.
./.git
./.git/hooks
./.git/info
./.git/logs
./.git/logs/refs
./.git/logs/refs/heads
./.git/logs/refs/remotes
./.git/logs/refs/remotes/origin
./.git/objects
./.git/objects/info
./.git/objects/pack
./.git/refs
./.git/refs/heads
./.git/refs/remotes
./.git/refs/remotes/origin
./.git/refs/tags
./grep-results.txt

```   

"-size" followed by the size allows you to find all files that fit under the criteria. For example, my first example of +1M shows that no files are bigger than 1 megabyte BUT there are many files that are under 1 megabyte.   

___"-maxdepth"___:   
**Example 1:**   
```
$ find -type f -name "*.txt" -maxdepth 1
find: warning: you have specified the global option -maxdepth after the argument -type, but global options are not positional, i.e., -maxdepth affects tests specified before it as well as those specified after it.  Please specify global options before other arguments.
./biomed-sizes.txt
./find-results.txt
./grep-results.txt
./plos-sizes.txt

```

**Example 2:**   
```
$ find -type f -name "*.java" -maxdepth 2
find: warning: you have specified the global option -maxdepth after the argument -type, but global options are not positional, i.e., -maxdepth affects tests specified before it as well as those specified after it.  Please specify global options before other arguments.
./DocSearchServer.java
./Server.java
./TestDocSearch.java

```

"-maxdepth" caps how deep the search goes. For example, a maxdepth of 1 will only permit a depth of one directory to be searched but 2 will allow 1 more.
