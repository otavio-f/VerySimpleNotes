# VerySimpleNotes
The same app in a number of frameworks

The main objective of this repository is to demonstrate the implementation of the "same app" in different languages, with different frameworks.

## Business Rules ##
The application must process the storage of **notes** that have some basic properties, but most importantly it's **title** and **content**. For other purposes, 
the **creation timestamp** and **last modification timestamp** must be stored too. The timestamps must be set automatically by the server, and can not be altered
by request. Other details must be ommitted from requests and responses. The essential fields are displayed in the table:

|Attribute|Json|Type|Change by|
|---|---|---|---|
|Title|"title"|Single line of text|Request|
|Content|"content"|Text|Request|
|Creation time|"created_at"/"createdAt"|Timestamp|Server, at creation|
|Last modified|"last_modified"/"lastModified"|Timestamp|Server, at modification|
***

## API ##
The common endpoint must be **api/v1/**. Api implements the CRUD operations, the details can be seen on the table below.

|Title|Endpoint|Method|Request body|On Success|On Fail|
|---|---|---|---|---|---|
|Fetch All|/api/v1/|GET| |200-Ok, response body has list with all notes|500-Internal Error|
|Fetch One|api/v1/{id}|GET| |200-Ok, response body has the note details|404-Not Found|
|Create|api/v1/|POST|note details|201-Created, Location header points to the new resource|400-Bad Request or 500-Internal Error|
|Update|api/v1/{id}|PUT or POST|note details|204-No Content|400-Bad Request or 404-Not Found or 500-Internal Error|
|Delete|api/v1/{id}|DELETE| |204-No Content|404-Not Found or 500-Internal Error|

Codes Meaning:
 - **200**: Everything is ok.
 - **201**: A resource has been created on the server. Look at the "Location" header on the response to get a relative url.
 - **204**: Modified a resource on the server, but there was nothing to send back.
 - **400**: Caused by sending a json with incomplete data, eg. missing a field on the business rules.
 - **404**: The request points to a resource id that doesn't exist on the server.
 - **500**: Generic error on the server.

[Html response codes reference](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status)
