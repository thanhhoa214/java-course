# JavaWeb

## Front-end

### 1. Rereading this feature requirements 2-3 times.

### 2. Need view ?

### 3. Using data inside or not ? 

- JSP
- HTML

### 4. Purpose ?

- Naming

### 5. Title & h1

### 6. Anywhen wanna move to an other page ?

-  <a>
- form

### 7. Show list data

- table

	- 1. table border=1
	- 2. table row >> tr

		- table header >> th

	- 3. table row >> tr

		- 1. table data >> td
		- 2. If submit data single row, form with hidden field and show button “Submit”

##  Database

### 1. Sketching without digital device. 
(100% concentrated)

### 2. Writing schema script by hand for editable further more.

## Back-end

### Structure

- name.packages

	- SamplesDAO
(CRUD)

		- Create
		- Read
		- Update
		- Delete

	- SamplesDTO

		- Mapped model with SQL Table Row
		- Constructor full and without params
		- Getter & Setter
		- toString

- name.controllers

	- MainController

		- Declares any routing through pages & Controllers.

	- FeatureController

- name.filters

	- Layers what request meets first.
	- Run Top to Bottom
(web.xml preferences)

- name.utils

	- Services, utils without definition in Database
	- Example: ShoppingCart, EmailService

- name.db

	- getConnection()

## Configuration Files

### context.xml

- Point to Dynamic Database Connection

	- Why need Dynamic Database Connection?

### web.xml

- Setup routing
- Setup filters

## 0. Setup Project

### 1. Create new folder.

### 2. Create git repo & link with the folder above.

### 3. Create folder “db”

### 4. Create folder “diagram”

### 5. Create folder “document”

### 6. Create project inside

### 7. Writing README.md for running project

### 8. Run project

### 9. Push to master

### 10. Checkout develop

## Essential Document

### Setup

- Netbean 8.2
- SQL Server 2014
- git

### Specific JAR

- jstl 2.2
- jdbc
- strut2

### Notes

- Thinking flow: FE > DB > BE
(Test-first development)
- Coding flow: Setup > (FE > DB > BE) x n

## implements Serializable

## Practice

### 1. Create

- view_samples.jsp
- ViewSamplesController
- hoant.samples

	- SamplesDAO
	- SamplesDTO

### 2. Inject ViewSamplesController into MainController (switch-case routing)

- Testing for ensure routing reaches ViewSampleController

### 3. Writing view_samples.jsp

### 4. Writing SamplesDTO

### 5. Writing SamplesDAO

- Read

	- 1. Define input, output & name of the method

		- public ArrayList<SamplesDTO> getAll() {

	- 2. Create  appropriate variable for data receiving & returning

		- ArrayList<SamplesDTO> samples = new ArrayList<>();

	- 3. Create selectQuery

		- String selectQuery = "SELECT id, name, .... FROM table";

	- 3.5. Create try statement Java 8 for auto-closing connection. (Only use with closable variables)

		- try (

	- 4. Create Connection

		- Connection connection = MyConnection.getConnection();

	- 5. Create PreparedStatement

		- PreparedStatement selectStatement = 
connection.prepareStatement( selectQuery );

	- 6. Create ResultSet for receiving query result

		- ResultSet resultSet = selectStatement.executeQuery();

	- 6.5. Close try statement Java 8 for auto-closing connection.

		- ) {

	- 7. Loop through resultSet to get & return data back.

		- while (resultSet.next()) { 

	- 8. Create dummy sample (SamplesDTO) for receiving & parsing data

		- SamplesDTO sample = new SamplesDTO();

	- 9. Set data for attributes

		- sample.setId( resultSet.getString("id") );
		- sample.setName( resultSet.getString("name") );
		- .....

	- 10. Add dummy to our samples

		- samples.add( sample)

	- 11. Close resultSet loop

		- }

	- 12. Return samples

		- return samples;

	- 12.5. Close block try statement Java 8 for auto-closing connection.

		- }

	- 13. Close method

		- }

### 6. Writing ViewSamplesController

- 1. Define input, output & name of the method
(as attributes of ViewSamplesController Class)

	- private static final String FAIL = "";
private static final String SUCCESS = "view_samples.jsp";

- 2. Create  appropriate variable for data receiving & returning 
(inside processRequest())

	- String url = FAIL;

- 3. Handle error by try-catch-finally block

	- try {
	- } catch (SQLException ex) {
         Logger
         .getLogger (ViewSamplesController.class.getName())
         .log(Level.SEVERE, null, ex);
} catch (ClassNotFoundException ex) {
         Logger
         .getLogger (ViewSamplesController.class.getName())
         .log(Level.SEVERE, null, ex);
} catch (NamingException ex) {
         Logger
         .getLogger (ViewSamplesController.class.getName())
         .log(Level.SEVERE, null, ex);
}
	- } finally {
     request.getRequestDispatcher( url ).forward( request, response);
     // or use response.sendRedirect( url );
}

- 4. Use SamplesDAO for retrieving data
(inside try block)

*XMind - Trial Version*