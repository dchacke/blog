---
layout: post
title: "Running Custom Logic in Rails Devise Controller"
date: 2021-01-07 15:58:57 -0800
tags:
 - coding
---

Today, I ran into the problem of needing to make a change to a user instance in the `RegistrationsController` using the [Devise](https://github.com/heartcombo/devise) authentication gem. I couldn't do it in a model callback because I needed access to cookies.

Luckily, Devise allows you to [pass a custom block](https://github.com/heartcombo/devise/blob/e3a00b27d19ba995891d7dd92394fe2900a789c2/app/controllers/devise/registrations_controller.rb#L20), which will be given the resource (e.g., the `user` object).

Assuming you already have a custom controller like this one

```rb
class RegistrationsController < Devise::RegistrationsController
end
```

you can achieve this pretty easily by passing a block:

```rb
class RegistrationsController < Devise::RegistrationsController
  def create
    super do |resource|
      # do stuff with resource...
      resource.foo = 'bar'
      resource.save
    end
  end
end
```

Unfortunately, the block is invoked *after* the resource is saved to the database, so you'll need to save it again if you're making any changes that need to be persisted.

The call to `super` works because the `RegistrationsController` inherits from `Devise::RegistrationsController` as defined [here](https://github.com/heartcombo/devise/blob/e3a00b27d19ba995891d7dd92394fe2900a789c2/app/controllers/devise/registrations_controller.rb). `super` will call `Devise::RegistrationsController#create` and pass it the block, where it then gets invoked with the resource.

As you can see in the source code, Devise offers support for blocks in `#new`, `#update`, and `#destroy` as well.

Unless you require functionality that's only available in controllers (such as cookies, as I mentioned), I recommend using model callbacks instead. But if you do need to do your magic in controllers, this approach should work.
