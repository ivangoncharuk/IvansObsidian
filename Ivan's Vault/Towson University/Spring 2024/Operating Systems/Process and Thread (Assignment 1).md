- Ivan Goncharuk



## Task 1: Elemental Transformation (`task1.c`)

 `task1.c` allows the user to select an elemental transformation (fire, water, earth, air), then forks a new process to handle the selected transformation. 
 The parent process waits for the child process to complete before exiting.

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/wait.h>

int main() {
    // Input selection
    printf("Choose your elemental transformation: fire, water, earth, or air.\n");
    char choice[10];
    scanf("%s", choice);

    // Forking a new process
    pid_t pid = fork();

    if (pid == 0) { // Child process
        // Executing corresponding elemental program based on user choice
        // Parent and Child PID logging
        exit(0); // Child process exits
    } else if (pid > 0) { // Parent process
        // Waiting for child process to complete
    } else {
        // Forking failed
        return 1;
    }

    return 0;
}
```

### Child Process
```c
printf("Child process with PID: %d\n", getpid());
if (strcmp(choice, "fire") == 0) {
	execl("./bin/fire_elemental", "fire_elemental", NULL);
} else if (strcmp(choice, "water") == 0) {
	execl("./bin/water_elemental", "water_elemental", NULL);
} else if (strcmp(choice, "earth") == 0) {
	execl("./bin/earth_elemental", "earth_elemental", NULL);
} else if (strcmp(choice, "air") == 0) {
	execl("./bin/air_elemental", "air_elemental", NULL);
} else {
	printf("Unknown elemental transformation.\n");
}
// Ensure the child process exits after execution
exit(0);  // Child process exits
```

### Parent Process
```c
printf("Parent PID: %d, reporting Child PID: %d\n", getpid(), pid);
wait(NULL); // waiting for the child process to finish
```
### Process Overview

1. **User Input**: Prompts for and reads the user's choice of elemental transformation.
2. **Process Forking**:
   - Uses `fork()` to create a child process.
   - The child process identifies the user's choice using `strcmp()` and executes the corresponding elemental program with `execl()`.
   - The parent process waits for the child to finish using `wait(NULL)`.
3. **Process Identification**:
   - The child process prints its PID using `getpid()`.
   - The parent process prints both its PID and the child's PID for identification.

### Key Functions
- `fork()`: Creates a new process.
- `execl()`: Executes a specified executable.
- `wait()`: Waits for a child process to finish.
- `getpid()`: Retrieves the current process's ID.
- `strcmp()`: Compares two strings.

## Task 2: Threads of Harmony and Cooperation (`task2.c`)

This program creates five threads (Factorions) to calculate factorials of numbers 1 through 5 and sums the squares of these factorials in a global variable, protected by a mutex.

### Key Functions
- `pthread_create()`: Creates a new thread.
- `pthread_join()`: Blocks until a thread completes.
- `pthread_mutex_lock()`, `pthread_mutex_unlock()`: Lock and unlock a mutex.
- `factorial()`: Recursively calculates the factorial of a number.

### Process

1. **Initialization**:
   - Declares an array with numbers 1 to 5.
   - Initializes a mutex for thread synchronization.
2. **Thread Creation**:
   - For each number in the array, a thread (`pthread_create()`) is created to calculate its factorial.
3. **Factorial Calculation**:
   - Each thread calculates the factorial of its assigned number.
4. **Global Summation**:
   - Threads safely add the square of their factorial result to a global result variable using a mutex (`pthread_mutex_lock()` and `pthread_mutex_unlock()`).
5. **Finalization**:
   - Waits for all threads to complete (`pthread_join()`).
   - Prints the summation of squares.
   - Destroys the mutex.


This program demonstrates a multi-threaded approach to calculate and sum the squares of factorials of the first five positive integers, using a global variable for the sum, protected by a mutex to ensure thread safety.

### Components

#### Initializations
   - An array `int arr[NUM_FACTORS] = {1, 2, 3, 4, 5};` holds the numbers for which factorials will be calculated.
   - A global `int result = 0;` stores the sum of the squares of the factorials.
   - A `pthread_mutex_t lock;` mutex ensures that updates to `result` are thread-safe.
   - The `ThreadParam` structure holds thread-specific data, including the number and its factorial result.

```c
typedef struct {
    int number;    // The number to calculate the factorial of
    int factorial; // The result of the factorial calculation
} ThreadParam;
```

#### Thread Creations

`void *threadFunction(void *arg)` calculates the factorial of its assigned number and safely adds the square of this factorial to the **global** `result` using the *mutex*.

This function is designed to be executed by each thread created in the program. Its purpose is to calculate the factorial of a given number and then add the square of this factorial to a **global** sum, ensuring thread safety using *mutexes*.

- This signature `void *arg` is required for functions that will be executed by threads in a POSIX threads (pthread) environment.

```c
// The argument `void *arg` allows passing any type of data to the function by casting it to `void *`.
void *threadFunction(void *arg) {
	// The void pointer `arg` is cast back to a pointer of type `ThreadParam`. 
	// This allows access to the `number` and `factorial` fields within the passed structure. 
	// The `number` field contains the specific number for which this thread will calculate the factorial.
    ThreadParam *param = (ThreadParam *)arg;

	// Calls the `factorial` function, passing `param->number` as the argument. 
	// The result is stored back in `param->factorial`. 
	// This calculates the factorial of the number assigned to this thread.
    param->factorial = factorial(param->number);

	// Before updating the global `result`, 
	// the mutex `lock` is locked to prevent other threads from accessing `result` simultaneously. 
	// This ensures that the update to `result` is thread-safe, preventing race conditions.
    pthread_mutex_lock(&lock);

	// Adds the square of the factorial (`param->factorial * param->factorial`) to the global `result`.
	// This operation is done within the critical section protected by the mutex 
	// to ensure that no two threads can perform this update at the same time.
    result += param->factorial * param->factorial;

	// Releases the mutex `lock`, allowing other threads to lock it and safely update `result`. 
	// This step is crucial for allowing concurrency while maintaining data integrity.
    pthread_mutex_unlock(&lock);

	// Since the function is to return a `void *`, it returns `NULL`.
    return NULL;
}
```

#### Factorial Calculation

A recursive function `int factorial(int n)` calculates the factorial of a given number `n`.

```c
int factorial(int n) {
    if (n == 0)
        return 1;
    return n * factorial(n - 1);
}
```


#### Main function

Here is the process of the main function:

- Initializes the mutex.
- Creates five threads, each assigned to calculate the factorial of numbers 1 through 5.
- Waits for all threads to complete their calculations.
- Prints the final sum of the squares of the factorials.
- Destroys the mutex to clean up.

```c
int main() {
	// Declares an array named `threads` of type `pthread_t`, 
	// which will store the identifiers for the threads that the program will create.
	// NUM_FACTORS is the size of the array, a thread for each factor
    pthread_t threads[NUM_FACTORS];

	// This array will hold the parameters for each thread, 
	// including the number each thread will calculate the factorial of.
    ThreadParam params[NUM_FACTORS];

	// Initializes the mutex `lock` with default attributes (`NULL`). 
	// This mutex is used to synchronize access to the global `result` variable, and 
	// ensures thread-safe updates.
    pthread_mutex_init(&lock, NULL);

	// Iterates `NUM_FACTORS` times to create threads. For each iteration:
	// - Assigns the current factor from the `arr` array to `params[i].number`, 
	//  setting the parameter for the thread.
	// - Calls `pthread_create` to create a new thread, passing a pointer to `threads[i]`
	//  to store the thread identifier, `NULL` for default thread attributes, `threadFunction`
	//  as the function each thread will execute, and a pointer to `params[i]` as the argument 
	//  to `threadFunction`.
    for (int i = 0; i < NUM_FACTORS; i++) {
        params[i].number = arr[i];
        pthread_create(&threads[i], NULL, threadFunction, &params[i]);
    }

	// Iterates over the `threads` array, calling `pthread_join` for each thread id. 
	// blocks the calling thread (which is the main thread here) until the specified 
	// thread terminates, ensuring that all threads have completed their execution before proceeding.
	// Passing `NULL` as the second argument means that the return value of the 
	// thread function isn't used.
    for (int i = 0; i < NUM_FACTORS; i++) {
        pthread_join(threads[i], NULL);
    }

	// print final result
    printf("The magical operation result is: %d\n", result);
    // Destroys the mutex `lock`, releasing any resources it might hold. 
    // This is cleanup step to prevent resource leaks
    pthread_mutex_destroy(&lock);


    return 0;
}
```