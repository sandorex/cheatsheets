+++
title = "Displaying Fundamentally Different Data"
slug = "/bridge-pattern/examples/displaying-fundamentally-different-data"
date = 2020-05-13T14:30:15+02:00
type = "subpost"
+++

> **WARNING** the code is a mix between java and pseudocode, and should not be used directly

For this example imagine we have a GUI and we have three very different objects that we want to display

Let's use `Book`, `Car` and `House`, and we have to be able to display them in short concise view (`ThumbnailView`) and long detailed view (`DetailedView`)

If we were to make a class for every combination there would be total of 6 classes and code repetition would be awful but with bridge pattern it's a lot easier to extend with no code repetition

![UML Diagram](/design-patterns/bridge/displaying-data-01.svg)

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
