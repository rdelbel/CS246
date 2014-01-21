Human vs Machine Testing
=
**Human Testing** 
* humans read code and look for failutres
**Machine Testing** 
* run the program on selected inputs, check against spec 
* can't test everything * need to choose carefully

**Black-box testing** no knoweldge of implementation
**White-box testing** full knoweldge of implementation
**Grey-box testing** some knoweldge of implementation
How to Test
*
* Start with black-box, supplement with white-box
* check various classes of input, eg numeric ranges, positive vs negative,
differences between ranges (edge cases)
* Multiple simulataneous boundaries (corner cases)
* Extreme Cases 
* Intuition and experience

**White box Testing**

* check all logical paths through the program
* make sure every function runs
* Test loops that run 0, 1, many times
* Keep tests as small as possible and have many of them

Questions that testing can answer
*
* Does my program work? (correct?) Functional testing
* Did my change just break something (Regression Testing)
* Is my program fast enough? **Performance testing**
* Can I handle large and smal inputs? **Voume Testing**

Module 2: C++
= 

```c++
#include <iostream>
using namespace std;
int main(){
cout<<"Hello world" << endl;
return 0;
}
```

**Notes**

* main **must** return type in in c++
* stdio.h, printf still available in c++

 preferred: C++ I/O: 
header <iostream>
std::cout<< ... << ... <<< ... <<< std::endl

* using namespace std lets you refer to std::cout, std::endl as just cout, endl
* **return** returns a stats to the shell ($?) If not specified, main returs 0.

**Compiling C++ programs**

* g++ program.cc -o program
* **-0 program** is the name of the executable. If not specified then it will
  be a.out
* ./program to run.

```bash
g++ hello.cc -o hello
./hello
```

Most C programs are valid C++ programs

C++ Input/Output
-

We've seen
```c++
 cout<<stuff<<endl;
```

C++ provides 3 I/O stream objects:
* **cout** for printing to stdout
* **cin** for reading from stdin
* **cerr** for printing to stderr

**I/O operators**
<< "put to" (outout)
>> "get from" (input)
