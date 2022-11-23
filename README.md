# data-loader-firestore

data-loader-firestore is a utility to reduce requests to Firestore via memoisation.

## Usage

To add data-loaer-firestore to your project:

```bash
npm install --save data-loader-firestore
```

Get the document 'userId' from the users collection:

```ts
import { getFirestore } from "firebase-admin/firestore";
import { FirestoreDataLoader } from "data-loader-firestore";

const firestore = getFirestore();

const users = new FirestoreDataLoader(firestore, "users");
const user = await users.load("userId");
```

Get the document 'postId' from the posts collection of the user 'userId' in the users collection:

```ts
const userPosts = new FirestoreDataLoader(firestore, "users", "posts");
const post = await userPosts.load("userId", "postId");
```

Get all users with the role 'student':

```ts
const users = new FirestoreDataLoader(firestore, "users");
const students = await users.getQuery((usersCollection) =>
  usersCollection.where("role", "==", "student")
);
```

## Planned features

- [x] Data memoisation
- [x] Getting documents by ID
- [x] Getting documents by query
- [ ] Creating documents
- [ ] User-defined dataloader support
- [ ] Collection group support
- [ ] Clearing a memoised document
- [ ] Caching support

## Installation

If you'd like to contribute to this project, you can install the dependencies with:

```bash
npm install
npm install -g firebase-tools
firebase login
```

Set up your code editor to use the ESLint and Prettier on save.

## Testing

Tests are run automatically on pre-commit via Husky. You can also run them manually with:

```bash
firebase emulators:start --only firestore
npm run test
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](LICENSE)
