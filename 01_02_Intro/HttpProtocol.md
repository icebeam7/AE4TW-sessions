# Understanding HTTP Protocol with curl (Status Codes & Response Headers)

## Objectives

- Send HTTP requests using `curl`
- Interpret HTTP status codes
- Analyze response headers
- Understand the difference between request and response
- Identify common error responses (400, 404, 500)

---

## Requirements

- Terminal (Linux, macOS, or Windows with Git Bash / WSL)
- `curl` installed  

1. Verify installation:

```bash
curl --version
```

2. If `curl` is not installed, follow [these steps](https://developers.greenwayhealth.com/developer-platform/docs/installing-curl).

## Part 1 - Your First GET Request

3. We'll use a public test API. Enter the following command in the Terminal

```bash
curl https://jsonplaceholder.typicode.com/posts/1
```

<img width="1616" height="504" alt="image" src="https://github.com/user-attachments/assets/87ed5218-9659-44c2-a0b2-03dd4308c5fb" />


What just happened?

* Default method: `GET`
* Resource URL requested
* Server returned JSON data

## Task 1. Questions:

A. What type of content did the server return?

B. Where do you see the resource ID?

C. Can you see the HTTP status code?

> Note: By default, `curl` does not show response headers.

## Part 2 - Viewing Response Headers

4. Run:

```bash
curl -i https://jsonplaceholder.typicode.com/posts/1
```

The -i flag shows headers + body.

<img width="1616" height="1636" alt="image" src="https://github.com/user-attachments/assets/8e1ae891-4a06-47fa-bb65-9b3cac80a16c" />


## Analyzing the Response

5. Find the following elements in the response: Status line, Content-Type, Content-Length, Connection

a) Status line (example: `HTTP/1.1 200 OK`)

It includes:

* Protocol version
* Status code
* Status message

## Task 2. Questions:

D. What does 200 mean?

E. What category of status code is it?

F. What other codes do you know?

b) Important headers:

* Content-Type: Indicates the type of content returned. Example: `Content-Type: application/json`
* Content-Length: Indicates the size of the response body in bytes.
* Connection: Common values are `keep-alive` and `close`

## Task 3. Questions:

G. What would happen if Content-Type were `text/html` instead?

H. Does the content-length match the actual size of the body?

I. Why is Connection important in high-traffic systems?

## Part 3 - Simulating HTTP Errors

6. Enter the following command in the Terminal

```
curl -i https://jsonplaceholder.typicode.com/posts/999999
```

`404` status code represents a non-existing resource

<img width="1760" height="1328" alt="image" src="https://github.com/user-attachments/assets/9ee598c1-6bdc-4367-bdc7-bb7bfcda74b6" />

## Task 4. Questions

J. What status code did you receive?

K. Is there a response body?

L. How does it differ from the successful case?

## Part 4 - Sending data with POST request

7. Enter the following command in the Terminal

```
curl -i -X POST https://jsonplaceholder.typicode.com/posts \
-H "Content-Type: application/json" \
-d '{"title":"HTTP Lab","body":"Testing POST","userId":1}'
```

<img width="1760" height="1668" alt="image" src="https://github.com/user-attachments/assets/156b5efd-cc98-4831-bb3b-c07d12d63a93" />

## Task 5. Questions

M. What status code did the server return?

N. What does it mean?

O. What headers appear in this response?

## Part 5 - Sending Custom Headers

8. Enter the following command in the Terminal

```
curl -i https://jsonplaceholder.typicode.com/posts/1 \
-H "Authorization: Bearer TEST_TOKEN"
```

<img width="1760" height="1668" alt="image" src="https://github.com/user-attachments/assets/faa30cb5-f63e-4ef1-946d-8d613c37e80f" />

## Task 6. Questions

P. Does this API actually validate the token?

Q. What status code would a real secure API return if the token were invalid?

R. What is the difference between `401` and `403`?

## Part 6 - Headers Only (No Body)

9. Enter the following command in the Terminal

```
curl -I https://jsonplaceholder.typicode.com/posts/1
```

The `-I` flag retrieves headers only.

<img width="1760" height="1272" alt="image" src="https://github.com/user-attachments/assets/21d21181-9a3d-4394-bba9-c628d6141566" />


## Task 7. Questions

S. When would this be useful?

T. Why might monitoring systems use this approach?

## Part 7 - Status Code Classification

U. Complete the following table:

| Code    | Category | Meaning |
| -------- | ------- | ------- |
| 200  | Success    | OK. The action requested by the client was received, understood, and accepted |
| 201 | ?     | ?     |
| 400 | ?     | ?     |
| 401 | ?     | ?     |
| 403 | ?     | ?     |
| 404 | ?     | ?     |
| 500 | ?     | ?     |

## Part 8 - Discussion

V. Why is it bad practice to always return `200`, even on errors?
