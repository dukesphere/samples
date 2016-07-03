---
title: SDK Overview
keywords: testDuke, retestDuke, etcDuke
last_updated: June 30, 2016
summary: "Sanitized version a Getting Started section for a proprietary SDK"
sidebar: product1_sidebar
permalink: /duke_sdk_overview/
---

Here, you build and run a sample application, HelloCodeCheck, then send the defects it 
finds to the CodeChecker database. Note that this documentation assumes that you are 
familiar with basic Code Analyzer commands.

**Requirements:**

* You must have an installation of the CodeChecker UI with a valid license. 

* You must have access to an installation of Code Analyzer. 


**Recommended:**

As a best practice, you (or a CodeChecker administrator) should set up a separate 
_project_ in the CodeChecker UI with a test _channel_ into which you can send defects 
found by the HelloCodeCheck application. You will need the _project_ name and a 
CodeCheck role that gives you permission to send reports of defects to the database 
and to view them in the _channel_.


### Writing the HelloCodeCheck application {#write}

In this section, you create a simple CodeCheck SDK application (`hello_codecheck.cpp`) 
designed to print every defect that is passed into `SOME_FUNCTION`. In subsequent sections, 
you will compile and run this application, then send the defects that it finds in a code 
sample to the CodeCheck UI.

**To create the HelloCodeCheck application:**

1. Type or copy the following source code into a text editor:

   `PROPRIETARY SAMPLE CODE REMOVED FROM THIS WRITING SAMPLE`
    
   The source code and makefile for this application are located in the 
   `<install_dir>/sdk/samples/hello_codecheck` directory.

   Unlike CodeAnalyzer, this application restricts the level of information that is 
   returned by using an `if` statement before calling some_function.

2. Save this file as `hello_codecheck.cpp` in a directory that is outside of the CodeCheck SDK 
   installation directory.

   Saving the file inside of the installation directory can make the upgrade process for
   CodeCheck SDK more difficult.

### Compiling HelloCodeCheck {#compile}

