## ezportal Advisory v5.6 has a SQL injection

#### Vendor Homepage: https://www.ezportal.com/

#### Software Link: https://custom.simplemachines.org/index.php?mod=1461

#### Version: v5.6 (latest version)

#### Google Dork: inurl:index.php?action=ezportal

#### Tested on: Windows 10

                 ###############
                 # Explication:#
                 ###############

ezportal is a portal mod for Simple Machine Forum, if you have it installed this flaw in it presents a database error,
personally tested on the v5.6 version of the portal.
Probably also present on previous ezportal versions.

                 ###############
                 # Procedure:  #
                 ###############

The bug is present once logged in as administrator, and occurs when editing blocks located in the portal index.
the error generated is the classic database error, exploitable with SQL injection.


                ################
                # Execution:   #
                ################

This is the bugged Query:

***************************************************
* index.php?action=ezportal;sa=editblock;block=-1 *

***************************************************