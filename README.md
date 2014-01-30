Human vs Machine Testing
=
**Human Testing** 
* humans read code and look for failutres
**Machine Testing** 
* run the program on selected inputs, check against spec 
* can't test everything: need to choose carefully

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

**Questions that testing can answer**

* Does my program work? (correct?) Functional testing
* Did my change just break something (Regression Testing)
* Is my program fast enough? **Performance testing**
* Can I handle large and smal inputs? **Voume Testing**

Module 2: C++
= 

```c++
//Hello World Program
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
* preferred: C++ I/O: 
header <iostream>
std::cout<< ... << ... <<< ... <<< std::endl

* using namespace std lets you refer to std::cout, std::endl as just cout, endl
* **return** returns a stats to the shell ($?) If not specified, main returs 0.

**Compiling C++ programs**

* g++ program.cc -o program
* -0 **program** is the name of the executable. If not specified then it will
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

Read all ints and echo on stdout until EOF
skip non-integer output

```c++
int main(){
    int i;
    while(true){
        if(!(cin>>i)){
            if(cin.eof()) break; //eof
            else{//badint
                cin.clear() //clear the fail bit
                cin.ignore() //ignores the current inut char
}
}
else{//no fail
cout<<i<<endl;
}
}
```

Reading Strings
-
* c++ provides type std::string

```c++
#include<iosstream>
#includetring>
using namespace std;
int main(){
    string s;
    cin>>s;
    cout<<s<<endl;
}
```

```
g++ readstrings.cc
./a.out
hello world
hello
```

**Semantics**
* reads next charaters into a string, stopping at the next whitespace and
  skipping leading whitespace. 
* cin will always read a string a word at a time
* We see that reading and prining strings and int are basically the same.
* What if you want the whitespace?
* getline(cin,s); reads everything from where you are to the newline character
* What if we want to change the format of our cout?
* Use I/O manipulators
* cout<<hex<<i<<endl;
* hex is a manipulator
* tells cout to print all subsequent values in hexadecimal
* To o back to decimal 
* cout<<dec;
* Some require #include<iomanip>
* The stream abstraction applies to other sources of data

**EX** read data from a specific file instead of stdin
* Use filestream objects #include<fstream>
* ifstream  to read files
*ofstream to write file

```c
//how to read file in C
#include<stdio.h>
int main(){
    char s[255]; //hope 255 is enough
    FILE *f=fopen("suite.txt","r")
    while(true){
        fscanf(f,"%s",s);
        if(feof(f)) break;
        printf("%s\n",s);
        }
    fclose(f);
}
```

```c++
//same program in C++
#include<iostream>
#include<fstream>
using namespace std;
int main(){
    ifstream f("suite.txt");
    sting s;
    while(f>>s){
        cout<<s<<endl;
    }
}
```

* Declaring the ifstream opens the file.
* file is closed when the ifstream object goes out of scope
* f is on the stack. at the end of main the stack is popped, f gets closed.
* anything you can do with cin yo u can do with an ifstream
* anything you can do with cout you can do with an ofstream

**EX** Might want to read and write data from a string. Want to read it as if
it were a file
* can attach a stream to a string and either read from or write to it
* #include<sstream>. Use istringstream for reading to a string
* use ostringstream for writing to a string

**EG**
int lo = ...., hi= .....
ostingstream ss;
ss<<"Enter a # between "<<lo<<" and "<<high;
string s=ss.str();
cout<<s<<endl;

**EG** converting a sting to a #
```c++
int n;
while(true){
    cout<<"Enter a #"<<endl;
    sting s;
    cin >> s; \\will not fail. no bad strings.
    istreamstream ss(s);
    if(ss>n) break;
    cout<<"Not a number"<<endl;
}
```

Strings in C++
-

* In C arrays of characters. Terminated by \0 (null)
* Need to explicitly manage memory
* Need to allocate when strings get bigger
* Deallocate when done
* can overwrite \0 for a huge disaster

* In C++ we do have strings
* Grow and shrink as needed (no memory memory management)
* Safter to manipulate

**EG**
* string s="Hello";
* "Hello" is a c-style sting
* Null terminated hello array
* H E L L O \0
* on initialization "Hello" is converted to a c++ string


**Things that you can do with strings**
* Equality s1==s2
* Inequality s1!=s2. strings are not pointers!
* Comparison s1<=s2
* Length s1.length()
* Extract chars s1[0], s1[1], ...
* Concatenation sting s3=s1+s2

Default Arguments
-

```c++
void print suiteFile(string name="suite.txt"){
    ifstream f(name.c_str()); //stream initializer requires a C style string.
_.c_str() produces one. This is one of the only times you need to go back to C
style strings in c++.
    string s;
    while(f>>s) cout<<s<<endl;
}

printSuiteFile("Suite2.txt")//prints suite2.txt
printSuiteFile();//Prints suite.txt
```
Note: optimal params must be last

Overloading
-

In C: 
```c
int negInt(inta){
    return -a;
}
bool negBool(bool b){
    return !b;
}
```
In C++ functions with different paramater lists can share the same name.
(overloading)
```c++
int neg(int a){
    return -a;
}
bool neg(bool b){
    return !b;
}
```

* Compiler uses the number of types of the arguments to pick the right "neg" to
use.
* overloads must differ in number of types of arguments
* may not differ on just return type
* We've sen this already
* <<,>> are overloaded. Bitshift or I/O
* behaviour changes based on type of args

Declaration Before Use
-
* cannot use something before its declared.
* Mutual recursion?
```c++
bool even(unsigned n){
    if (n==0) return true;
    return odd(n-1);
}
bool odd(unsigned n){
    if(n==0) return false;
    return even(n-1);
}
```
* fails 0 odd is not delcared at the point where it is used
* solution: introduce a forward declaratin 

```c++
bool odd(unsigned n);//forward decleration
bool even(unsigned n){
    if (n==0) return true;
    return odd(n-1);
}
bool odd(unsigned n){
    if(n==0) return false;
    return even(n-1);
}
```

Important distinction between
* **declaration** only asserts the existence of the entity. 
* eg bool odd(unsigned);
* **definition** all details, implementation, including allocation of space if
  necessary.
* eg bool odd(unsigned n){...}

**Note**
* decleration (not definition) before use
* An entity can be declared several times, but defined only once

**Pointers**
* Recall: 
* int n=5;
*int *p = &n;
* p is a pointer to an int
* p contains the address of n
* cout<<p<<endl;//hex#
* cout<<*p<<endl;//5
* int **pp; /ptr to ptr to int
* pp=&p;
* **pp=10;//n becomes 10

**Arrays**
* int a[]={(1,2,4,8)};
* an array is not a pointer
* The name of the array is shorthand for the address of the first element
  (&a[0])
* a==&a[0]
* *a==a[0]
* *(a+1)==a[0]

**Structs**
```C
struct Node{
    int data;
    struct Node *next;
}; //Dont forget the semicolon. Java does not need it. It comes to us from C.
We use it so we can do this

struct Node{
    int data;
    struct Node *next;
} n1, n2; 
//In C++ we dont need the struct

struct Node{
    int data;
    Node *next;
}; 

//Why is this wrong?

sturct Node{
    int data;
    node next;
};
//It is bad because... how big is a node? 4bytes + size of node. We need to
know size of node if we want to allocate a node. We know what the size of a
pointer is.
```

**constants**
* const int maxGrade=100;
* must be initalized
* should make as many things const as you can
* const Node n1={5,NULL}
* What does this mean?
* const int *p=&n;
* let p point to n which is 5.
* this is a pointer to a constant int
* you can make it point to somethign else. (p can be reassigned. p=&m)
* the thing that p is pointing to can not be mutated. (*p=10 wont work)
* you can still make the change to n or m its self
* to read c++ decleration start at variable and work out
* p is a pointer to a constant integer 
* compare
* int *const p=&n
* p is a constant pointer to integer
* p is a constant pointer to a non-constant int
* cant change where p points 
* cont int * const p=&n
```

**Parameter Passing**
```c++
 void inc(int n){
    n+=1;
}

int x=5
inc(x);
cout<<x<<endl; // prits 5
```

* Parameters in c++ are passed by value. 
* inc gets a copy of x, increments the copy
* original unchanged
* If a function must modif, its argument must be a pointer
```c++
void inc(int *n){
    *n+=1;
}
int x=5
inc (&x);
cout<<x<<endl;//6
```
* x's address is passed by value
* inc changes the data at that address
* visible to caller

**Q** Why cin >> x and not cin >>(&x)?
**A** C++ provides another pointer-like type known as the reference

```c++
int y=10;
int &z=y; 
// z is a reference to int. Like a const ponter. similar to int *const z=&y;
```
Refs are oke cont ptrs with automatic dereferencing
z=12; (NOT *z =12;)
y is now 12;

* int *p=&z;
* gives the address of y
* anything i try and do with z does it to y.

I will add to my notes
