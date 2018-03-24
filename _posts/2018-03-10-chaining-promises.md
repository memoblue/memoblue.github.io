---
layout: post
title:  "Chaining Promises"
date:   2018-03-10 09:12:15 -08:00
tags: ['Coding','JavaScript']
---

A simple example of how to chain promises in JavaScript.

```js
const booksMockData = [
  { bookId: 1, authorId: 1, title: 'The Adventures of Sherlock Holmes' },
  { bookId: 2, authorId: 1, title: 'The Sign of the Four' },
  { bookId: 3, authorId: 2, title: 'The Jungle Book' },
];

const authorsMockData = [
  { authorId: 1, name: 'Conan Doyle', bio: 'Best writer ever!' },
  { authorId: 2, name: 'Rudyard Kipling', bio: 'Second best writer ever…' },
];

let list;

function getBooksByAuthorId(id) {
  return new Promise((resolve, reject) => {
    const booksByAuthor = booksMockData.filter(book => book.authorId === id);
    if (booksByAuthor.length >= 1) {
      resolve(booksByAuthor);
    } else {
      reject(Error(`No book by author id ${id}`));
    }
  });
}

function getAuthorId(name) {
  return new Promise((resolve, reject) => {
    const author = authorsMockData.find(a => a.name === name);
    if (author) {
      resolve(author.authorId);
    } else {
      reject(Error(`ID for author ${name} could not be found`));
    }
  });
}

function listBooksBy(name) {
  getAuthorId(name)
    .then(data => getBooksByAuthorId(data))
    .then((data) => {
      list = data.map(book => book.title);
    })
    .catch((err) => {
      console.log(`Could not get books by ${name}`);
    });
}

listBooksBy('Conan Doyle');
setTimeout(() => {
  console.log(list); // [("The adventures of Sherlock Holmes", "The Sign of Four")];
}, 200);
```
