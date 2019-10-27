# [Design Patterns Cheatsheet](https://sandorex.github.io/cheatsheets/design-patterns/)
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

![UML Diagram](assets/proxy/pattern.svg)

### Examples
<details>
<summary>Lazy Loading</summary>

For this example imagine we have a large amount of data inside a database and we want to get a piece of data inside the database, so we have a <code>Database</code> class that reads a database and has <code>String get(String key)</code> method to get the data

![UML Diagram](assets/proxy/lazy-loading-01.svg)

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

But now every time we instantiate <code>Database</code> it's gonna read and parse the database and we may not even use it, this is where proxy comes into play

![UML Diagram](assets/proxy/lazy-loading-02.svg)

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
</details>

## Bridge
Bridge pattern basically allows combinations of implementations

> **NOTE** the UML diagram is really confusing but you should see it anyways

![UML Diagram](assets/bridge/pattern.svg)

### Examples
<details>
<summary>Displaying Fundamentally Different Data</summary>
For this example imagine we have a GUI and we have three very different objects that we want to display lets use <code>Book</code>, <code>Car</code> and <code>House</code>, now we have to be able to display them in short concise view (<code>ThumbnailView</code>) and long detailed view (<code>DetailedView</code>)

If we were to make a class for every combination there would be total of 6 classes and code repetition would be awful but with bridge pattern it's a lot easier to extend with no code repetition

![UML Diagram](assets/bridge/displaying-data-01.svg)

```java
interface IDataAdapter {
   public String get_title();
   public Picture get_thumbnail();
   public Picture[] get_pictures();
}

class DataView {
   IDataAdapter adapter = null;

   public DataView(IDataAdapter adapter) {
      this.adapter = adapter
   }

   public abstract show();
}

class ThumbnailView extends DataView {
   public show() {
      ... // show the gui
   }
}

class DetailedView extends DataView {
   public show() {
      ... // show the gui
   }
}

class Book {
   public String title;
   public String year;
   public String author;
   public Picture cover;
   public Picture[] pictures;
}

class BookDataAdapter implements IDataAdapter {
   Book book = null;
   
   public BookDataAdapter(Book book) {
      this.book = book;
   }

   public String get_title() {
      return this.book.title + " (" + this.book.year + ") by " + this.book.author;
   }

   public Picture get_thumbnail() {
      return this.book.cover;
   }

   public Picture[] get_pictures() {
      return this.book.pictures;
   }
}

class Car {
   public String model;
   public String year;
   public String manufacturer;
   public Picture[] pictures;
}

class CarDataAdapter implements IDataAdapter {
   Car car = null;
   
   public CarDataAdapter(Car car) {
      this.car = car;
   }

   public String get_title() {
      return this.car.manufacturer + " " + this.car.model + " (" + this.car.year + ")";
   }

   public Picture get_thumbnail() {
      return this.car.pictures[0];
   }

   public Picture[] get_pictures() {
      return this.car.pictures;
   }
}

class House {
   public String address;
   public String year;
   public String owner;
   public Picture[] pictures;
}

class HouseDataAdapter implements IDataAdapter {
   House house = null;
   
   public HouseDataAdapter(House house) {
      this.house = house;
   }

   public String get_title() {
      return this.house.address + " (" + this.house.year + ")";
   }

   public Picture get_thumbnail() {
      return this.house.pictures[0];
   }

   public Picture[] get_pictures() {
      return this.house.pictures;
   }
}
```

</details>

## Template Method
Template Method pattern allows defining skeleton of an algorithm and then changing parts of it to change the behaviour, this pattern is mostly used in frameworks

![UML Diagram](assets/template-method/pattern.svg)

### Examples

> **TODO** i could not find a good example

## Composite
## Iterator
## State
## Null Object
