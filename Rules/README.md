# Using ACFR-MI validations with Arelle 

Download and install the [Arelle open source XBRL processor](https://arelle.org/pub)

## Run with compiled Xule rules from a command prompt ([What's Xule](https://xbrl.us/xule)?)
The minimum parameters that need to be passed are the following:
* **`--xule-rule-set`** : The location of the compiled Xule ruleset.zip validations used to evaluate the filing.
* **`-f`** : The location of the instance file to be evaluated. This will take a zip file, XML instance or inline XBRL file.
* **`-v`**: Instructs the processor to validate the filing with the compiled rule set.

A typical command line syntax for Arelle is as follows (including optional parameters defined below:

`.\arellecmdline.exe --xule-rule-set {compiled rule set file as a .zip} -f {instance file or zip file} -v --noCertificateCheck --logFile {log file name}`

**Example:**  
Results for this command will display in the terminal window because no log file is defined:

`.\arellecmdline.exe --plugins xule --xule-rule-set https://github.com/xbrlus/acfr/raw/master/Rules/acfr-2022-v1-ruleset.zip -f https://xbrlus.github.io/acfr/samples/67/Ogemaw-20190930.htm -v --xule-time .005 --xule-debug --noCertificateCheck`

In addition the following optional parameters can be passed:

* **`--logFile`** : Specifies where the output of running the rules should be sent. To get an XML file the file needs to end with .xml. To get a json file it needs to end with .json. If a log file is not specified, output will be displayed in the command window.
* **`--noCertificateCheck`** : This is used to ensure that files from the internet are not rejected if there is no SSL certificate on the machine running the ACFR-MI plugin.
* **`--xule-bypass-packages`** : This option will ignore packages included in the ruleset.  
* **`--packages`** : This option will accept additional taxonomy packages
* **`--xule-rule-set`** : The location of the compiled ruleset to use. 

To get additional options use the option `--help` (eg. `arelleCmdLine --plugins validate/ACFR-MI --help`)

The ACFR-MI plugin options will be displayed at the bottom of the list under the title "ACFR-MI validation plugin". All ACFR-MI specific options start with `--ACFR-MI` or `--xule`.

## Install a plug-in and validate from the command prompt or in Arelle's GUI

[Download](https://github.com/xbrlus/acfr/raw/master/Rules/ACFR-MI-plugin.zip) and extract or copy the 
- [ACFR-MI.py](https://github.com/xbrlus/acfr/raw/master/Rules/ACFR-MI.py) to the `/plugin/`**`validate`** folder where Arelle is installed 
- [acfrMIRulesetMap.json](https://github.com/xbrlus/acfr/raw/master/Rules/acfrMIRulesetMap.json) to the `/plugin/`**`xule`** folder where Arelle is installed 

### Command line
In this example, the plugin is specified and routes the selection of the rule set through the rulesetMap.json file, instead of specifying the rule set to be used.

**Example:**  
`.\arellecmdline.exe --plugins "validate/ACFR-MI" -f https://xbrlus.github.io/acfr/samples/67/Ogemaw-20190930.htm -v --xule-time .005 --xule-debug --noCertificateCheck --logFile C:/output.xml`   

### GUI
* Open Arelle.
* Choose the "Help" menu and select "Manage plug-ins" 
* Use the "Select" button to bring up teh "Select Plug-in Module" dialog. 
* Select the **ACFR-MI.py** file (under "Validate"). Next to the file, the name will appear as "ACFR-MI Rules Validator". Click on "OK". 
* The "Select Plug-in Module" will close. On the "Plug-in Manager" dialog click on "Close". When the dialogue box appears requesting a program restart, choose "Yes".
* After restarting, choose the "Tools" menu and "Validation" and confirm there is a check mark for "ACFR-MI Rules". If not, select this item from the menu.

#### Checking version and rule set map
* Choose the "Tools" menu and mouse-over the ACFR-MI option to see four options:
    * "Version ..." displays the current xule version installed.
    * "Display rule set map ..." shows the current rule sets targeted by the plugin.
    * "Check rule set map ..." verifies the cached rulesetMap.json file references the most-current available ruleset.zip files.
    * "Update rule set map ..." provides an interface for either appending or overwriting the cached rulesetMap.json file.

#### Checking a filing with DQC Rules
* Choose the "File" menu and either "Open file" or "Open Web" to select an XBRL file.
* After the instance has been processed by Arelle, choose the "Tools" >> "Validation" menu and select "Validate".
* Monitor the "messages" window at the bottom of Arelle, to see _[DQC] Starting validation - filename_ appears.
* After the message _[DQC] Finished validation - filename_ appears, review any error messages. The results can be saved by selecting the messages window (right-click on a Windows PC) and choosing "Save to file".

© Copyright 2015 - 2022 XBRL US, Inc. All rights reserved.   
See [License](https://xbrl.us/dqc-license) for license information.  
See [Patent Notice](https://xbrl.us/dqc-patent) for patent infringement notice.
