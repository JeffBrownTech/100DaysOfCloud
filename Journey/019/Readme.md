![](./img/banner.png)

## Introduction

This is the last module in Matt Allford's Azure Functions for DevOps Engineers course over at CloudSkills. This topic focuses on how to develop and deploy Azure functions.

## Prerequisite

- Azure subscription
- Azure DevOps tenant/environment

## Use Case

- Develop Azure Functions locally on system
- Automate deployment of Azure Functions using Azure DevOps pipelines

## Try yourself

I won't show a lot of examples from this module, but I learned about command line tools such as the Az.Functions PowerShell module (part of the larger Azure PowerShell group of modules). You can view existing functions, create new functions, remove functions, restart functions, and configure function app settings.

Next is the Azure Functions Core Tools. This is a command line utility for generating Function files and structure to allow you to run functions on your local system. You can then publish the functions to Azure. This eliminates the need to use the browser environment while you write your code. You'll need to install an npm manager in order to install the core tools. You can then install the tools using the following command (this install version 3):

```
npm install -g azure-functions-core-tools@3
```

You can then use commands in the command line to create functions. To create a new functions project, run:

```
func init
```

And select the language for the project (.net, nodejs, python, powershell). This will then create the necessary files and folders for the project. From here, you create the first function using the *func new* command and select the type of trigger to create (like HTTP trigger). From here, you can open the folder in your favorite code editor to create the code. Once you have the code created, you can run an instance of the function on your local system using the *func start* command. This will then display a local URL to call the function.

Once the local function development has completed, you can push the function out to Azure. You'll need to log into your account from the command line using *Connect-AzAccount*. Create a new function app using the *New-AzFunctionApp*. Before publishing the local function to Azure, understand that publishing the local project into the function app in Azure will stop and delete any existing functions. When you publish this, no relationship is created between the local project and the Azure function app.

To publish the local function, run the following core tools command, specifying the name of the Azure function:

```
func azure functionapp publish <az function name>
```

If you use VS Code, you can use an extension named "Azure Functions" that uses the core tools to create and publish functions directly from VS Code. This adds a new icon on the left rail for managing Azure functions. You can convert existing local functions to work best with VS Code. You can start the function inside VS Code and get the same local URL for testing the function. You can also deploy the function to Azure from within VS Code. Lots of great integrated functionality and a better development environment that the browser. One thing to note is the function code in Azure won't be editable since it was deployed as a package file. The idea is to go back to the environment where the function was developed and use it instead.

Azure Functions also have deployment slots. This allows for testing new code in a different instance with their own endpoints. You can create a "dev" slot for testing new code, then "swap" that slot with production to make it the new production code.

Finally, the course completes with walking through how to use ARM templates to create Azure Function resources, then pull the function code from an Azure DevOps repo.

## Next Steps

I have an Azure Functions project that I want to deploy using the knowledge from this course. I'll document the solution when it is completed.

## Social Proof

[Twitter](link)
[LinkedIn](link)
