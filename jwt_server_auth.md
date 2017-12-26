[JSON Web Tokens](http://jwt.io) are replacing cookies for authentication purposes pretty significantly. In this blog post I am going to show you how you can implement JWT in your api. I am going node express in this example.

<hr>

## What is a JSON Web token

Formal is definition in official site. _JSON Web Tokens are an open, industry standard RFC 7519 method for representing claims securely between two parties._ So:-

1. JWT is based on [RFC 7519](https://tools.ietf.org/html/rfc7519) Industry standard.
2. Used to securely communicate JSON objects.
3. They are self contained mean they all information use to decrypt the token is in the token itself except the secret obviously.
4. JWT consists of a header, payload and signature. These three parts are connect by **_._**

<hr>

## A JWT looks like this

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNDkyNjg1MDUwLCJleHAiOjE0OTUyNzcwNTB9.bHMstzcHfZQBND3QrugO4v3kTa7Zy7yifuuhWJbwhI0
```

You may see here three parts separated by _**.**_ The information we wanna store sits in the second part.

<hr>

## Lets Code a Login API using JWT

<script src="https://gist.github.com/pantharshit00/444626d3f627e1cfcc1691d90c5bcc67.js"></script>

<hr>

## Result(Using postman to test APIs)

<hr>

## Trying to access protected api without authorization token

Got unauthorized error
![ss1](/content/images/2017/08/dca4db87cdbd634ee7ffdac6b3bae76b.jpg)

<hr>

## Logging in with right credentials

Got the token back in the response
![ss2](/content/images/2017/08/9d9455fb1bb9947e780be9640f6d320a.jpg)

<hr>

## Accessing protected route with authorization token

Successfully entered the api
![f99365a296a3435e358fd35c2cadb252](/content/images/2017/08/f99365a296a3435e358fd35c2cadb252.jpg)
