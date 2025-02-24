# PALOS-CPP Rule/Inference Engine (Still In Development)
Open source project PALOS Rule/Policy Engine with C/C++.
This project is based on original project [PALOS Rule/Inference Engine.](https://github.com/DeanLee77/Nadia).
As this project is titled, this project is written in C/C++. 

In addition, this C/C++ version of PALOS includes its own script engine unlike Java and C# version because C/C++ language does not support JavaScript engine. The script engine is implemented based on a book of 'Crafting Interpreters' written by Robert Nystrom, which can be found at a link of ['Crafting Interpreters'](http://www.craftinginterpreters.com/).

In order to see an example of implementation of back-end database and front-end, please see [PALOS Java REST](https://github.com/NExST-RnDLabs/NadiaRS).
<br/>
<br/>
Video is also avaiable at [PALOS Policy / Business rules Engine from NExST.R&DLabs](https://youtu.be/xyWjscJ3LxI) <br/>
or <br/>
another link is [ Introduction of PALOS Policy / Business rules Engine from NExST.R&DLabs.](https://youtu.be/O-itMgYHRvc)

# ***Relevant PALOS project list***
[PALOS Java](https://github.com/DeanLee77/Nadia)<br/>
[PALOS Java REST](https://github.com/NExST-RnDLabs/NadiaRS)<br/>
[PALOS C#](https://github.com/DeanLee77/NADIA-C.Sharp)<br/>

## 1. Introduction
This project is building a Rules(Policies)/Inference Engine with ease of use and maintain rules/policies. It aims to be:

* A rule author is allowed to write rules or policies in a plain text file for the engine rule parser
* A rule author or business person does NOT need to implement the rules/policies separately like other rules engines
* A user of the engine can carry out Foward-chaining and Backward-chaining with a given rule/policy set

## 2. Installation/Running Project in Local
Note: current source code is developed in Mac XCode.

In order to install the project in your workspace, you may need to do followings;
 1. Install C++ compiler(current source code is targeted for GNU++17(C++) and GNU 11(C)).
 
 *Please note that there will be Demo video available soon.
## 3. Roadmap
Add more features as follows (particularly this C/C++ version);

* Completing an Interpreter for evaluating calculations within rules
* GUI for Rule IDE (it is just more than editor. working as an development IDE)
* Retrieving Rule/Policy file from database (DONE with PostgreSQL in this version)
* Workflow engine with GUI based diagram editor 
* Machine Learning type inference mechanism (DONE in this version)

## 4. Contribution
If you would like to contribute to this project, then please create your own branch and name the branch clearly. Once the work is done in the branch then do 'pull request' and send an email to 'nexst.rndlabs@gmail.com'.

## 5. Make your own Rules/Policies
Please have a look at a file of testing rule. Within the example file, all indented rules uses 'Tab' key for indentation. The rule scanner considers of an indented rule as a child rule of previous rule in a rule text.

## Note:
If you need a commercial or coustomised version of PALOS engine, then please contact on 'nexst.rndlabs@gmail.com'.

## 6. How does it work
There is a number of key components as follows;

* Rule reader     : reads a rule/policy file, stream source, string source
* Rule scanner    : scans what 'Rule reader' reads
* Rule parser     : parses what 'Rule scanner' scans into a rule/policy graph
* TopoSort        : sorts the graph parsed by 'Rule parser'
* Inferece Engine : checking all truth or calculated value within forward-chaining, and retrieving next rule/policy within backward-chaining to check in order to complete rule set logic

### How Backward-chaining and Forward-chaining work
Suppose there are following rules:


1. IF either <br/>
      &nbsp;&nbsp;&nbsp;&nbsp;'statement B' is true; or <br/>
      &nbsp;&nbsp;&nbsp;&nbsp;'statement C' is true <br/>
   THEN <br/>
      &nbsp;&nbsp;&nbsp;&nbsp;'statement A' is true.
2. IF  both<br/>
      &nbsp;&nbsp;&nbsp;&nbsp;'statement D' is true; and <br/>
      &nbsp;&nbsp;&nbsp;&nbsp;'statement E' is true <br/>
   THEN <br/>
      &nbsp;&nbsp;&nbsp;&nbsp;'statement C' is true.
3. IF <br/>
      &nbsp;&nbsp;&nbsp;&nbsp;'statement F' is true<br/> 
   THEN <br/>
      &nbsp;&nbsp;&nbsp;&nbsp;'statement D' is false.
4. IF<br/> 
     &nbsp;&nbsp;&nbsp;&nbsp; 'statement G' is false <br/>
   THEN <br/>
      &nbsp;&nbsp;&nbsp;&nbsp;'statement E' is true.

#### Backward-chaining:
An inference engine when using backward chaining searches the inference rules until it finds one which has a consequent (Then clause) that matches a desired goal. For instance, if we want to know whether or not the rule of 'statement A' is 'true' or 'not true(false)', an engine finds out which rule has to be checked to conclude. In this case, the engine needs information about the rule of 'statement B' is 'true' or 'not true(false)', or 'statement F' and 'statement G' are 'true' or 'not true(false)' respectively.

#### Forward-chaining
An inference engine using forward chaining searches the inference rules until it finds one where the antecedent (If clause) is known to be true. For instance, if we do have facts that 'statement G' is true and 'statement F' is true then the engine concludes as follows;
* 'statement G' is true
* 'statement F' is true
* 'statement E' is false due to that 'statement G' is not false
* 'statement D' is false due to that 'statement F' is true
* 'statement C' is false due to that 'statement D' is true and 'statement E' is false
* 'statement B' is unknown due to that there is not given information to infer about 'statement B'
* 'statement A' is false with given information of 'statement B' and 'statement C', however it could be changed based on conclusion  of 'statement B' because 'statement B' is unknown.

## 7. License
Copyright (c) 2017-2025 individual contributors.
PALOS-CPP is open source project and released under AGPL 3.0 License.
