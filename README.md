
# 15 C# 👓👓👓🕶 Best Coding Practice with Suitable XML Comments
One of the most important skills of a C# programmer is writing clean, efficient code that performs well and can be easily maintained by others who will inherit your code after you’ve moved on to other projects. This can seem like an impossible task, as there are many factors to consider when writing C# code, including variables, methods, classes, and types, just to name a few. But with these c# tips and tricks, you can learn how to write clean C# code that’s easy to read and understand by others on your team.
## 1. Name the functions with what they do👌
A bad practice is to name functions with incorrect or incomplete names. **Just by reading the name of the function we should know almost 100% of what EXACTLY it does**, otherwise this only causes confusion.
 **Good Practice:**

```c#
///<summary>
/// This sends notification to users
///</summary>
///<returns>
///Implement or calls  a method Send
///</returns>
public class SlackNotification
{
    /// This is basically showing a slack notification.
    ///It is appropraitely named with what the function is doing

    public void Send()
    {
        SendMessage(this._to, this._files, this._body);
    }
}

var message = new SlackNotification(...);
// Clear and obvious
message.Send();
```
The best recommendation is to spend a little more time thinking of a name that is very descriptive for the function. If you don’t do this good practice — just to save a couple of seconds in defining a good name, you will waste a lot more time in the future reading those lines of code and trying to understand what they do.


## 2. Never Save Unused Code😃
This bad practice reminds me of when we keep or collect “stuff” at home but never make use of it. This is the same, if you have code that is not used, delete it. There is no point in having it taking up space and bothering you.


**Good Practice**:
```c#
///<summary>
/// All the unused codes are deleted and the ones to be used are saved
///</summary>
///<returns>
///Returns a string
///</returns>
public void RequestMethod(string url)
{
    ///
}

var request = RequestMethod(requestUrl);
SlackChannel("bytehide", request, "get users");

```
**Remember**: Don’t bite off more than you can chew. If you haven’t used that code, there’s no point in keeping it there. You can still check it again in the version history in case you ever need it.

## 3.One level of abstraction per function❤💕👓🤷‍♀️🚗
If you are developing and you find that a function does not have only one level of abstraction, but has several, this means that the function is doing too many things by itself.

This bad practice, apart from in the future generating questions like: What is this? What exactly does it do? It makes it difficult to reuse code because it does many things at the same time.

```c#

///<summary>
/// This class uses implements abstraction
///</summary>
///<returns>
///Returns a string
///</returns>
class Tokenizer
{
    public string Tokenize(string code)
    {
        var regexes = new string[] {
            // ...
        };

        var statements = explode(" ", code);
        var tokens = new string[] {};
        foreach (var regex in regexes)
        {
            foreach (var statement in statements)
            {
                tokens[] = /* ... */;
            }
        }

        return tokens;
    }
}

class Lexer
{
    public string Lexify(string[] tokens)
    {
        var ast = new[] {};
        foreach (var token in tokens)
        {
            ast[] = /* ... */;
        }

        return ast;
    }
}

class BetterJSAlternative
{
    private string _tokenizer;
    private string _lexer;

    public BetterJSAlternative(Tokenizer tokenizer, Lexer lexer)
    {
        _tokenizer = tokenizer;
        _lexer = lexer;
    }

    public string Parse(string code)
    {
        var tokens = _tokenizer.Tokenize(code);
        var ast = _lexer.Lexify(tokens);
        foreach (var node in ast)
        {
            // parse...
        }
    }
}
```
This, apart from leaving the code cleaner, will allow you to reuse code and test it (which you could not do properly before due to the large amount of things the function does).

## 4.Never write in global functions👏
This bad practice consists of **“contaminating”** the globals. This is not a good thing because you could have problems and even crash with another library. Any user could run into this problem and would not realize it until the exception occurred.

**Good Practice:**
```c#

///<summary>
/// This class configures a dictionary
///</summary>
///<returns>
///Returns a string
///</returns>

class Configuration
{
    private Dictionary<string, string> _configuration;

    public Configuration(Dictionary<string, string> configuration)
    {
        _configuration = configuration;
    }

    public string[] Get(string key)
    {
        return _configuration.ContainsKey(key) ? _configuration[key] : null;
    }
}

```
After this, we load the configuration and when it is ready, we create an instance of the Configurationclass
```c#
///<summary>
/// we create an instance of the Configurationclass
///</summary>
///<returns>
///Returns a string
///</returns>
var configuration = new Configuration(new Dictionary<string, string>() {
    ["product"] = "shield"
});

```

