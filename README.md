# ArrayList Implementation

A from scratch implementation of an arraylist in Java without using the Java Collections framework.



Class stub

```java
/** Represents an array.
 * @version 1.5
 * @since 1.0
 * @author Junaid Dodhia
*/
public class MyArray {

}
```

Variables

```java
/**
 * Internal array of Type String.
 */
 private String[] internalArray;

/**
 * Size of the underlying array (number of elements).
 */
 private int arraySize;
```

Functions

```java
public MyArray()
public MyArray(int initialCapacity)
public void add(String text)
public boolean search(String key)
public int size()
public int getCapacity()
public void display()
public void removeDups()
```

Default constructor

```java
/**
 * Default constructor.
 */
public MyArray() {
	 arraySize = 0;
	 internalArray = new String[10];
}
```

Parameterized constructor

```java
/**
 * Parameterized constructor.
 *
 * @param initialCapacity the initial capacity of internalArray
 */
public MyArray(int initialCapacity) {
	arraySize = 0;
				// internal array initialized with the capacity passed in
	  if (initialCapacity >= 0) {
	    internalArray = new String[initialCapacity];
	  } else {
        // internal array initialized with default capacity as 10
        internalArray = new String[10];
      }
}
```

A function to add a word to the array after performing the required checks

```java
/**
 * Adds the word to the array after performing required checks.
 *
 * Worst-case running time complexity: Amortized O(1)
 *
 * @param text string to add to internalArray
 */
public void add(String text) {

    // check if text is not null and is a sequence of letters
		if (text != null && text.matches("[A-Za-z]+")) {

            // check if the array is empty
            if (size() == 0) {
                internalArray = new String[1];
            }

            // double the capacity of the array if size is equal to the capacity
            if (size() == getCapacity()) {
                String[] temp = new String[2 * getCapacity()];
                System.arraycopy(internalArray, 0, temp, 0, size());
                internalArray = temp;
            }

            // add the text to the internal array
            internalArray[arraySize++] = text;
		}
}
```

A function to search for a given word in the array and return true if found or false if not

```java
/**
 * Searches for a given word in the array and returns true if found or false if not.
 *
 * Worst-case running time complexity: O(n)
 *
 * @param key the word to be searched in the array
 * @return a boolean value to indicate if the word was found
 */
public boolean search(String key) {
        try {
            for (int i = 0; i < getCapacity(); i++) {
                // check if the word is equal to the search string
                if (internalArray[i].equals(key)) {
                    // word found
                    return internalArray[i].equals(key);
                }
            }
        } catch (NullPointerException e) {
            // word not found
            return false;
        }
        return false;
}
```

A function to return the size of the array

```java
/**
 * Returns the size of the array.
 *
 * Worst-case running time complexity: O(1)
 *
 * @return size of internalArray
 */
public int size() {
	return arraySize;
}
```

A function to return the capacity of the array

```java
/**
 * Returns the capacity of the array.
 *
 * Worst-case running time complexity: O(1)
 *
 * @return capacity of internalArray
 */
 public int getCapacity() {
	 return internalArray.length;
 }
```

A function to display the content of the array

```java
/**
 * Prints all the words in one line and puts a space between words.
 *
 * Worst-case running time complexity: O(n)
 */
 public void display() {
	StringBuilder stringBuilder = new StringBuilder();
        for (int i = 0; i < getCapacity(); i++) {
            if (internalArray[i] != null) {
                stringBuilder.append(internalArray[i]).append(" ");
            }
        }
        // trims out the last space appended
        String displayText = stringBuilder.toString().trim();
        System.out.println(displayText);
        stringBuilder.trimToSize();
}
```

A function to remove duplicates from the array

```java
/**
 * Removes duplicate words from the array.
 *
 * Worst-case running time complexity: O(n^2)
 */
 public void removeDups() {
        StringBuilder stringBuilder = new StringBuilder();
        stringBuilder.append(" " + internalArray[0] + " ");
        int duplicateCount = 0;
        int i = 1;
        while (i < getCapacity()) {
            if (internalArray[i] != null) {
                // check for duplicates
                if (stringBuilder.toString().contains(" " + internalArray[i] + " ")) {
                    duplicateCount++;
                    // delete the duplicate
                    System.arraycopy(internalArray, 0, internalArray, 0, i);
                    System.arraycopy(internalArray, i + 1, internalArray, i, getCapacity() - i - 1);
                } else {
                    stringBuilder.append(" " + internalArray[i] + " ");
                    i++;
                }
            } else {
                i++;
            }
        }
        arraySize = size() - duplicateCount;
        stringBuilder.trimToSize();
}
```
