# Lab Report 2 - Servers and Bugs
---
## Part 1

Image of my code for the String server:
![StringServerCode](StringServerCode.png) <br/><br/>

Image of adding "Hello" message: <br>
![HelloMsg](HelloMsg.png) <br/><br/>

- The method in my code called is `handleRequest(URI url)` which takes in a URL as an argument, in this case it took http://localhost:4090/add-message?s=Hello and returns the string "Hello"
- The relevant arguments to the method are the `url.getPath().contains("/add-message")` if statement which checks if we are using the command `/add-message` on the URL and the `parameters[0].equals("s")` if statement which checks for the "s" in `/add-message?s`. The relevant fields in the class are `String single` which contains the value "Hello" and `String[] parameters` which contains the value "s" on index 0 and value "Hello" on index 1.
- The value of the `String[] parameters` became "s" on index 0  and "Hello" on index 1 by `url.getQuery().split("=")` splitting the "s" and "Hello" from the `add-message?s=Hello` by the "=" value. String single changed from "" to "Hello\n" if parameters[0] was "s". <br/><br/>

Image of adding "How are you" message: <br>
![HowAreYouMsg](HowAreYouMsg.png) <br/><br/>

- The method in my code called is `handleRequest(URI url)` which takes in a URL as an argument, in this case it took http://localhost:4090/add-message?s=How%20are%20you and returns the string "How Are You"
- The relevant arguments to the method are the `url.getPath().contains("/add-message")` if statement which checks if we are using the command `/add-message` on the URL and the `parameters[0].equals("s")` if statement which checks for the "s" in `/add-message?s`. The relevant fields in the class are `String single` which contains the value "How are you" and `String[] parameters` which contains the value "s" on index 0 and value "How are you" on index 1.
- The value of the `String[] parameters` became "s" on index 0  and "How are you" on index 1 by `url.getQuery().split("=")` splitting the "s" and "How are you" from the `add-message?s=How are you` by the "=" value. String single changed from "" to "How are you\n" if parameters[0] was "s". <br/><br/>

## Part 2

Failure Inducing Input: <br>
```
@Test 
public void testReversed2() { 
  int[] input1 = { 3, 0, 8 }; 
  assertArrayEquals(new int[]{ 8, 0, 3}, ArrayExamples.reversed(input1)); 
}   
 ```

Successful Inducing Input:
```
@Test
public void testReversed() {
  int[] input1 = { };
  assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
} 
 ```
Symptom: <br/>
![Symptom](Symptom.png) <br/>

Code Before:
```
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
}
```
<br/>
Code After:

```
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    newArray[i] = arr[arr.length - i - 1];
  }
  return newArray;
}
```
- I noticed that the old code was copying `newArray[]` onto `arr[]` within the for loop. The goal of this code is to copy an array onto a new array therefore I changed the for loop to contain `newArray[i] = arr[arr.length - i - 1];` in order to start copying the `arr[]` onto the `newArray[]` in every index with the for loop. The old code also returned the old array which is not what we want, we want to return the new array so I used `return newArray;`.


## Part 3

Something that I learned from lab 2 that I didn't know before are what ports are and do. Every website you've ever been to has a port. Ports are extra parts added onto URLs that indicate which specific port websites are using. This part of the URL is usually hidden though. The port could vary between many numbers and public sites use either the ports 80 or 443.
