MaaSCMS Android SDK
================

Version 1.0.3

This is the Android SDK for the MaaS Content Management System module. Visit http://maas.phunware.com/ for more details and to sign up.

Getting Started
---------------

- [Download MaaSCMS](https://github.com/phunware/maas-cms-android-sdk/archive/master.zip) and run the included sample app.
- Continue reading below for installation and integration instructions.
- Be sure to read the [documentation](http://phunware.github.io/maas-cms-android-sdk/) for additional details.



Installation
------------

The following libraries are required:
````
MaaSCore.jar
````

MaaSCMS has a dependency on MaaSCore.jar which is available here: https://github.com/phunware/maas-core-android-sdk

It's recommended that you add the MaaS libraries to the 'libs' directory. This directory should contain MaaSCore.jar and MaaSCMS.jar  as well as any other MaaS libraries that you are using.



Documentation
------------

Documentation is included in the Documents folder in the repository as both HTML and .jar. You can also find the latest documentation here: http://phunware.github.io/maas-cms-android-sdk/.



Overview
-----------

The MaaSCMS SDK allows developers to fetch and manage the various pieces of data in the Content Management System including containers, schemas, structure, and content. The CMS spans across your entire organization so different applications can potentially share the same content.


### Container

**Containers** hold a single structure. You can create any number of containers in MaaS Portal. You can also associate tags with containers to assist with fetching.

### Schema

**Schemas** are applied to **Structure** items and define what fields of data a particular structure item can contain.. You can create any number of schemas in MaaS Portal. You can also associate tags with schemas to assist with fetching.

### Structure

**Structure** items are used to build the structure and hierarchy of the data. Each **Structure** item that is defined as an object can also optionally be assigned a **Schema** that defines what content can be saved to those **Structure** items

### Content

The structure of the **Content** object relies completely on the layout of structures and schemas.



Integration
-----------

The primary methods in MaaSCMS revolve fetching, creating, updating, and deleting content. You can also get structures, containers, and schemas.

### Getting Content

````java
	// Get a specific piece of content for the specified context, container ID, and content ID. 
	// The contents are always returned a JSONObject. It's recommended that you parse the JSONObject into a model object.
    JSONObject content = PwCMSModule.getContent(this, containerId, contentId);

````

### Updating Content

````java
	// Update content for the specified content ID, container ID, and structure ID. 
	// Any fields that are ommitted will maintain their previous values.
	  PwCMSModule.updateContent(this, contentId, newContent, structureId);
````

### Creating Content

````java
  // Add content to the specified container ID, structure ID, and parent content ID. 
	// Ideally the new content object has all the fields as specified by the structure and schema. 
	// If not, the required fields will be created for you with empty values.
	
	  // Required parent content ID for new content that needs to be link up to any dynamic children of a structure item. 
    PwCMSModule.addContent(this, containerId, structureId, parentId, data);
    or
    // If no parent content exists then parent content ID is not required. 
    // Otherwise, use above method to properly link up child elements.
    PwCMSModule.addContent(this, containerId, structureId, data);
````

### Deleting Content

````java
	// Delete content for the specified content ID as well as all content children
    PwCMSModule.deleteContent(this, contentId, traverse);   
    
    or
  // Delete all content children for the specified content ID
    PwCMSModule.deleteContentAllChildren(context, contentId);

````

### Containers

````java
	// Fetch all containers
    PwContainers containers = PwCMSModule.getContainers(this);
    
  // Fetch a specific container item
    PwContainer container = PwCMSModule.getContainer(this, containerId);
    
  // Get an array of containers that match an array of tags
    PwContainers containers = PwCMSModule.getContainers(this, anyTags, allTags);

````

### Schemas

````java
  // Fetch all schemas
    PwSchemas schemas = PwCMSModule.getSchemas(this);
    
  // Fetch a specific schema item
    PwSchema schema = PwCMSModule.getSchema(this, schemaId);
    
  // Get an array of schemas that match an array of tags
    PwSchemas schemas = PwCMSModule.getSchemas(this, anyTags, allTags);
````

### Structure

````java
  // Get a structure with the specified stucture and container ID. 
  // In this example we want to traverse into all child structures but not include schema.
    withSchema = false;
    PwStructure structure = PwCMSModule.getStructure(this, structureId, containerId, depth, withSchema);
    
  // Get an structures object containing an array of structures for the specified container ID. 
  // In this example we want to traverse into all child structures and include schema.
    withSchema = true;
    PwStructures structures = PwCMSModule.getStructures(this, containerId, depth, withSchema);
````



Requirements
------------

- MaaSCore v1.0.0 or greater.