## 5.Limiting function arguments💖💖👍
It is very important to limit the number of parameters that a function has. Remember: The simpler, the better. The problem comes when a function has more than 3 arguments, because it can cause many problems in understanding what it does.
**Bad Practice**:

```c#
///<summary>
/// Too many arguements used
///</summary>
///<returns>
///void
///</returns>
```c#

public void ProtectApplication(string path, string configurationPath, string outPutPath, CancellationToken cancellationToken)
{
    // ...
}

```

**Good practice:**
```c#
///<summary>
/// We have used properties instead of many parameters
///</summary>
///<returns>
///protected application configuration
///</returns>
```c#
public class ProtectionConfig
{
    public string Path { get; set; }
    public string ConfigurationPath { get; set; }
    public string OutPutPath { get; set; }
    public CancellationToken cancellationToken { get; set; }
}

var config = new ProtectionConfig
{
    Path = "./app.exe",
    ConfigurationPath = "./shield.config.json",
    OutPutPath = "./app_protected.exe",
    CancellationToken = source.Token;
};

public void ProtectApplication(ProtectionConfig config)
{
    // ...
}

```
The best option is to use 1 or 2 arguments. Can you use more? Of course you can, but only if you are aware that in a couple of months you will have to figure out what is supposed to do what. The ideal would be to group when there are 3 or more.

If you have more than 2 arguments in your function, it means that function is doing too many things.


## 6.Use searchable names🤷‍♂️🤷‍♀️
I am sure that more than once you forget where something is and you start looking for that something but you can’t find it because you don’t remember what name you gave to the variable or directly, you don’t remember if you named that constant. For your better understanding:

**Bad Practice:**
```c#
// In the future we will not remember what 86400000 means.
clearBacklog(backlog, 86400000);

```

**Good Practice:**
```c#
// Declare constants with a searchable name
var MILLISECONDS_PER_DAY = 60 * 60 * 24 * 1000; //86400000;

clearBacklog(backlog, MILLISECONDS_PER_DAY);


```

## 7. Do use null conditional operator👍🔥🔥
The null conditional operator also called coallescing operator isto be used in a well defined manner. Failure to do some can get you stuckedin a bug.
The **bad practice** is shown below:
```c#
///<summary>
/// We defined variable "employeeName" and a coalescing/null operator
///</summary>
///<returns>
///There is no return code here, we are basically show aflaw in using null operator using if/else
///</returns>
var employeeName=””;
Session[“Name”]=”test”;
If(Session[“Name”]!=null)
{
employeeName=Session[“Name”].ToString();
}
else
{
employeeName=””;
}

```


**Good Practice:**

```c#
///<summary>
/// We defined variable "employeeName" and a coalescing/null operator
///</summary>
///<returns>
///There is no return code here
///</returns>
var employeeName=””;
Session[“Name”]=”test”;
employeeName=Session[“Name”]?.ToString() ?? “”

```
## 8. Avoid Extra Braces👓🕶
As much as possble, try avoiding extra braces so that the code in your editor doesn't look messy.
**Bad practice:**
```c#
///<summary>
/// We implicity declared a variable but the if condition statement has extra braces
///</summary>
///<returns>
///implements count
///</returns>
var count=10;
if(count>0)
{
count++;
}

```

**Good Practice:**
```c#
///<summary>
/// We implement if condition statement without extra braces
///</summary>
///<returns>
///implements count
///</returns>

If(count>0) count++;

```


## 9. Optimizing Syntax🤞✌

- To declare an empty method that only returns a view in c#, we should use the expression body.But we need to always optimize the syntax as much as possible.
**Bad Practice:**
```c#
//We implement a public function with  extra braces
Public ActionResult Login()
{
return View();
}
```

A better implementation of this is to eliminate unnecessary braces, return statements and use an arrow function instead.
**Good Practice:**
```c#
// we could optimize the syntax using Arrow functions
Public ActionResult Login() => View();

```
## 10 Always Prefix an Interface with 'I"👏😃🕶👓
Naming convention is so important even in the implementation of an interface.Using **I** to start the name of an Interface is definately a way forward.
**Good Practice:**
```c#
/*<summary>
/// We implement an interface using a public accessor
///</summary>
///<returns>
///byte Points
///</returns>*/
 Public interface IPointy
    {
        //implicitly public and abstract
        //byte GetNumberOfPoints(); //member  definition or single method


        //However, .NET interface types are able to define any number of property prototypes
        //a read-write property in an interface is like
        //retType PropName { get; set; }

        //while write only property in an interface would be like
        //retType PropName { set; }

        byte Points { get; }
    }
```
## 11.  Do not suffix enum names with Enum.😍
Create an Enum with Suffixing it with **Enum** keyword. Adding theEnum keyword is not necessary and doesn't look professional.
**Bad Practice:**
```c#
//its unprofessional to suffix Enum keyword to our enum name
Public enum DirectionEnum
{
//..
}
```

