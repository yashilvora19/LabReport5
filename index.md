# Lab Report 5

## Optimizing Lab Report 4 using a Bash Script

This lab report will take a closer look at the sequence of commands that we ran in lab report 4. I will make use of a bashscript to make all the commands run together instead of typing them in the terminal and running them individually. This will save a lot of time and work at a very fast speed every time.

**Note:** We will assume that the fork of the repository exists in our github account. 

# Making the bash script

I wrote a bash script to carry out all the tasks simultaneously. At the start I tried including the `ssh` command in the bash script but realized that it will stop running when I'm in the remote server and resume when I run it locally. Hence, I first logged into the remote server using `ssh cs15lwi23aqv@ieng6.ucsd.edu` command annd then ran the bash script in the ieng6 server. Here is the code for the bash script:

```
# Cloning the repository
git clone git@github.com:Yonder-Deep/lab7.git
# Changing directory to lab7
cd lab7

# Compiling and running the tester (which gives an error)
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests

# Editting the text file using sed
sed -i '43s/index1/index2/g' ListExamples.java

# Compiling and running the tester (all tests pass)
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests

# Adding, committing, and pushing the changes
git add ListExamples.java
git commit -m "[FIXED] Error in code"
git push
```

Here is what this bash script does step-by-step.

1. Cloning the repository using the `git clone` command.
2. Changing directory to `lab7` where all the files are stored.
3. Compiling and running the files using the `javac` and `java` commands. Running this command should give an output of failed JUnit tests.
4. This step was important since it editted the file without using the `nano` command. I wanted to look for a way to edit files using a bash script and found a powerful command called `sed`. This command `sed -i '43s/index2/index1/g' ListExamples.java` goes to line 43 in 'ListExamples.java' and replaces 'index1' with 'index2'. This fixes the bug of an infinite loop and makes sure the tests pass.
5. Compiling and running the files using the `javac` and `java` commands. Running this command should now give an output of all JUnit tests passing.
6. Using `git add`, `git commit`, and `git push` to save the changes to GitHub.

All of these commmands worked successfully and the output could be seen in the terminal. Creating a bashscript made the entire process much more faster and made me realize the power of how useful these scripts can be in carrying out complicated tasks such as these.

Here is what the output looked like on my terminal.



