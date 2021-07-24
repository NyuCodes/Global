<h1 align="center">
  <img src="https://media.discordapp.net/attachments/713367706736525332/867802837182054410/unknown.png" width="224px"/><br/>
  Global.Discord
</h1>


<div align="center">
<h2> Global.Discord is a Plug-N-Play package designed to allow any users to quickly setup a discord bot in under 5 minutes with no prior coding experience.</h2>
&nbsp;  
&nbsp;
&nbsp;
<h4>
  <a href="https://github.com/michaelukz">Developed by Nyu</a> This <a href="https://www.nuget.org/packages/Global.Discord">package</a> is designed as educational in purpose and is not meant to serve as a replacement for a proper Command handler, This package is limited and not meant for long term use.
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
</div>
