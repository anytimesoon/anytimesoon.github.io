---
layout: post
title:  "Prepared statements when dealing with SQL"
date:   2017-03-10 20:09:12 +0000
---

Here I am stuck on this problem with prepared statements. I'm writing this out to help with my current thought process.

The code:
```
def self.find(id, db)
  search = db.prepare("SELECT * FROM pokemon WHERE id = ?")
  search.execute(id)
end
```
	
The error:
```
1) Pokemon .find finds a pokemon from the database by their id number and returns a new Pokemon object                                                              
     Failure/Error: expect(pikachu_from_db.id).to eq(1)                                                                                                                
                                                                                                                                                                      
     NoMethodError:                                                                                                                                                    
       undefined method `id' for #<SQLite3::ResultSet:0x00000001a67c40>                                                                                                
     # ./spec/pokemon_spec.rb:37:in `block (3 levels) in <top (required)>'
```

So what's going on here?

I'm pretty sure that the "?" at the end of the prepared statement is there as a placeholder which then gets replaced with the variable passed into the #execute method. I'm obviously doing something wrong, but what?

... Much time has passed, and the solution (as always) was right in front of my face.

```
  search = db.execute("SELECT * FROM pokemon WHERE id = ?", id)
```

Which returns a nested array of all each column from the row where the id column is equal to the id variable. Alternatively, adding [0] to the end of the statement will return a simple array (no longer nested), which makes it easier to work with.

```
  search = db.execute("SELECT * FROM pokemon WHERE id = ?", id)[0]
```
