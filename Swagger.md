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

.NET CLI: `dotnet add TodoApi.csproj package Swashbuckle.AspNetCore`

Package Manager: `Install-Package Swashbuckle.AspNetCore`

Add the swagger generator to the service collection:
```C#
builder.Services.AddSwaggerGen();
```

Add swagger middlewares:
```C#
app.UseSwagger(); 
app.UseSwaggerUI();
```
_NB: ASP.NET Core WebAPi Project comes with Swagger_

## Configuration and Settings:
We can display more information about the project by passing options as parameter while adding SwaggerGen service.
```C#
builder.Services.AddSwaggerGen(options =>
{
    options.SwaggerDoc("v1", new OpenApiInfo
    {
        Version = "v1",
        Title = "Project Name",
        Description = "Project Description",
        TermsOfService = new Uri("https://example.com/terms"),
        Contact = new OpenApiContact
        {
            Name = "Contact Info",
            Url = new Uri("https://example.com/contact")
        },
        License = new OpenApiLicense
        {
            Name = "License Info",
            Url = new Uri("https://example.com/license")
        }
    });
});
```

## Customize Swagger UI:
To add custom CSS and JS follow this steps

```C#
app.UseStaticFiles();
```
This line enable evering static files from wwwroot directory

```C#
app.UseSwaggerUI(options =>
{
    options.InjectStylesheet("/swagger/style.css");
    options.InjectJavascript("/swagger/script.js");
});
```
Pass the url of CSS or JS file path through the options in UseSwaggerUI middleware

## Adding Authentication:
To add Token based authentication add options in Swagger Generator service
```C#
builder.Services.AddSwaggerGen(options =>
{
    //...
    options.AddSecurityDefinition("Bearer", new OpenApiSecurityScheme
    {
        In = ParameterLocation.Header,
        Description = "Please enter token",
        Name = "Authorization",
        Type = SecuritySchemeType.Http,
        BearerFormat = "JWT",
        Scheme = "bearer"
    });

    options.AddSecurityRequirement(new OpenApiSecurityRequirement
    {
        {
            new OpenApiSecurityScheme
            {
                Reference = new OpenApiReference
                {
                    Type=ReferenceType.SecurityScheme,
                    Id="Bearer"
                }
            },
            new string[]{}
        }
    });
    //...
});

```

## Documentation Formatting:
We can format documentation using couple methods. Such as
- XML
- Data Annotations
- ProducesReponseType
- Produces
- Consumes
- Example
- IOperationFilter
- Custom Attribute




