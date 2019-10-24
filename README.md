# Design Patterns Cheatsheet
**Huge thanks to [Christopher Okhravi](https://www.youtube.com/channel/UCbF-4yQQAWw-UnuCd2Azfzg) for his [playlist](https://www.youtube.com/playlist?list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc) on design patterns, i really recommend you watch it!**

> **WARNING** the code is a mix between java and pseudocode, it's simplified and should not be used directly

## Strategy
## Observer
## Decorator
## Factory Method
### Abstract Factory
## Singleton
## Command
## Adapter
## Facade
## Proxy
Proxy pattern is basically adding a **proxy** (*a person who is given the power or authority to do something for someone else*) between interfaces for multitude of reasons like caching, security or remote objects that require additional processing to be used

![UML Diagram](assets/proxy-pattern.svg)

### Example
For this example imagine we have a large amount of data inside a database and we want to get a piece of data inside the database, so we have a `Database` class that reads a database and has `String get(String key)` method to get the data

![UML Diagram](assets/proxy-pattern-example-01.svg)

```java
interface IDatabase {
   String get(String key);
}

class Database implements IDatabase {
   String[] database = {};

   public Database(String path) {
      ... // expensive database parsing
   }

   public String get(String key) {
      return this.database[key];
   }
}
```


But now every time we instantiate `Database` it's gonna read and parse the database and we may not even use it, this is where proxy comes into play

![UML Diagram](assets/proxy-pattern-example-02.svg)

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

Now every time we try get data from the database it's gonna be parsed then return the data, while this may not always be the best approach it can be useful

## Bridge
## Template Method
## Composite
## Iterator
## State
## Null Object
