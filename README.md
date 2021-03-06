# createDoc<br />
**Created Date:** 6/14/2011<br />
**Last Updated:** 6/27/2011<br />
**Description:** This application is intended to help generate {xfMethod} & {xfParam} attributes from existing source files, or from the XML documented created by GENXML.
It can also generate documentation comments.<br />
**Platforms:** Windows; Unix; OpenVMS<br />
**Products:** Synergy DBL<br />
**Minimum Version:** 9.5.1a<br />
**Author:** William Hawkins
<hr>

**Additional Information:**

Starting with Synergy source file
--------------------------

dbr createDoc -s <dblFile> <elbName> -i <interface> -x <xmlFile> -o <outFile>

This will read through the <dblFile> and will create the <xmlFile> in GENXML
format. The <elbName> and <interface> are used to populate data in <xmlFile>.

Once the <xmlFile> has been created, the program analyzes the <xmlFile> and
creates the <outFile> as a dummy Synergy source file. Note, the <xmlFile>
created is not deleted, so that it can be used as an import file for importing
into the Synergy Method Catalog (SMC).


Starting with populated SMC
---------------------------

Run MDU and export the methods to <xmlFile>

dbr createDoc -x <xmlFile> -o <outFile> [-i <interface>]

This will read through the <xmlFile> and create <outFile> as a dummy Synergy
source file. If <interface> is specified, only methods in the selected
interface are processed. If <interface> is not specified, all interfaces /
methods are processed.

Once the output file is generated, you can cut/paste the resulting {xf}
attributes and/or documentation comments into your application source code.


Known Issues
------------

If you wish to use the <xmlFile> generated by createDoc as an import file
for SMC, you must ensure that all parameters are correctly defined in the
Synergy source file, including parameter size.

If you use .INCLUDE files as parameters, createDoc will treat the entire
.include line as the parameter name to be used in the <xmlFile>, and will
interrogate the contents of the .include file for the name of the GROUP.
This will result in an XML file that cannot be imported into SMC. If you
want to use group parameters, they must in included from Repository.

It's possible to use the same Synergy method as the execution method for
more than one xfNetLink method (e.g. with/without data table options). In
this scenario, you will get more than one version of the named Synergy
routine in the output, each version will be attributed correctly.
