Configuration Options
=====================

The module comes with a set of attributes to configure. The following is the list of all available options: 

#### enableRegistration (type: `boolean`, default: `true`)

Setting this attribute allows the registration process. If you set it to `false`, the module won't allow users to 
register by throwing a `NotFoundHttpException` if the `RegistrationController::actionRegister()` is accessed. 

#### enableEmailConfirmation (type: `boolean`, default: `true`)

If `true`, the module will send an email with a confirmation link that user needs to click through to complete its 
registration process.


#### enableFlashMessages (type: `boolean`, default: `true`)

If `true` views will display flash messages. 

#### generatePasswords (type: `boolean`, default: `true`)

If `true` the password field will be hidden on the registration page and passwords will be generated automatically and 
sent to the user via email.

#### allowUnconfirmedEmailLogin (type: `boolean`, default: `false`)

If `true` it will allow users to login with unconfirmed emails.
  
#### allowPasswordRecovery (type: `boolean`, default: `true`)

If `true` it will enable password recovery process.

#### allowAccountDelete (type: `boolean`, default: `true`)

If `true` users will be able to remove their own accounts. 

#### emailChangeStrategy (type: `integer`, default: `MailChangeStrategyInterface::TYPE_DEFAULT`)

Configures one of the three ways available to change user's password:

- **MailChangeStrategyInterface::TYPE_DEFAULT**: A confirmation message will be sent to the new user's email with a link 
    that needs to be click through to confirm  it.
- **MailChangeStrategyInterface::TYPE_INSECURE**: Email will be changed without any confirmation message. 
- **MailChangeStrategyInterface::TYPE_SECURE**: A confirmation message will be sent to the previous and new user's email 
    with a link that would require both to be click through to confirm the change.
    
#### rememberLoginLifespan (type: `integer`, default: `209600`)

Configures the time length in seconds a user will be remembered without the need to login again. The default time is 2 
weeks. 

#### tokenConfirmationLifespan (type: `integer`, default: `86400`)

Configures the time length in seconds a confirmation token is valid. The default time is 24 hours.
  
#### tokenRecoveryLifespan (type: `integer`, default: `21600`)

Configures the time length in seconds a recovery token is valid. The default time is 6 hours.

#### administrators (type: `array`, default: `[]`)

Configures the usernames of those users who are considered `admininistrators`. The administrators can be 
configured here or throughout RBAC with a special permission name. The recommended way is throughout 
`administratorPermissionName` as they can be set dynamically throughout the RBAC interface, but use this attribute for 
simple backends with static administrators that won't change throughout time.   

#### administratorPermissionName (type: `string`, default: `null`)

Configures the permission name for `administrators`. See [AuthHelper](../../src/User/Helper/AuthHelper.php).
 
#### prefix (type: `string`, default: `user`) 

Configures the URL prefix for the module. 


#### mailParams (type: `array`, default: `[]`)

Configures the parameter values used on [MailFactory](../../src/User/Factory/MailFactory.php). The default values are: 

```php
[
    'fromEmail' => 'no-reply@example.com',
    'welcomeMailSubject' => Yii::t('usuario', 'Welcome to {0}', $app->name),
    'confirmationMailSubject' => Yii::t('usuario', 'Confirm account on {0}', $app->name),
    'reconfirmationMailSubject' => Yii::t('usuario', 'Confirm email change on {0}', $app->name),
    'recoveryMailSubject' => Yii::t('usuario', 'Complete password reset on {0}', $app->name),
]
```

#### blowfishCost (type: `integer`, default: `10`)

Is the cost parameter used by the Blowfish hash algorithm. The higher the value of cost, the longer it takes to generate 
the hash and to verify a password against it. Higher cost therefore slows down a brute-force attack. For the best 
protected against brute-force attacks, set it to the highest value that is tolerable on production servers. The time 
taken to compute the hash doubles for every increment by one of `$blowfishCost`.


#### classMap (type: `array`, default: `[]`)

Configures the definitions of the classes as they have to be override. For more information see 
[Overriding Classes](../enhancing-and-overriding/overriding-classes.md). 

#### routes (type: `array`, default: `[]` )

The routes (url rules) of the module for the URL management. The default values are: 

```php 
[
    '<id:\d+>' => 'profile/show',
    '<action:(login|logout)>' => 'security/<action>',
    '<action:(register|resend)>' => 'registration/<action>',
    'confirm/<id:\d+>/<code:[A-Za-z0-9_-]+>' => 'registration/confirm',
    'forgot' => 'recovery/request',
    'recover/<id:\d+>/<code:[A-Za-z0-9_-]+>' => 'recovery/reset',
    'settings/<action:\w+>' => 'settings/<action>',
]
```

#### viewPath (type: `string`, default: `@Da/User/resources/views`)

Configures the root directory of the view files. See [overriding views](../enhancing-and-overriding/overriding-views.md).



© [2amigos](http://www.2amigos.us/) 2013-2017
