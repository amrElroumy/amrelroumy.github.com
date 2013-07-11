# C++ Threads

## Working with Threads

### Threads' Instantiation

The instantiation of a thread is as easy as declaring a `std::thread` and passing a function pointer to it.

```cpp
void do_something();
std::thread spawned_thread(do_something);
```

Can also work with any callable type, e.g.
```cpp
class background_worker
{
	private:
	void do_something() const
	{
		std::cout << "Hello world" << std::endl;
	}
public:
	void operator() () const
	{
		do_something();
	}
};

int main()
{
	background_worker mWorker;
	std::thread(mWorker);
}
```

A pitfall because of C++'s most [vexing parse](http://en.wikipedia.org/wiki/Most_vexing_parse), is that passing a function object while constructing it causes a compilation error later on operating on this thread. This is because there is an ambiguity between function declaration and object initialization. Priority is given to the first. 

```cpp
std::thread mThread1 ( background_worker() );	// Compilation Error
```

A possible solution to avoid the parsing ambiguity is by adding extra parenthesis

```cpp
std::thread mThread1 ( (background_worker() ) );
```

Another way to instantiate an object is through uniform initialization (based on initializer list constructor)

```cpp
std::thread mThread1 { background_worker() };	// Not supported by VS2012
```

### Thread Management

#### Abandon/Wait for thread to finish execution
After thread instantiation, comes the choice whether to wait for the thread to finish its execution before exiting the main thread (the thread where the secondary thread branched from) or forfeit ownership of the thread and leave it to run in the background with no direct way of communicating with it. This type of background threads are sometimes referred to as ***daemon threads*** after the UNIX concept of a daemon process that run in the background without any explicit user interface.

In order to detach from a thread or join a thread, there must be a thread object to detach or join as you can't call `detach()/join()`on std::thread

Important points about `detach()` and `join()`

