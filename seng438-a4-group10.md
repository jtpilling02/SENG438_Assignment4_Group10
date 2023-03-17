**SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report \#4 – Mutation Testing and Web App Testing**

| Group: 10      |
|-----------------|
|J. Ty|   
|Kairos|   
|Luis|   
|Sayma|

# Table of Contents
1. [Introduction](#introduction)
2. [Analysis of 10 Mutants of the Range class](#par1)
3. [Statistics and the mutation score for each test class](#par2)
4. [Effectiveness of each of the test classes.](#par3)
5. [Effect of equivalent mutants on mutation score accuracy](#par4)
6. [How to improve the mutation score of test suites.](#par5)
7. [Advantages and disadvantages of mutation testing.](#par6)
8. [SELENIUM test case design process](#par7)
9. [Use of assertions and checkpoints](#par8)
10. [How did you test each functionality with different test data](#par9)
11. [Advantages and disadvantages of Selenium vs Sikulix](#par10)
12. [How team work/effor was divided and managed](#par11)
13. [Difficulties encountered, challanges overcome, and lessons learned](#par12)
14. [Comments/feedback on the lab itself.](#par13)

# Introduction <a name="introduction"></a>
In this lab, we were tasked with two separate tasks to complete. The first task was to use mutation testing to further the coverage our previously made test cases for *Range* and *DataUtilities.* The second portion of this assignment was to use *SELENIUM IDE* plug-in to perform automated GUI testing on a popular website, in this case *amazon.ca*. 
# Analysis of 10 Mutants of the Range class <a name="par1"></a>

|Test Case|Mutant|Explanation|
|------|------|------|
|![Alt text](/media/tc1.png?raw=true "Test Case 1")|Substituted -9.0 with -1.0 (survived)|Since only the upper bound is returned and the mutant changes the lower bound values, the mutant survives and the test passes.|
|![Alt text](/media/tc2.png?raw=true "Test Case 2")|Substituted -9.0 with 9.0 (killed)|Since only the upper bound is returned and the mutant changes to the previous lower bound to be the new upper bound, the mutant is killed and the test fails.|
|![Alt text](/media/tc3.png?raw=true "Test Case 3")|Substituted -9.0 with -1.0 (survived)|Since only the upper bound is returned and the mutant changes the lower bound values, the mutant survives and the test passes.|
|![Alt text](/media/tc4.png?raw=true "Test Case 4")|Substituted .000000001 with 1.0 (survived)|Since the only value being adjusted is the decimal point formatting of the answer, the length value does not change and thus the mutant survives ad the test passes.|
|![Alt text](/media/tc5.png?raw=true "Test Case 5")|Substituted 0 with 1.0 in ExampleRange1 (killed)|Since the upper bound of the range is adjusted by 1, the total length changes and the mutant is killed, since the test fails.|
|![Alt text](/media/tc6.png?raw=true "Test Case 6")|Substituted 2147483647 with 1.0 in ExampleRange2 (killed)|Since the upper bound of the range is changed to 1, the total length changes and the mutant is killed, since the test fails.|
|![Alt text](/media/tc7.png?raw=true "Test Case 7")|Substitute 3.0 with 1.0 (survived)|Since only the upper bound is changed, and only the lower bound is changed by the mutant, the mutant survives and the test passes.|
|![Alt text](/media/tc8.png?raw=true "Test Case 8")|Substituted 1.0 with -1.0 in ExampleRange1 (killed)|Since the upper bound of 1.0 is changed to -1.0 the range no longer contains the value 0, thus the mutant is killed and the test fails.|
|![Alt text](/media/tc9.png?raw=true "Test Case 9")|Removed call to org/free/data/Range::contains (killed)|Since the assertTrue no longer calls the contains method, the mutant is killed and the test fails.|
|![Alt text](/media/tc10.png?raw=true "Test Case 10")|Substitute 6.0 with 5.0 in ExampleRange4 (survived)|Since the upper bound is changed from 6 to 5, the value of -1 is still not within the range, and thus the mutant survives and the test passes.|

# Statistics and the mutation score for each test class <a name="par2"></a>
Below in *Figure 1* are the mutation score statistics for the *Range* and *DataUtilities* classes before we adjusted any of our test suite from Assignment 3. *Figure 2* showcases the new mutation score statistics after we adjusted the mutation score of our test suite.

*Figure 1 - Mutation Coverage from Assignment 3*
![Alt text](/media/originalmut.jpg?raw=true "Original Mutation Coverage")
*Figure 2 - Mutation Coverage from Assignment 4*
![Alt text](/media/newmut.jpg?raw=true "New Mutation Coverage")

# Effectiveness of each of the test classes <a name="par3"></a>

# Effect of equivalent mutants on mutation score accuracy <a name="par4"></a>

# How to improve the mutation score of test suites <a name="par5"></a>

# Advantages and disadvantages of mutation testing <a name="par6"></a>
One of the biggest advantages of mutation testing is that it helps create a reliable and stable end program for the user, as it tests ambiguities within the source code itself. It also provides a high amount of overall coverage of the source program, along with a high amount of error detection. The largest drawback of mutation testing is the amount of time that it takes to perform. Due to this large time cost, it also likely requires external tools to help automate the mutation testing in order to actually complete the tests in a reasonable amount of time. Finally, due to mutation testing directly affecting the source code, it is not a valid to be used of testing for a black box testing process. 
# SELENIUM test case design process <a name="par7"></a>
In order to design our test cases for SELENIUM, each member of our group chose 2 functions of the amazon.ca website to test.
# Use of assertions and checkpoints <a name="par8"></a>

# how did you test each functionality with different test data <a name="par9"></a>

# Advantages and disadvantages of Selenium vs. Sikulix <a name="par10"></a>
One of the biggest advantages of the Selenium IDE plug-in was that any actions that are performed on the root website are automatically recorded and can be replayed at any point in time. This saves a lot of time for developers carrying out end-to-end tests as they do not have to learn how to get the web locators manually as well as recording it in a language such as python or javascript using Robot Framework.

One of the biggest disadvantages of Sikulix IDE is that there is no record and replay functionality that is built-in to the IDE, which requires developers carrying out end-to-end testing to manually write test cases. The syntax to write the test case can be hard to pick up, which makes it harder for teams to develop test cases rapidly. Our team greatly appreciates the convenience and ease of use that Selenium brings, which is not provided by Sikulix.

# How the team work/effort was divided and managed <a name="par11"></a>

Our team came together to generate the mutation testing reports based on the original test suites that we submitted for the previous assignment. We then split into pairs and worked on the two classes concurrently, where we reviewed the mutants generated by PIT and managed to change our test suites such that each mutation coverage increased by at least 10%.

For the selenium portion of the assignment, we managed to set up and record test cases individually during the lab session. We then shared our findings and made sure that the test suites were sufficient by giving feedback to one another. Following which, we managed to deconflict the functionality to demonstrate during the next lab session, where we will have to demonstrate the test to the TA.

Overall, the work and effort was divided and managed equally amongst the group members.

# Difficulties encountered, challenges overcome, and lessons learned <a name="par12"></a>

One of the biggest difficulties that we faced was setting up the new project and figuring out why the PIT mutation tests weren’t running. After troubleshooting the issue at hand and referring to the guides available online, we found out that some of the libraries provided were not working. We overcame this challenge by importing the libraries from Assignment 2, which proved to work and we could run our PIT mutation tests.

The lesson learnt from this issue we had is to understand how the tool works, and not just blindly use it based on a set of instructions. It is imperative to understand how mutation testing works at its core, and analyze the validity of the results presented by this tool. We should also be wary of how the dependencies and libraries affect the way our test suites work.

# Comments/feedback on the lab itself <a name=”par13”></a>

Overall, this lab was extremely insightful and we managed to learn in-depth on how mutation testing can be carried out with a tool and how to effectively use Selenium IDE plug-in to carry out end-to-end functionality testing. These set of skills that we acquired provides us with practical skill sets, which can be applied into our future careers as software engineers. The lab also showed us that testing should be treated seriously so that we can weed out any potential errors or faults, so as to prevent failures in the systems. With tools such as PIT and selenium, we can be slightly more confident in the code that we write during the development process.
