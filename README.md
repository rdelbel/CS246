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

**How to Test**
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
```c++
<< // "put to" (outout)
>> // "get from" (input)

cout<<x; // put x to stdout 
cerr<<x; // put x to stderr
cin>>x; // get x from stdin
```

operator points in the direction of information flow 

**Example** get two numbers and add them

```c++
#include<iostream>
using namespace std;
int main(){
    int x,y;
    cin>>x>>y;
    cout<<x+y<<endl;
}
```

**Notes**
* cin >> ignores whitespace
* cin >> x >> y; looks for two ints on stdin, ignoring whitespace
* any # of spaces, tabs, newlines between x and y

What if input doesn't cointain an int next?

```bash
./a.out
4 five
4
```
```bash
./a.out
4 5.5 
9
```
Statement fails, var is unassigned.

What if input is exhausted before we get 2 ints? Same.

```bash
./.out
4
^D
4
```
```bash
./.out
4
^C
```

Always do ^D unless you have to ^C.

How can we tell if a read has failed (bad input), or if the input stream is
exhausted?

* If the read failed: cin.fail() will be true
* If EOF: cin.eof() and cin.fail() with both be true
* But not until an attempted read failed. 
* They will not be turned on until you try the read and fail it.

**Example** Read all ints from stdin and echo them, one per line. Stop if a non
integer is encountered or end of file is hit.

```c++
int main(){
    int i;
    while(true){
        cin>>i;
        if(cin.fail())
            break
        cout<<i<<end;
}
```

```bash
./a.out
1 2 3 4 5
1
2
3
4
5
6
6
7
7
```

Note:
* There is an implicit conversion from cin to void*
* void * is a pointer to something whos type is not defiend
* void* can point to anything. It is a generic pointer.
* cin can be used in these numeric contexts. 
* cin can be used a condition
* void* can be converted to bool

Therefore
```c++
if(cin)// is true if !cin.fail()
       // false if cin.fail()
```

**Example v2.0**
```c++
// This code will do the same thing as before
int main(){
    int i;
    while(true){
        cin>>i;
        if(!cin) break;
        cout<<i<endl;
    }
}
```

**Note**
* operator >> is the C right bitshift operator
* in C a>>b means shoft a's bit representation by b slots to the right

**EG**
* 21 in binary is 10101_2
* 21>>3 = 10_2 = 2_10
* can still do this in c++ but when the LHS is cin  it means "get from"

** operator >> **
* inputs: cin (type istream), data (various types)
* Output? Returns cin back to you! (type istream)
* so cin >> i has the side effect of populating i, and has the value of cin.
* Why is this useful?
* This is why we can write cin >> x >> y >>x; 
* cin >> x >> y >> x;
* cin >> y >> x;
* cin >> x;
* cin;

**Example 3.0**
```c++
// Does exactly the same thing as the previous example
int main(){
    int i;
    while (true){
        if(!cin>>i)
            break
        cout<<i<<endl;
    }
}
```

**Example 4.0**
```c++
// Does exactly the same thing as the previous example
int main(){
    int i;
    while(cin>>i){
        cout<<i<<endl;
    }
}   
```
