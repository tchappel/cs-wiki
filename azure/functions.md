# Azure Functions

Explain functional differences between Azure Functions, Azure Logic Apps, and WebJobs
Describe Azure Functions hosting plan options
Describe how Azure Functions scale to meet business needs

**Azure Functions** are serverless compute platform provided as a Platform as a Service (PaaS) offering, enabling event-driven, compute-on-demand systems.

## Azure Function App

The fundamental unit for organizing and managing Azure Functions is the **Function App** [1, 3]. A Function App acts as a **container for one or more individual functions**, grouping them into a logical unit for easier deployment, management, and sharing of resources, settings, and connections [1, 3]. A Function App also requires linking to/creating a **Storage Account** for its operation, such as storing function code and logs [2].

This is where you set runtime stack, version, region, that will be shared by all functions in the function app.

## Azure Functions

- Individual **Azure Functions** are the pieces of code that execute server-side logic. Each function is triggered by exactly one **trigger**. Common trigger types include **HTTP triggers** for responding to web requests, **Timer triggers** for scheduled execution, and triggers based on events from Azure services like **Storage (Blob, Queue, Cosmos DB, SQL)**, **Event Hubs**, and **Event Grid**.
- Functions can optionally use **bindings** to simplify connecting to other Azure resources for input and output data. **Input bindings** allow a function to read data from another service, while **output bindings** enable writing data to a destination.
- **Function Apps scale dynamically** by adding more instances based on the number of events that trigger the functions within them [1, 13]. All functions within a Function App share the resources of the app instance and scale together [1].

- Several features enhance the functionality and management of Azure Functions:
  - **API Management (APIM)** provides security and routing for HTTP-triggered functions, enabling them to be exposed as REST APIs [15].
  - **Azure Application Insights** offers built-in integration for monitoring function execution [5].
  - **Deployment slots** allow running different instances (slots) of a function app, providing a safe environment for testing new versions before swapping them into production [15].

**Azure Functions Core Tools** to run functions locally during development [15].

- Azure Functions follows an **event-based architecture**, where functions are designed to be small and focused, processing incoming data and potentially raising new events [18]. This makes them suitable for various scenarios like sending emails, processing data, task scheduling, and building serverless workflows using Durable Functions or Logic Apps [18].

## Develop Functions locally

A Functions project directory contains the following files in the project root folder, regardless of language:

host.json
local.settings.json

app settings
