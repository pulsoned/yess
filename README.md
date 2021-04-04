
YESS (Y86 Simulator)
========
 
YESS is a (currently incomplete) working simulator of the Y86 assembly architecture.  It allows you to input a text file containing working Y86 code and will simulate that code as if run by the Y86 architecture.
 
Features
--------
 
- Simulates a working Y86 architecture
- Allows user-inputted Y86 code to be run
- Is very cool
 
Installation
------------
 
Install YESS by downloading [here](https://github.com/pulsoned/yess)* or use: 

    $ git clone https://github.com/pulsoned/yess

and run via unix bash.
 
<sub>*note that the current implementation of the YESS is incomplete and will not currently run Y86 code fully.</sub>
    
Support
-------
 
If you are having issues or would like to report a bug, you can contact me at [pulsoned@appstate.edu](mailto:pulsoned@appstate.edu).

FAQs
-------
***What is this program used for?***

Mostly, this program is an exercise in my basic understanding of C++ and Computer Systems, however it can (or will be able to) be used to successfully run working Y86 code.

***When will the YESS be complete?***

The YESS should be complete by the end of April at the latest.

Contribute
----------
 
Contribution is currently not supported due to the YESS being in an unfinished state. Since the program is a project for an ongoing course, the code cannot be open-source without violating Appalachian State's Academic Integrity Code. However, you are more than welcome to contact me to report a bug at [pulsoned@appstate.edu](mailto:pulsoned@appstate.edu).

How to use
-------
 
Navigate to the folder that contains `yess` and ensure you have a file of the type `.yo` somewhere in your directory, then simply type:

    ./yess -fdemw <filepath>/<yofilename>.yo

where `<filepath>` is the path to the file you'd like to run and `<yofilename>` is the name of the file, press enter, and your file will run! You may select specific stages of the Y86 pipeline you would like to run with the command-line argument as shown in the example, `-fdemw`, although it is advised to run every stage as not doing so may cause problems in, especially in the current unfinished state of the YESS.
