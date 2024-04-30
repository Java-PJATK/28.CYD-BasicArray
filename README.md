# CYD-BasicArray
Listing 28 CYD-BasicArray/BasicArr.java Page 54

# Section 7. Arrays  

Arrays are the simplest data structure. An array can be viewed as a **fixed-sized collection** of elements of the same type in which elements are ordered and can be accessed by specifying their **index**. 

Indices start with 0 (first element), so the last element has index size-1, where size is the size (length, dimension) of the array, i.e., number of its elements. 

In Java, arrays are _objects_ — this means that they carry not only information on their elements but also some other information, in particular on their size. 

It also means that they are always created on the heap and never have names: we can refer to them only using _references_ to them (i.e., in C/C++ language, pointers — variables which hold, as their values, _addresses_ of objects).  

## 7.1 Creating arrays  

Arrays can be created in several ways, illustrated in the example below. Points to note:  

* When an array is created, its size must be specified and then cannot be modified.  

* The type _reference to array of elements of type_ `Type` is denoted by `Type[]`. Statement `int[] arr;` means that `arr` is a reference to array of `int`s — only a reference (with value `null`) is created, not an array! One can also write `int arr[];` but this notation is not recommended.

* If `arr` is a reference to an array, the expression `arr.length` is of type `int` and its value is the length (size, dimension) of the array referenced to by `arr`.

* Individual elements of an array can be accessed by their indices — if `arr` is the reference to an array, the expression `arr[i]` denotes its ith element; remember, however, that **indexing starts from zero!**  

* There is a special kind of loop which can be used to iterate over elements of an array (and, as we will see later, over elements of other types of collections as well). It’s sometimes called a ‘for-each loop’ and has the form:  

`for (Type elem : arr) { ... }`  

where `Type` is the type of elements of the array `arr`, `elem` is any identifier, and `arr` is the reference to an array. In consecutive iterations of the loop, `elem` will be a _copy_ of the consecutive element of the array.  

For example, this is how we can create an 10-element array of chars and fill it with random capital Latin letters (note the keyword `new`). Then we print its elements, separated by spaces, in one line. 

```java
char[] arr = new char[10];
for (int i = 0; i < arr.length; ++i) {
    arr[i] = (char)('A' + (int)(Math.random()*26));
}
for (char c : arr)
    System.out.print(c + " ");
System.out.println();
```

Note that the condition in the `for`-loop is `i < arr.length` with strict inequality, as the index `arr.length` (i.e., 10) would be illegal: indexing starts with 0, so the last element has index 9. Note also the use of the for-each loop to print the elements.  

This is how we can create an array and initialize it at the same time; note that we don’t specify its size, because the compiler will be able to infer it from the initializer in braces; after creation, we print it in reverse order:  

```java
int[] arr = {1, 2, 8, 9};
for (int i = arr.length-1; i >= 0; --i)
    System.out.print(arr[i] + " ");
System.out.println();
```

Next example shows still another way to create and initialize an array:  

```java
int[] a0 = new int[]{1, 2, 3};
int[] a1 = {4, 5, 6};
int[] arrsum = new int[a0.length]; // contains zeros
for (int i = 0; i < arrsum.length; ++i)
    arrsum[i] = a0[i] + a1[i];
for (int n : arrsum)
    System.out.print(n + " ");
```

prints

```java
5 7 9
```

The example below shows how to find the value of the maximum element of an array  

```java
int[] arr = {1, -6, 9, -2, 7};
int mx = arr[0];
for (int i = 1; i < arr.length; ++i)
    if (arr[i] > mx) mx = arr[i];
System.out.println("Maximum element is " + mx);
```

Sometimes what we want is rather the index of the maximum element:  

```java
int[] arr = {1, -6, 9, -2, 7};
int indmax = 0;
for (int i = 1; i < arr.length; ++i)
    if (arr[i] > arr[indmax]) indmax = i;
System.out.println("Maximum element has index " + indmax);
```

How to reverse the order of elements in an array arr of, say, `int`s? It’s simple:  

```java
for (int i = 0, j = arr.length-1; i < j; ++i, --j) {
        int tmp = arr[i];  // swapping two elements
        arr[i] = arr[j];
        arr[j] = tmp;
}
```

Note that the condition `i < j` cannot be replaced by `i < arr.length` — we would then reverse the order of elements twice thus restoring the original order!  

And now – how to randomly shuffle elements of an array?  

```java
int[] arr = {1, 2, 3, 4, 5, 6};
  // shuffling
for (int i = 0; i < arr.length-1; ++i) {
      // random index from interval [i, arr.length-1]
  int r = i + (int)((arr.length-i)*Math.random());
      // swapping
  int tmp = arr[i];
  arr[i] = arr[r];
  arr[r] = tmp;
}
```

Let us consider the following example. Note that `printArr` is a function which just prints the content of an array passed to it as the first argument (just after the opening parenthesis); it will also print the string passed as the second argument. More about functions in the next section (Sec. 6, p. 44).  

## Listing 28 CYD-BasicArray/BasicArr.java

```java
// CYD-BasicArray/BasicArr.java
 
public class BasicArr {

    public static void main(String[] args) {
        int[] a1 = {1,2,3};
        printArr(a1, "Array a1");

        int[] a2;  //  <-- no array here, only reference!
        a2 = new int[]{4,5,6};
        printArr(a2, "Array a2");

        a1 = a2;   // <-- whatever was in a1 is lost!
        printArr(a1, "After a1=a2, a1 is");

          // a1 and a2 now refer to the same array!
        a1[0] = 44;
        a2[2] = 66;
        printArr(a1, "After modifications a1 is");
        printArr(a2, "After modifications a2 is");

          // ad hoc array
        printArr(new int[]{7,8,9}, "Ad hoc array");
    }


    /**
     *  prints an array of integer numbers
     */
    private static void printArr(int[] a, String message) {
        System.out.print(message + ": [");
        for (int i : a)
            System.out.print(" " + i); // <-- i unmodifiable
        System.out.println(" ]; size = " + a.length);
    }
}
```

