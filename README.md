# brainCloud Library for Java

brainCloud is a ready-made back-end platform for the development of feature-rich games, apps and things. brainCloud provides the features you need – along with comprehensive tools to support your team during development, testing and user support.

brainCloud consists of:
- Cloud Service – an advanced, Software-as-a-Service (SaaS) back-end
- Client Libraries – local client libraries (SDKs)
- Design Portal – a portal that allows you to design and debug your apps
- brainCloud Architecture

![architecture](/Screenshots/bc-architecture.png?raw=true)

## What's the difference between the brainCloud Wrapper and the brainCloud Client?
The wrapper contains quality of life improvement around the brainCloud Client. It may contain device specific code, such as serializing the user's login id on an Android or iOS device.
It is recommended to use the wrapper by default.

![wrapper](/Screenshots/bc-wrapper.png?raw=true)

## How do I initialize brainCloud?
If using the wrapper use the following code.
```java
_bc = new BrainCloudWrapper(); // optionally pass in a _wrapperName
_bc.initialize(_appId, _secret, _appVersion); // optionally pass in an _applicationContext
```
On Android, to use the wrapper serialization features, you also need to pass in or set the application context.
```java
_bc.setContext(_applicationContext);
```
Your _appId, _secret, is set on the brainCloud dashboard.

![wrapper](/Screenshots/bc-ids.png?raw=true)

_wrapperName prefixes saved operations that the wrapper will make. Use a _wrapperName if you plan on having multiple instances of brainCloud running.

_appVersion is the current version of our app. Having an _appVersion less than your minimum app version on brainCloud will prevent the user from accessing the service until they update their app to the lastest version you have provided them.

![wrapper](/Screenshots/bc-minVersions.png?raw=true)

## How do I authenticate a user with brainCloud?
The simipliest form of authenticating with brainCloud Wrapper is an Anonymous Authentication.
```java
_bc.authenticateAnonymous();
```
This method will create an account, and contiune to use a locally saved anonymous id.
To login with a specfic anonymous id, use the brainCloud client.
```java
_bc.getClient().getAuthenticationService().setAnonymousId(_anonymousId); // re-use an Anon id
_bc.getClient().getAuthenticationService().setAnonymousId(_bc.getClient().getAuthenticationService().generateAnonymousId()); // or use brainCloud to generate one
_bc.getClient().GetAuthenticationService().AuthenticateAnonymous(_forceCreate, _callback);
```
Setting _forceCreate to false will ensure the user will only login to an existing account. Setting it to true, will allow the user to register a new account

## How do I attach an email to a user's brainCloud profile?
After having the user create an anonymous with brainCloud, they are probably going to want to attach an email or username, so there account can be access via another platform, or or when there local data is discarded.
Attaching email authenticate would look like this.
```java
_wrapper.getIdentityService().attachEmailIdentity(_email, _password, _callback);
```
There are many authentication types. You can also merge profiles and detach idenities. See the brainCloud documentation for more information:
http://getbraincloud.com/apidocs/apiref/?java#capi-auth
