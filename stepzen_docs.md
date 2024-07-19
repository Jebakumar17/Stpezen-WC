# StepZen Docs

**Last Updated:** 2023-06-29

## Consuming GraphQL APIs

Learn how to consume GraphQL APIs using StepZen, using tools such as `stepzen request` and the Explorer in the StepZen Dashboard.

## Building GraphQL APIs

Learn how to build GraphQL APIs using StepZen for all your data sources using GraphQL Schema Definition Language (SDL). StepZen supports the root operation types: Query, Mutation, and Subscription.

There are two ways to create your GraphQL API in StepZen:

1. Specify the data source you want to GraphQL-ize on the command line (`stepzen import ...`) and let StepZen generate the schema for you, or
2. Write your schema using GraphQL directives (`@rest`, `@dbquery`, `@graphql`) - powerful declarative constructs that provide a simpler, more efficient way to build GraphQL.

The code you generate using a `stepzen import` command writes the schema including the `@rest`, `@dbquery`, and `@graphql` directives for you. Whether you build a graph or federate graphs, StepZen's declarative approach lets you create concise APIs with built-in performance, cost, and reliability optimizations.

# How to . . . Docs section

## Convert Each Backend into a Graph

There are two ways to create your GraphQL API:

1. **Generate your Schema using `stepzen import` CLI** (Quickstart):
   The quickest way to get started. Using the `stepzen import` CLI, you specify an existing backend data source - StepZen introspects the endpoint and auto-generates a GraphQL schema for you.

2. **Write Schema Code using Declarative Constructs** (Write GraphQL Schemas):
   Write your schema code in a GraphQL Schema Definition Language (SDL) file. Use GraphQL directives (`@rest`, `@dbquery`, `@graphql`) to connect and configure backends, and link types using `@materializer`. Design a schema with interfaces to enable access to multiple backends. With a few lines of declarative code, you have a working schema.

## Secure your Schema and Endpoint

Use Admin Keys, API Keys, JWTs, and Field Policies to secure access to your schemas, endpoints, and backends.

## GraphQL Federation

Combine subgraphs into a supergraph. Build subgraphs in StepZen or other tools, and federate them in StepZen. Easily enable subgraphs for Apollo Federation.

## Troubleshooting & Testing

Learn to troubleshoot, test, and measure the performance of your GraphQL API.

## Reference Docs section

- **CLI Reference** (StepZen CLI Reference):
  The StepZen CLI is the primary tool for creating, uploading, deploying, and testing your StepZen API. It is available via npm: `npm install -g stepzen`.

- **GraphQL Directives Reference**:
  A schema defines your GraphQL APIs and incorporates annotations called directives to control how your schema is executed. GraphQL directives (`@rest`, `@dbquery`, `@graphql`, `@materializer`, `@sequence`, etc.) allow you to code your data connections, sequence queries, stitch schemas, and more - declaratively in StepZen.

- **Connect Frontends**:
  How to connect StepZen to frontends like Postman, JavaScript, and Node.js.

- **Features Reference**:
  Learn how to encode Form Data into a request or on an HTTP POST method. Explore built-in GraphQL Scalar Types and custom StepZen Scalar Types. Learn how to use mock data to test your queries and schemas and how to create sequences of queries.

# Install and Set up StepZen

**Last Updated:** 2023-06-29

Learn how to sign up for a StepZen account, install the CLI, and use your keys.

## Install StepZen

### Install StepZen CLI

The StepZen command-line interface (CLI) provides commands to set up and manage StepZen.

To install the StepZen CLI, use npm:

```bash
npm install -g stepzen

Here is the content converted into Markdown format:

```markdown
# Install and Set up StepZen

**Last Updated:** 2023-06-29

Learn how to sign up for a StepZen account, install the CLI, and use your keys.

## Install StepZen

### Install StepZen CLI

The StepZen command-line interface (CLI) provides commands to set up and manage StepZen.

To install the StepZen CLI, use npm:

```bash
npm install -g stepzen
```

Note: The StepZen CLI is supported on Windows, OSX, and Linux. If you encounter EACCES errors when installing globally, consult npm's official documentation.

## Create an account

1. **Sign up for a free StepZen account**.
2. Your account provides you with:
   - Admin Key: Required for uploading, modifying, configuring, and deploying StepZen APIs.
   - API Key: Grants access to consume/query your StepZen GraphQL API.

