GHS Code Size
=============

Crunch GHS NM output to determine what code is taking up the most space

Author:   Chip Boling
  Date:   Dec. 18, 2014

When using GNM to create the input file, use the '-h -v -p -no_debug -S -a -X' options
for best results.  For example, with **input.bin** as the ELF image create by *multi* and
**nm.txt** as the path/filename.

    $ gnm -h -v -p -no_debug -S -a -X input.bin > /tmp/nm.output.txt

Requirements
------------
The only requirement is for a recent version of the *R* programming language.  This script
was tested under version 3.1.2 of *R* and developed/debugged with *RStudio* version 0.98.1091.
*RStudio* is not required to run this program.  The program makes uses of the *data.table*, 
*stringr*, *plyr*, and *getopt* libraries but the script will auto-install these if needed as
well as any other libraries these main libraries may require.

*R* is available for most platforms (Linux, Windows, Mac) from http://r-project.org

Should you have trouble with the auto-install of any packages, you can manually install them
using the command:

    $ R
    > install.packages("pkg-name")  <-- where pkg-name is the name of the package such as Rcpp
    > ^d                            <-- to exit the R shell

To install *R* under Ubuntu, you can use:  **sudo apt-get install r-base r-base-dev**

If the downloaded version of *R* is less than version **3**, you may need to specify a different
linux install location such as:

    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
    sudo sh -c "echo 'deb http://streaming.stat.iastate.edu/CRAN/bin/linux/ubuntu quantal/' >>  /etc/apt/sources.list" 
    sudo apt-get update 
    sudo apt-get install r-base r-base-dev

Running the program
-------------------

Then run the script, make sure that 'codeSize.R' is executable, (**chmod +x codesize.R** on
Linux) and then just enter command below.

    $ *./codeSize.R*.

To see allowed options, enter the command:
    
    $ ./codeSize.R --help
    Usage: ./codeSize.R [--file|f] <file>]
                        [--symSize|s <octets>]
                        [--secSize|S] <minSecoctetstSize>]
                        [--maxSymb|m <octets>]
                        [--dirSize|D] <octets>]
                        [--fileSize|F <octets>]
                        [--maxLines|m <lines>]
                        [--verbose|v] [--help|?]
    where:
        -f|--file       The input file path, default is nm.txt in the current working directory
        -s|--symSize    Discard symbols smaller than this. Default is 1 octet
        -S|--secSize    Discard sections smaller than this. Default is 256 octets
        -m|--maxSymb    Only report symbols this size and larger in max symbol report. Deault is 4096 octets
        -D|--dirSize    Size that the sum of all symbols in a directory (and subdirectories) must be to make it into the directory report. Default is 128K.
        -F|--fileSize   Size that the sum of all symbols in a file must be to make it into the file report.  Default is 64K.
        -m|--maxLines   Maximum number of output lines per report/sub-report for sections that may have many.  Default is 100.
        -v|--verbose    Enable verbose output
        -?|--help       Print out help text

The output will is sent to *stdout*

The parameters to the *code_size* function are:

Parameter       | Description
--------------- | ---------------------------------
inputFile       | Input NM filename created with GHS *'gnm'* and the *'-h -v -p -S -a -X'* options.  Default is **'ram.nm.txt'**
inputDir        | Input base directory.  Default is the current working directory
minSymSize      | Minimum symbol size (in octets). All symbols smaller than this will be discarded. Default is **1 octet** (*zero* length symbols discarded)
minSectSize     | Minimum section size (in octets). All sections smaller than this will be discarded. Default is **256 octets**
maxSymbolCutoff | Size a symbol must be to make it into the maximum symbol report. Default is **4096 octets**
maxDirectoryCuttoff | Size that the sum of all symbols in a directory (and subdirectories) must be to make it into the directory report. Default is 128K.
maxFileCuttoff  | Size that the sum of all symbols in a file must be to make it into the file report.  Default is 64K.
verbose         | Verbose output flag for debugging purposes

Sample Output
-------------

Below is some sample (and condensed) output from the program.

    **TODO**
