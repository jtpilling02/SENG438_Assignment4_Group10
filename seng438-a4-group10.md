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
4. [Effect of equivalent mutants on mutation score accuracy](#par4)
5. [How to improve the mutation score of test suites.](#par5)
6. [Advantages and disadvantages of mutation testing.](#par6)
7. [SELENIUM test case design process](#par7)
8. [Use of assertions and checkpoints](#par8)
9. [How did you test each functionality with different test data](#par9)
10. [Advantages and disadvantages of Selenium vs Sikulix](#par10)
11. [How team work/effor was divided and managed](#par11)
12. [Difficulties encountered, challanges overcome, and lessons learned](#par12)
13. [Comments/feedback on the lab itself.](#par13)

# Introduction <a name="introduction"></a>
In this lab, we were tasked with two separate tasks to complete. The first task was to use mutation testing to further the coverage our previously made test cases for `Range` and `DataUtilities.` The second portion of this assignment was to use `SELENIUM IDE` plug-in to perform automated GUI testing on a popular website, in this case *amazon.ca*. 
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
Below in *Figure 1* are the mutation score statistics for the `Range` and `DataUtilities` classes before we adjusted any of our test suite from Assignment 3. *Figure 2* showcases the new mutation score statistics after we adjusted the mutation score of our test suite.

*Figure 1 - Mutation Coverage from Assignment 3*
![Alt text](/media/originalmut.jpg?raw=true "Original Mutation Coverage")
*Figure 2 - Mutation Coverage from Assignment 4*
![Alt text](/media/newmut.jpg?raw=true "New Mutation Coverage")

Here you can see that both of the classes mutation coverage increased by over 10% after our adjustments to our test cases. For our test cases, it can be seen that our `Range` test suite is overall effective, as it kills more mutants that survive. The same is not true for our `DataUtilities` test suite, since it had more suriving mutants than those that were killed.

# Effect of equivalent mutants on mutation score accuracy <a name="par4"></a>
Equivalent mutants are mutations that exhibit the exact behaviour of the program in which they mutated from. They effective act as a sort of false positive within the test case, and thus cannot be caught by a test case. One way in which a equivelent mutant can be determined after the execution of a mutation test is that all killed mutants will never be an equivalent mutant, as they exhibited different behaviour from the program. Therefore, we know that any equivalent mutants were either not covered due to lack of coverage, or survived.
A mutation score should not be impacted by the amount of equivalent mutations within a system, as the mutation score is the number of killed mutants divided by the total number of non-equivalent mutants.

Some of the equivalent mutants found within our test suite were many test cases within `Range` in which the value that was determined was set to a specific decimal length using *0.000000001d* and was changed to another number. This lead to equivalent mutants as these test cases were not affected by the amount of decimal places included in the final result.

Currently the main way of finding equivalent mutants would be to go through all of the surviving mutants in the system and check each one by hand to see if they are equivalent or not based on what was changed within the code. Automatically finding equivalent mutants is still a difficult task to do, and has not been fully perfected. One way in which this might be possible is through the use of constraining the type of test cases that are created, so that no equivalent mutants are created to begin with.
One major advantage of this would be cutting down both the execution time of mutation testing, and remove the need to look for equivalent mutants afterwards. One disadvantage of this strategy would be the time it would take to create and calculate a script to constrain test cases. This idea assumes that it is even possible to set limitations on what can and cannot be mutated within a test case.
# How to improve the mutation score of test suites <a name="par5"></a>
In order to increase the mutation scores of a test suite, the amount of surviving mutants needs to go down, and the amount of killed mutants needs to rise. We did this by looking at the list of surviving mutants within our test suites, and then designing new test cases in which the mutant is still used, but the test is designed to fail. This will cause the mutation to be killed.
# Advantages and disadvantages of mutation testing <a name="par6"></a>
One of the biggest advantages of mutation testing is that it helps create a reliable and stable end program for the user, as it tests ambiguities within the source code itself. It also provides a high amount of overall coverage of the source program, along with a high amount of error detection. The largest drawback of mutation testing is the amount of time that it takes to perform. Due to this large time cost, it also likely requires external tools to help automate the mutation testing in order to actually complete the tests in a reasonable amount of time. Finally, due to mutation testing directly affecting the source code, it is not a valid to be used of testing for a black box testing process. 
# SELENIUM test case design process <a name="par7"></a>
In order to design our test cases for SELENIUM, each member of our group chose 2 functions of the amazon.ca website to test. We avoided any test cases in which we needed to log in to an account, since when you log into an account SELENIUM will store the username and passwords within the test script, and we did not want to put any of our information onto a public repository for anyone to access. Because of this, we each just tested some functionalities within the site that required no account to use.
# Use of assertions and checkpoints <a name="par8"></a>
Since we did not use any login systems due to the reasons stated above, and mainly just tested button based functionalities we did not use any assertions, as we were unable to assert that anything was true. We used some checkpoints in the form of breakpoints just to confirm that the desired outcome occured within the script.
# how did you test each functionality with different test data <a name="par9"></a>
For many of our test cases, we used the scripts in multiple ways (such as for changing language from English to French and back to English). This was the best way we found to adjust the data in which our test scripts used. Any tests that did not use this technique, we found it unsuitable to adjust the data, as they were just testing the functionalities of static buttons on the site.
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
