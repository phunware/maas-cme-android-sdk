CME Change Log
==========

Version 1.1.5 *(2016-08-01)*
----------------------------
 * Update from .jar to maven repo
 * Now uses updated PWCore 3.0.0

Version 1.1.4 *(2015-09-30)*
----------------------------
 * Change phunware.com endpoints to HTTPS
 * Rename the lib from MaaSCMS.jar to PWCME.jar

Version 1.1.3 *(2014-02-26)*
----------------------------
 * Fixed builds to produce Java 6 compatible binaries using 'sourceCompatibility' and 'targetCompatibility' equal to '1.6'.
 * Requires MaaSCore v1.3.5

Version 1.1.2 *(2014-01-27)*
----------------------------
 * getSchemas allows an input of a limit and offset. The default limit is 10.
 * PwSchemas now includes a PwPagination object to help use pagination logic.

Version 1.1.0 *(2013-12-06)*
----------------------------
 * Cleaned up code
 * Re-branded code from CMS to CME

Version 1.0.5 *(2013-11-23)*
----------------------------
 * Fixed encoding bug with unicode (special) characters.

Version 1.0.4 *(2013-11-08)*
----------------------------
 * Added the ability to retrieve all structures by traversing all children of container.

Version 1.0.3 *(2013-09-24)*
----------------------------
 * Removed deprecated methods.
 * Added getContent that takes a structureId.
