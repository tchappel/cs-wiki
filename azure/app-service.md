# Azure App Service

Service for hosting web applications, REST APIs, and mobile back ends adn azure functions.

## Features of Azure App Service

- Built-in **auto scale** support
- **Container support**
  - OS: Windows and Linux
  - Containers: Windows containers or Docker
  - Image Registries: Azure Container Registry or Docker Hub
  - orchestration: supports multi-container apps using Docker Compose on Linux and Windows containers
- out-of-the-box **Continuous integration/deployment**:
  - Azure DevOps Services, GitHub, Bitbucket, FTP, or a local Git repository
  - Containerized web apps: Azure Container Registry or Docker Hub.
- **Deployment slots**
  - deployment environments for staging, testing, production
  - live apps with their own host names
  - swap slots with zero-downtime
- **App Service on Linux**
  - lets you host web applications natively on Linux-based
  - supports both built-in runtime stacks
  - supports custom Linux containers (Web App for Containers)
- **App Service Environment**
  - fully isolated and dedicated environment for running App Service apps
  - improved security at high scale
  - compute is dedicated to a single customer

## App Service Plan

App Services run on an App Service Plan (it’s like a shared server environment for your apps.)

Apps in the same App Service plan all share the same compute resources

App Service plans defines:

- region (datacenter) of the physical server
- compute resources (CPU, memory, storage)
- Pricing tier (in the basic pricing tier your apps run on the same Azure VM as other App Service apps, including those of other customers)
- scaling options (according to the pricing tier)

## Deploy to App Service

- **automated deployment** (CD - continuous deployment):
  - Azure DevOps Services, GitHub, Bitbucket
- **manual deployment**:
  - Git
  - CLI: `az webapp up` command of Azure CLI.
  - Zip deploy: Use curl or a similar HTTP utility
  - FTP/S

### Continuously deploy containers

For custom containers from Azure Container Registry or other container registries, deploy the image into a staging slot and swap into production to prevent downtime. The automation is more complex than code deployment because you must push the image to a container registry and update the image tag on the webapp.

Build and tag the image: As part of the build pipeline, tag the image with the git commit ID, timestamp, or other identifiable information. It’s best not to use the default "latest" tag. Otherwise, it’s difficult to trace back what code is currently deployed, which makes debugging far more difficult.
Push the tagged image: Once the image is built and tagged, the pipeline pushes the image to our container registry. In the next step, the deployment slot will pull the tagged image from the container registry.
Update the deployment slot with the new image tag: When this property is updated, the site automatically restarts and pulls the new container image.

### Sidecar containers

In Azure App Service, you can add up to nine sidecar containers for each sidecar-enabled custom container app. Sidecar containers let you deploy extra services and features to your container application without making them tightly coupled to your main application container. For example, you can add monitoring, logging, configuration, and networking services as sidecar containers.

You can add a sidecar container through the Deployment Center in the app's management page.

## built-in authentication and authorization feature in App Service

Azure App Service provides a convenient and powerful built-in mechanism for authenticating users and authorizing access to web apps, RESTful APIs, mobile backends, and Azure Functions. This feature allows developers to integrate various identity providers with minimal to no code, saving time and effort by leveraging platform-level security. By handling the complexities of authentication and token management, App Service enables developers to focus on their core application logic.

Main Themes and Important Ideas:

1\. Convenience and Reduced Development Effort:

App Service offers "out-of-the-box authentication with federated identity providers, allowing you to focus on the rest of your application."
It eliminates the need to write custom authentication and authorization code or rely heavily on framework-specific security features.
The feature is built directly into the platform, requiring "minimal or no code" and no specific "language, SDK, security expertise, or code."

2\. Federated Identity and Multiple Provider Support:

App Service utilizes a federated identity model, where third-party identity providers manage user identities and the authentication flow.
It supports several default identity providers:

- Microsoft Entra ID (/.auth/login/aad)
- Facebook (/.auth/login/facebook)
- Google (/.auth/login/google)
- X (/.auth/login/x)
- GitHub (/.auth/login/github)
- Any OpenID Connect provider (/.auth/login/<providerName>)

Developers can offer users "any number of these sign-in options."

3\. Platform Middleware for Authentication and Authorization:

The authentication and authorization functionality is implemented as a platform middleware component that runs on the same VM (or a separate container for Linux and containers) as the application.
"When enabled, every incoming HTTP request passes through it before being handled by your application."
This middleware handles key tasks:
"Authenticates users and clients with the specified identity provider."
"Validates, stores, and refreshes OAuth tokens issued by the configured identity provider."
"Manages the authenticated session."
"Injects identity information into HTTP request headers."
Configuration is done through Azure Resource Manager settings or a configuration file, requiring no changes to application code or specific SDKs.

4\. Authentication Flow Variations:

The authentication flow differs based on whether a provider's SDK is used:
Without provider SDK (Server-directed/Server flow): The application delegates the sign-in process to App Service. This is common for browser-based applications where the user can be redirected to the provider's login page. The sign-in endpoint is /.auth/login/<provider>, and the callback is /.auth/login/<provider>/callback. "The server code manages the sign-in process..."
With provider SDK (Client-directed/Client flow): The application handles the user sign-in with the provider's SDK and then submits the authentication token to App Service for validation at the /.auth/login/<provider> endpoint. "The application code manages the sign-in process..." This is typical for "browser-less apps" like REST APIs, Azure Functions, JavaScript browser clients, and native mobile apps.

5\. Authorization Behavior Configuration:

The Azure portal allows configuration of how App Service handles unauthenticated requests:
Allow unauthenticated requests: Authorization is deferred to the application code. App Service still passes authentication information for authenticated requests. "This option provides more flexibility in handling anonymous requests. It lets you present multiple sign-in providers to your users."
Require authentication: Unauthenticated traffic is rejected. This can be a redirect to a configured provider's login page for browser clients (to /.auth/login/<provider>) or an HTTP 401 Unauthorized response for native mobile apps. It can also be configured to return HTTP 401 Unauthorized or HTTP 403 Forbidden for all requests.
Caution: Restricting access entirely might not be suitable for applications requiring a public-facing home page.

6\. Built-in Token Store:

App Service provides a "built-in token store," which automatically becomes available when authentication is enabled with any provider.
This store is a repository of tokens associated with application users. 7. Logging and Tracing:

Authentication and authorization traces are integrated into application logs if application logging is enabled.
This simplifies debugging authentication-related issues by providing a centralized location for relevant details. "If you see an authentication error that you didn't expect, you can conveniently find all the details by looking in your existing application logs."
Key Takeaways:

Azure App Service offers a significant advantage by providing built-in authentication and authorization, reducing the burden on developers.
Its support for multiple identity providers and flexible configuration options makes it adaptable to various application scenarios.
Understanding the different authentication flows (server-directed and client-directed) is crucial for implementing the feature correctly based on the application type.
Careful consideration of the authorization behavior configuration is necessary to ensure the desired level of access control while maintaining the required public accessibility.
The integrated token store and logging capabilities enhance the manageability and debuggability of application security.

built-in = minimal or no code
identity providers
App Service authentication flows:

- "server-directed flow"
- "client-directed flow"
  "Require authentication" setting
  token store in Azure App Service
  explore authentication errors
  built-in authentication module in Linux and containerized App Services cannot directly integrate with specific language frameworks
