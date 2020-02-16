Events
======

The events in this plugin follow these conventions `<Plugin><Category>.<EventName>`:

* `Users.Component.UsersAuth.isAuthorized`
* `Users.Component.UsersAuth.beforeLogin`
* `Users.Component.UsersAuth.afterLogin`
* `Users.Component.UsersAuth.afterCookieLogin`
* `Users.Component.UsersAuth.beforeLogout`
* `Users.Component.UsersAuth.afterLogout`
* `Users.Component.UsersAuth.beforeRegister`
* `Users.Component.UsersAuth.afterRegister`
* `Users.Component.UsersAuth.beforeSocialLoginUserCreate`
* `Users.Component.UsersAuth.failedSocialLogin`
* `Users.Component.UsersAuth.afterResetPassword`
* `Users.Component.UsersAuth.onExpiredToken`
* `Users.Component.UsersAuth.afterResendTokenValidation`

The events allow you to inject data into the plugin on the before* plugins and use the data for your
own business, for example

```
/**
 * beforeRegister event
 */
public function eventRegister()
{
    $this->eventManager()->on('Users.Component.UsersAuth.beforeRegister', function ($event) {
        //the callback function should return the user data array to force register
        return $event->data['usersTable']->newEntity([
            'username' => 'forceEventRegister',
            'email' => 'eventregister@example.com',
            'password' => 'password',
            'active' => true,
            'tos' => true,
        ]);
    });
    $this->register();
    $this->render('register');
}
```
