# BIMbots-FreeCAD

A FreeCAD plugin to communicate with BIMbots services - http://bimbots.org/

**This is a work in progress.**

The plugin consists (so far) of one python script, that can be run directly from the terminal, in which case it prints a list of services it was able to reach, or imported as a python module (py2 and py3 compatible), in which case you have access to several utility functions to retrieve an communicate with BIMbots services.

It (will) also works as a [FreeCAD](http://www.freecadweb.org) macro. If launched from the FreeCAD macros menu, the plugin will autodetect that it is running inside FreeCAD and launch a full GUI that allows to run different BIMbots services.

### So far it can:

* Retrive a list of BIMbots services
* Authenticate with any of the services
* Keep authentication credentials in a config file
* Test services (send a minimal IFC file, get the results)

When running inside FreeCAD:

* Show the interface in FreeCAD
* Gather list of available services

### To do:

* Design icons
* Write python mocule documentation
* Write user (GUI) documentation

### How to test

### From the command line (linux/mac only ATM)

```bimbots.py

Reading config from /home/yorik/.BIMbots
FreeCAD not available
Reading config from /home/yorik/.BIMbots
Reading config from /home/yorik/.BIMbots
Reading config from /home/yorik/.BIMbots
Available services:
Reading config from /home/yorik/.BIMbots
Service Simple Analyses Service from ifcanalyses - not authenticated
Reading config from /home/yorik/.BIMbots
Service Detailed Analyses Service from ifcanalyses - not authenticated
Reading config from /home/yorik/.BIMbots
Service IFC Analytics Service from ifcanalyses - not authenticated
Reading config from /home/yorik/.BIMbots
Service FixedFileService from ifcanalyses - not authenticated
Reading config from /home/yorik/.BIMbots
Error: unable to read services list from http://localhost:8080/servicelist
Reading config from /home/yorik/.BIMbots
Error: unable to connect to service provider at http://localhost:8081/servicelist
Reading config from /home/yorik/.BIMbots
Reading config from /home/yorik/.BIMbots
Service IFC Analytics Service from Yorik's test BIMserver - authenticated as http://localhost:8082/servicelist , service 2097206
Reading config from /home/yorik/.BIMbots
Service Simple Analyses Service from Yorik's test BIMserver - not authenticated
Reading config from /home/yorik/.BIMbots
Service Detailed Analyses Service from Yorik's test BIMserver - not authenticated
Reading config from /home/yorik/.BIMbots```

#### From Python

```>>> import bimbots
Reading config from /home/yorik/.BIMbots
FreeCAD not available
>>> bimbots.get_service_providers()
Reading config from /home/yorik/.BIMbots
Reading config from /home/yorik/.BIMbots
[{u'listUrl': u'https://ifcanalysis.bimserver.services/servicelist', u'name': u'ifcanalyses'}, {u'listUrl': u'http://localhost:8080/servicelist', u'name': u'Default localdev BIMserver', u'description': u'Default localdev BIMserver'}, {u'listUrl': u'http://localhost:8081/servicelist', u'name': u'2nd localdev BIMserver', u'description': u'2nd localdev BIMserver'}, {u'listUrl': u'http://localhost:8082/servicelist', u'name': u'Default JAR runner', u'description': u'Default JAR runner'}, {u'listUrl': u'https://thisisanexperimentalserver.com/servicelist', u'name': u'Experimentalserver.com', u'description': u'Experimental BIMserver'}]
>>> bimbots.get_services('http://localhost:8082/servicelist')
Reading config from /home/yorik/.BIMbots
[{u'inputs': [u'IFC_STEP_2X3TC1'], u'resourceUrl': u'http://localhost:8082/services', u'description': u'IFC Analytics Service', u'outputs': [u'IFC_ANALYTICS_JSON_1_0'], u'providerIcon': u'/img/bimserver.png', u'provider': u"Yorik's test BIMserver", u'oauth': {u'tokenUrl': u'http://localhost:8082/oauth/access', u'registerUrl': u'http://localhost:8082/oauth/register', u'authorizationUrl': u'http://localhost:8082/oauth/authorize'}, u'id': 2097206, u'name': u'IFC Analytics Service'}, {u'inputs': [u'IFC_STEP_2X3TC1'], u'resourceUrl': u'http://localhost:8082/services', u'description': u'BIMserver plugin that provides an analysis of a model and and outputs it into json', u'outputs': [u'UNSTRUCTURED_UTF8_TEXT_1_0'], u'providerIcon': u'/img/bimserver.png', u'provider': u"Yorik's test BIMserver", u'oauth': {u'tokenUrl': u'http://localhost:8082/oauth/access', u'registerUrl': u'http://localhost:8082/oauth/register', u'authorizationUrl': u'http://localhost:8082/oauth/authorize'}, u'id': 2162742, u'name': u'Simple Analyses Service'}, {u'inputs': [u'IFC_STEP_2X3TC1'], u'resourceUrl': u'http://localhost:8082/services', u'description': u'BIMserver plugin that provides a detailed analysis of a model and outputs it into json', u'outputs': [u'UNSTRUCTURED_UTF8_TEXT_1_0'], u'providerIcon': u'/img/bimserver.png', u'provider': u"Yorik's test BIMserver", u'oauth': {u'tokenUrl': u'http://localhost:8082/oauth/access', u'registerUrl': u'http://localhost:8082/oauth/register', u'authorizationUrl': u'http://localhost:8082/oauth/authorize'}, u'id': 2228278, u'name': u'Detailed Analyses Service'}]
>>>```

#### From FreeCAD

* Copy this whole directory (or symlink it) inside your user Mod directory (which you get by issuing `App.getUserAppDataDir()+"Mod"` in the FreeCAD python console, usually ~/.FreeCAD/Mod on linux/mac)
* Restart FreeCAD if already running
* in the FreeCAd python console, type: `import bimbots`
