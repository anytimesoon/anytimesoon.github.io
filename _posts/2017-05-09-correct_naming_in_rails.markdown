---
layout: post
title:  "Correct naming in Rails"
date:   2017-05-09 20:35:11 +0000
---


Rails follows conventions, so as long as you know these conventions, everything runs smoothly. If you should dare to step outside of these seemingly trivial rules, you are taking your life into your own hands. Take for instance the following form:

```	
<%= form_for recipe do |f| %>
	<%= f.label :name %>
	<%= f.text_field :name %>

	<%= f.collection_check_boxes :ingredients, Ingredient.all, :id, :name%>

	<%= f.submit %>
<% end %>
```

For the purpose of this example, I'll focus on the following line:

```<%= f.collection_check_boxes :ingredients, Ingredient.all, :id, :name%>```

If you want for this line to find existing ingredients and add them to your recipe, you better be ready to build your own ingredient= method in the recipe model, because rails won't be doing any heavy lifting here. If on the other hand, you'd rather let rails automagically do it all for you, all you need to do is this:

```<%= f.collection_check_boxes :ingredient_ids, Ingredient.all, :id, :name%>```

Simple!

...

Took me all do to figure that out. Now I know and you do too.