Here, you compile [HelloCodeCheck source code](#write).

1. From the source directory that contains `hello_codecheck.cpp`, invoke the `build-app` command:

   ```
   > cd mysourcedir
   > <install_dir>/sdk/build-app hello_codecheck
   ```
   
   Note that the argument is `hello_codecheck`, not `hello_codecheck.cpp`.
   
   `<install_dir>` is the CodeCheck root directory.
   
   Upon success, the build command prints the following:

   ```
   SUCCESS! Your application has been compiled to ./hello_codecheck
   ```
   
   If an error occurs, set your `PATH`. 
   
   **Note:**
   
   * On Unix, you can run the makefile for the sample application instead of running 
     `build-app`. This file is located in the  `<install_dir>/sdk/samples/hello_codecheck` 
     directory.
     
   * On Windows, if you see the following error when compiling your application, you 
     must either restart your console as an administrator or make a copy of the samples 
     directory:

     ```     
     C:/Program Files/path/to/sdk/bin/build-app.exe:
     cannot open output file hello_codecheck.exe: Permission denied
     collect2: ld returned 1 exit status
     ERROR: Application "hello_codecheck" did not successfully compile.
     ```
     Locate the following output in your source directory:

     * `hello_codecheck` (on Unix)
     * `hello_codecheck.exe` (on Windows)

    This output is the application, which supports a command-line interface similar to 
    `another-command`, except that `hello_codecheck` and `hello_codecheck.exe` only run 
    one CodeCheck application.

### Running HelloCodeCheck {#run}

1. Create some sample input for the application.

   You can save the following code as a file called `HELLO/test1/hello_codecheck.test.c`:

   ```   
   PROPRIETARY CODE REMOVED FROM THIS WRITING SAMPLE.
   ```

2. Prepare CodeChecker for your compiler.

   For example, to set up gcc and g++ compilers with CodeChecker:
   
   ```
   > cd <install_dir>/bin
   > ./comp-prep --gcc
   ```
   To set up the Microsoft C/C++ compiler cl.exe with CodeChecker:

   ```
   > cd <install_dir>\bin
   > comp-prep --msvc
   ```
   
   For all configurations, see [[fake/nonfunctional link to a list of configs]](#doesntwork).
   
  **Note** 
  
  The remaining steps in this section assume that you are using the Unix-based gcc 
  compiler. If you are using a different compiler, set it up instead, and adjust the 
  command lines to use the appropriate command-line syntax for that compiler and 
  operating system.
   
2. Use `build-app` to generate the CodeCheck application.

   On Unix:

   ```   
   > cd <HELLO>
   > <install_dir>/bin/build-app --dir my_dir gcc -c test1/hello_codecheck.test.c
   ```
   
   On Windows:
   
   ```
   > <install_dir>\bin\build-app --dir my_dir cl test1\hello_codecheck.test.c
   ```
   
   Upon success, this command prints the following output:
   
   ```
   [...]
   
   The build-app utility completed successfully.
   
   This command creates a ... [PROPRIETARY INFO OMITTED]
   
   ```

3. Use HelloCodeCheck (`hello_codecheck`) to analyze your source code:

    1. Copy the application into the Code Analyzer bin directory.
    
       For example, on Unix:
       
       ```    
       > cp hello_codecheck <install_dir>/bin
       ```
       
       On Windows:
       
       ```
       > cp hello_codecheck <install_dir>\bin
       ```
       Run `hello_codecheck` from your <HELLO> directory:

       ```
       > cd <HELLO>
       > <install_dir>/bin/hello_codecheck --dir my_dir --force
       ```        
        **Note:**
        The options to the `hello_codecheck` application are the same as those for 
        the `another-command` command.

        The output looks something like the following:

       ```
       [PROPRIETARY DETAILS OMITTED FROM THIS WRITING SAMPLE]
       ```
       Aside from the usual `another-command` text, the output consists of one line for 
       each call to the NAME_OMITTED function.
       
       The application also creates `my_dir/<programming_language>/output/hello.errors.xml`, 
       which contains the output in a format that can be sent to the CodeChecker UI.

### Sending the defect reports to the CodeChecker UI

Just as you can send the output of `another-command` to CodeChecker, you can also send 
the defects that HelloCodeCheck finds.

1. Prepare CodeChecker to receive the defect report:
   1. Start the CodeChecker UI.
   
      The startup command is located in the CodeChecker `/bin` directory:
      
      ```
      > cd install_dir_acme/bin 
      > ./start-acme
      ```
      
   2. Log into the CodeChecker UI.

   3. Create a _channel_ that is configured with a _project_ for the C/C++ programming language.

      For example: `hello_codecheck` in the `codechecker_sdk _project`.
    
      **Note:**
    
      If you need help with any of these steps, contact your CodeChecker UI administrator.

2. Use the `send-stuff` command to send the defect data to the CodeChecker database:

   ```
   > <install_dir>/bin/send-stuff \
     --host <server_hostname> \
     --port <port_number> \
     --name_omitted hello_widget \
     --user admin \
     --dir my_dir
   ```
   
   This command produces output similar to the following on the console:
   
   ~~~
    Connecting to server sduke-xxxx:9090
    2015-08-06 21:54:57 UTC - Committing 4 xxxxx ...
    |0----------25-----------50----------75---------100|
    ****************************************************
    2015-08-06 21:54:57 UTC - Committing 4 xxxxx ...
    |0----------25-----------50----------75---------100|
    ****************************************************
    2015-08-06 21:54:56 UTC - Calculating 4 xxxxx ...
    |0----------25-----------50----------75---------100|
    ****************************************************
    2015-08-06 21:54:57 UTC - Committing 4 xxxxx ...
    |0----------25-----------50----------75---------100|
    ****************************************************
    2015-08-06 21:54:58 UTC - Committing 0 xxxxx ...
    2015-08-06 21:54:58 UTC - Committing 15 xxxxx ...
    |0----------25-----------50----------75---------100|
    ****************************************************
    2015-08-06 21:54:59 UTC - Committing 3 xxxxx ...
    |0----------25-----------50----------75---------100|
    ****************************************************
    New defect ID 10004 added.
    Elapsed time: 00:00:04
   ~~~
   
### Creating a makefile for convenience

When creating your own applications, you can adapt the HelloCodeCheck makefile 
(`install_dir/samples/hello/Makefile`) and the other makefiles that it includes: 
`application.mk` and `include.mk`.

* Makefile for the HelloCodeCheck application:
  `PROPRIETARY FILE CONTENTS REMOVED FROM THIS WRITING SAMPLE`
  
* The `application.mk` file for the HelloCodeCheck application:

   `PROPRIETARY FILE CONTENTS REMOVED FROM THIS WRITING SAMPLE`

* The `include.mk` file for the HelloCodeCheck application:

   `PROPRIETARY FILE CONTENTS REMOVED FROM THIS WRITING SAMPLE`