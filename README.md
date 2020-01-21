# Angular Modular Application

A proposal for creating an Angular 8 application that can be made extensible.

## Scope

This *Markdown* document is concerned with a technical proposal of creating an **_Angular 8_** modular application. Modular, in this sense, means an application that can be extended with new modules past its compilation and deployment time in Angular

## Requirements

The business requirement is to develop an **_Angular 8_** web application that does not have to be changed/recompiled/rebuilt whenever a new module (e.g. new device sub-page) is developed.

## Proposal

The proposal can be summarized in the following bullet-points:

* Use localStorage to hold the JWT token using a **common** interceptor/service that will be used _website-wide_. Specifically the modules that will extend the TNG website.
* To access any _'modular'_ resource, use a _.json_ file that will generate menu points, or other access points to the modular parts. This _.json_ file is the only file that must be changed/appended to when a new module is _installed_. This json file contains the following data:

	```json
	[
	{displayName: 'Trima', contentPath: 'module_trima' },
	{displayName: 'Atreus', contentPath: 'module_atreus' },
	{displayName: 'TSCD-III', contentPath: 'module_tscd3' }
	]
	```
	|Member|Description|
	|--|--|
	|displayName|The name which is going to be displayed on the menu|
	|contentPath|The path, relative to the base website path

* Each module will be a seperate _**Angular 8**_ website, using shared libraries. As stated in previous points, the **JWT** interceptors must be exactly the same and must use _localStorage_. This way, the main _website_ and the _sub modules_ can reuse **JWT** credentials.

* Each module is loaded as an **iframe** inside the main content container of the TNG app. This will be a seamless experience for the user.

* Routing must be disabled on menu elements that are generated through the special modules .json file.
