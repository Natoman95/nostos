# Project Nostos 
> The prototype moving truck permitting application for the City of Boston 

## Table of Contents
- [Project Description](#project-description)
	- [Overview](#overview)
	- [Structure](#structure)
	- [Configuring the Project](#configuring-the-project)

- [Running the Project](#running-the-project)
    - [Dependencies](#dependencies)
    - [Running the React.js client](#Running-the-React.js-client)
    - [Running the Node.js Express server](#Running-the-Node.js-Express-server)
        - [Server API](#server-api)
    - [Database](#database)
        - [Schema](#schema)

- [Resources](#resources)
    - [Development Tools](#development-tools)
    - [External Resources](#external-resources)

- [About the Project](#about-the-project)
    - [Issue](#issue)
    - [Questions](#questions)
    - [Scope of Work](#scope-of-work)
    - [Scoping Resources](#scoping-resources)

## Project Description
> What is "Project Nostos"? What are the key components, and what do I need to do before running the project? All of these questions are covered in this section.

### Overview 

### Structure

```
└── client				# The front-end, a react.js based web application

    ├── build                  		# Contains static build of the front end
    
    ├── public         			# Resources used during build, such as the favicon and index.html 
    
    ├── src              		# Unit tests
    
    	├── actions			# Handles state changes
	
	└── components			# Contains mountable components, organized by purpose
		
		├── common		# Components such as the header which are used on multiple pages
		
		├── forms		# Pages with web-forms for the user to fill out
		
		├── images		# Static images, fairly self-explanatory
		
		└── maps		# Components which utilize the Mapbox SDK
		
	└── containers			# Components are aggregated into a page, which is stored here
	
	├── middleware			# Additional functions that utilize actions, but do not directly modify the state
	
	└── reducers 			# specify how the application's state changes in response to actions sent to the store
	
└── Server	

	├── bin                   	# Contains our main file, www, on which the server is configured and ran

	├── config         		# Contains the config.js file, using defaults unless specified in a .ENV file 

	├── controllers              	# Helper functions for interacting with database models

	├── middleware			# Helper finctions which span multiple models

	├── models			# Build Schemas with hooks and custom methods

	├── routes			# Our endpoints for the RESTful API 

	└── services			# Additional methods used in the running and maintaining of our server
```	
	
### Configuring the Project

## Running the Project
Information regarding dependencies, requirements, and commands used to build or run the project. To run this project, there is a private configuration file used by the back end. 

> **Note:** Without these files, you will be unable to successfully run the project. Please contact the respository owner for access to these files, or you can create your own. See [Database](#database) for more information on this.

This information can be used for both testing the project and preparing it for deployment in a production setting.

### Dependencies
Before running the project, there are several dependencies for the front end and the back end.

First, make sure you have the latest version of NPM and Node.js installed. You can download and install it [here](https://nodejs.org/en/download/) or follow the instructions on their site to install it through other means.

Make sure node is up to date with :

`npm i npm@latest -g`

With NPM installed, download and install yarn with:

`npm i --global yarn` 

Run `yarn` in the top-level directory, as well as in the "client" and "server" directories.

This should install all dependencies for the project using our yarn.lock files. Yarn will further be used to run the front end and back end concurrently.

Install nodemon using

`npm i nodemon -g`

Nodemon is used for managing live updates to our Node.js server

Install concurrently using

`npm i -g concurrently`

This allows us to run two commands simulataneously, using react-scripts and nodemon to manage live updates for both the front end and the back end.

Finally, in the top level, run

`yarn dev`
To serve the client and the server on their respective ports concurrently.


### Running the React.js client
To run only the front end, use

`cd client && npm start`

To change the port your front end runs on, change the `start:` parameter to `"PORT=3006 react-scripts start"`

To create a static build of the client, run

`cd client && npm run build`

This makes it possible to host the project from `build/index.html`, which is less resource intensive then having a live-reload version running on a port.

### Running the Node.js Express server
To run the server separate from the front end, use

`cd server && nodemon server.js`

This will run the node server with live-reload capabilities. The environment and port are specified in the `.env` file,
otherwise, the defaults will be used.

### Database
The project server requires a connection to a MYSQL System to store data. The system only needs one database, which is specified along with authentication credentials in a `.env` file. If there is no `.env` file, the config.json file will use default parameters. 

> **Note:** For the back-end to run properly, the config.json file must have an appropriate entry for each variable pulled from a `.env` file. This file can be provided by the repository owner, or you can make your own.

Upon running the back-end, the specified database will be populated with the appropriate tables, designed in the `/server/models` directory.

Therefore, one must have access pre-existing database, or run your own with appropriate security measures, to store any data.

#### Schema

> User Table
```xml
<database name="nostos_test">
	<table_structure name="Users">
		<field field="id" type="int(11)" null="NO" key="PRI" default="<null>" extra="auto_increment" />
		<field field="first" type="varchar(255)" null="NO" key="" default="<null>" extra="" />
		<field field="last" type="varchar(255)" null="NO" key="" default="<null>" extra="" />
		<field field="title" type="varchar(255)" null="YES" key="" default="<null>" extra="" />
		<field field="Company" type="varchar(255)" null="YES" key="" default="<null>" extra="" />
		<field field="email" type="varchar(255)" null="YES" key="UNI" default="<null>" extra="" />
		<field field="phone" type="varchar(255)" null="YES" key="UNI" default="<null>" extra="" />
		<field field="password" type="varchar(255)" null="YES" key="" default="<null>" extra="" />
		<field field="address1" type="varchar(255)" null="NO" key="" default="<null>" extra="" />
		<field field="address2" type="varchar(255)" null="YES" key="" default="<null>" extra="" />
		<field field="city" type="varchar(255)" null="NO" key="" default="<null>" extra="" />
		<field field="state" type="varchar(255)" null="NO" key="" default="<null>" extra="" />
		<field field="zip" type="varchar(255)" null="NO" key="" default="<null>" extra="" />
		<field field="createdAt" type="datetime" null="NO" key="" default="<null>" extra="" />
		<field field="updatedAt" type="datetime" null="NO" key="" default="<null>" extra="" />

		<options name="Users" engine="InnoDB" version="10" row_format="Dynamic" rows="14" avg_row_length="1170" data_length="16384" max_data_length="0" index_length="32768" data_free="0" create_time="2018-04-08 16:45:25" update_time="2018-04-16 20:29:51" collation="latin1_swedish_ci" create_options="" comment="" />
   	</table_structure>
	
</database>
```

## Resources
> Information regarding the tools and resources essential to the design and development of the project 

### Developement Tools
These development kits and tools were used to devlop and/or run the project. Becoming familiar with their documentation may prove useful in future development.

[Visual Studio Code](https://code.visualstudio.com)

[React.js](https://reactjs.org)

[Create React App](https://github.com/facebook/create-react-app)

[Node.js](https://nodejs.org/en/docs/)

[Nodemon](https://nodemon.io)

[Concurrently](https://www.npmjs.com/package/concurrently)

[Yarn](https://yarnpkg.com/en/)

### External Resources
These components were developed by third-party teams, and used for the execution of this prototype.

[City of Boston Patterns Library](https://github.com/CityOfBoston/patterns)

[City of Boston Public Data Portal](https://data.boston.gov)

[MapBox](https://www.mapbox.com)

## About the Project
> Information regarding the process and purposes of this project

### Issue
Moving day--September 1--is a big day in Boston. 
A large number of permits for moving trucks and moving pods are pulled for the day. 
While moving occurs citywide, permits are always pulled for the neighborhoods of Fenway, Mission Hill, and the North End. 
These neighborhoods are small, and permit spaces are finite.
These neighborhoods host a high density of movers.
Permits are presently issued for entire days, but trucks or pods often occupy spaces for a set of hours.
Only some people are able to hold moving spaces legally, producing both free riding on permitted spaces as well as illegal moves which may cause further congestion and safety hazards.

### Questions
Focusing on one neighborhood with high moving permitting, can we create a system that maximizes people’s ability to move legally and safely?
For what streets are moving permits ALWAYS pulled on moving day (Sept 1)?
How would people ‘reserve’ a space?
How long should people ‘reserve’ a space for?
How would a permitting officer/ticketing officer know who has the space reserved on a specific day and time?

### Scope of Work
Gordon College Consultants (below) will help Principle Stakeholders identify preliminary answers to the above Questions by prototyping a digital solution to the above Issue. The prototyped digital solution will require a deep spatial understanding of permitting data, a deep understanding of the experience of the current permitting system, and the skills and resources necessary to fabricate a working alpha (or beta!) digital system. This prototype will be delivered by the end of the Gordon College spring semester. Should the Gordon College team submit with ample time left (and should they be interested in pursuing a next step of those prototype), there is possibility for additional scoping.

The New Urban Mechanics will provide access to data, key stakeholders, and other resources as necessary. They will also provide regular feedback (frequency established in partnership with the team).

The prototype delivered by Gordon College Consultants will be used as a proof-of-concept design and catalyst for internal stakeholder conversations around moving day permitting, and may not be adopted as a final solution to the above Issue.

## Scoping Resources
[Moving Truck Permit Dataset](https://data.boston.gov/dataset/open-moving-truck-permits)

[Current Street Sweeping Schedules](https://data.boston.gov/dataset/street-sweeping-schedules)

[Current Moving Permit Reservation System](https://www.boston.gov/how-reserve-parking-spot-your-moving-truck)

[General Moving Day Information](https://www.boston.gov/movingx)

