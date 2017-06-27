## Building your first chatbot 
#HSLIDE

##I am Boris Modylevsky
##I am not a bot
#HSLIDE
A chatbot is a computer program which conducts a conversation via auditory or textual methods.
#HSLIDE

### FinBot video

![Video](https://www.youtube.com/embed/8vAzybPv1fo)
#HSLIDE

### Synthetic Intelligence Markup Language

```xml
<Siml>
  <Concept Name="Introduction">
    <Model>
	  <Pattern>HELLO</Pattern>
	  <Response>
		Hi there! My name is Fin. What's your name?
	  </Response>
    </Model>
  </Concept>
</Siml>
```
#HSLIDE

### Multiple patterns

```xml
<Model>
  <Pattern>
	<Item>HI</Item>
	<Item>HEY</Item>
	<Item>HELLO</Item>
  </Pattern>
  <Response>
    Hi there! My name is Fin. What's your name?
  </Response>
</Model>
```
#HSLIDE

### Random response

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

### Wildcards

```xml
<Model>
	<Pattern>MY NAME IS *</Pattern>
	<Response>Hello <Match /></Response>
</Model>
```
#HSLIDE

### More wildcards

%  Matches zero or more words

\_  Matches one or more words

$ Matches zero or more words but ranks lower than %

\* Matches one or more words but ranks lower than \_

#HSLIDE

### Bot Variables

```xml
<Model>
	<Pattern>WHAT IS YOUR NAME</Pattern>
	<Response>My name is <Bot Get="Name"></Bot>.</Response>
</Model>
```

#HSLIDE

### User Variables

```xml
<Model>
	<Pattern>MY NAME IS *</Pattern>
	<Response>
		Nice to meet you <User Set="Name"><Match/></User>.
	</Response>
</Model>
<Model>
	<Pattern>WHAT IS MY NAME</Pattern>
	<Response>Your name is <User Get="Name" /></Response>
</Model>
```

#HSLIDE

### Custom adapter

```xml
<Concept Name="Balance" 
	xmlns:finbot="http://finbot.com/ns">
	<Model>
	  <Pattern>{WHAT IS MY BALANCE}</Pattern>
	  <Response>
		Your balance is <finbot:Balance></finbot:Balance>
	  </Response>
	</Model>
</Concept>
```
#HSLIDE

### Install nuget package

```Powershell
Install-Package Syn.Bot
```

#HSLIDE

### Implement custom adapter

```C#
using Syn.Bot.Siml;
public class BalanceAdapter : IAdapter
{
	public XName TagName
	{
		get
		{
			XNamespace ns = "http://finbot.com/ns";
			return ns + "Balance";
		}
	}	
	public override string Evaluate(Context context)
	{
		/// Your code goes here
	}
}
```

@[1](Add using)
@[2](Define Adapter class)
@[4-11](Define XML Tag)
@[12-15](Implement Evaluate method)

#HSLIDE

### Consume SIML package

```C#
using Syn.Bot.Siml;

SimlBot simlBot =  new SimlBot();

simlPackage = File.ReadAllText("FinBot.simlpk");
simlBot.PackageManager.LoadFromString(simlPackage);

simlBot.Adapters.Add(new BalanceAdapter());

ChatResult chatResult = simlBot.Chat(input);
```

@[1](Add using)
@[3](Create SimlBot)
@[5-6](Load package)
@[8](Load adapters)
@[10](Get chat result)

#HSLIDE

## Demo

#HSLIDE

## Thank you!
https://github.com/borismod/simlbot
https://github.com/borismod/finbotapp
