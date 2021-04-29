YESS (Y86 Simulator)
========
 
YESS is a working simulator of the Y86 assembly architecture.  It allows you to input a text file containing working Y86 code in the form of a `.yo` file and will simulate that code as if run by the Y86 architecture. After the code is fully simulated, the program will output each cycle of the code as well as showing any changes to the registers and memory.
 
Features
--------
 
- Simulates a working Y86 architecture
- Allows user-inputted Y86 code to be run
- Outputs a comprehensive overview of the code that was run

Materials
--------
A keyboard is required to run the simulator and an internet connection is required to download it. A unix machine along with a working Y86 assembly file with the `.yo` extension are also required to run the program. 

A working `.yo` file looks something like this:

![working yo file](https://user-images.githubusercontent.com/78573722/116626729-c045ab80-a919-11eb-8660-cca34ef8f061.png)

Code Examples
--------
Due to YESS being a project for an ongoing course, not much code may be shared, however, here are some examples of code written for the YESS:

### Main method

 	int main(int argc, char *argv[])
 		{
	 	if (argc < 2){
			 usage();
		 	return 0;
		 }
	
	bool f=false,d=false,e=false,m=false,w=false;
	 char *new_argv = getOptions(argc,argv,&f,&d,&e,&m,&w);

	 char* infile = new_argv;
	 y86.reset();
	 if (y86.load(infile))
	 {
		 y86.setTrace(f,d,e,m,w);   // this must come after the load, before entering while loop
		 bool stop = false;
		 while (!stop)
		 {

			 y86.clock();
			 y86.trace();
			 stop = y86.getStat();
		 }
	 }
    // After exiting simulation loop, always dump state
	y86.dumpProcessorRegisters();
	y86.dumpProgramRegisters();
	y86.dumpMemory();

    return 0;
 	} // end main
 
This method checks the command-line arguments to ensure that there are not too many, that the file is of the correct type, and which stages the simulator should use.

### Y86::readFile method

    int lnNum = 1;
    string line;
    uint64_t address;
    string data;
    unsigned length;
    uint64_t lastAddr = 0;
    unsigned lastLength = 0;
    
    while (getline(infile, line))
    {
      //if poor format do nothing
      if (!checkLine(lastAddr, lastLength, line))
      {
        cout << "Error on line " << lnNum << "\n" << line << endl;
        return false;
      }
      else
      {
        address = getAddress(line);
        data = getData(line);
        length = hasValidData(line);
        if (length)
          writeMemory(data, address);
        lnNum++;
      }

      if (length)
      {
        lastAddr = address;
        lastLength = length;
      }
        memory = mem;
    }

    memory = mem;

    return true;
    }

This method, located in the `Y86.cpp` class, checks to see if each line is valid using several helper functions and loads that line into the simulator.

Installation
------------
 
Install YESS by downloading [here](https://github.com/pulsoned/yess)* 
![how to download](https://user-images.githubusercontent.com/78573722/113520422-fb460080-9560-11eb-9a9a-3e1df536f0e2.png)

or use: 

    $ git clone https://github.com/pulsoned/yess

and run via unix bash.
    
Support
-------
 
If you are having issues or would like to report a bug, you can contact me at [pulsoned@appstate.edu](mailto:pulsoned@appstate.edu).

FAQs
-------
***What is this program used for?***

Mostly, this program is an exercise in my basic understanding of C++ and Computer Systems, however it can (or will be able to) be used to successfully run working Y86 code.

***Why is the program not open-source?***

The YESS is not open source because it is a project completed for a class at Appalachian State University that is still a core part of the CS curriculum, therefore it cannot be open-source without violating ASU's Academic Integrity Code.

Contribute
----------
 
Since the program is a project for an ongoing course, the code cannot be open-source without violating Appalachian State's Academic Integrity Code. However, you are more than welcome to contact me to report a bug at [pulsoned@appstate.edu](mailto:pulsoned@appstate.edu).

How to use
-------
 
Navigate to the folder that contains `yess` and ensure you have a file of the type `.yo` somewhere in your directory, then simply type:

    ./yess -fdemw <filepath>/<yofilename>.yo

where `<filepath>` is the path to the file you'd like to run and `<yofilename>` is the name of the file, press enter, and your file will run! You may select specific stages of the Y86 pipeline you would like to run with the command-line argument as shown in the example, `-fdemw`, by omitting letters from the argument to omit the corresponding stage (in the order of: fetch, decode, execute, memory, and writeback), although it is advised to run every stage as not doing so may cause problems.

![example](https://user-images.githubusercontent.com/78573722/116627634-7eb60000-a91b-11eb-8aa8-88152f387d07.png)

For example, as you can see, the only two files in the directory are the simulator (`yess`), and the `.yo` file, `lab12d.yo`. Using the command as shown will result in the file being fully simulated and will output something like this:

![output](https://user-images.githubusercontent.com/78573722/116627822-d5233e80-a91b-11eb-8ded-f955e6a8f3de.png)

If you scroll up, you will see each cycle in full detail and what instruction is being carried out at any time, similar to the lines starting with `Cycle 148`.
