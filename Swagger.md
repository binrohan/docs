# Swagger & Swashbuckle

## What is Swagger ?
Swagger aka OpenAPI Specification helps make information about how to use an API more accessible and understandable for developers. It's like a friendly guide that explains how to talk to a piece of software so that different programs can work together effectively.

Let’s learn some swagger features to make our .NET web api project more accessible for other developers.

First we need to know about **What is Swashbuckle ?**
Swashbuckle is a library for the .NET platform that integrates with .NET Web API projects. It's specifically designed to work with Swagger. Swashbuckle helps generate Swagger documentation automatically for your ASP.NET Web API.

## How Swashbuckle Works:
- **Build Process**: When you build your .NET application, _Swagger_ examines the API controllers, actions, and associated attributes in your code.
- **OpenAPI JSON Generation**: _Swagger_ dynamically generates the OpenAPI Specification in JSON format based on the information gathered during the build process.
- **Swagger UI or Documentation Endpoint**: he generated OpenAPI JSON can be exposed through a UI (HTML, CSS, JS) or a dedicated endpoint in your application, allowing developers to interactively explore the API documentation.

### Now we see, there are **Three Main Components in Swashbuckle**.
- **Swashbuckle.AspNetCore.SwaggerGen**: A Swagger generator that builds SwaggerDocument objects directly from your routes, controllers, and models. It's typically combined with the Swagger endpoint middleware to automatically expose Swagger JSON.
- **Swashbuckle.AspNetCore.Swagger**: A Swagger object model and middleware to expose SwaggerDocument objects as JSON endpoints.
- **Swashbuckle.AspNetCore.SwaggerUI**: an embedded version of the Swagger UI tool. It interprets Swagger JSON to build a rich, customizable experience for describing the web API functionality. It includes built-in test harnesses for the public methods. 

## Installation:
Add **Swashbuckle** nuget package in web api project:
`dotnet add TodoApi.csproj package Swashbuckle.AspNetCore`

Add the swagger generator to the service collection:
`builder.Services.AddSwaggerGen();`

Add swagger middlewares:
```
app.UseSwagger(); 
app.UseSwaggerUI();
```


