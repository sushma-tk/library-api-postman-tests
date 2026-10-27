# Library API – Postman Tests

Postman collection that tests a Library REST API end to end.

## What's in it

- **3 requests** covering a full lifecycle: POST AddBook → GET GetBook → DELETE DeleteBook
- **17 assertions** (`pm.test`): status codes, response messages, headers, response time and JSON schema
- **Request chaining:** the new book ID is saved to an environment variable and used by GET and DELETE
- **Dynamic test data:** a pre-request script generates a unique ISBN on every run
- **Business-rule check:** confirms the API builds the book ID as ISBN + aisle
- **Multiple environments:** `{{BASE_URL}}` lets the same collection run against QA and UAT

## Files

- `Library.postman_collection.json` – the test collection
- `QA.postman_environment.json` – QA environment
- `UAT.postman_environment.json` – UAT environment

## Setup

1. Import the collection and both environment files into Postman.
2. Add a global variable named `companyCode` (any short prefix, e.g. `RS`). The AddBook pre-request script uses it to generate a unique ISBN.
3. Select the QA or UAT environment and run the collection.

## Run with Newman

Install Newman:

```
npm install -g newman
```

Run on QA:

```
newman run Library.postman_collection.json -e QA.postman_environment.json --global-var "companyCode=RS"
```

Run on UAT:

```
newman run Library.postman_collection.json -e UAT.postman_environment.json --global-var "companyCode=RS"
```

Run 3 iterations:

```
newman run Library.postman_collection.json -e QA.postman_environment.json --global-var "companyCode=RS" -n 3
```

Generate an HTML report:

```
npm install -g newman-reporter-htmlextra
```
```
newman run Library.postman_collection.json -e QA.postman_environment.json --global-var "companyCode=RS" -r htmlextra
```

The HTML report is saved in the `newman/` folder
