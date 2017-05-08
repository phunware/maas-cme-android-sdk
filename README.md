MaaS Content Management SDK for Android
================

Version 1.1.6

This is Phunware's Android SDK for the Content Management module. Visit http://maas.phunware.com/ for more details and to sign up.

Requirements
------------

* Android SDK 4.0.3+ (API level 15) or above


Getting Started
---------------

- [Download MaaS Content Management](https://github.com/phunware/maas-cms-android-sdk/archive/master.zip) and run the included sample app.
- Continue reading below for installation and integration instructions.
- Be sure to read the [documentation](http://phunware.github.io/maas-content-management-android-sdk/) for additional details.



Installation
------------
Add the following to your `repositories` tag in your top level `build.gradle` file.

```XML
projects {
  repositories {
    ...
    maven {
        url "https://nexus.phunware.com/content/groups/phunware-core/"
    }
    ...
  }
}
```

In the `dependencies` tag in your app's `build.gradle`,  add the following line:

```XML
dependencies {
  ...
  compile 'com.phunware.cme:cme:1.1.6'
  ...
}
```



Documentation
------------

Documentation is included in the Documents folder in the repository as both HTML and via maven. You can also find the latest documentation here: http://phunware.github.io/maas-content-management-android-sdk/



Overview
-----------

The Content Management SDK allows developers to fetch and manage the various pieces of data in the Content Management Engine, including containers, schemas, structure and content. PW Content Management spans across your entire organization, so different applications can potentially share the same content.


### Container

**Containers** hold a single structure. You can create any number of containers in the MaaS portal. You can also associate tags with containers to assist with fetching.

### Schema

**Schemas** are applied to **structure** items and define what fields of data a particular structure item can contain. You can create any number of schemas in the MaaS portal. You can also associate tags with schemas to assist with fetching.

### Structure

**Structure** items are used to build the structure and hierarchy of the data. Each **structure** item that is defined as an object can also optionally be assigned a **schema** that defines what content can be saved to those **structure** items.

### Content

The structure of the **content** object relies completely on the layout of structures and schemas.



Integration
-----------
### Installing CME module to core

Before using the CME it has to be added to the CoreSession as a module.

````java
// This is usually included in the onCreate() of application.
   PwCoreSession.getInstance().installModules(PwCMEModule.getInstance());
````

### Registering the keys for Core module. If you have not already registered the keys for Core, then do so.
````java
//Register the Appid,accessKey,signatureKey and encryption Key.
PwCoreSession.getInstance().registerKeys(context, Appid, Accesskey,
				Signaturekey, Encryptionkey);
PwCMEModule.getInstance().setModuleHttpCacheTtl(DEFAULT_HTTP_CACHE_TTL);
````
The primary methods in PW Content Management revolve fetching, creating, updating and deleting content. You can also get structures, containers and schemas.

### Getting Content

````java
	// Get a specific piece of content for the specified context, container ID and content ID.
	// The contents are always returned as a JSONObject. It's recommended that you parse the JSONObject into a model object.
    JSONObject content = PwCMEModule.getContent(this, containerId, contentId);
````

### Updating Content

````java
	// Update content for the specified content ID, container ID and structure ID.
	// Any fields that are omitted will maintain their previous values.
	  PwCMEModule.updateContent(this, contentId, newContent, structureId);
````

### Creating Content

````java
  // Add content to the specified container ID, structure ID and parent content ID.
	// Ideally, the new content object has all the fields specified by the structure and schema.
	// If not, the required fields will be created for you with empty values.

	  // The required parent content ID for new content needs to be linked up to any dynamic children of a structure item.
    PwCMEModule.addContent(this, containerId, structureId, parentId, data);
    or
    // If no parent content exists, then the parent content ID is not required.
    // Otherwise, use the above method to properly link child elements.
    PwCMEModule.addContent(this, containerId, structureId, data);
````

### Deleting Content

````java
	// Delete content for the specified content ID as well as all content children.
    PwCMEModule.deleteContent(this, contentId, traverse);

    or
  // Delete all content children for the specified content ID.
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
  // Fetch a structure with the specified structure and container ID.
  // In this example, we want to traverse into all child structures but not include schema.
    withSchema = false;
    PwStructure structure = PwCMEModule.getStructure(this, structureId, containerId, depth, withSchema);

  // Fetch a structure object containing an array of structures for the specified container ID.
  // In this example, we want to traverse into all child structures and include schema.
    withSchema = true;
    PwStructures structures = PwCMEModule.getStructures(this, containerId, depth, withSchema);
````
-----------

Privacy
-----------
You understand and consent to Phunware’s Privacy Policy located at www.phunware.com/privacy. If your use of Phunware’s software requires a Privacy Policy of your own, you also agree to include the terms of Phunware’s Privacy Policy in your Privacy Policy to your end users.

Terms
-----------
Use of this software requires review and acceptance of our terms and conditions for developer use located at http://www.phunware.com/terms/
