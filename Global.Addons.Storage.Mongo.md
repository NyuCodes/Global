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
