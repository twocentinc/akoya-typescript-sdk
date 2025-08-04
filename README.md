
# Getting Started with Akoya APIs v2.4.0

## Introduction

Akoya product APIs for data access. Default servers are set for the Akoya sandbox environment.

Akoya APIs include the following updates:

- v2.4.0
  - Added Tax product
- v2.3.0
  - Removed erroneous `accountId` query param from Taxlots endpoint
  - Added TaxLots endpoint
- v2.2.2
  - Added mode query parameter to Account Information, Balances, Investments, and Transactions to support standard mode.
  - Edited callouts for Account Holder endpoint
- v2.2.1
  - Fixed typo in `accountIds` query parameter for `/accounts-info`, `/balances`, `/accounts`
  - Added security method for `Account holder information` to bear token. Missing method defaulted to basic auth.
  - Added examples and descriptions to some schemas
  - Added HTTP status `429` FDX error `1207`.
- v2.2 Additions
  - Added optional `x-akoya-interaction-type` header to all endpoints to specify if a request is part of a batch process
  - Update of tags to organize endpoints by Akoya product
  - `206` response added to `/accounts-info`, `/balances`, `/accounts`
- v2.1 New Statements product and Customers product updated with additional endpoint, `Account holder information`.
- v2.0 Launch of Akoya products: Account Info, Balances, Investments, Transactions, Payments, Customers.

## Building

### Requirements

The SDK relies on **Node.js** and **npm** (to resolve dependencies). It also requires **Typescript version >=4.1**. You can download and install Node.js and [npm](https://www.npmjs.com/) from [the official Node.js website](https://nodejs.org/en/download/).

> **NOTE:** npm is installed by default when Node.js is installed.

### Verify Successful Installation

Run the following commands in the command prompt or shell of your choice to check if Node.js and npm are successfully installed:

* Node.js: `node --version`

* npm: `npm --version`

![Version Check](https://apidocs.io/illustration/typescript?workspaceFolder=Akoya&step=versionCheck)

### Install Dependencies

- To resolve all dependencies, go to the **SDK root directory** and run the following command with npm:

```bash
npm install
```

- This will install all dependencies in the **node_modules** folder.

![Resolve Dependencies](https://apidocs.io/illustration/typescript?workspaceFolder=Akoya&workspaceName=akoya&step=resolveDependency)

## Installation

The following section explains how to use the generated library in a new project.

### 1. Initialize the Node Project

- Open an IDE/text editor for JavaScript like Visual Studio Code. The basic workflow presented here is also applicable if you prefer using a different editor or IDE.

- Click on **File** and select **Open Folder**. Select an empty folder of your project, the folder will become visible in the sidebar on the left.

![Open Folder](https://apidocs.io/illustration/typescript?step=openProject)

- To initialize the Node project, click on **Terminal** and select **New Terminal**. Execute the following command in the terminal:

```bash
npm init --y
```

![Initialize the Node Project](https://apidocs.io/illustration/typescript?step=initializeProject)

### 2. Add Dependencies to the Client Library

- The created project manages its dependencies using its `package.json` file. In order to add a dependency on the *Akoya* client library, double click on the `package.json` file in the bar on the left and add the dependency to the package in it.

![Add Akoya Dependency](https://apidocs.io/illustration/typescript?workspaceFolder=Akoya&workspaceName=akoya&step=importDependency)

- To install the package in the project, run the following command in the terminal:

```bash
npm install
```

![Install Akoya Dependency](https://apidocs.io/illustration/typescript?step=installDependency)

## Initialize the API Client

**_Note:_** Documentation for the client can be found [here.](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/client.md)

The following parameters are configurable for the API Client:

| Parameter | Type | Description |
|  --- | --- | --- |
| environment | `Environment` | The API environment. <br> **Default: `Environment.Sandbox`** |
| timeout | `number` | Timeout for API calls.<br>*Default*: `0` |
| httpClientOptions | [`Partial<HttpClientOptions>`](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/http-client-options.md) | Stable configurable http client options. |
| unstableHttpClientOptions | `any` | Unstable configurable http client options. |
| logging | [`PartialLoggingOptions`](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/partial-logging-options.md) | Logging Configuration to enable logging |
| authorizationCodeAuthCredentials | [`AuthorizationCodeAuthCredentials`](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/auth/oauth-2-authorization-code-grant.md) | The credential object for authorizationCodeAuth |

The API client can be initialized as follows:

```ts
import { Client, Environment, LogLevel, OauthScope } from 'akoya';

const client = new Client({
  authorizationCodeAuthCredentials: {
    oauthClientId: 'OAuthClientId',
    oauthClientSecret: 'OAuthClientSecret',
    oauthRedirectUri: 'OAuthRedirectUri',
    oauthScopes: [
      OauthScope.Openid,
      OauthScope.Profile
    ]
  },
  timeout: 0,
  environment: Environment.Sandbox,
  logging: {
    logLevel: LogLevel.Info,
    logRequest: {
      logBody: true
    },
    logResponse: {
      logHeaders: true
    }
  },
});
```

## Environments

The SDK can be configured to use a different environment for making API calls. Available environments are:

### Fields

| Name | Description |
|  --- | --- |
| Sandbox | **Default** |
| Production | - |

## Authorization

This API uses the following authentication schemes.

* [`acgAuth (OAuth 2 Authorization Code Grant)`](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/auth/oauth-2-authorization-code-grant.md)

## List of APIs

* [Accountinformation](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/controllers/accountinformation.md)
* [Tax Beta](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/controllers/tax-beta.md)
* [Balances](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/controllers/balances.md)
* [Customers](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/controllers/customers.md)
* [Investments](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/controllers/investments.md)
* [Payments](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/controllers/payments.md)
* [Statements](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/controllers/statements.md)
* [Transactions](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/controllers/transactions.md)

## SDK Infrastructure

### Configuration

* [HttpClientOptions](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/http-client-options.md)
* [RetryConfiguration](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/retry-configuration.md)
* [ProxySettings](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/proxy-settings.md)
* [PartialLoggingOptions](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/partial-logging-options.md)
* [PartialRequestLoggingOptions](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/partial-request-logging-options.md)
* [PartialResponseLoggingOptions](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/partial-response-logging-options.md)
* [LoggerInterface](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/logger-interface.md)

### HTTP

* [HttpRequest](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/http-request.md)

### Utilities

* [ApiResponse](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/api-response.md)
* [ApiError](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/api-error.md)
* [CursorPagedResponse](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/cursor-paged-response.md)
* [LinkPagedResponse](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/link-paged-response.md)
* [OffsetPagedResponse](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/offset-paged-response.md)
* [NumberPagedResponse](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/number-paged-response.md)
* [PagedAsyncIterable](https://www.github.com/akoya-llc/akoya-typescript-sdk/tree/0.2.0/doc/paged-async-iterable.md)

