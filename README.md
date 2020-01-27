# trello-client

This project is a **partial** implementation of the [Trello REST API](https://developers.trello.com/reference).
Endpoints will be added as they are needed for projects.

<!-- toc-head -->
<!-- toc-tail -->

## Current functionality

```bash
npm install @openlab/trello-client
```

```ts
import { TrelloClient, labelColors } from '@openlab/trello-client'

// Load in environment variables
const { TRELLO_APP_KEY, TRELLO_TOKEN, BOARD_ID } = process.env

//
// Create a client instance
//
const trello = new TrelloClient(TRELLO_APP_KEY, TRELLO_TOKEN)

//
// Fetch the organizations for the current user
//
const orgs = await trello.fetchOrganizations()

//
// Fetch boards for the current user
//
const boards = await trello.fetchBoards()

//
// Fetch the labels from a board
//
const labels = await trello.fetchLabels(BOARD_ID)

//
// Fetch the lists on a board
//
const lists = await trello.fetchLists(BOARD_ID)

//
// Create a new label
//
const newLabel = await trello.createLabel(BOARD_ID, {
  name: 'To-do',
  color: 'sky'
})

//
// Create a new card
// See types.ts – CardRequest for more parameters
//
const newCard = await trello.createCard({
  name: 'Document project',
  desc: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
  idList: 'some-list-mongo-id'
})
```

There are also types and interfaces exported from [types.ts](./src/types.ts)

## Future work

- Add more endpoints
- Add more complex types to capture `?fields` query parameters which have varadic responses

## Development

### Setup

To develop on this repo you will need to have [node.js](https://nodejs.org)
installed on your dev machine and have an understanding of it.
This guide assumes you have the repo checked out and are on macOS, but equivalent commands are available.

You'll only need to follow this setup once for your dev machine.

```bash
# Install npm dependencies
npm install
```

### Regular use

These are the commands you'll regularly run to develop the API, in no particular order.

```bash
# Run tests and re-run on changes
# -> Exit with control+C
npm run test -- --watch
```

### Irregular use

These are commands you might need to run but probably won't, also in no particular order.

```bash
# Test-run the preversion hook
# -> Runs automated tests
# -> Compiles typescript to javascript
npm run preversion

# Compiles typescript to javascript
npm run build

# Generate the table of contents in this readme
npm run generate-toc
```

### Testing

This repo uses [unit tests](https://en.wikipedia.org/wiki/Unit_testing)
to ensure that everything is working correctly, guide development, avoid bad code and reduce defects.
The [Jest](https://www.npmjs.com/package/jest) package is used to run unit tests.
Tests are any file in `src/` that end with `.spec.ts`, by convention they are inline with the source code,
in a parallel folder called `__tests__`.

```bash
# Run the tests
npm test -s

# Generate code coverage
npm run coverage -s
```

### Code formatting

This repo uses [Prettier](https://prettier.io/) to automatically format code to a consistent standard.
It works using the [yorkie](https://www.npmjs.com/package/yorkie)
and [lint-staged](https://www.npmjs.com/package/lint-staged) packages to
automatically format code whenever it is commited.
This means that code that is pushed to the repo is always formatted to a consistent standard.

You can manually run the formatter with `npm run prettier` if you want.

Prettier is slightly configured in [package.json](/package.json)
and will ignore files defined in [.prettierignore](/.prettierignore).

### Publishing

This repo is responsible for the `@openlab/trello-client` NPM package.

```bash
# Create a new version of the project
# -> Picks a new version based on the commits since the last version
# -> Following https://www.conventionalcommits.org/en/v1.0.0/
# -> Generates the CHANGELOG.md based on those commits
npm run release

# Publish the npm package
npm publish
```

---

> The code on https://github.com/unplatform/trello-client is a mirror of https://openlab.ncl.ac.uk/gitlab/catalyst/trello-client
