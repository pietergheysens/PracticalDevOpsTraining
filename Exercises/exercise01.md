# Exercise 1


## Learnings

1. How to create a RESTful Web API project with OWIN from scratch
1. Understand the importance of NuGet (will become even more important with .NET Core)
1. Learn very basics about ASP.NET Web API development (this will not be a deep dive as we focus on DevOps, not just Dev) 
1. Commit solution to a git repository in VSTS


## Creating Project in Visual Studio

1. [Optional] Learn more about REST and Web API [https://blogs.msdn.microsoft.com/martinkearn/2015/01/05/introduction-to-rest-and-net-web-api/]

1. [Optional] Learn more about OWIN and Katana [http://www.asp.net/aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana]

1. Start Visual Studio

1. Create a new web project. **Disable** Application Insights for now. We will add Application Insights later.<br/> 
   ![New Web Project in VS](img/visual-studio-new-web-project.png)

1. Use the **ASP.NET 4.5.2 "Empty" Template**:<br/>
   ![New Web Project in VS](img/visual-studio-new-web-project-02.png)

1. Switch to latest version of .NET:<br/>
   ![Switch to latest .NET](img/switch-to-dotnet-4_6.png)

1. Install necessary NuGet packages by running the following commands in Visual Studio's *Package Manager Console* (you can use *Manage NuGet Packages for Solution* instead if you prefer GUI over PowerShell):
   * `Install-Package Microsoft.AspNet.WebApi.Owin`
   * `Install-Package Microsoft.Owin.Host.SystemWeb`
   * `Install-Package Microsoft.Owin.Cors`
   * `Install-Package Microsoft.ApplicationInsights.Web`
   * `Install-Package WindowsAzure.Storage`

1. Add an OWIN Startup Class:<br/>
   ![Add OWIN Startup Class](img/create-startup-class.png)

1. Replace the `Configuration` method with the following sample code.
   ```
    public void Configuration(IAppBuilder app)
    {
        app.Run(context => context.Response.WriteAsync("Hello World!"));
    }
   ```

1. Run the program and see if the browser shows `Hello World` for all paths.


## Add Service Implementation

1. Open *Add References*:<br/>
   ![Add References](img/add-references.png)

1. Add references to the following framework assemblies:
   * `System.ComponentModel.Composition`
   * `System.ComponentModel.Composition.Registration`
   * `System.Reflection.Context`

1. Copy `.cs` files from [Excercise-1-Service-Implementation](Assets/Exercise-1-Service-Implementation) into your project. Note that you can overwrite `Startup.cs`.

1. Add the following `appSettings` to your `web.config` file. These settings control how many random books are generated by the Web API.
   ```
    <?xml version="1.0" encoding="utf-8"?>
    ...
    <configuration>
        <appSettings>
            <add key="MinimumNumberOfBooks" value="1"/>
            <add key="MaximumNumberOfBooks" value="5"/>
        </appSettings>
        ...
    </configuration>
   ```

1. Build your solution. There should be no errors.

1. Run your program and try the URL `http://localhost:2690/api/books` (this assumes that your app runs on port 2690; you have to replace this port with the port that your Visual Studio has chosen).

1. Refresh the URL mentioned above multiple times. Note how random books with random names are generated.

1. *Postman* is a very handy tool for testing Web APIs. You can get it here: [Postman on Chrome Web Store](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop). Install *Postman* and try the Web API.<br/>
   ![Postman](img/postman.png)
   
## Commit Code to Visual Studio Team Services

1. In Visual Studio's *Team Explorer*, select *Connect to Team Project*.<br/>
   ![Connect to Team Project](img/visual-studio-connect-project.png)

1. Add the "PracticalDevOps" VSTS server and select your team's Team Project.

1. Clone the project to a **new local directory** and remember the local folder to copy over the already created books solution (next step).<br/>
   ![Clone project](img/clone-project.png)

1. Copy the code your created in the previous exercises into the new local directory.

1. Look at the Changes tab in Team Explorer and see what type of files Visual Studio wants to add to a commit. You should for example see that the bin folder is part of the included changes.

1. Copy the `.gitignore` file from [Exercise-1-VSTS-Source-Control](Assets/Exercise-1-VSTS-Source-Control/.gitignore) into the new local directory.

1. In Visual Studio's *Team Explorer*, goto *Changes*, review the changes that Visual Studio has detected (see image below), and commit your changes.<br/>
   ![Commit Changes](img/commit-changs.png)

1. Take a look at the committed code in the VSTS portal.<br/>
   ![Code in Portal](img/code-in-vsts.png)