**Good Practice:**
```c#
//We can remove the Enum suffix
Public enum Direction
{
//..
}

```
## 12. Don’t repeat yourself (DRY)👍😥
This error is very common because we unconsciously repeat names or words. This bad practice in the long run makes you have a very dirty code since there will be many things that will be repeated. Let’s get down to practice:
**Bad Practice:**
```c#
/*<summary>
/// We implement an instance called MountainBike from Bike Class
///</summary>
///<returns>
///string
///</returns>*/
Bike MountainBike = new(){
   bikeBrand = "Trek",
   bikeModel = "MX Mountain",
   bikeColor = "Green"
};

void paintBike(Bike mountainBike, string color){
     mountainBike.bikeColor = color;
}
```

**Good Practice**
```c#
/*<summary>
/// We implement an instance called MountainBike from Bike Class
///</summary>
///<returns>
///string
///</returns>*/
Bike MountainBike = new(){
   brand = "Trek",
   model = "MX Mountain",
   color = "Green"
};

void paintBike(Bike mountainBike, string color){
     mountainBike.color = color;
}

```

## 13.Always encapsulate conditionals
Encapsulation is a way that helps isolate implementation details from the behavior exposed to clients of another class.

**Bad way:**

```c#
//without Encapsulation
if (website.state == "down")
{
    // ...
}
```
**Good Practices:**
```c#
//Use of Encapsulation
if (website.IsDown())
{
    // ...
}

```

## 14. Learn to use setters and getters👍👓😃👌
Many times we do not set public, private or protected methods. This prevents us from better controlling the modification of the object’s properties.

**Bad Way:**
```c#
///<summary>
/// We implement a Bank Account Class
///</summary>
///<returns>
///int
///</returns>
class BankAccount
{
    public double Balance = 5000;
}

var bankAccount = new BankAccount();

// Buy a cappuccino ☕️ ...
bankAccount.Balance -= 15;

```

**Good Practice:**

```c#
///<summary>
/// We implement a Bank Account Class
///</summary>
///<returns>
///int
///</returns>
class BankAccount
{
    private double _balance = 0.0D;

    pubic double Balance {
        get {
            return _balance;
        }
    }

    public BankAccount(balance = 1000)
    {
       _balance = balance;
    }

    public void WithdrawBalance(int amount)
    {
        if (amount > _balance)
        {
            throw new Exception('Amount greater than available balance.');
        }

        _balance -= amount;
    }

    public void DepositBalance(int amount)
    {
        _balance += amount;
    }
}

var bankAccount = new BankAccount();

// Buy a cappuccino ☕️ ...
bankAccount.WithdrawBalance(price: 15);

balance = bankAccount.Balance;

```

## 15.Composition is better than inheritance👌😃👓🔥🤞✌💖😎
Although many do not know whether to use inheritance or composition, let me tell you that it is better to choose to use composition.

At first, many programmers think that inheritance is better but, you always have to ask yourself if composition could somehow model the problem better.

**Bad way:**
```c#
///<summary>
/// We implement a Car Class
///</summary>
///<returns>
///string
///</returns>
class Car
{
    private string Model { get; set; }
    private string Brand { get; set; }

    public Car(string model, string brand)
    {
        Model = model;
        Brand = brand;
    }

    // ...
}

// Bad because Car "have" engine data.
// CarEngineData is not a type of Car

class CarEngineData : Car
{
   private string Model { get; set; }
   private string Brand { get; set; }

   public CarEngineData(string model, string brand, string displacement, string horses)
    {
         // ...
    }

    // ...
}

```
**Good Practice:**
```c#
///<summary>
/// We implement a Car Class
///</summary>
///<returns>
///string
///</returns>
class CarEngineData
{
    public string Displacement { get; }
    public string Horses { get; }

    public EmployeeTaxData(string displacement, string horses)
    {
        Displacement = displacement;
        Horses = horses;
    }

    // ...
}

class Car
{
    public string Model { get; }
    public string Brand { get; }
    public CarEngineData EngineData { get; }

    public Car(string model, string brand)
    {
        Model = model;
        Brand = brand;
    }

    public void SetEngine(string displacement, double horses)
    {
        EngineData = new CarEngineData(displacement, horses);
    }

    // ...
}

```

To know when it is best to use which one, let’s look at a [Quick Example](https://github.com/thangchung/clean-code-dotnet#classes)
Relationship “is-a” (Human-Animal)
Relationship “has-a” (User-UserDetails)
