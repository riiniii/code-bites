---
title: "User Authention in Django"
date: "2021-12-05T07:26:03.284Z"
description: "A quick intro to Django's nice user authentication system"
categories: [django, python, web-framework]
comments: true
---

## Introduction

Django has a built in extendable user authentication system that covers both authorization and authentication. Here are some notes on what it has and what it covers!

The authorization system can authorize users, permissions of users, grouping users, a pre-existing configurable password hashing system, a [pluggable backend system](https://docs.djangoproject.com/en/3.2/ref/contrib/auth/), forms and view tools for logging in users or restricting contents.

The authentication system is more generic but has some well used third-party packages that support password strength checking, throttling of login attempts, authentication against third parties, and [object-level permissions](https://www.django-rest-framework.org/api-guide/permissions/#object-level-permissions).

The above are supported by the the module _[django.contrib.auth](https://docs.djangoproject.com/en/3.2/ref/contrib/auth/)._ This module contains models such as User, AnonymousUser, Permission, and Group. They all have some handy fields, attributes, methods, and more. There is also a Validators class for validating strings, a few different authetntication backend that we can work off of, and some login and logout signals that we can use to see when a user logins or logouts.

With the _django.contrib.auth_ library, creating users, setting passwords, setting permissions, creating sessions for users, and authenticating them, become as easy as calling pre-existing methods from the module.

## Password Management

Django also knows the password management is difficult to implement well, so it's done a lot of the hard work for us! Django has a specific way for [password management](https://docs.djangoproject.com/en/3.2/topics/auth/passwords/) that by default uses the PBKDF2 hashing algorithm, though you could use other popular ones like [Argon2](https://en.wikipedia.org/wiki/Argon2), bcrypt, or your own manual hasher. If you see Django storing your password in an illegible format, it's likely because the it's formatted with the following pattern:

```jsx
<algorithm>$<iterations>$<salt>$<hash>
```

You can easily set which password hashed you would like to use by setting in your settings.py, PASSWORD_HASHERS value to:

```jsx
PASSWORD_HASHERS = [
  "django.contrib.auth.hashers.PBKDF2PasswordHasher",
  "django.contrib.auth.hashers.PBKDF2SHA1PasswordHasher",
  "django.contrib.auth.hashers.Argon2PasswordHasher",
  "django.contrib.auth.hashers.BCryptSHA256PasswordHasher",
]
```

The above format indicates that the default hasher will be the hasher available at PASSWORD_HASHERS[0], but that if we have a different algorithm stored, we can support that one too - though you likely will need to install some extra packages!

If you want a more personalized password management system, Django not only supports using your own preferred password hasher, but also supports [increasing the salt entropy](https://docs.djangoproject.com/en/3.2/topics/auth/passwords/#increasing-the-salt-entropy), [increasing the work factor](https://docs.djangoproject.com/en/3.2/topics/auth/passwords/#increasing-the-work-factor), automated password hasher upgrading, writing your own hasher, implementing your own password validation aside from the [default password validator](https://docs.djangoproject.com/en/3.2/topics/auth/passwords/#module-django.contrib.auth.password_validation) one.

## [Customizing authentication](https://docs.djangoproject.com/en/3.2/topics/auth/customizing/#authentication-backends)

If what you need is not doable by Django's out of the box functionality, fear not since Django allows for easy extensibility. You can extend models, permissions, authentication backend systems, or completely replace them as well
