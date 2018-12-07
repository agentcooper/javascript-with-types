# Nominal vs structural

```typescript
interface Book {
  title: string;
  author: string;
}

function toString(book: Book) {
  return `${book.title} by ${book.author}`;
}

toString({
  title: "The Great Gatsby",
  author: "F. Scott Fitzgerald",
});
```

Following example will type check in both TypeScript and Flow as expected.

Now we change `Book` to be a class:

```typescript
declare class Book {
  title: string;
  author: string;
}

function toString(book: Book) {
  return `${book.title} by ${book.author}`;
}

toString({
  title: "The Great Gatsby",
  author: "F. Scott Fitzgerald",
});
```

The TypeScript will still type check, but Flow will show an error:

```
Cannot call `toString` with object literal bound to `book` because object literal [1] is incompatible with `Book` [2].
```

TypeScript uses structural typing for both objects and classes.

Flow uses nominal (by name) typing for classes and structural for objects.

- [Flow docs](https://flow.org/en/docs/lang/nominal-structural/)
- [TypeScript issue](https://github.com/Microsoft/TypeScript/issues/202)
