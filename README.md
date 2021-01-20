# SOLID

## Interface Segregation

### Exercises

A common pitfall in development is the naming of interfaces or abstract classes after real-world things. The problems that arise from this error are twofold:
	* the collection of methods defined in one interface increases as you add more functionality to it (which also violates Single Responsibility)
	* implementing a larger interface means implementing several methods, some of which may be unnecessary

Consider the following three modules:

* Bird.java (interface)
* Falcon.java (class, implements Bird.java)
* Dodo.java (class, implements Bird.java)

```java
public interface Bird{
    public void fly();
    public void layEggs();
}
```
```java
public class Falcon implements Bird{
    private String currentLocation;
    private int numberOfEggs;

    public Falcon(int initialEggCount) {
        this.setNumberOfEggs(initialEggCount);
    }

    public void fly() {
        this.setCurrentLocation("soaring above the clouds");
    }

    public void layEggs() {
        this.setNumberOfEggs(getNumberOfEggs() + 1);
    }

    public String getCurrentLocation() {
        return currentLocation;
    }

    public void setCurrentLocation(String currentLocation) {
    this.currentLocation = currentLocation;
    }

    public int getNumberOfEggs() {
        return numberOfEggs;
    }

    public void setNumberOfEggs(int numberOfEggs) {
        this.numberOfEggs = numberOfEggs;
    }
}
```
```java
public class Dodo implements Bird {
    private String currentLocation;
    private int numberOfEggs;

    public Dodo(int initialEggCount) {
        this.setNumberOfEggs(initialEggCount);
    }

    public void fly() {
        throw new UnsupportedOperationException();
    }

    public void layEggs() {
        this.setNumberOfEggs(getNumberOfEggs() + 1);
    }

    public void goExtinct() {
        this.setCurrentLocation("in a museum");
    }

    public String getCurrentLocation() {
        return currentLocation;
    }

    public void setCurrentLocation(String currentLocation) {
        this.currentLocation = currentLocation;
    }

    public int getNumberOfEggs() {
        return numberOfEggs;
    }

    public void setNumberOfEggs(int numberOfEggs) {
        this.numberOfEggs = numberOfEggs;
    }
}
```
It might make sense at first to make a Bird interface, but when encountered with things that don't fit the usual specification for a Bird, things get difficult to deal with quickly.

Refactor this code to adhere to the Interface Segregation Principle, using the following modules, to complete this excercise:

* EggLayingCreature.java
* FlyingCreature.java
* ExtinctCreature.java
* Dodo.java
* Falcon.java

```java
package com.qa.main;

public interface EggLayingCreature {
	public void layEggs();
}
```

```java
package com.qa.main;

public interface FlyingCreature {
	public void fly();
}
```

```java
package com.qa.main;

public interface ExtinctCreature {
	 public void goExtinct();
}
```

```java
package com.qa.main;

public class Dodo implements EggLayingCreature, ExtinctCreature{
    private String currentLocation;
    private int numberOfEggs;

    public Dodo(int initialEggCount) {
        this.setNumberOfEggs(initialEggCount);
    }

//    public void fly() {
//        throw new UnsupportedOperationException();
//    }

    public void layEggs() {
        this.setNumberOfEggs(getNumberOfEggs() + 1);
    }

    public void goExtinct() {
        this.setCurrentLocation("in a museum");
    }

    public String getCurrentLocation() {
        return currentLocation;
    }

    public void setCurrentLocation(String currentLocation) {
        this.currentLocation = currentLocation;
    }

    public int getNumberOfEggs() {
        return numberOfEggs;
    }

    public void setNumberOfEggs(int numberOfEggs) {
        this.numberOfEggs = numberOfEggs;
    }
}
```

```java
package com.qa.main;

public class Falcon implements EggLayingCreature, FlyingCreature{
    private String currentLocation;
    private int numberOfEggs;

    public Falcon(int initialEggCount) {
        this.setNumberOfEggs(initialEggCount);
    }

    public void fly() {
        this.setCurrentLocation("soaring above the clouds");
    }

    public void layEggs() {
        this.setNumberOfEggs(getNumberOfEggs() + 1);
    }

    public String getCurrentLocation() {
        return currentLocation;
    }

    public void setCurrentLocation(String currentLocation) {
    this.currentLocation = currentLocation;
    }

    public int getNumberOfEggs() {
        return numberOfEggs;
    }

    public void setNumberOfEggs(int numberOfEggs) {
        this.numberOfEggs = numberOfEggs;
    }
}
```