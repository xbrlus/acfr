# Using ACFR-MI validations with Arelle 

### Install and confirm the ACFR-MI Arelle plugin 

Download and install the [Arelle open source XBRL processor](https://arelle.org/pub)

[Download](https://github.com/xbrlus/acfr/raw/master/validation/ACFR-MI-plugin.zip) and extract or copy the 
- [ACFR-MI.py](https://github.com/xbrlus/acfr/raw/master/validation/ACFR-MI.py) to the `/plugin/`**`validate`** folder where Arelle is installed 
- [acfrMIRulesetMap.json](https://github.com/xbrlus/acfr/raw/master/validation/acfrMIRulesetMap.json) to the `/plugin/`**`xule`** folder where Arelle is installed 

From a command prompt, browse to the location of Arelle on the computer and run `arelleCmdLine --plugin validate/ACFR-MI` (Linux) or `.\arellecmdline.exe --plugin validate/ACFR-MI` (Windows).

You should see an activation message for the plugin:
`
[info] Activation of plug-in ACFR-MI Rules Validator successful, version Check version using Tools->ACFR-MI->Version on the GUI or --ACFR-MI-version on the command line. - validate/ACFR-MI
`  

The minimum parameters that need to be passed are the following:
* **`--plugins validate/ACFR-MI`** : Loads the ACFR-MI plugin. The SEC transformations are also needed for Inline XBRL filings. Both plugins can be specified using **--plugins "validate/ACFR-MI|transforms/SEC"**. The pipe character `|` separates the plugins. Specifying the SEC transforms plugins will have no affect on traditional XBRL filings, so it can be included for all SEC filings.
* **`-f`** : The location of the instance file to be evaluated. This will take a zip file, XML instance or inline XBRL file.
* **`-v`**: Instructs the processor to validate the filing including running the ACFR-MI rules.

A typical command line syntax for Arelle is as follows (including optional parameters defined below:

`
.\arellecmdline.exe --plugins "validate/ACFR-MI|transforms/SEC" -f {instance file or zip file} -v --noCertificateCheck --logFile {log file name}
`

**Example:**  
`
.\arellecmdline.exe --plugins "validate/ACFR-MI|transforms/SEC" -f https://xbrlus.github.io/acfr/samples/68/SOUTHHAVEN.htm -v --xule-time .005 --xule-debug --noCertificateCheck --logFile C:/output.xml
`   

In addition the following optional parameters can be passed:

* **`--logFile`** : Specifies where the output of running the rules should be sent. To get an XML file the file needs to end with .xml. To get a json file it needs to end with .json. If a log file is not specified, output will be displayed in the command window.
* **`--noCertificateCheck`** : This is used to ensure that files from the internet are not rejected if there is no SSL certificate on the machine running the ACFR-MI plugin.
* **`--xule-bypass-packages`** : This option will ignore packages included in the ruleset.  
* **`--packages`** : This option will accept additional taxonomy packages
* **`--xule-rule-set`** : The location of the compiled ruleset to use. 

To get additional options use the option `--help` (eg. `arelleCmdLine --plugins validate/ACFR-MI --help`)

The ACFR-MI plugin options will be displayed at the bottom of the list under the title "ACFR-MI validation plugin". All ACFR-MI specific options start with `--ACFR-MI` or `--xule`.
 
© Copyright 2015 - 2022 XBRL US, Inc. All rights reserved.   
See [License](https://xbrl.us/dqc-license) for license information.  
See [Patent Notice](https://xbrl.us/dqc-patent) for patent infringement notice.
