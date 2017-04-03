---
layout: post
title:  "Database associations"
date:   2017-04-03 17:29:58 -0400
---


Activerecord makes dealing with databases much easier. There's no need to deal with sql, as everything is done in ruby. Migrations take care of creating and modifying tables, and associating them to their respective ruby objects.

The relationships between these objects (and by extention the tables) is also easily done, but there are some very subtle, yet important syntax rules to pay attention to. Let's take the following example:

An Artist can have multiple songs and multiple genres
A Genre can have multiple artists and multiple songs
A Song can belong to ONE Artist and multiple genres

If we start with the most basic relationship. An Astist can have many Songs, and a Song belongs to one Artist. Our Artist class should now look like this:

```
class Artist < ActiveRecord::Base
  has_many :songs
end
```

and the Song class:

```
class Song < ActiveRecord::Base
  belongs_to :artist
end
```

Notice that the `has_many :songs` is pluralised, where `belongs_to :artist` is not. This a subtlety, which makes the code easier to read, but important to remember.

Next we will want to connect the Songs and Genres. This will need to be done through the :song_genres join table. Again, notice that the reference to song is singular and genres is plural. This is a convention that must be followed. The order the table names come in doesn't matter, but the first must be singular, and the second must be pluarlised.

First we must declare the relationship that Songs have with the join table model SongGenre. 

```
class Song < ActiveRecord::Base
  belongs_to :artist
  has_many :song_genres
end
```

and the SongGenre class:

```
class SongGenre < ActiveRecord::Base
  belongs_to :song
end
```

Then the same for Genres.

```
class Genre < ActiveRecord::Base
  has_many :song_genres
end
```

and SongGenre:

```
class SongGenre < ActiveRecord::Base
  belongs_to :song
  belongs_to :genre
end
```

It is important to declare the relationship to the join table *before* declaring the relationship between the two main tables. We are about to tell activerecord that Songs have many Genres. This is done through the join table, so activerecord must be aware of the join table before anything can happen.

Our Song and Genre classes should now look like this:

```
class Song < ActiveRecord::Base
  belongs_to :artist
  has_many :song_genres
  has_many :genres, through: :song_genres
end
```

and

```
class Genre < ActiveRecord::Base
  has_many :song_genres
  has_many :songs, through: :song_genres
end
```

Everything is working now, except that Artists also have many Genres, and Genres have many Artists. We do not need a special join table for this, because Songs acts as our join table. We can create that final relationship like this:

```
class Artist < ActiveRecord::Base
  has_many :songs
  has_many :genres, through: :songs
end
```

```
class Genre < ActiveRecord::Base
  has_many :song_genres
  has_many :songs, through: :song_genres
  has_many :artists, through: :songs
end
```


And that's it. Activerecord takes care of the rest for us. The main thing to keep an eye on is how some tables need to be refered to in the singular, while others are pluralised.
