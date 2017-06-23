## Building your first chatbot 

#HSLIDE

##I am Boris Modylevsky
##I am not a bot

#HSLIDE

A chatbot is a computer program which conducts a conversation via auditory or textual methods.

#HSLIDE

FinBot video
![Video](https://www.youtube.com/watch?v=8vAzybPv1fo)

#HSLIDE

Boris: Hello

Fin: Hi there! My name is Fin. What's your name?

Boris: My name is Boris

Fin: Hello Boris. It's nice to meet you. How can I help you?

Boris: Can you tell me my bank account balance?

Fin: Sure, your balance is $36,000

#HSLIDE

## Synthetic Intelligence Markup Language

#HSLIDE
```xml
<Model>
  <Pattern>HELLO</Pattern>
  <Response>Hi there! My name is Fin. What's your name?</Response>
</Model>
```
#HSLIDE
```xml
<Model>
  <Pattern>
	<Item>HI</Item>
	<Item>HEY</Item>
	<Item>HELLO</Item>
  </Pattern>
  <Response>Hi there! My name is Fin. What's your name?</Response>
</Model>
```
#HSLIDE
```xml
<Model>
  <Pattern>HOW ARE YOU</Pattern>
  <Response>
	<Random>
		<Item>I am doing great</Item>
		<Item>I am fine thank you</Item>
		<Item>Never been better</Item>
	</Random>
</Response>
</Model>
```
#HSLIDE
```xml
<Model>
	<Pattern>MY NAME IS *</Pattern>
	<Response>Hello <User Set="Name"><Match /></User>.</Response>
</Model>
```
#HSLIDE
```xml
<Model>
	<Pattern>WHAT IS MY NAME</Pattern>
	<Response>Your name is <User Get="Name" /></Response>
</Model>
```
#HSLIDE
```xml
<Concept Name="Balance" 
	xmlns:finbot="http://finbot.com/namespace#finbot">
	<Model>
	  <Pattern>{WHAT IS MY BALANCE}</Pattern>
	  <Response>
		Your balance is <finbot:Balance></finbot:Balance>
	  </Response>
	</Model>
</Concept>
```
#HSLIDE
```C#
public class BalanceAdapter : IAdapter
{
	public XName TagName
	{
		get
		{
			XNamespace ns = "http://finbot.com/namespace#finbot";
			return ns + "Balance";
		}
	}	

	public override string Evaluate(Context context)
	{
		return FinancialServices.GetTotalBalance().ToString();
	}
}
```
#HSLIDE
```C#
public class BotController : ApiController
{
	private SimlBot _simlBot =  new SimlBot();
	
	public BotController()
	{
		string simlPackage = File.ReadAllText("FinBot.simlpk");
        _simlBot.PackageManager.LoadFromString(simlPackage);
        _simlBot.Adapters.Add(new BalanceAdapter());
	}

	[HttpGet]
	public string Get([FromUri] string input)
	{
	    return _simlBot.Chat(normalizedInput).BotMessage;
	}
}
```
#HSLIDE
## Thank you!
https://github.com/borismod/simlbot
https://github.com/borismod/finbotapp


