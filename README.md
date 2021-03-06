# NgxSocialLogin [![npm version](https://badge.fury.io/js/ngx-social-login.svg)](https://badge.fury.io/js/ngx-social-login)

This module's intention is to provide an easy to use social login service, which can be integrated easily into any environment.

This project has been inspired by [Angularx Social Login](https://github.com/abacritt/angularx-social-login)

I have created the fork to solve the problems with facebook (using promises). User does not accept pull request.

## Getting started

### Install via npm/yarn

```sh
npm install --save ngx-social-login-pro
```

```sh
yarn add ngx-social-login-pro
```

### Import the module

Import `NgxSocialLoginModule` into your `Module`.
You can provide any configuration that is supported by Oauth providers.

Google:

-   https://developers.google.com/identity/sign-in/web/reference#gapiauth2clientconfig

Facebook:

-   https://developers.facebook.com/docs/javascript/reference/FB.init/v2.12
-   https://developers.facebook.com/docs/reference/javascript/FB.login/v2.12#params

```javascript
@NgModule({
    declarations: [ ... ],
    imports: [
        ...
        NgxSocialLoginModule.init(
            {
                google: {
                    client_id: 'YOUR_CLIENT_ID'
                },
                facebook: {
                    initOptions: {
                        appId: 'YOUR_APP_ID'
                    },
                     loginOptions: {
                        auth_type: 'rerequest',
                        scope: 'email' // request permission to get email
                    }
                }
            }
        )
        ...
    ],
    providers: [ ... ]
})
export class AuthModule {
}
```

### How to use

```javascript
@Component({
  selector: 'app-login-page',
  templateUrl: './app-login-page.component.html',
  styleUrls: ['./app-login-page.component.css']
})
export class LoginPageComponent {

    constructor(private _service: SocialLoginService) {}

      loginWithFacebook(): void {
            const user = await this._service.login(Provider.FACEBOOK) 
            console.log(user);
      }

      loginWithGoogle(): void {
          const user = await this._service.login(Provider.GOOGLE).toPromise();
          console.log(user);
      }

      logout(): void {
          this._service.logout().subscribe({
               complete: ()=> console.log('Logout success'),
               error: err => console.log(err)
           });
      }

}
```

### Demo

```bash
git clone https://github.com/wermerb/ngx-social-login.git
cd ngx-social-login-pro
Add your Google and/or Facebook client id to AppModule's config
yarn / npm install
npm i ngx-social-login-pro 
ng build ngx-social-login-pro #generate lib
ng serve
```
