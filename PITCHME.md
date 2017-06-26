<!-- .slide: class="center" -->
## Building your first chatbot 
#HSLIDE
<!-- .slide: class="center" -->
##I am Boris Modylevsky
##I am not a bot
#HSLIDE
<!-- .slide: class="center" -->
A chatbot is a computer program which conducts a conversation via auditory or textual methods.
#HSLIDE
<!-- .slide: class="center" -->
![Video](https://www.youtube.com/embed/8vAzybPv1fo)
#HSLIDE

Boris: Hello

Fin: Hi there! My name is Fin. What's your name?

Boris: My name is Boris

Fin: Hello Boris. It's nice to meet you. How can I help you?

Boris: Can you tell me my bank account balance?

Fin: Sure, your balance is $36,000

#HSLIDE
<!-- .slide: class="center" -->
## Synthetic Intelligence Markup Language
#HSLIDE
<!-- .slide: class="center" -->
```xml
<Model>
  <Pattern>HELLO</Pattern>
  <Response>Hi there! My name is Fin. What's your name?</Response>
</Model>
```
#HSLIDE
<!-- .slide: class="center" -->
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
<!-- .slide: class="center" -->
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
<!-- .slide: class="center" -->
```xml
<Model>
	<Pattern>MY NAME IS *</Pattern>
	<Response>Hello <User Set="Name"><Match /></User>.</Response>
</Model>
```
#HSLIDE
<!-- .slide: class="center" -->
```xml
<Model>
	<Pattern>WHAT IS MY NAME</Pattern>
	<Response>Your name is <User Get="Name" /></Response>
</Model>
```
#HSLIDE
<!-- .slide: class="center" -->
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
<!-- .slide: class="center" -->
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
```Powershell
Install-Package Syn.Bot
```
#HSLIDE
<!-- .slide: class="center" -->
```C#
SimlBot simlBot =  new SimlBot();
simlPackage = File.ReadAllText("FinBot.simlpk");
simlBot.PackageManager.LoadFromString(simlPackage);
simlBot.Adapters.Add(new BalanceAdapter());
ChatResult chatResult = simlBot.Chat(input);
```
#HSLIDE
## Thank you!
https://github.com/borismod/simlbot
https://github.com/borismod/finbotapp
<!-- .slide: class="center" -->

