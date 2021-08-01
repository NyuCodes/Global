<h1 align="center">
  <img src="https://media.discordapp.net/attachments/713367706736525332/867802837182054410/unknown.png" width="224px"/><br/>
  Global.Discord
	<img alt="Nuget" src="https://img.shields.io/nuget/v/Global.Discord?color=cyan&logoColor=red&style=plastic">
</h1>


<div align="center">
<h2> Global.Discord is a Plug-N-Play package designed to allow any users to quickly setup a discord bot in under 5 minutes with no prior coding experience.</h2>
&nbsp;  
&nbsp;
&nbsp;
<h4>
  <a href="https://github.com/michaelukz">Developed by Nyu</a> This <a href="https://www.nuget.org/packages/Global.Discord">package</a> is designed as educational in purpose and is not meant to serve as a replacement for a proper Command handler, This package is limited and not meant for long term use.
	
Click on package or search Global.Discord on NPM to download.
  </h4>
</div>
<div></div>
<div></div>
<div></div>
<div></div>
<div class ="Usage">
<h1>Usage:</h1>
public class Program
    {
        public static void Main(string[] args)
            => new Program().ProgramAsync().GetAwaiter().GetResult();

        public DiscordSocketClient _Client;
        public CommandService _Commands;
        public IServiceProvider _Services;
        public async Task ProgramAsync()
        {
            var PublicClient = new DiscordSocketClient();
            var Engine = new DiscordEngine();
            var Client = await Engine.StartupAsync("Configuration.json", PublicClient);
            _Client = Client;
            _Commands = new CommandService();
            _Services = Engine.ConfigureServices(_Client,_Commands);
            await _Commands.AddModulesAsync(Assembly.GetEntryAssembly(), _Services);
            var count = _Commands.Commands as List<CommandInfo>;
            await Task.Delay(-1);
        }
</div>
	<div class="Usage-Adding-an-Event">
	To add an event, simply add:
		
	_Client.EventNameHere += MethodNameHere
<div>
	<h1> Creating a command handler. </h1>
	Within your program class add
	
	_Client.MessageReceived += CommandHandler;
	
Then we add our Method, you can also press tab when typing within visual studio to auto complete the method for you.
	
	private async Task CommandHandler(SocketMessage arg)
	{
		int pos = 0; // This is the position of the command trigger IE !ping, the trigger differentiating between command and message is the '!'
		var _msg = arg as SocketUserMessage; // Here we cast arg to a SocketUserMessage, this has many benefits, but mainly it has certain methods, IE 'Author.IsBot'
		if (!_msg.Author.IsBot) // We now check if the user is not a bot, that '!' inverts the if to be 'if-is-not [bot]'
		{
			await Task.Delay(100);
			Console.WriteLine("[" + _msg.Author.Username + "]" + ": " + _msg.Content); // Now we write the message into the console, you can jazz this up in many ways including changing the color, but I will leave that up to you
			if (_msg.HasStringPrefix(DiscordEngine.Configuration.Load().Prefix.ToLower(), 	ref pos, StringComparison.OrdinalIgnoreCase) // This is checking if our assigned prefix has been detected at the start, and it tells it to ignore case
			|| _msg.HasMentionPrefix(_Client.CurrentUser, ref pos)) // This checks if the bot has been mentioned instead of a prefix, you can disable this by deleting this
			{
				var _Context = new SocketCommandContext(_Client, _msg); // Now we create a command context with our client, and our message
				var result = await _Commands.ExecuteAsync(_Context, pos, _Services); // Now we attempt to execute the command
				if (!result.IsSuccess) // checking if the command failed (notice the '!')
				{
					await _Context.Channel.SendMessageAsync($"[Error]: {result.ErrorReason}"); // tells the bot to respond with the error message
				}
			}
		}
	}
</div>
		<div>
			<h2>Time to make our first command</h2>
			<a>I prefer to create mine in a seperate class, the benefit to this is simple navigation, rather than sorting through a massive list to edit 1 command, you just open the correct file.</a>
			
	using Discord.Commands;
	using System.Threading.Tasks;
	namespace YourBotsNameHere
	{
		public class Ping : ModuleBase<SocketCommandContext>
		{
			[Command("ping")] // Here you set the name of the command, this will become '!ping' in chat
			public async Task DoPing() // Here we name our method and request any potential information.
			{
				await ReplyAsync("Pong!"); // Here we respond with pong!
			}
		}
	}
And that's it, time to start making your own bots!
</div>
</div>
