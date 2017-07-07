---
layout: post
title: OAuth 2.0 vs SAML 2.0
comments: true /*disqus comments enabled for this post*/
description: Understanding about how OAuth and SAML works in a Single-Sign On Solution
keywords: oauth, saml, sso
---

"Log in with Facebook", "Log in with Google". I think these are the two buttons which really makes us happy whenever we see them on any application we newly install or web application we browse. The reason being, we don't have to go through the long process of creating an account for that application OR remembering the username/password for that particular application. So how does this "Log in with Google" thing works?
The short answer is they have implemented something called as Single-Sign On (SSO) solution. And in this blog post, I am writing about OAuth and SAML, the two specifications used in order to achieve single-sign on user experience. 

## SAML 2.0 Basics
Security Assertion Markup Language 2.0 is a version of SAML standard for exchanging authentication and authorization data between security domains. SAML 2.0 is an XML-based protocol that uses security based tokens containing assertions to pass information about the user between the web server you are trying to access information on and the service provider. In SAML 2.0 specification there are three main actors:

1. Service Provider (Resource Server): This is the web server you are trying to access information on.
2. Client: Your web browser
3. Identity Provider (Authorization Server): This is the server that owns the user credentials and identity. 

## SAML 2.0 Workflow

A simple SAML workflow inorder to understand the process better can be shown as below:
![saml_example](/public/saml_example.png)

The above example can be described in words as: 
1. First I click on "login with SSO". This is similar to clicking on login with Facebook on your web browser.
2. Then the application server which receives the login request generates the authentication request to be sent to the Authorization server.
3. Now the application server makes an HTTP Post request with an Authentication request to the authorization server.
4. This authentication request is then verified on the authorization server.
5. Now once verified, the authorization server redirects the user's browser session on its login page. 
6. This is where the user inserts his/her username/password for facebook (for example) on the login page. 
7. Now if the credentials for that user are verified on authorization server (for example Facebook side), then and only then the authorization server at Facebook will generate a SAML token.
8. The user is now redirected to the web application with the SAML Token.
9. Using this SAML token the application authenticates the user using Facebook credentials and still does not store user's username/password.


## Limitations about SAML 2.0 
There are certain cases where SAML specification does not work or to be specific I should say difficult to make it work. One case is for Thick Client or Native applications. 
Because in this case, Step 8, is difficult to achieve. In the above example Step 8 is achieved by using HTTP Redirect binding. This makes the user redirected back to the mentioned URL. However, this cannot be achieved when we are dealing with a native application installed on your machine or a mobile application installed on your phone. One harder way in order to get this working is to scrape the SAML token from the HTTP request coming from the authorization server using a proxy server in between. Once you pull out the SAML token you can make an HTTP request using this token in order to get access. 

## OAuth Basics
Unlike SAML 2.0, OAuth 2.0 is a protocol for authorization. It focuses on how to deliver authorization flows for web applications, desktop applications, mobile phones and other devices. In OAuth there are following main actors:
1. Service Provider (Resource Server): This is the web server you are trying to access information on.
2. Client: It can be the browser based web application, mobile application, desktop application or even a server-side application.
3. Identity Provider (Authorization Server): This is the server that owns the user identities and credentials. It's who the user actually authenticates and authorizes with.

## OAuth Workflow

A simple OAuth workflow in order to understand the process better can be shown as below:
![oauth_example](/public/oauth_example.png)
1. First I click on "login with Facebook" on Spotify mobile app. 
2. The Service Provider at Spotify gives me an authorization grant in order to login with Facebook.
3. Now, my mobile app will use this authorization grant in order to request an access token from the Identity Provider, in our example, Facebook.
4. Facebook checks whether the authorization grant is valid and grants the access token if valid. This access token is now used by the client (in our case Spotify mobile app)
5. Now, when Spotify (Service Provider) receives this access token, it might not directly let you access the app as logged in user. It will validate this access token again with Facebook. If Facebook finds this token valid, then and only then it will send back the user information to Spotify.
6. After successful validation of access token, Spotify logs in the user with his/her Facebook credentials without owning the user's username/password.

This is the most common OAuth flow. There are various other things about OAuth such as refresh tokens, where the client asks for refresh tokens to the Authorization server instead of again authenticating itself via the common OAuth flow, but I am keeping this post an introductory to Single-Sign On process. 

The difference between SAML 2.0 and OAuth 2.0 here is, OAuth does not assume that the client is a web browser.  And also in the OAuth flow, the token is sent in the HTTP redirects as the query parameter. Hence it is easy to absorb on the application side too. Other difference is SAML 2.0 has the identity information in the SAML token itself, while OAuth token does not have that. It again has to validate the token against the Identity provider which increases the request/response overhead but is more SECURE.

This is it for now on SAML & OAuth. Now that we are on this topic would just like to tell you there is something more called "OpenID Connect" similar to SAML & OAuth. I will leave you here to search about it.

References:

1. [The OAuth 2.0 Authorization Framework](https://tools.ietf.org/html/rfc6749#section-10)
2. [Security Assertion Markup Language (SAML) 2.0 Profile for OAuth 2.0 Client Authentication and Authorization Grants](https://tools.ietf.org/html/rfc7522)
3. [Choosing an SSO Strategy: SAML vs OAuth2](https://www.mutuallyhuman.com/blog/2013/05/09/choosing-an-sso-strategy-saml-vs-oauth2/)
4. [Dev Overview of SAML](https://developers.onelogin.com/saml)
