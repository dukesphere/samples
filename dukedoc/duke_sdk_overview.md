---
title: Getting Started with an SDK
keywords: testDuke, retestDuke, etcDuke
last_updated: July 7, 2016
summary: "Sanitized sample from a proprietary SDK doc"
sidebar: dukedocs_sidebar
permalink: /duke_sdk_overview/
---

Here, you build and run a sample application, HelloCodeCheck, then send the defects it 
finds to the CodeChecker database. Note that this documentation assumes that you are 
familiar with basic [CodeChecker commands](../placeholder).

**Requirement:**

* You must have access to an installation of CodeChecker and a valid license for it. 

**Recommended:**

* As a best practice, you (or a CodeChecker administrator) should set up a separate 
_project_ in the CodeChecker UI with a test _lane_ into which you can send defects 
found by the HelloCodeCheck application. You will need the _project_ name and a 
CodeChecker role that gives you permission to send reports of defects to the database 
and to view them in the _lane_. See [CodeChecker administration](../placeholder) for
details.

### Writing the HelloCodeCheck application {#write}

In this procedure, you create a simple CodeChecker SDK application (`hello_codecheck.cpp`) 
designed to print every defect that is passed into `SOME_FUNCTION`. In subsequent 
procedures, you will compile and run this application on some sample source code, then 
send the defects that it finds in a code sample to the CodeChecker UI.

1. Type or copy the following source code into a text editor:

   `PROPRIETARY SAMPLE CODE REMOVED FROM THIS WRITING SAMPLE`
    
   The source code and makefile for this application are located in the 
   `<install_dir>/sdk/samples/hello_codecheck` directory.

2. Save this file as `hello_codecheck.cpp` in a directory that is outside of the 
   CodeChecker SDK installation directory.

   Saving the file inside of the installation directory can make the upgrade process for
   CodeCheck SDK more difficult.

### Compiling HelloCodeCheck (hello_codecheck.cpp) {#compile}

Here, you compile the `hello_codecheck.cpp` source code you created in
[Writing the HelloCodeCheck application](#write).

1. From your source directory that contains `hello_codecheck.cpp`, invoke the 
   `build-app` command:

   ```
   > <install_dir>/sdk/build-app hello_codecheck
   ```
   
   * Note that the argument is `hello_codecheck`, not `hello_codecheck.cpp`.
   
   * `<install_dir>` is the CodeChecker root directory.
   
   Upon success, the build command prints the following:

   ```
   SUCCESS! Your application has been compiled to ./hello_codecheck
   ```
   
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

2. Locate the following output in your source directory:

     * `hello_codecheck` (on Unix)
     * `hello_codecheck.exe` (on Windows)

    This output is your custom CodeCheck application, similar to `another_command`, 
    except that `hello_codecheck` and `hello_codecheck.exe` only run one CodeChecker 
    application, rather than the built-in suite of CodeChecker applications.
    
### Preparing source code for analysis {#prepare}

1. Provide some sample code for the `hello_codecheck` to analyze.

   For example, you can save the following code as a file called 
   `test_code/hello_codecheck_test.c`:

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

   **Note:**
   We recommend that you use one of the compilers above to complete this demonstration. 
   However, if you want to try a different compiler, you can set it up instead and 
   adjust the steps below to use the appropriate command-line syntax for that compiler 
   and operating system.  
 
   For all supported configurations, see [compilers](../placeholder).

3. Prepare your test code for analysis.

   On Unix:

   ```
   > <install_dir>/bin/compile-app \ 
     --dir my_dir gcc \
     -c path/to/hello_codecheck.test.c
   ```
   
   On Windows:
   
   ```
   > <install_dir>\bin\compile-app --dir my_dir cl path\to\hello_codecheck.test.c
   ```
   
   `--dir my_dir` is a name you provide for the directory into which your analysis
   results will go. 
   
   Upon success, this command prints the following output:
   
   ```
   PROPRIETARY DETAILS OMITTED FROM THIS WRITING SAMPLE.
   
   The compile-app utility completed successfully.
   ```

### Running HelloCodeCheck (`hello_codecheck`) on source code {#run}

1. Copy `hello_codecheck` into the CodeChecker `bin` directory.
   
   For example, on Unix:
   
   ```
   > cp hello_codecheck <install_dir>/bin
   ```
   
   On Windows:
   
   ```
   > cp hello_codecheck <install_dir>\bin
   ```
   
2. Run `hello_codecheck` from your source code directory:

   ```
   > cd <HELLO>
   > <install_dir>/bin/hello_codecheck --dir my_dir --force
   ```
   
   **Note:**
   The options to the `hello_codecheck` application are the same as those for 
   `another-command`.
   
   The output looks something like the following:
   
   ```
   [PROPRIETARY DETAILS OMITTED FROM THIS WRITING SAMPLE]
   ```
   
   Aside from the usual `another-command` text, the output consists of one line for 
   each call to the `NAME_OMITTED` function.
   
   The application also creates `my_dir/<programming_language>/output/hello.errors.xml`, 
   which contains the output in a format that can be sent to the database for the 
   CodeChecker UI.

### Sending the defect reports to the CodeChecker database

Just as you can send the output of `another-command` to CodeChecker, you can also send 
the defects that HelloCodeCheck finds.

1. Prepare CodeChecker to receive the defect report:
   1. Start the CodeChecker UI.
   
      The startup command is located in the CodeChecker `/bin` directory:
      
      ```
      > cd <install_dir>/bin 
      > ./start-cc
      ```
      
   2. Log into the CodeChecker UI.

   3. Create a _lane_ that is configured with a _project_ for the C/C++ programming language.

      For example: `hello_codecheck` in the `codechecker_sdk _project`.
    
      **Note:**
    
      If you need help with any of these steps, contact your CodeChecker UI administrator.

2. Use the `send-stuff` command to send the defect data to the CodeChecker database:

   ```
   > <install_dir>/bin/send-stuff \
     --host <server_hostname> \
     --port <port_number> \
     --name hello_codecheck \
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
   
{% include glossary.md %}