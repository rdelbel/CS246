Human vs Machine Testing
=
**Human Testing** 
-humans read code and look for failutres
**Machine Testing** 
-run the program on selected inputs, check against spec 
-can't test everything - need to choose carefully

**Black-box testing** no knoweldge of implementation
**White-box testing** full knoweldge of implementation
**Grey-box testing** some knoweldge of implementation
How to Test
-
* Start with black-box, supplement with white-box
* check various classes of input, eg numeric ranges, positive vs negative,
differences between ranges (edge cases)
* Multiple simulataneous boundaries (corner cases)
* Extreme Cases 
* Intuition and experience

White box Testing
-
* check all logical paths through the program
* make sure every function runs
* Test loops that run 0, 1, many times
* Keep tests as small as possible and have many of them

Questions that testing can answer
-
* Does my program work? (correct?) Functional testing
* Did my change just break something

