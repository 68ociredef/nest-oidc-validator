# Nest oidc validator

OIDC Token validator for Nestjs.


## Getting started

Install Nest oidc validator

```
npm install nest-oidc-validator
```




## Usage

In authModule 

```ts
import {NestOidcModule} from 'nest-oidc-validator';
```

```ts
@Module(
  imports: [
    NestOidcModule.forRoot(
      issuer: 'http://.......',  //issuer url
      jwksUri: 'http://.......',  //jwks url
      clientId: 'client',   // cleint id
      jwksRequestsPerMinutes: 5, // optional
      userProp:  'name;family_name...' //token properties for the user.
    )
  ]
)

forRootAsync is available too.
  
```

In controller 

```ts
import {NVAuthGuard, NVRoleGuard} from 'nest-oidc-validator';
```

```ts
....

@Roles('admin')
@UseGuards(NVRoleGuard) // role guard.
@UseGuards(NVAuthGuard) // Authentication guard.
@Get("/path")
getSomething() {
  return this.somethingService.getAll();
}
  
```

If pipes are defined globally and you want some controllers is public you can use @Public decorator:

```ts
import {Public} from 'nest-oidc-validator';
```

```ts
....

@Public()
@Get("/path")
getSomethingPublic() {
  return this.somethingServicePublic.getAll();
}
  
```
