---
layout:     post
title:      2020-08-23-RESTful Developer Path CP05
subtitle:   Web Security: OAuth and OpenID Connect
date:       2020-08-23
author:     BY Elon
header-img: img/post-bg-map.jpg
catalog: true
tags:
    - Web Development
    - REST
    - API
---
## What is OAuth (2.0)?
It is a framework designed for AuthZ service(Authorization). It is extensible.

### OAuth VS SAML
SAML is defined in 2002-2003, mainly for Single Sign On(SSO) - AuthN on PC websites. It is not that perfect to compatible with current Mobile devices and RESTful API technologies. That is why OAuth comes out. 
- SAML is XML-based, so heavy payloads
- SAML is not designed for delegated access, login via Google, LinkedIn, Twitter or else.

### Approches to API AuthN + AuthZ
* API keys

* Accout Identifier + Secret

* OAuth
	- Easy to delegate selective access
	- Easy to revoke access
	- Common, well-supported in most tech stacks
	- Not easy to implement

### OAuth vs OpenID Connect
Because OAuth is just for AuthZ. To specify identity, we have OpenID Connect(OIDC) designed for AuthN. It is a simple extension on top of OAuth 2.0. It defines specific fields (content and structure) for sharing profile information, such as addr, phone number, email and other fields. This is done through an ID token. OIDC is not for AuthZ.

## OAuth Terms
- RFC 6749 - OAuth Core endpoints
	* /authorize
	The endpoint which the end user (resource owner) interacts with to grant permissions to the resource for the application.
	Could return an auth code or access token.
	* /token
	The endpoint which the application uses to trade an authorization code or refresh token for an access token

- RFC 7009 - Token Revocation
	* /revoke
	The endpoint which applications use to deactivate/invalidate a token.
- RFC 7662 - Token Introspection
	* /introspect
	The endpoint which apps use to learn more about a token whether it is active or not.

- RFC 7591 - Dynamic Client Registration
	* /register
	The endpoint which apps use to creat new OAuth clients(client_id and client_secret) for provisioning new apps or users.
- OpenID Connect Core
	* /userinfo
	The endpoint that apps uses to retrieve profile info about the authenticated user. It returns a pre-defined set of fields, depending on the permission(scope) requested.
- Working Draft: Server Discovery
	* /.well-known/openid-configuration
	Apps use to retrieve the config info of the ODIC server. 

### Access Token and Refresh Token

### [RFC7519 JWT (JSON Web Token)](www.jsonwebtoken.io)
- "iss" - the issuer of the token, an entity we trust
- "sub" - the subject(user) of the token
- "aud" - the audience or intended recipient of the token
- "exp" - the expiration time of the token

### Scope and Claims
Scope is a group of permissions that a user can grant to an application to take action on their behalf.
Claim is a key/value pair within the token that gives the client app info.

- Efforts to standardize Scopes and Claims
	* Healthcare - http://openid.net/wg/heart
	* FHIR - http://www.hl7.org/implement/standards/fhir
	* Financial API - http://openid.net/wg/fapi

## Dig Deeper on Grant Type
### Client Credentials: Authorization for microservices
It is designed specially for server-to-server interactions, similar to "server accounts" from Active Directory and other backend services.
No user involved(therefore not compatible with OIDC)

Concerns:
* Private clients only
* Must use secure communications
* Don't have a user for logging or audit purposes
* Validating our access token

### Implicit or Hybrid for Mobile Devices and SPA
Designed specifically for untrusted or "public" clients, where a malicous user could get access to the source code. This is only for users who explicitly grant authorization via an authentication and user-content flow.

Pros:
* For Android or iOS/Swift, use **AppAuth**
* For single page apps, use **Passport**
Concerns:
* Test your redirect_uri whitelist 

### Authorization Code for web applications
Use a well-established library instead of creating your own.
Concerns:
* Protect auth code
* Be careful of active browser sessions
* Test your redirect_uri whitelist
* Make sure all resources validate access tokens? How

### Resource Owner Password Flow for legacy applications
Not recommended.

### Server-Side Implementations
- [Configure an OAuth server in PHP](oauth2.thephpleague.com)
- Configure an OAuth Server in Node
- [OAuth 2.0 as a service using Okta](developer.okta.com)

### Other resources
- OAuth 2.0 Simplified Book
- [OAuth 2.0 Server](www.oauth.com)
- Map of OAuth 2.0 Specs