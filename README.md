# dotnet-ef-starter
A walk through of starting a simple EF MVC.NetCore Application aimed at learning coders

#First Some Prerequiests
We are going to need .Net Core, I will be using version 6.0, any version latter then that should work. This is downloadable from https://dotnet.microsoft.com/en-us/download 

We are going to need something to edit files I would suggest Visual Studio Code a free editor from Microsoft.

We are going to be using a command line interface, Visual Studio Code as one built in sitting right in there for you. 

## FLow 1 
I intend to produce a few different flows of varying degrees of complexity. This flow is the simplist, and cuts a few corners that I would not do as a software professional. 


## Step 1
In your editor open the folder you will be working with, either a new empty folder, or the folder this README.md is stored in. 

Open a terminal in the same folder, if you are using Visual Studio Code you can use the menu `Terminal -> New Terminal`

### Step 1.1
In the terminal type the following command (You don't type the % sign that is a common prompt within terminal programs though yours may us $ or >)

    % dotnet --version

You should see a response similar to 

    6.0.102

If you don't you will need to sort out your install of Dotnet Core before procedding.


### Step 1.2
Create a solution, a solution is a collection of projects, a project is a collection of code files that work together. As you progress you will want to break you code into related area. A project is one of these related areas. A solution is a collection of projects that work together. In this flow we will work with only one project to keep things as simple as possible. 

Type the following:

    % dotnet new sln --name EfStarterFlow1Mvc

You should see

    The template "Solution File" was created successfully.

In your editor you should now see the file `EfStarterFlow1Mvc.sln` available to you. 

### Step 1.3
Create a project file as part of the solution.

Type the following

    % dotnet new mvc --name AllInOneMvc --no-https --auth none  

You should see


    The template "ASP.NET Core Web App (Model-View-Controller)" was created successfully.

Read the rest of the message as well.

This has created a bunch of new folders and files with the start of a website you can modify. 

You can read about the different parameters at https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-new-sdk-templates#web-options
But in short `dotnet` programe your running, all the rest of the line are arguments or instructions to that programe.
`new` asks to create a something new based on templates available to `dotnet`.
`mvc` says what we are creating is a new [ModelViewController](https://www.codecademy.com/article/mvc) project.
`--name AllInOneMvc` gives the new project a name.
`--no-https` means the website will not be encrypted, this is ok for running on your local machine, but should not be put on the internet like this.
`--auth none` means that there not going to be a way configured for users to login.

This has created a folder structure to get you off to a good start. 
`Controllers` - is a place to put your logic, your ifs your loops, your maths should go in side files in this folder.
`Models` - Models take the data from the Controller and pass it to the `View`s which know how to display it. Inside your Models folder should be simple classes designed to carry data only, no logic.
`Views` - Views worry about creating HTML pages from the data passed to them in Models from the Controllers. 
`wwwroot` - Is the place for javascript, css, images. The static content. 

### Step 1.4 
Add the new mvc project to the solution. 

Type the following

    dotnet sln add AllInOneMvc

You should see

    Project `AllInOneMvc/AllInOneMvc.csproj` added to the solution.

### Step 1.5
Run the website. You may not have personalised it yet, but you have made a website. Lets see what it looks like.

    dotnet run --project AllInOneMvc 

You should see 

    Building...
	info: Microsoft.Hosting.Lifetime[14]
	      Now listening on: http://localhost:5111
	info: Microsoft.Hosting.Lifetime[0]
	      Application started. Press Ctrl+C to shut down.
	info: Microsoft.Hosting.Lifetime[0]
	      Hosting environment: Development
	info: Microsoft.Hosting.Lifetime[0]
	      Content root path: /Users/davidwaters/dev/dotnet-ef-starter/AllInOneMvc/

You can now open [your website](http://localhost:5111) in a brower!

When you have had enough looking at your website go back to the terminal and hit `ctrl+c` to stop it. 

### Step 1.6
Feel free to have a look around in the editor, look at `Views/Home/Index.cshtml` try making changes and restarting the website. Have a look at `Program.cs` and `Controllers/HomeController.cs`, Program.cs may not make a lot of sense yet. HomeController does not do alot yet. 

When you are ready carry on to Step 2


### Step 2
We are going to add a simple Greating Model, set some values in the controller and display these in the view.

### Step 2.1
Create a new file `Models/GreatingModel.cs`

Add the following text to your new file

    namespace AllInOneMvc.Models
	{
	    public class GreatingModel
	    {
	        public string? FirstName{get; set;}
	    }
	}


This creates a place to store a FirstName. 

The `namespace` keyword gives GreatingModel the full name AllInOneMvc.Models.GreatingModel. This helps other code refer to the correct class.
The keyword `public` means other code can see and use the class `GreatingModel` and the `FirstName` property.

### Step 2.2
Save and Compile
Save the changes to your file and in your terminal type:

    dotnet build

Hopefully it will respond with text ending with

	Build succeeded.
	    0 Warning(s)
	    0 Error(s)
     
	Time Elapsed 00:00:04.07

If not read the warnings and errors, look for red or yellow underlined words in your code for hints about what has gone wrong. Holding your mouse over these will give more details on the problem. 

### Step 2.3
Use the new class and property in the View.
Open `Views/Home/Index.cshtml` in your editor.
Add a new line at the start of the file

    @model AllInOneMvc.Models.GreatingModel

This tells this page that the Model passed to it will always be a greating Model. 

Change the line

    <h1 class="display-4">Welcome</h1>

To 

    <h1 class="display-4">Welcome @Model.FirstName</h1>

Save the file.

### Step 2.4
Save all your changes and check that everything compiles just like you did in step 2.2.

### Step 2.5
Change the controller to assign your name to the GreatingModel. 
Open `Controllers/HomeController.cs` in your editor. 
Find the Index method and replace it with the following:

    public IActionResult Index()
    {
        var greating = new GreatingModel{
            FirstName = "YourFirstName"
        };
        return View(greating);
    }

Save your changes and compile to check that there are no problems.

### Step 2.6
Run your website again just like we did in Step 1.5, when you open your site in your browser you now see you are being welcomed personally. 

For your next steps see [the next branch](https://github.com/dwat001/dotnet-ef-starter/tree/Flow1.Step3)



