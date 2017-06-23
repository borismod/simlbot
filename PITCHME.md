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
```
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
```
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
```
<Model>
	<Pattern>{MY NAME IS} *</Pattern>
	<Response>Hello <User Set="Name"><Match /></User>.</Response>
</Model>
```
#HSLIDE
```
<Model>
	<Pattern>WHAT IS MY NAME</Pattern>
	<Response>Your name is <User Get="Name" /></Response>
</Model>
```
#HSLIDE
```xml
<Concept Name="Balance" xmlns:finbot="http://finbot.com/namespace#finbot">
	<Model>
	  <Pattern>
			<Item>{WHAT IS MY BALANCE}</Item>
			<Item>{WHAT MY BALANCE IS}</Item>
	   </Pattern>
	  <Response>Your balance is <finbot:Balance></finbot:Balance></Response>
	</Model>
</Concept>
```
#HSLIDE
```C#
public class BalanceAdapter : IAdapter
{
	private readonly IFinancialServices _financialServices;

	public BalanceAdapter(IFinancialServices financialServices)
	{
		_financialServices = financialServices;
	}

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
		return _financialServices.GetTotalBalance().ToString();
	}
}
```
#HSLIDE

## Thank you!
https://github.com/borismod/simlbot
https://github.com/borismod/finbotapp


