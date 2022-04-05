# memory
memory
malloc() function in C
The C malloc() function stands for memory allocation. It is a function which is used to allocate a block of memory dynamically. It reserves memory space of specified size and returns the null pointer pointing to the memory location. The pointer returned is usually of type void. It means that we can assign C malloc() function to any pointer.

Syntax of malloc() Function:

ptr = (cast_type *) malloc (byte_size);
Here,

ptr is a pointer of cast_type.
The C malloc() function returns a pointer to the allocated memory of byte_size.
Example of malloc():

Example: ptr = (int *) malloc (50)
When this statement is successfully executed, a memory space of 50 bytes is reserved. The address of the first byte of reserved space is assigned to the pointer ptr of type int.

Consider another example:
#include <stdlib.h>
int main(){
int *ptr;
ptr = malloc(15 * sizeof(*ptr)); /* a block of 15 integers */
    if (ptr != NULL) {
      *(ptr + 5) = 480; /* assign 480 to sixth integer */
      printf("Value of the 6th integer is %d",*(ptr + 5));
    }
}
Output:

Value of the 6th integer is 480

*Notice that sizeof(*ptr) was used instead of sizeof(int) in order to make the code more robust when *ptr declaration is typecasted to a different data type later.
*The allocation may fail if the memory is not sufficient. In this case, it returns a NULL pointer. So, you should include code to check for a NULL pointer.
*Keep in mind that the allocated memory is contiguous and it can be treated as an array. We can use pointer arithmetic to access the array elements rather than using brackets [ ]. We advise to use + to refer to array elements because using incrementation ++ or += changes the address stored by the pointer.
*Malloc() function can also be used with the character data type as well as complex data types such as structures.



calloc() function in C
The C calloc() function stands for contiguous allocation. This function is used to allocate multiple blocks of memory. It is a dynamic memory allocation function which is used to allocate the memory to complex data structures such as arrays and structures.

Malloc() function is used to allocate a single block of memory space while the calloc() in C is used to allocate multiple blocks of memory space. Each block allocated by the calloc() function is of the same size.

Syntax of calloc() Function:

ptr = (cast_type *) calloc (n, size);
*The above statement is used to allocate n memory blocks of the same size.
*After the memory space is allocated, then all the bytes are initialized to zero.
*The pointer which is currently at the first byte of the allocated memory space is returned.
*Whenever there is an error allocating memory space such as the shortage of memory, then a null pointer is returned.

Example of calloc():

The program below calculates the sum of an arithmetic sequence.

#include <stdio.h>
    int main() {
        int i, * ptr, sum = 0;
        ptr = calloc(10, sizeof(int));
        if (ptr == NULL) {
            printf("Error! memory not allocated.");
            exit(0);
        }
        printf("Building and calculating the sequence sum of the first 10 terms \ n ");
        for (i = 0; i < 10; ++i) { * (ptr + i) = i;
            sum += * (ptr + i);
        }
        printf("Sum = %d", sum);
        free(ptr);
        return 0;
    }
Result:

Building and calculating the sequence sum of the first 10 terms
Sum = 45



calloc() vs. malloc(): Key Differences
Following is the key difference between malloc() Vs calloc() in C:

*The calloc() function is generally more suitable and efficient than that of the malloc() function. While both the functions are used to allocate memory space, calloc() can allocate multiple blocks at a single time. You don’t have to request for a memory block every time. The calloc() function is used in complex data structures which require larger memory space.

*The memory block allocated by a calloc() in C is always initialized to zero while in function malloc() in C, it always contains a garbage value.




free() function is used to deallocate memory used by one program and move it back to available memory area so that other operating system processes can use that memory location. Also free function takes any type of pointer that points to that memory location. The memory for variables is automatically deallocated at compile time. In dynamic memory allocation, you have to deallocate memory explicitly. If not done, you may encounter out of memory error.

The free() function is called to release/deallocate memory in C. By freeing memory in your program, you make more available for use later.


The free() function frees the memory space pointed to by a pointer ptr which must have been returned by a pre‐ vious call to malloc(), calloc() or realloc(). Otherwise, or if free(ptr) has already been called before, undefined behavior occurs. If ptr is NULL, no operation is performed.

You have to use the free() function when you are allocating the memory dynamically.

If you are using that as a static variable then it may lead to unintended behavior.

example:
int a = 10;  // suppose 2 byte is allocated ie location 1000 and 1001
Now this 2 byte of memory belongs to specific problem; hence OS will not give this memory location to another process (memory is now allocated memory not available memory)

 int *ptr =&a;
 /*ptr is pointer variable pointing to 1000  
 as it is int pointer therefore ptr++ will move pointer to 1002*/
Now if we do free(ptr), it will check the pointer type and depending on type free function deallocate memory in this case 2 bytes starting from 1000.

Now interesting point is your data will be there until OS allocates this memory to some other process and that process overwrites it.

Also ptr is pointing to 1000 even after free() function but that memory location does not belong to our program hence ptr pointer has given new name DANGLING POINTER.

*ptr may or may not give the same value therefore it is better to make ptr =null.

Things to keep in mind:

*Never free memory twice. This can happen for example if you call free on ptr twice and value of ptr wasn't changed since first call to free. Or you have two (or more) different pointers pointing to same memory: if you call free on one, you are not allowed to call free on other pointers now too.

*When you free a pointer you are not even allowed to read its value; e.g., if (ptr) not allowed after freeing unless you initialize ptr to a new value

*You should not dereference freed pointer

*Passing null pointer to free is fine, no operation is performed.

*ptr may or may not give the same value therefore it is better to make ptr =null.


Summary
We can dynamically manage memory by creating memory blocks as needed in the heap
In C Dynamic Memory Allocation, memory is allocated at a run time.
Dynamic memory allocation permits to manipulate strings and arrays whose size is flexible and can be changed anytime in your program.
It is required when you have no idea how much memory a particular structure is going to occupy.
Malloc() in C is a dynamic memory allocation function which stands for memory allocation that blocks of memory with the specific size initialized to a garbage value
Calloc() in C is a contiguous memory allocation function that allocates multiple memory blocks at a time initialized to 0
Realloc() in C is used to reallocate memory according to the specified size.
Free() function is used to clear the dynamically allocated memory.
