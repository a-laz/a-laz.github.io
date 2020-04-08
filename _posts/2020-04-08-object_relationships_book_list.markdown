---
layout: post
title:      "Object Relationships: Book List"
date:       2020-04-08 18:07:25 +0000
permalink:  object_relationships_book_list
---


So my friends and I always talk to each other about the different books we read. Normally i'd keep track of these books in my notes app on my iPhone. However i thought why don't i make a program that can keep track of each book on my book list, have a boolean, that is true if i read the book and false if i haven't, and keep track of each author for each book.

So lets get started!

![](https://media1.tenor.com/images/daa4f0a1d42c1eda1fc9a6ceffab903c/tenor.gif?itemid=10327197)

First i'll need to create two classes: Author and Book

```
class Book
end
```

```
class Author
end
```

Great!

Both  of these classes have a direct relationship to each other. Author has-many books and each Book has one Author.

Let's focus on  ```class Book```

Every book has a title, an author, and as we said before a boolean that states wheter or not the book has been read.

```
class Book
     attr_accessor :title, :author, :read
		
	 def initialize(title, author)
		   @title = title
		   @author = author
		   @read = false
		 end
		 
 end
 ```
 
 Sweet! 
 
 Now we need to remember that we need a list of all the books in our book list so our Book class needs a class variable
 ```@@all``` to store all of the book instances. 
 
 ```
 class Book
     attr_accessor :title, :author, :read
		 
	 @@all = []
		
	 def initialize(title, author)
		     @title = title
			 @author = author
			 @read = false
	 end
		 
 end
```

Every time we initialize a new Book instance with ```Book.new``` we need the instance to be saved into our ```@@all``` variable. We can use something like ```@@all << self``` but for the purpose of making our code look better im going to move that functionality into a seperate method called #```save```

 ```
 class Book
     attr_accessor :title, :author, :read
		 
	 @@all = []
		
	 def initialize(title, author)
		     @title = title
			 @author = author
			 @read = false
			 save
	 end
	 
	 def save
	     @@all << self
	 end
		 
 end
```

So let's head to the Author class. Each author has a name, books, and the Author class should keep track of all the author instances.

```
class Author
  attr_accessor :name, :book
  @@all = []

  def initialize(name)
    @name = name
		@books = []
    save
  end

  def save
    @@all << self
  end
end
```

Now how do we access all of the author's books? We need to dive back into the Book class first. We need a method access all of our books. 

```
class Book
  attr_accessor :title, :author, :read

  def initialize(title, author)
    @title = title
    @author = author
    @read = false
    save
  end

  def save
    @@all << self
  end

  def self.all
    @@all
  end
end
```
Perfect now lets jump back into the Author class. We need to make an author class can add a book to its @books.

```
class Author
 '''
  def add_book(book)
    @book << book
    book.author = self unless book.author == self
  end
end
```
	
Now the Book needs to be able to add an author object to itself. So lets remove the argument of author from the #initialize method and write a seperate method.


```
class Book
  attr_accessor :title, :author, :read

  def initialize(title)
    @title = title
    @read = false
    save
  end

  def save
    @@all << self
  end

  def self.all
    @@all
  end

  def author_name(author)
    self.author = author unless self.author == author
  end
end
```


Now lets write a method that returns all the books an author has written.

```
class Author
 '''
 def books
  Book.all.select{|book| book.author == self}
 end
end
```

What if we were looking for a specific author?
We could find them by name *wink *wink

```
class Author
 '''
 def find_by_name(name)
  self.all.find{|author| author.name == name}
 end
end
```

Let's up the anty a little bit. 

![](https://assets.rbl.ms/16517440/980x.gif)

Now say we don't have the author we are looking for we should be able to create that author using their name.
So let's write this method.

```
class Author
 '''
   def self.find_or_create_by_name(name)
    self.find_by_name(name) ? self.find_by_name(name) : self.new(name)
  end
end
```
Now when we have book we want to have the book be able to add that author to its author attribute, if it exsists, and create a new artist if it doesn't. We'll take out the old author_name method and replace it with this setter/writter method. 

```
class Book
 '''
   def author_name=(name)
    self.author = Author.find_or_create_by_name(name)
    author.add_book(self)
  end
end
```

So all that we are missing now is a method to change a books state from not read to read. SO behold.

```
class Book
 '''
 def now_read
  @read = true
 end
end
```

Let's add some more functionality to the Author class. Lets say given an Authors name we want to see the books that are on our reading list that we have not read. Lets define the method.

```
class Author
 '''
 def self.find_not_read_by_author(name)
   self.find_by_name(name).books.select{|book| book.read == false}
 end
end
```

We can do the same for books read by that author.

```
class Author
 '''
 def self.find_read_by_author(name)
  self.find_by_name(name).books.select{|book| book.read == true}
 end
end
```

Now lets see our finished classes.

```
class Book
  attr_accessor :title, :author, :read

  def initialize(title)
    @title = title
    @read = false
    save
  end

  def save
    @@all << self
  end

  def self.all
    @@all
  end

  def author_name=(name)
    self.author = Author.find_or_create_by_name(name)
    author.add_book(self)
  end
end

class Author
  attr_accessor :name
  @@all = []

  def initialize(name)
    @name = name
    save
  end

  def save
    @@all << self
  end

  def self.all
    @@all
  end

  def add_book(book)
    @book << book
    book.author = self unless book.author == self
  end

  def books
    Book.all.select{|book| book.author == self }
  end

  def self.find_by_name(name)
    self.all.find{|author| author.name == name}
  end

  def self.find_or_create_by_name(name)
    self.find_by_name(name) ? self.find_by_name(name) : self.new(name)
  end

  def self.find_not_read_by_author(name)
    self.find_by_name(name).books.select{|book| book.read == false}
  end

  def self.find_read_by_author(name)
    self.find_by_name(name).books.select{|book| book.read == true}
  end
end
```

Now we have added functionality to our own Booklist!

Happy Coding!!





 
		 