## Running StepZen

### Cloud

To run StepZen in the cloud, connect the CLI to your account to get a private and secure endpoint or use StepZen with a public account.

After installing the CLI, log in with:

```bash
stepzen login <your_domain>.ibm.steprz.net
```

Replace `<your_domain>` with your server domain (e.g., us-east-a).

Follow the prompts to enter your StepZen account name and admin key.

### Local development using Docker

For local development, run StepZen using Docker. This allows you to create a GraphQL API without signing up for an account or uploading data to StepZen's cloud.

Proceed to build your GraphQL API by:
- Specifying a backend on the command line for StepZen to introspect and generate a GraphQL schema.
- Using the Getting Started Wizard or the `stepzen import` CLI for quick setup.
- Writing GraphQL schemas using directives like `@rest`, `@dbquery`, and `@graphql`.

For more details, refer to the [Write GraphQL Schemas](#) documentation.
```

Save this content in a Markdown file (e.g., `stepzen_installation.md`) to preserve the formatting and structure. Adjust the placeholders like `<your_domain>` with actual values as needed.

Here's the provided content converted into Markdown format:

```markdown
# Getting Started by Transforming REST to GraphQL

**Last Updated:** 2023-06-29

Create a GraphQL API for backends with REST interfaces in seconds; deploy instantly in the cloud.

There are two ways to create your GraphQL API with StepZen when you have a REST backend:

1. Use the command-line interface (CLI) command `stepzen import curl` to specify an existing REST endpoint - StepZen introspects the endpoint and auto-generates a GraphQL schema for you.
2. Write your schema code in a `.graphql` GraphQL Schema Definition Language (SDL) file. Use the powerful GraphQL directive `@rest` to connect the REST endpoint, and with just a few lines of code, you have a working schema. See [How to Connect a REST Service](#) for how to write your GraphQL schema using `@rest`.

## Before you begin

Install and set up your StepZen account and the CLI.

## Use `stepzen import curl`

In this section, we use `stepzen import curl` on an existing REST API. This command sends a curl request to StepZen and parses the GraphQL types from the JSON response.

### GET requests

Auto-generate your schemas and resolvers using the following StepZen CLI command:

```bash
stepzen import curl https://introspection.apis.stepzen.com/customers --query-name "customers" --query-type "Customer" --name "customers"
```

Run `stepzen start` to upload and deploy your introspected schema.

### What `stepzen import curl` does

- StepZen issues the curl call and converts the returned JSON into a set of GraphQL types.
- The root of the returned JSON is given a special name (`CustomerEntry` in this example) based on the `query-type` flag.
- It generates a query with the value of the `--query-name` flag for executing the query.
- Stores the generated schema in a directory named in the `--name` flag.

### curl with headers

StepZen stores all headers in a `config.yaml` file. For example:

```bash
stepzen import curl https://api.foo.com/bar -H 'Authorization: Bearer 347ack988dkey'
```

Creates a `config.yaml`:

```yaml
configurationset:
  - configuration:
      name: some-auto-generated-name
      Authorization: Bearer 347ack988dkey
```

### curl with query parameters

StepZen automatically converts curl query parameters to GraphQL arguments:

```bash
stepzen import curl https://api.foo.com/bar?name=anant&country=US
```

Generates a GraphQL query:

```graphql
type Query {
  myQuery(name: String!, country: String!): RootEntry
    @rest(endpoint: "https://api.foo.com/bar")
}
```

### curl with path parameters

StepZen converts path parameters into GraphQL arguments:

```bash
stepzen import curl https://example.com/users/jane/posts/12 --path-params '/users/$userId/posts/$postId'
```

Generates a GraphQL query:

```graphql
type Query {
  myQuery(userId: String!, postId: Int!): RootEntry
    @rest(endpoint: "https://example.com/users/$userId/posts/$postId")
}

### Customizing the autogenerated schema

The `@rest` directive generated from `stepzen import curl` can be customized with transforms, filters, setters, and `resultroot` to change field names.

### POST requests

For POST requests, parameter substitution is applied to the body:

```bash
stepzen import curl 'http://dummy.restapiexample.com/api/v1/create' -d '{"key1":"value1", "key2":"value2"}' -H 'Content-Type: application/json'
```

Generates a GraphQL mutation:

```graphql
type Mutation {
  myQuery(key1: String, key2: String): RootEntry
    @rest(
      method: POST
      endpoint: "http://dummy.restapiexample.com/api/v1/create"
    )
}
```

### Best practices

- Use `--query-name`, `--query-type`, `--prefix`, and `--name` flags to manage imported curl requests effectively.
- Delete generated directories and edit `index.graphql` to undo mistakes.

## Learn More

Congratulations! You've created a GraphQL API based on a REST API that includes queries, parameters, and mutations.

To extend your schema or start from scratch to write your schema code yourself, you can use the GraphQL declarative construct `@rest`. See [How to Connect a REST Service](#) for more details.
```

This Markdown structure maintains the hierarchy and details provided in the original content. Adjust the placeholders like `[How to Connect a REST Service](#)` with actual links or placeholders as per your needs.

# GraphQL Basics

**Last Updated:** 2023-06-29

Learn the basics of GraphQL by exploring how to connect to and query a simple GraphQL API.

GraphQL is a query language for APIs that offers some major benefits over alternatives such as:

- **Ask for and receive only what you need:** A GraphQL query specifies only the data you need, and the result returned by the query will only include the data requested.
- **Predictable results:** Results from a GraphQL query are returned in the same structure as the request, enabling you to quickly predict and code for those results.
- **Get multiple resources in a single request:** GraphQL APIs have a single endpoint for all their data, and multiple resources can be requested via a single GraphQL query.

You can learn more about the benefits of GraphQL at [GraphQL.org](https://graphql.org).

StepZen provides all the advantages of GraphQL for your applications without needing to build and maintain your own GraphQL server. In this section, we'll explore how to use GraphQL to consume a StepZen API in your application.

## Connect to an API

A GraphQL API has a single endpoint for all its data. Some GraphQL APIs are public and open, allowing you to query them directly. For example, the Rick and Morty API is available at [https://rickandmortyapi.com/graphql](https://rickandmortyapi.com/graphql).

Many GraphQL APIs, particularly public ones, include a built-in query editor. For example, the Rick and Morty API provides a GraphQL Playground editor:

```plaintext
https://rickandmortyapi.com/graphql

Here's the provided content converted into Markdown format:

```markdown
# GraphQL Basics

**Last Updated:** 2023-06-29

Learn the basics of GraphQL by exploring how to connect to and query a simple GraphQL API.

GraphQL is a query language for APIs that offers some major benefits over alternatives such as:

- **Ask for and receive only what you need:** A GraphQL query specifies only the data you need, and the result returned by the query will only include the data requested.
- **Predictable results:** Results from a GraphQL query are returned in the same structure as the request, enabling you to quickly predict and code for those results.
- **Get multiple resources in a single request:** GraphQL APIs have a single endpoint for all their data, and multiple resources can be requested via a single GraphQL query.

You can learn more about the benefits of GraphQL at [GraphQL.org](https://graphql.org).

StepZen provides all the advantages of GraphQL for your applications without needing to build and maintain your own GraphQL server. In this section, we'll explore how to use GraphQL to consume a StepZen API in your application.

## Connect to an API

A GraphQL API has a single endpoint for all its data. Some GraphQL APIs are public and open, allowing you to query them directly. For example, the Rick and Morty API is available at [https://rickandmortyapi.com/graphql](https://rickandmortyapi.com/graphql).

Many GraphQL APIs, particularly public ones, include a built-in query editor. For example, the Rick and Morty API provides a GraphQL Playground editor:

```plaintext
https://rickandmortyapi.com/graphql
```

### Query the API Directly

To query a GraphQL API directly, you can use tools like GraphQL Playground or write queries programmatically in your application.

### Query the API with curl

You can also use curl commands to interact with GraphQL APIs. For example, to query the Rick and Morty API with curl:

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  --data '{ "query": "{ characters { results { name } } }" }' \
  https://rickandmortyapi.com/graphql
```

### Query the API with Postman

Postman provides a user-friendly interface for testing and querying GraphQL APIs. You can import your GraphQL schema or manually configure requests to interact with your API.

---

This Markdown structure captures the essential information from your provided content. Adjust the URLs, examples, or details as per your specific requirements or additional content.