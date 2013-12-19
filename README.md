MaaS Content Management SDK for Android
================

Version 1.1.0

This is the Android SDK for the MaaS Content Management module. Visit http://maas.phunware.com/ for more details and to sign up.



Getting Started
---------------

- [Download MaaS Content Management](https://github.com/phunware/maas-cms-android-sdk/archive/master.zip) and run the included sample app.
- Continue reading below for installation and integration instructions.
- Be sure to read the [documentation](http://phunware.github.io/maas-cms-android-sdk/) for additional details.



Installation
------------

The following libraries are required:
````
MaaSCore.jar
````

MaaS Content Management has a dependency on MaaSCore.jar which is available here: https://github.com/phunware/maas-core-android-sdk



Documentation
------------

Documentation is included in the Documents folder in the repository as both HTML and as a .jar. You can also find the latest documentation here: http://phunware.github.io/maas-content-management-android-sdk/



Overview
-----------

The MaaSCME SDK allows developers to fetch and manage the various pieces of data in the Content Management Engine, including containers, schemas, structure and content. The CME spans across your entire organization, so different applications can potentially share the same content.


### Container

**Containers** hold a single structure. You can create any number of containers in MaaS Portal. You can also associate tags with containers to assist with fetching.

### Schema

**Schemas** are applied to **Structure** items and define what fields of data a particular structure item can contain.. You can create any number of schemas in MaaS Portal. You can also associate tags with schemas to assist with fetching.

### Structure

**Structure** items are used to build the structure and hierarchy of the data. Each **Structure** item that is defined as an object can also optionally be assigned a **Schema** that defines what content can be saved to those **Structure** items.

### Content

The structure of the **Content** object relies completely on the layout of structures and schemas.



Integration
-----------

The primary methods in MaaSCME revolve fetching, creating, updating and deleting content. You can also get structures, containers and schemas.

### Getting Content

````java
	// Get a specific piece of content for the specified context, container ID and content ID. 
	// The contents are always returned a JSONObject. It's recommended that you parse the JSONObject into a model object.
    JSONObject content = PwCMEModule.getContent(this, containerId, contentId);
````

### Updating Content

````java
	// Update content for the specified content ID, container ID and structure ID. 
	// Any fields that are ommitted will maintain their previous values.
	  PwCMEModule.updateContent(this, contentId, newContent, structureId);
````

### Creating Content

````java
  // Add content to the specified container ID, structure ID and parent content ID. 
	// Ideally, the new content object has all the fields as specified by the structure and schema. 
	// If not, the required fields will be created for you with empty values.
	
	  // Required parent content ID for new content that needs to be link up to any dynamic children of a structure item. 
    PwCMEModule.addContent(this, containerId, structureId, parentId, data);
    or
    // If no parent content exists, then parent content ID is not required. 
    // Otherwise, use above method to properly link child elements.
    PwCMEModule.addContent(this, containerId, structureId, data);
````

### Deleting Content

````java
	// Delete content for the specified content ID as well as all content children.
    PwCMEModule.deleteContent(this, contentId, traverse);
    
    or
  // Delete all content children for the specified content ID
    PwCMEModule.deleteContentAllChildren(context, contentId);
````

### Containers

````java
	// Fetch all containers.
    PwContainers containers = PwCMEModule.getContainers(this);
    
  // Fetch a specific container item.
    PwContainer container = PwCMEModule.getContainer(this, containerId);
    
  // Get an array of containers that match an array of tags.
    PwContainers containers = PwCMEModule.getContainers(this, anyTags, allTags);
````

### Schemas

````java
  // Fetch all schemas.
    PwSchemas schemas = PwCMEModule.getSchemas(this);
    
  // Fetch a specific schema item.
    PwSchema schema = PwCMEModule.getSchema(this, schemaId);
    
  // Get an array of schemas that match an array of tags.
    PwSchemas schemas = PwCMEModule.getSchemas(this, anyTags, allTags);
````

### Structure

````java
  // Get a structure with the specified stucture and container ID. 
  // In this example, we want to traverse into all child structures but not include schema.
    withSchema = false;
    PwStructure structure = PwCMEModule.getStructure(this, structureId, containerId, depth, withSchema);
    
  // Get a structure object containing an array of structures for the specified container ID. 
  // In this example, we want to traverse into all child structures and include schema.
    withSchema = true;
    PwStructures structures = PwCMEModule.getStructures(this, containerId, depth, withSchema);
````
