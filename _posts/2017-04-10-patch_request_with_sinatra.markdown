---
layout: post
title:  "Patch request with Sinatra"
date:   2017-04-10 21:09:10 +0000
---

Allowing a user to edit a record is a very common occurance on the web these days. The ability to interact with a website is what makes the internet so much more engaging than other forms of media. I had a hard time getting this to work in my Sinatra project, so here's what I tried, and how it got it to work.

This is my user edit form.

```
<form action="/users/<%=@user.slug%>" method="post">
  <input type="hidden" name="_method" value="patch">
  <input type="text" name="name" placeholder="Username" value="<%=@user.name%>">
  <input type="text" name="email" placeholder="Email" value="<%=@user.email%>">
  <input type="text" name="address" placeholder="Address" value="<%=@user.address%>">
  <input type="submit">
</form>
```

Notice this line: `<input type="hidden" name="_method" value="patch">`. This changes the method from post to patch. It needs to be coupled with `use Rack::MethodOverride` in the 'config.ru' file. As shown below:

```
use AdminController
use UsersController
use CartController
use ProductsController
use LoginController
use SignupController
use Rack::MethodOverride
run ApplicationController
```

In the controller, the route looks like this:

```
  patch '/users/:slug' do
    @user = User.find_by(slug: params[:slug])
    @user.update(params)
    @user.slugifier
    erb :'/users/show'
  end
```

Strangely, this directs me to the infuriating 'Sinatra doesn't know this ditty' page. So what is wrong with this code? Everything is there, but it's not working. The answer is in the config.ru file. `Rack::MethodOverride` needs to be loaded before any of the contollers, otherwise they will not have the access to the override.

```
use Rack::MethodOverride
use AdminController
use UsersController
use CartController
use ProductsController
use LoginController
use SignupController
run ApplicationController
```

