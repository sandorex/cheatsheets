+++
title = "Lazy Loading"
slug = "/proxy-pattern/examples/lazy-loading"
date = 2020-05-13T15:06:57+02:00
type = "subpost"
+++

> **WARNING** the code is a mix between java and pseudocode, and should not be used directly

For this example imagine we have a large amount of data inside a database and we want to get a piece of data inside the database  
So we have a `Database` class that reads a database and has `String get(String key)` method to get the data

![UML Diagram](/design-patterns/proxy/lazy-loading-01.svg)

```java
interface IDatabase {
   String get(String key);
}

class Database implements IDatabase {
   Map<String, String> database = null;

   public Database(String path) {
      ... // expensive database parsing
   }

   public String get(String key) {
      return this.database[key];
   }
}
```

But now every time we instantiate `Database` it's gonna read and parse the database and we may not even use it, this is where proxy comes into play

![UML Diagram](/design-patterns/proxy/lazy-loading-02.svg)

```java
class LazyDatabaseProxy implements IDatabase {
   String path = null;
   Database database = null;
   
   public LazyDatabaseProxy(String path) {
      this.path = path;
   }
   
   private void initialize_database() {
      if (this.database == null)
         this.database = Database(path)
   }
   
   public String get(String key) {
      this.initialize_database()
      
      return this.database.get(key)
   }
}
```

> **NOTE** Usually there is gonna be multiple methods that return data thats why `initialize_database()` would be useful, but with just `get()` it is redundant

Now every time we try to get data from the database it's gonna be parsed if it wasn't parsed already then return the data, while this may not always be the best approach it can be useful
