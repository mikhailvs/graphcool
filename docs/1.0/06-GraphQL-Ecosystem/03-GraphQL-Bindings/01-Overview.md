---
alias: quaidah9ph
description: GraphQL Bindings
---

# Overview

🔗 [`graphql-binding`](https://github.com/graphcool/graphql-binding/) is a package that simplifie the process of creating your own GraphQL bindings.

GraphQL bindings effectively proxy your GraphQL schema, and make it accessible to you as methods on your newly created binding object. Read the full blog post introducing the idea of GraphQL bindings [here](https://medium.com/@graphcool/reusing-composing-graphql-apis-with-graphql-bindings-80a4aa37cff5).

## Install

```sh
yarn add graphql-binding
```

## Example

```js
const { makeExecutableSchema } = require('graphql-tools')
const { Binding } = require('graphql-binding')

const users = [
  {
    name: 'Alice',
  },
  {
    name: 'Bob',
  },
]

const typeDefs = `
  type Query {
    findUser(name: String!): User
  }
  type User {
    name: String!
  }
`

const resolvers = {
  Query: {
    findUser: (parent, { name }) => users.find(u => u.name === name),
  },
}

const schema = makeExecutableSchema({ typeDefs, resolvers })

const findUserBinding = new Binding({
  schema,
})

findUserBinding.findUser({ name: 'Bob' })
  .then(result => console.log(result))
```

More examples:

- [`graphql-binding-github`](https://github.com/graphcool/graphql-binding-github)
- [`graphcool-binding`](https://github.com/graphcool/graphcool-binding)