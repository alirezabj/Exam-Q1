# Exam-Q1

For this question, , in order to solve the two tasks, I will employ the principle of encapsulation. In other words, I will design a read-only interface for players and an editable class so that sdministrators can edit card details. 


### Read-only view for players (Card Interface):

Players should only be able to view the card details. I define an interface  `CardView` that provides only getter methods.

```java
/**
 * interface for read-only card access for Players
 */
interface CardView {
    /**
     * Returns the title of the card
     * 
     * @.pre true
     * @.post RESULT == title of the card
     */
    String getTitle();

    /**
     * Returns the cost of the card
     * 
     * @.pre true
     * @.post RESULT == cost of the card
     */
    int getCost();

    /**
     * Returns the type of the card
     * 
     * @.pre true
     * @.post RESULT == type of the card
     */
    String getType();

    /**
     * Returns the damage value of the card
     * 
     * @.pre true
     * @.post RESULT == damage of the card
     */
    int getDamage();
}

```

##### Consequences:
1. Players can only access card data.
2. Since no setters are provided, players are not able to do modifications.


### Card class for administrative use

The `Card` class implements `CardView` and extends it with setters for administrative access. 

```java
/**
 * card class representing a card in the FireStone game
 * implementing CardView for read-only access
 */
class Card implements CardView {
    private String title;
    private int cost;
    private String type;
    private int damage;

    /**
     * Constructs a new Card
     * 
     * @.pre title != null && !title.isEmpty() && type != null && !type.isEmpty() && cost >= 0 && damage >= 0
     * @.post this.title == title && this.type == type && this.cost == cost && this.damage == damage
     */
    public Card(String title, int cost, String type, int damage) {
        if (cost < 0 || damage < 0) {
            throw new IllegalArgumentException("cost and damage must be positive");
        }
        this.title = title;
        this.cost = cost;
        this.type = type;
        this.damage = damage;
    }

    /**
     * Returns the title of the card
     * 
     * @.pre true
     * @.post RESULT == title of the card
     */
    @Override
    public String getTitle() { return title; }

    /**
     * Returns the cost of the card
     * 
     * @.pre true
     * @.post RESULT == cost of the card
     */
    @Override
    public int getCost() { return cost; }

    /**
     * Returns the type of the card
     * 
     * @.pre true
     * @.post RESULT == type of the card
     */
    @Override
    public String getType() { return type; }

    /**
     * Returns the damage value of the card
     * 
     * @.pre true
     * @.post RESULT == damage of the card
     */
    @Override
    public int getDamage() { return damage; }

    /**
     * Sets the title of the card for admins
     * 
     * @.pre title != null && !title.isEmpty()
     * @.post this.title == title
     */
    public void setTitle(String title) {
        if (title == null || title.isEmpty()) {
            throw new IllegalArgumentException("title cannot be empty");
        }
        this.title = title;
    }

    /**
     * Sets the cost of the card for admins
     * 
     * @.pre cost >= 0
     * @.post this.cost == cost
     */
    public void setCost(int cost) {
        if (cost < 0) {
            throw new IllegalArgumentException("cost must be positive");
        }
        this.cost = cost;
    }

    /**
     * Sets the type of the card for admins
     * 
     * @.pre type != null && !type.isEmpty()
     * @.post this.type == type
     */
    public void setType(String type) {
        if (type == null || type.isEmpty()) {
            throw new IllegalArgumentException("type cannot be empty");
        }
        this.type = type;
    }

    /**
     * Sets the damage value of the card for admins
     * 
     * @.pre damage >= 0
     * @.post this.damage == damage
     */
    public void setDamage(int damage) {
        if (damage < 0) {
            throw new IllegalArgumentException("damage must be positive");
        }
        this.damage = damage;
    }
}
```

























