---
course_id: 6-825-techniques-in-artificial-intelligence-sma-5504-fall-2002
layout: course_section
parent_title: Assignments
title: 'Project 1, Part B: Tools'
type: course
uid: 2ceb9b1b12cdc3aa054dbf4d06429f42

---

  
zChaff

zChaff is a very efficient implementation of the complete SAT solver, Chaff. zChaff takes sentences in CNF form and produces an assignment, if one exists.  
More information about zChaff can be found at the [zChaff homepage](http://www.princeton.edu/~chaff/zchaff.html).  
Information on the standard DIMACS CNF format can be found [here](http://logic.pdmi.ras.ru/~basolver/dimacs.html). Here is ;[one example](/courses/electrical-engineering-and-computer-science/6-825-techniques-in-artificial-intelligence-sma-5504-fall-2002/assignments/test1.dimacs) ;of a CNF sentence in the DIMACS format, and here is ;[another example](/courses/electrical-engineering-and-computer-science/6-825-techniques-in-artificial-intelligence-sma-5504-fall-2002/assignments/test2.dimacs).  
  
To get zChaff, download one of the following files:  

| &nbsp; | Instructions | Tested On |
| [zChaff binary for Linux](/coursemedia/6-825-techniques-in-artificial-intelligence-sma-5504-fall-2002/1e484279d52db2d90a3d6eecb49319ef_zchaff2001217linux.gz) |  {{< br >}}{{< br >}} 1.  Download the gzipped file{{< br >}}2.  Execute: gunzip zchaff.2001.2.17.linux.gz{{< br >}}3.  Execute: chmod +x zchaff.2001.2.17.linux{{< br >}}4.  To Run: ./zchaff.2001.2.17.linux ;test1.dimacs {{< br >}}{{< br >}}  | RedHat Linux 6.2, Debian GNU/Linux 2.4.9, Mandrake 8.0 |
| [zChaff binary for Solaris](/coursemedia/6-825-techniques-in-artificial-intelligence-sma-5504-fall-2002/0f4f40c0262b72e94df669611bca7011_zchaff2001217solaris.gz) |  {{< br >}}{{< br >}} 1.  Download the gzipped file{{< br >}}2.  Execute: gunzip zchaff.2001.2.17.solaris.gz{{< br >}}3.  Execute: chmod +x zchaff.2001.2.17.solaris{{< br >}}4.  To Run: ./zchaff.2001.2.17.solaris test1.dimacs {{< br >}}{{< br >}}  | Athena |
| [zChaff C++ source code](/coursemedia/6-825-techniques-in-artificial-intelligence-sma-5504-fall-2002/0f40483f080d35f36254b06e7cad62ce_zchaff2001217srctar.gz) |  {{< br >}}{{< br >}} 1.  Download the gzipped tar file{{< br >}}2.  Execute: gunzip zchaff.2001.2.17.src.tar.gz{{< br >}}3.  Execute: tar -xvf zchaff.2001.2.17.src.tar{{< br >}}4.  Execute: make  {{< br >}}    or  {{< br >}}    make TARGET{{< br >}}5.  To Run: ./asap test1.dimacs {{< br >}}{{< br >}}  | Compiles and runs on Debian GNU/Linux 2.4.9 and Mandrake 8.0, but not on RedHat 6.2.  {{< br >}}Requires libstdc++-libc6.1-2.so.3 

What remains is to turn sentences in our CNF format into DIMACS format, and to turn zChaff's assignments into Interpretations for the original sentences.  
We have written routines to do the two conversions as part of the ; techniques.PL.CNF class.  
  
Here is how you can use the routines:  

1.  In your program, convert the CNF sentence into a DIMACS-format sentence, and record the mapping of CNF variable names to DIMACS variable names:
    
    *   CNF.pl2dimacs( CnfFilenameString ); ;// creates two files: "CnfFilenameString.dimacs" and "CnfFilenameString.dimacs.map"
    *   CNF.pl2dimacs( CnfFilenameString, DimacsFilneameString ); // creates two files: "DimacsFilneameString" and "DimacsFilneameString.map"
    *   CNF.pl2dimacs( CnfSentence, DimacsFilenameString ); // creates two files: "DimacsFilneameString" and "DimacsFilneameString.map"
    
      
    
2.  At the command line (or with a system call), run zChaff on the DIMACS file  
    
    *   zchaff.2001.2.17.solaris `mysentence.dimacs >! mysentence.zchaff`
    
      
    
3.  In your program, convert the zChaff output into an Interpretation for the original CNF sentence. ;Note that the Interpretation will be `null` if zChaff did not find an assignment.
    *   Interpretation interp = CNF.zchaffToInterpretation( "mysentence.zchaff","mysentence.dimacs.map");