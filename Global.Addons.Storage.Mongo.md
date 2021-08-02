<h1 align="center">
  <img src="https://media.discordapp.net/attachments/713367706736525332/867802837182054410/unknown.png" width="224px"/><br/>
  Global.Addons.Storage.Mongo
	<img alt="Nuget" src="https://img.shields.io/nuget/v/Global.Addons.Storage.Mongo?color=cyan&logoColor=red&style=plastic">
</h1>


<div align="center">
<h2> Get quick access to a mongo database and collection in just two lines, create multiple connection quick and easy with this package..</h2>
&nbsp;  
&nbsp;
&nbsp;
<h4>
  <a href="https://github.com/michaelukz">Developed by Nyu</a> This <a href="https://www.nuget.org/packages/Global.Addons.Storage.Mongo">package</a> is a early project intented for quick access to MongoDB.
	
Click on package or search Global.Addons.Storage.Mongo on NPM to download.
  </h4>
</div>
<div></div>
<div></div>
<div></div>
<div></div>
<div class = "Current-Methods">
<details><summary>Existing Methods and Usage:</summary>
<summary>Further methods will assume the Namesake 'Mongo' has been used for the MongoInitializer.</summary>
<details><summary>Connect</summary>

<h3>Method is asynchronous, Parameters include: ConnectionString, Database, Collection </h3>To connect first create an instance of the MongoInitializer.</h3>
	
	var Mongo = new MongoInitializer();
	
Now we connect using our Mongo Connection string, The name of the database you want to connect to, and the name of the collection you wish to connect to.
	
	await Mongo.Connect<YourClassHere>("127.0.0.1:23135", "DatabaseNumberOne", "WeAreNumberOne");
	
This will log into console if using a Console Application.
</details>
<details>
<summary>FindOneAsync</summary>

<h3>Method is asynchronous, Parameters include: ObjectId.</h3>
<summary>Please note that the string provided must be parsable.</summary>

	var SpecificUser = await Mongo.FindOneAsync<User>("6106e09b720680d5d7de8b6a");
	
This will return the first User with the "_id" of "6106e09b720680d5d7de8b6a" as type User.
</details>
	<details>
<summary>ReturnListAsync</summary>

<h3>Method is asynchronous, No parameters required.</h3>

	var List = await Mongo.ReturnListAsync<User>();
	
This will return the a list of Users within the connected collection and return it as type List<User>.
</details>
<details>
<summary>AddOne</summary>

<h3>Method is synchronous, Parameters include: TDoc.</h3>
<summary>Please note that the string provided must be parsable.</summary>

	var User1 = new User() { _id= "6106e09b720680d5d7de8b6a", FirstName = "Object", SecondName="One",Position = Role.Supervisor}
	Mongo.AddOne(User);
	
This does not return anything.
</details>
<details>
<summary>AddMany</summary>
<h3>Method is synchronous, Parameters include: IEnumerable<TDoc>.</h3>

	var User1 = new User() { _id= "6106e09b720680d5d7de8b6a", FirstName = "Object", SecondName="One",Position = Role.Supervisor}
	var User2 = new User() { _id= "6106e09b720680d5d7de8b6b", FirstName = "Object", SecondName="One",Position = Role.Supervisor}
	var List = new List<User>() {User1, User2};
	Mongo.AddMany(List);
	
This does not return anything.
</details>
<details>
<summary>DeleteOne</summary>
<h3>Method is synchronous, Parameters include: TDoc.</h3>
	
	var User1 = new User() { _id= "6106e09b720680d5d7de8b6a", FirstName = "Object", SecondName="One",Position = Role.Supervisor} // Assuming this exact data exists within your collection
	Mongo.DeleteOne(User1); 
	
This does not return anything.
</details>
<details>
<summary>DeleteMany</summary>
<h3>Method is synchronous, Parameters include: TDoc.</h3>
	
	var User1 = new User() { _id= "6106e09b720680d5d7de8b6a", FirstName = "Object", SecondName="One",Position = Role.Supervisor}
	var User2 = new User() { _id= "6106e09b720680d5d7de8b6b", FirstName = "Object", SecondName="One",Position = Role.Supervisor}
	var list = new List<User>() {User1, User2}; // Assuming both of these users exist within your collection.
	Mongo.DeleteMany(list); 
	
This does not return anything.
</details>
</details>
</div>
<div class ="Usage">
<h1>Usage:</h1>

	public async Task GetAllEmployees()
	{
		var Init = new MongoInitializer(); // Create a new instance of the Initializer Class
		await Init.Connect<BsonDocument>("AccessKey", "DatabaseName", "CollectionName"); // Connect with your access key, Database name, and Collection name.
		var ListOfEmployees = await Init.ReturnList<EmployeeClass>(); // Returns a List<EmployeeClass>
		var SecondInit = new MongoInitializer(); // Create a second instance.
		await SecondInit.Connect<BsonDocument>("AccessKey", "SecondDatabaseName", "CollectionName"); // Once again connecting to database (This will also log into a console if one is provided.)
		var ListOfCompanies = await SecondInit.ReturnList<Companies>(); // Return a list of <Companies>
	}
</div>
