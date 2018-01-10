#Code Challenge One

##Usage
###Search bar
Use search bar for all-text search. It will look into any text field of the database.

###Filter
You can further filter the results returned by Search Bar. The reset buttom will reload the whole page.

###Tab: records
This is where you investigate data details. Specifically, doulbe click any table row gives you a pop-up modal to view and edit details; you can also update the record from here. Delete button for each row pops up the deletion confirmation modal.

###Tab: import from XML
Import data or wipe the database from here. The only accepted data file is this degree records in the format of XML. Before loaded into the database, the data can be previewed.

##Code base

###Application Architecture
PHP scripts as the backend handle all the CRUD operations. The PHP scripts only presents a single view during the whole lifecycle of the application.

Frontend rendering is handled by JQuery and AJAX calls. However, any changes that affect the state of data and database will trigger a whole-page reloading, to make sure the data displayed is up to date.

Though the search bar retrieves data from backend operations, any further filtering (by the name of school and academic level) relies on client side calculations performed by browsers.

###Infrastructure
Having been developing using MVC for years, I'm not very comfortable with a single .php file application. Instead, I brewed a hand-made, micro MVC frame work for this project, to ease the difficulties of development. Credits go to Chris_ Yu(article), Neil Rosenstech(article), and Anant Garg(article)

###Database
You will need manually, as the root user, execute the 2 .sql files to setup the schema. The schema is not strict 3NF because of the tight schedule of final weeks and the hardness of my boy's fever over the weekend.

There are 2 tables, degrees and schools. Some constraints are employed to guarantee the data consistency. For example, the degrees.school_id is a FK of CASCADE DELETION, referring to schools.id. Some UNIQUE constraints on composite keys are also used to prevent data repetition that may be caused by importing the same data file multiple times.

###Security
Again, due to tight schedule, I didn't implement any ACL or security module. However, it should not be hard to design and implement a middleware to guard the application.

###Routing
The home-made MVC uses a simple way to map url to array of controller, action and other parameters. Currently, it doesn't support path-only, beautiful urls.

###Data Access Layer
The data access layer of this MVC framework consists of a model class and a self-made MySQL lib. The MySQL lib will be automatically loaded during the initialization of the Application class. It manages the connections using mysqli library.And due to tight schedule, pagination module was not implemented.

###Controller
Since there no dedicated Routing module and Request class, I access the php super global variables directly, which I understand is not good practice, though it fastens the development.

###The V Part
By not using any template languages, the processing speed and the implementation of this home-made MVC are facilitated. require() statement is employed to ease debugging, though in production, include() should be employed more often.

The single application page is divided into 12 .php files, according to their functionality and page layout. The main page is test.php, which I know may not be a good name.

###JavaScript & CSS
JQuery is the major weapon for the front-end development of this project. Pure JQuery is employed, without any plugins, in order to make it easier to read the script.

Bootstrap3 is employed to render the style of ths application. Only 1 ad-hoc style sheet is placed in the head of the document to make the file uploader vertically centered. No inline style is used for the sake of layout consistency.

##Major bugs
1. Database
    1. NULL and unique row/index
       
       Data validation could be performed in either code base or dbms:
       * I/O no expensive and longer response time allowed -> code base
       * otherwise -> dbms 
    
##Future work (potential improvements)
###Backend
1. RESTFul
    1. Route / URL
    2. Controller methods
    
2. Database access
    1. DB access interface for different drivers
    
3. Pagination
###Frontend
####JavaScript
1. Parameterize Ajax calls
    * Abstract and wrap commons of current Ajax calls
    
2. Modularize current scripts
    * Introduce React and Redux
###UML
####Class diagram