- If I don't make a decision about whether to wait for a thread to terminate (thread.join()) or leave it to run on its own 
(thread.detach()) before the std::thread object is destroyed, then the program is terminated (the std::thread destructor calls std::terminate()
- When passing a local variable from main thread to a secondary thread either by reference or through a pointer we risk a dangling 
pointer/reference. Possible ways to handle this scenario:
- Make the thread function self-contained; copy the data into the thread rather than sharing data. Caution: be wary of pointers/references  in the copied object.
- Ensure that the thread has completed its execution before the  main thread exits by joining the thread.
- When writing to a console in a secondary thread, if the master thread exists and the second thread is not detached an exception is thrown. Either detach it from the main thread or wait for it to finish its execution by using thread.join() 
- thread.join() is simple and brute-force either wait for the thread to terminate or you don't.. If we need to have more fine-grained control over waiting for a thread we use condition variables and futures.
- The act of calling join()also cleans up any storage associated with the thread, so the std::threadobject is no longer associated with the now finished thread; it isn’t associated with any thread. This means that you can call join()only once for a given thread; once you’ve called join(), the std::thread object is no longer joinable, and joinable()will return false.


// **Todo:** Write code samples about join and detach + RAII for exceptional situations + Thread ownership `std::move()`

#### Passing arguments to threads
Passing arguments to threads is as easy as passing additional arguments to the `std::thread` constructor.

```cpp
void f(int i, std::string const& s);
std::thread t(f, 10, "hello world");
```

If you are interested in invoking a member function of an object, we follow a mechanism similar to that of `std::bind()`:

```cpp
class my_type
{
	public:
	void F(int i1, int i2)
	{
	printf("i1= %d - i2= %d\n", i1, i2);
}
};

my_type mObject;
std::thread t(&my_type::F, &mObject, 1, 2);
t.join();
```

**Caution - Common pitfalls** 

- Not knowing that passing a pointer/reference to an automatic variable might cause dangling pointer/reference if the main thread finishes execution before the spawned thread finishes its execution.

```cpp
// Example: passing a string literal to a function which takes a string, the string
//  the string literal is only converted to string in the context of the new thread

void f1(int i, const std::string& s)
{
	std::fstream file;
	char file_name[100];
	sprintf(file_name, "out_%d.txt", std::this_thread::get_id());
	file.open(file_name, std::ios_base::out);
	file << i << " " << s << std::endl;
	file.close();
}


void oops1(int some_param)
{
	char buffer[1024];
	sprintf(buffer, "%d", some_param);

	std::thread t1(f1, 3, buffer);               			// Dangling pointer scenario
	std::thread t2(f1, 3, std::string(buffer));		// Proper way to pass string to avoid dangling pointer

	t1.detach();	// Won't complete execution properly, will need to use t1.join to finish execution properly
	t2.detach();	// Will properly give output

}
```
- The other pitfall is when we want to do the opposite, pass a reference to the spawned thread. The thread constructor is oblivious to the types of arguments expected by the function and copies unknowingly the object instead of passing the reference

```cpp
void f2(int i, int &r, const int &cr)
{
	i++;
	r++;
}

void oops2()
{
	int a = 1, b = 2, c =3;

	std::thread t1(f2, a, b, c);
	t1.join();
	
	// No changes happen to the value of b
	printf("a= %d - b= %d - c= %d\n", a, b, c);		

	std::thread t2(f2, a, std::ref(b), std::cref(c));
	t2.join();

	// The problem is solved by wrapping the values in reference objects
	printf("a= %d - b= %d - c= %d\n", a, b, c);		
}
```

#### Controlling the number of running threads
To identify the maximum number of threads that can run concurrently we use `std::thread::hardware_concurrency()`. It returns 0 if this information is unavailable.

It is preferred to refrain from exceeding this value in order to avoid something called *oversubscription* that results when we run more threads than the hardware can support causing a lot of context switching, which in turn degrades the performance.

#### Identifying threads
It is useful to be able to identify which thread is executing a segment of the code, allowing easier management of the workload. There are 2 possible ways to get the id of a thread:

- The first is using `std::thread::get_id()` member function
```cpp
std::thread t(f);
t.get_id();
```

- The second is by using the static function `std::this_thread::get_id()` to get the identifier for the current thread
```cpp
int currentThreadID = std::this_thread::get_id();
```

### Sharing Data Between Threads
If all shared data is read-only, there’s no problem, because the data read by one thread is unaffected by whether or not another thread is reading the same data. However, if data is shared between threads, and one or more threads start modifying the data, there’s a lot of potential for trouble. In this case, we must take precautionary actions to ensure that nothing goes wrong.

*Race conditions* are possible causes for problems related to shared data. Race conditions occur when multiple threads of execution are accessing the same data concurrently while it is being modified by one or more thread.

Problematic race conditions typically occur where completing an operation requires modification of two or more distinct pieces of data. Because the operation must access two separate pieces of data, these must be modified in separate instructions, and another thread could potentially access the data structure when only one of them has been completed.

E.g. of race conditions: Invariant statements about a particular data structure which are broken during changes in the data structures.

Ways to deal with race conditions include:
- Using synchronization methods provided by the programming language or the operating system.
- Using lock-free programming, in which the code is redesigned so that modifications are done as a series of indivisible changes.
- Using *software transaction model (STM)* which is to handle the updates to the data structure as a transaction, just as updates to a database are done within a transaction. The required series of data modifications and reads is stored in a transaction log and then committed in a single step. If the commit can’t proceed because the data structure has been modified by another thread, the transaction is restarted.

The most primitive method for synchronization which is supported by the C++ standard is a `mutex`. The method of using a mutex is:
1. The thread making the changes locks the mutex before entering the critical section, causing other threads to wait (block) when reaching this critical section.
2. The thread that acquired the mutex, unlocks it when it has finished its modifications.

#### Usage of Mutexes

The process of using a mutex to synchronize access is as easy as declaring the mutex object and acquiring the lock in another statement.

```cpp
int my_precious;
std::mutex mutex_lock;

void modify_my_precious()
{
	std::lock_guard<std::mutex> guard(mutex_lock);
	my_precious = -1;
}
```

**Common pitfall:**
The usage of a mutex lock is not as simple as slapping `std::lock_guard` object in every member function; one stray pointer or reference, and all that protection is for nothing. In order to avoid this we must ensure that member functions don't pass references/pointers to the protected data object either out by returning them or into other functions they call.

```cpp
// An example of how naively protecting data with locks without accounting for 
// how acquired references  of the protected data can be used maliciously

class some_data
{
	int a;
	std::string b;
	public:
		void do_something();
};
class data_wrapper
{
	private:
		some_data data;
		std::mutex m;
	public:
		template<typename Function>
		void process_data(Function func)
		{
			std::lock_guard<std::mutex> l(m);
			func(data); 	// This argument can be received as a reference in the called function
		}
};

some_data* unprotected;
// A reference to the protected data object is acquired by the function
void malicious_function(some_data& protected_data)		
{
	unprotected=&protected_data;
}

data_wrapper x;
void foo()
{
	x.process_data(malicious_function); 
	unprotected->do_something(); 
}
```

---

##### Use Case - Designing the stack `pop()` and `top()` functions to overcome race conditions
The race conditions we are talking about is how the `empty()` and `size()` functions are not reliable, this is because the actual state of the data structure can be altered between the function call to them and the statement where the returned value is used.

A possible race condition that might occur is if the stack contains only 1 element, and after checking that the stack isn't empty we enter a sequence of code that works on this element, while another thread modifies the stack and removes this element. This causes undefined behaviour.

```cpp
stack<int> s;
s.push(1);	// Our stack contains only 1 element

if(!s.empty()) 
{
	// Another thread calls pop() on this stack removing the only element
	int const value = s.top();			// Undefined behaviour
	s.pop(); 
	do_something(value);
}
```
Another possible race condition is what could happen between `s.top()` and `s.pop()` where 2 threads can be executing this code sequence at the same time, if the calls are interleaved so that the 2 threads call the `s.top()` function and then the `s.pop()` calls are executed what will happen is that one element of the stack will be processed twice, while the next element will be skipped without processing. This type of race conditions is critical because there are no indicators of it in the run-time and causes annoying logical errors, unlike the previous one which causes an exception to be thrown.

Even if we use mutex locks internally in these functions, the interface of the data structure is prone to race conditions as we've noticed from the previous examples. This requires a proper redesign of the interface to properly handle these situations.



---
