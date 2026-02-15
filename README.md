# Ugeopgave: Objekter og lister

**Formål:** Træning i objekter og basic ArrayList operationer



## Opgaver

1. [Student klasse](#opgave-1-student-klasse)
2. [Product klasse](#opgave-2-product-klasse)
3. [BankAccount med ArrayList](#opgave-3-bankaccount-med-arraylist)
4. [Team Management System](#opgave-4-team-management-system)
5. [Library System med Access Modifiers](#opgave-5-library-system-med-access-modifiers)
6. [Game Inventory med Static](#opgave-6-game-inventory-med-static)

---

## Opgave 1: Student klasse

Lav en klasse der repræsenterer studerende og arbejd med flere studerende i et array.

**Student klasse med:**
- Felter: `name` (String), `age` (int)
- Constructor der tager name og age
- Metode: `printInfo()` - udskriver studentens info

**I main:**
1. Opret 3 studerende med forskellige navne og aldre
2. Put dem i et array
3. Brug en løkke til at udskrive info for alle studerende
4. Find og udskriv den ældste studerende

**Ekstra udfordring:** Tilføj et felt `studentId` (String) til klassen. Lav en metode der finder en studerende baseret på ID.

<details>
<summary>Trin-for-trin guide</summary>

1. Opret Student.java fil med klassen Student
2. Lav to felter: name og age
3. Lav en constructor der modtager name og age som parametre og tildeler dem til felterne
4. Lav `printInfo()` metode der udskriver navn og alder
5. I main: opret 3 Student objekter med new
6. Opret et Student array og læg objekterne ind
7. Brug for-each løkke til at kalde printInfo() på hver studerende
8. Brug en løkke med if til at finde den ældste

</details>

<details>
<summary>Se svar</summary>

```java
// Student.java
public class Student {
    String name;
    int age;
    String studentId;
    
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public Student(String name, int age, String studentId) {
        this.name = name;
        this.age = age;
        this.studentId = studentId;
    }
    
    public void printInfo() {
        System.out.println(name + " er " + age + " år");
        if (studentId != null) {
            System.out.println("  ID: " + studentId);
        }
    }
}

// Main.java
public class Main {
    
    public static Student findOldest(Student[] students) {
        Student oldest = students[0];
        for (Student s : students) {
            if (s.age > oldest.age) {
                oldest = s;
            }
        }
        return oldest;
    }
    
    public static Student findById(Student[] students, String id) {
        for (Student s : students) {
            if (s.studentId != null && s.studentId.equals(id)) {
                return s;
            }
        }
        return null;
    }
    
    public static void main(String[] args) {
        Student s1 = new Student("Anna", 21);
        Student s2 = new Student("Peter", 19);
        Student s3 = new Student("Maria", 23);
        
        Student[] students = {s1, s2, s3};
        
        System.out.println("Alle studerende:");
        for (Student s : students) {
            s.printInfo();
        }
        
        Student oldest = findOldest(students);
        System.out.println("\nÆldste studerende:");
        oldest.printInfo();
        
        // Ekstra udfordring
        System.out.println("\n=== Med student ID ===");
        Student st1 = new Student("Anna", 21, "S001");
        Student st2 = new Student("Peter", 19, "S002");
        Student st3 = new Student("Maria", 23, "S003");
        
        Student[] studentsWithId = {st1, st2, st3};
        
        Student found = findById(studentsWithId, "S002");
        if (found != null) {
            System.out.println("Fundet studerende med ID S002:");
            found.printInfo();
        }
    }
}
```

</details>

---

## Opgave 2: Product klasse

Lav en klasse der repræsenterer produkter i en webshop med tags.

**Product klasse med:**
- Felter: `name` (String), `price` (double), `tags` (String array)
- Constructor der tager name, price og tags
- Metode: `printInfo()` - udskriver produkt info inkl. tags
- Metode: `hasTag(String tag)` - returnerer true hvis produktet har det tag

**I main:**
1. Opret 4 produkter med forskellige tags (f.eks. "electronics", "sale", "new")
2. Put dem i et array
3. Find og udskriv alle produkter med "sale" tag
4. Find og udskriv det dyreste produkt

**Ekstra udfordring:** Lav en metode der finder alle produkter inden for et prisinterval (min, max).

<details>
<summary>Trin-for-trin guide</summary>

1. Opret Product.java med klassen Product
2. Lav felter for name, price og tags (String array)
3. Lav constructor der modtager alle tre parametre
4. Lav `printInfo()` der udskriver navn, pris og løber gennem tags med løkke
5. Lav `hasTag()` der løber gennem tags array og returnerer true hvis den finder matchet
6. I main: opret produkter, put i array
7. Løb gennem array og check hasTag("sale"), udskriv hvis true
8. Find dyreste produkt med løkke der sammenligner price

</details>

<details>
<summary>Se svar</summary>

```java
// Product.java
public class Product {
    String name;
    double price;
    String[] tags;
    
    public Product(String name, double price, String[] tags) {
        this.name = name;
        this.price = price;
        this.tags = tags;
    }
    
    public void printInfo() {
        System.out.println(name + " - " + price + " kr");
        System.out.print("  Tags: ");
        for (int i = 0; i < tags.length; i++) {
            System.out.print(tags[i]);
            if (i < tags.length - 1) {
                System.out.print(", ");
            }
        }
        System.out.println();
    }
    
    public boolean hasTag(String tag) {
        for (String t : tags) {
            if (t.equals(tag)) {
                return true;
            }
        }
        return false;
    }
}

// Main.java
public class Main {
    
    public static Product findMostExpensive(Product[] products) {
        Product mostExpensive = products[0];
        for (Product p : products) {
            if (p.price > mostExpensive.price) {
                mostExpensive = p;
            }
        }
        return mostExpensive;
    }
    
    public static void findProductsInPriceRange(Product[] products, double min, double max) {
        System.out.println("Produkter mellem " + min + " og " + max + " kr:");
        for (Product p : products) {
            if (p.price >= min && p.price <= max) {
                p.printInfo();
            }
        }
    }
    
    public static void main(String[] args) {
        Product p1 = new Product("Laptop", 5999, new String[]{"electronics", "new"});
        Product p2 = new Product("Mouse", 199, new String[]{"electronics", "sale"});
        Product p3 = new Product("Keyboard", 499, new String[]{"electronics", "sale"});
        Product p4 = new Product("Monitor", 2499, new String[]{"electronics"});
        
        Product[] products = {p1, p2, p3, p4};
        
        System.out.println("Produkter på tilbud:");
        for (Product p : products) {
            if (p.hasTag("sale")) {
                p.printInfo();
            }
        }
        
        System.out.println("\nDyreste produkt:");
        Product expensive = findMostExpensive(products);
        expensive.printInfo();
        
        // Ekstra udfordring
        System.out.println();
        findProductsInPriceRange(products, 200, 1000);
    }
}
```

</details>

---

## Opgave 3: BankAccount med ArrayList

Lav et system til at håndtere bankkonti med transaktionshistorik ved hjælp af ArrayList.

**Transaction klasse med:**
- Felter: `type` (String - "deposit" eller "withdrawal"), `amount` (double)
- Constructor
- Metode: `toString()` - returnerer formateret string med type og beløb

**BankAccount klasse med:**
- Felter: `owner` (String), `balance` (double), `transactions` (ArrayList<Transaction>)
- Constructor der tager owner og startBalance
- Metode: `deposit(double amount)` - tilføj penge, gem transaction
- Metode: `withdraw(double amount)` - hæv penge hvis muligt, gem transaction
- Metode: `printTransactionHistory()` - udskriv alle transactions
- Metode: `getBalance()` - returner balance

**I main:**
1. Opret en bankkonto
2. Lav flere deposits og withdrawals
3. Print transaction historik
4. Print final balance

**Ekstra udfordring:** Lav en metode `getLargestTransaction()` der finder den største transaction (deposit eller withdrawal).

<details>
<summary>Trin-for-trin guide</summary>

1. Opret Transaction klasse med type og amount
2. Lav toString() i Transaction klassen
3. Opret BankAccount klasse
4. I constructor: initialiser transactions som ny ArrayList
5. I deposit/withdraw: tilføj ny Transaction til ArrayList
6. I printTransactionHistory: brug for-each løkke gennem transactions
7. Test i main med forskellige transactions

</details>

<details>
<summary>Se svar</summary>

```java
import java.util.ArrayList;

// Transaction.java
public class Transaction {
    String type;
    double amount;
    
    public Transaction(String type, double amount) {
        this.type = type;
        this.amount = amount;
    }
    
    public String toString() {
        return type + ": " + amount + " kr";
    }
}

// BankAccount.java
public class BankAccount {
    String owner;
    double balance;
    ArrayList<Transaction> transactions;
    
    public BankAccount(String owner, double startBalance) {
        this.owner = owner;
        this.balance = startBalance;
        this.transactions = new ArrayList<>();
        // Tilføj start balance som transaction
        transactions.add(new Transaction("deposit", startBalance));
    }
    
    public void deposit(double amount) {
        if (amount > 0) {
            balance = balance + amount;
            transactions.add(new Transaction("deposit", amount));
            System.out.println("Indsatte " + amount + " kr");
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance = balance - amount;
            transactions.add(new Transaction("withdrawal", amount));
            System.out.println("Hævede " + amount + " kr");
        } else if (amount > balance) {
            System.out.println("Ikke nok penge på kontoen");
        }
    }
    
    public void printTransactionHistory() {
        System.out.println("\n=== Transaktionshistorik for " + owner + " ===");
        for (Transaction t : transactions) {
            System.out.println(t);
        }
    }
    
    public double getBalance() {
        return balance;
    }
    
    public Transaction getLargestTransaction() {
        if (transactions.size() == 0) {
            return null;
        }
        
        Transaction largest = transactions.get(0);
        for (Transaction t : transactions) {
            if (t.amount > largest.amount) {
                largest = t;
            }
        }
        return largest;
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("Anna", 1000);
        
        account.deposit(500);
        account.withdraw(200);
        account.deposit(1000);
        account.withdraw(300);
        account.withdraw(5000);  // Fejler
        
        account.printTransactionHistory();
        
        System.out.println("\nNuværende saldo: " + account.getBalance() + " kr");
        
        // Ekstra udfordring
        Transaction largest = account.getLargestTransaction();
        System.out.println("\nStørste transaktion: " + largest);
    }
}
```

</details>

---

## Opgave 4: Team Management System

Lav et system hvor spillere kan tilføjes til teams, og teams kan konkurrere mod hinanden.

**Player klasse med:**
- Felter: `name` (String), `skillLevel` (int fra 1-100)
- Constructor
- Metode: `toString()` - returner formateret string

**Team klasse med:**
- Felter: `teamName` (String), `players` (ArrayList<Player>)
- Constructor
- Metode: `addPlayer(Player p)` - tilføj spiller til team
- Metode: `getAverageSkill()` - beregn gennemsnitlig skill level
- Metode: `printTeam()` - udskriv team navn og alle spillere
- Metode: `compete(Team opponent)` - sammenlign average skill, print vinder

**I main:**
1. Opret to teams
2. Tilføj 3-4 spillere til hvert team
3. Print begge teams
4. Lad teams konkurrere mod hinanden

**Ekstra udfordring:** Lav en metode `findBestPlayer()` der returnerer spilleren med højest skill level på teamet.

<details>
<summary>Trin-for-trin guide</summary>

1. Lav Player klasse med name og skillLevel
2. Lav toString() i Player
3. Lav Team klasse med ArrayList<Player>
4. I Team constructor: initialiser ArrayList
5. I addPlayer: brug .add() på ArrayList
6. I getAverageSkill: loop gennem alle players, sum skills, divider med antal
7. I compete: sammenlign getAverageSkill() for begge teams

</details>

<details>
<summary>Se svar</summary>

```java
import java.util.ArrayList;

// Player.java
public class Player {
    String name;
    int skillLevel;
    
    public Player(String name, int skillLevel) {
        this.name = name;
        this.skillLevel = skillLevel;
    }
    
    public String toString() {
        return name + " (skill: " + skillLevel + ")";
    }
}

// Team.java
public class Team {
    String teamName;
    ArrayList<Player> players;
    
    public Team(String teamName) {
        this.teamName = teamName;
        this.players = new ArrayList<>();
    }
    
    public void addPlayer(Player p) {
        players.add(p);
        System.out.println(p.name + " tilføjet til " + teamName);
    }
    
    public double getAverageSkill() {
        if (players.size() == 0) {
            return 0;
        }
        
        int totalSkill = 0;
        for (Player p : players) {
            totalSkill = totalSkill + p.skillLevel;
        }
        return (double)totalSkill / players.size();
    }
    
    public void printTeam() {
        System.out.println("\n=== " + teamName + " ===");
        System.out.println("Spillere:");
        for (Player p : players) {
            System.out.println("- " + p);
        }
        System.out.println("Gennemsnitlig skill: " + getAverageSkill());
    }
    
    public void compete(Team opponent) {
        System.out.println("\n=== " + teamName + " vs " + opponent.teamName + " ===");
        double mySkill = getAverageSkill();
        double opponentSkill = opponent.getAverageSkill();
        
        System.out.println(teamName + " skill: " + mySkill);
        System.out.println(opponent.teamName + " skill: " + opponentSkill);
        
        if (mySkill > opponentSkill) {
            System.out.println("Vinder: " + teamName);
        } else if (opponentSkill > mySkill) {
            System.out.println("Vinder: " + opponent.teamName);
        } else {
            System.out.println("Uafgjort!");
        }
    }
    
    public Player findBestPlayer() {
        if (players.size() == 0) {
            return null;
        }
        
        Player best = players.get(0);
        for (Player p : players) {
            if (p.skillLevel > best.skillLevel) {
                best = p;
            }
        }
        return best;
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Team redTeam = new Team("Røde Dragoner");
        Team blueTeam = new Team("Blå Hajer");
        
        // Tilføj spillere til rødt hold
        redTeam.addPlayer(new Player("Anna", 85));
        redTeam.addPlayer(new Player("Peter", 72));
        redTeam.addPlayer(new Player("Maria", 90));
        
        // Tilføj spillere til blåt hold
        blueTeam.addPlayer(new Player("Lars", 78));
        blueTeam.addPlayer(new Player("Emma", 82));
        blueTeam.addPlayer(new Player("Simon", 88));
        blueTeam.addPlayer(new Player("Sofia", 75));
        
        // Print teams
        redTeam.printTeam();
        blueTeam.printTeam();
        
        // Konkurrence
        redTeam.compete(blueTeam);
        
        // Ekstra udfordring
        System.out.println("\nBedste spillere:");
        System.out.println(redTeam.teamName + ": " + redTeam.findBestPlayer());
        System.out.println(blueTeam.teamName + ": " + blueTeam.findBestPlayer());
    }
}
```

</details>

---

## Opgave 5: Library System med Access Modifiers

Lav et bibliotekssystem med ordentlig information hiding (private fields, getters/setters).

**Book klasse med:**
- **Private** felter: `title` (String), `author` (String), `available` (boolean)
- **Public** constructor
- **Public** getters for alle felter
- **Public** metode: `borrow()` - sæt available til false hvis tilgængelig
- **Public** metode: `returnBook()` - sæt available til true
- **Public** metode: `toString()` - returner formateret string

**Library klasse med:**
- **Private** felter: `libraryName` (String), `books` (ArrayList<Book>)
- **Public** constructor
- **Public** metode: `addBook(Book book)` - tilføj bog til collection
- **Public** metode: `findAvailableBooks()` - returner ArrayList af tilgængelige bøger
- **Public** metode: `findBookByTitle(String title)` - returner bog eller null
- **Public** metode: `printAllBooks()` - udskriv alle bøger med toString()

**I main:**
1. Opret et bibliotek
2. Tilføj 5 bøger
3. Lån nogle bøger
4. Find og print tilgængelige bøger
5. Return nogle bøger
6. Print alle bøger

**Ekstra udfordring:** Tilføj validering i Book klassen så title og author ikke kan være tomme strings.

<details>
<summary>Trin-for-trin guide</summary>

1. Lav Book klasse med PRIVATE felter
2. Lav public getters (getName(), getAuthor(), isAvailable())
3. Lav borrow() der checker available før ændring
4. Lav Library klasse med private ArrayList
5. I addBook: valider at book ikke er null
6. I findAvailableBooks: loop og check isAvailable()
7. Test at du IKKE kan tilgå fields direkte (skal bruge getters)

</details>

<details>
<summary>Se svar</summary>

```java
import java.util.ArrayList;

// Book.java
public class Book {
    private String title;
    private String author;
    private boolean available;
    
    public Book(String title, String author) {
        // Validering (ekstra udfordring)
        if (title == null || title.isEmpty()) {
            this.title = "Unknown";
        } else {
            this.title = title;
        }
        
        if (author == null || author.isEmpty()) {
            this.author = "Unknown";
        } else {
            this.author = author;
        }
        
        this.available = true;
    }
    
    public String getTitle() {
        return title;
    }
    
    public String getAuthor() {
        return author;
    }
    
    public boolean isAvailable() {
        return available;
    }
    
    public void borrow() {
        if (available) {
            available = false;
            System.out.println("Du har lånt: " + title);
        } else {
            System.out.println(title + " er ikke tilgængelig");
        }
    }
    
    public void returnBook() {
        available = true;
        System.out.println("Returneret: " + title);
    }
    
    public String toString() {
        String status = available ? "Tilgængelig" : "Udlånt";
        return title + " af " + author + " - " + status;
    }
}

// Library.java
public class Library {
    private String libraryName;
    private ArrayList<Book> books;
    
    public Library(String libraryName) {
        this.libraryName = libraryName;
        this.books = new ArrayList<>();
    }
    
    public void addBook(Book book) {
        if (book != null) {
            books.add(book);
            System.out.println("Tilføjet bog: " + book.getTitle());
        }
    }
    
    public ArrayList<Book> findAvailableBooks() {
        ArrayList<Book> available = new ArrayList<>();
        for (Book book : books) {
            if (book.isAvailable()) {
                available.add(book);
            }
        }
        return available;
    }
    
    public Book findBookByTitle(String title) {
        for (Book book : books) {
            if (book.getTitle().equalsIgnoreCase(title)) {
                return book;
            }
        }
        return null;
    }
    
    public void printAllBooks() {
        System.out.println("\n=== " + libraryName + " ===");
        System.out.println("Alle bøger:");
        for (Book book : books) {
            System.out.println("- " + book);
        }
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Library library = new Library("Københavns Bibliotek");
        
        // Tilføj bøger
        library.addBook(new Book("1984", "George Orwell"));
        library.addBook(new Book("Harry Potter", "J.K. Rowling"));
        library.addBook(new Book("Ringenes Herre", "J.R.R. Tolkien"));
        library.addBook(new Book("To Kill a Mockingbird", "Harper Lee"));
        library.addBook(new Book("Pride and Prejudice", "Jane Austen"));
        
        // Lån nogle bøger
        System.out.println("\n--- Lån bøger ---");
        Book book1 = library.findBookByTitle("1984");
        if (book1 != null) {
            book1.borrow();
        }
        
        Book book2 = library.findBookByTitle("Harry Potter");
        if (book2 != null) {
            book2.borrow();
        }
        
        // Find tilgængelige bøger
        System.out.println("\n--- Tilgængelige bøger ---");
        ArrayList<Book> available = library.findAvailableBooks();
        for (Book book : available) {
            System.out.println("- " + book);
        }
        
        // Return bog
        System.out.println("\n--- Return bog ---");
        if (book1 != null) {
            book1.returnBook();
        }
        
        // Print alle bøger
        library.printAllBooks();
        
        // Test at private fields ikke kan tilgås
        // book1.available = true;  // FEJL! available er private
        // System.out.println(book1.title);  // FEJL! title er private
    }
}
```

</details>

---

## Opgave 6: Game Inventory med Static

Lav et inventory system til et spil hvor vi holder styr på hvor mange items der er skabt totalt med static.

**Item klasse med:**
- **Private** felter: `name` (String), `value` (int), `type` (String)
- **Private static** felt: `totalItemsCreated` (int) - starter på 0
- **Public** constructor der øger totalItemsCreated
- **Public** getters for alle instance felter
- **Public static** metode: `getTotalItemsCreated()` - returner total items
- **Public** metode: `toString()` - returner formateret string

**Inventory klasse med:**
- **Private** felter: `playerName` (String), `items` (ArrayList<Item>), `maxCapacity` (int)
- **Public** constructor
- **Public** metode: `addItem(Item item)` - tilføj hvis der er plads
- **Public** metode: `getTotalValue()` - sum værdien af alle items
- **Public** metode: `findItemsByType(String type)` - returner ArrayList af items af given type
- **Public** metode: `printInventory()` - udskriv alle items

**I main:**
1. Opret to inventory objekter (to spillere)
2. Tilføj items til begge inventories
3. Print begge inventories
4. Print total items created (static metode)
5. Print total value for hver inventory

**Ekstra udfordring:** Lav en static metode `getAverageItemValue()` i Item klassen der beregner gennemsnitsværdien af alle items skabt.

<details>
<summary>Trin-for-trin guide</summary>

1. Lav Item klasse med private static int totalItemsCreated = 0
2. I constructor: øg totalItemsCreated med 1
3. Lav static metode getTotalItemsCreated() der returnerer den static variabel
4. Lav Inventory klasse med ArrayList
5. Test at totalItemsCreated tæller korrekt når items oprettes
6. Husk: static metode kaldes med Item.getTotalItemsCreated(), ikke på objekt

</details>

<details>
<summary>Se svar</summary>

```java
import java.util.ArrayList;

// Item.java
public class Item {
    private String name;
    private int value;
    private String type;
    private static int totalItemsCreated = 0;
    private static int totalValue = 0;  // For ekstra udfordring
    
    public Item(String name, int value, String type) {
        this.name = name;
        this.value = value;
        this.type = type;
        totalItemsCreated = totalItemsCreated + 1;
        totalValue = totalValue + value;  // For ekstra udfordring
    }
    
    public String getName() {
        return name;
    }
    
    public int getValue() {
        return value;
    }
    
    public String getType() {
        return type;
    }
    
    public static int getTotalItemsCreated() {
        return totalItemsCreated;
    }
    
    public static double getAverageItemValue() {
        if (totalItemsCreated == 0) {
            return 0;
        }
        return (double)totalValue / totalItemsCreated;
    }
    
    public String toString() {
        return name + " (" + type + ") - " + value + " gold";
    }
}

// Inventory.java
public class Inventory {
    private String playerName;
    private ArrayList<Item> items;
    private int maxCapacity;
    
    public Inventory(String playerName, int maxCapacity) {
        this.playerName = playerName;
        this.maxCapacity = maxCapacity;
        this.items = new ArrayList<>();
    }
    
    public void addItem(Item item) {
        if (items.size() < maxCapacity) {
            items.add(item);
            System.out.println(playerName + " picked up: " + item.getName());
        } else {
            System.out.println("Inventory fuld! Kan ikke tilføje " + item.getName());
        }
    }
    
    public int getTotalValue() {
        int total = 0;
        for (Item item : items) {
            total = total + item.getValue();
        }
        return total;
    }
    
    public ArrayList<Item> findItemsByType(String type) {
        ArrayList<Item> found = new ArrayList<>();
        for (Item item : items) {
            if (item.getType().equalsIgnoreCase(type)) {
                found.add(item);
            }
        }
        return found;
    }
    
    public void printInventory() {
        System.out.println("\n=== " + playerName + "'s Inventory ===");
        System.out.println("Capacity: " + items.size() + "/" + maxCapacity);
        for (Item item : items) {
            System.out.println("- " + item);
        }
        System.out.println("Total value: " + getTotalValue() + " gold");
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        // Opret to spillere med inventories
        Inventory player1 = new Inventory("Hero", 10);
        Inventory player2 = new Inventory("Warrior", 8);
        
        // Tilføj items til spiller 1
        player1.addItem(new Item("Iron Sword", 150, "weapon"));
        player1.addItem(new Item("Health Potion", 50, "potion"));
        player1.addItem(new Item("Wooden Shield", 100, "armor"));
        player1.addItem(new Item("Mana Potion", 75, "potion"));
        
        // Tilføj items til spiller 2
        player2.addItem(new Item("Steel Axe", 200, "weapon"));
        player2.addItem(new Item("Leather Armor", 180, "armor"));
        player2.addItem(new Item("Health Potion", 50, "potion"));
        
        // Print inventories
        player1.printInventory();
        player2.printInventory();
        
        // Print total items created (STATIC metode)
        System.out.println("\n=== Game Statistics ===");
        System.out.println("Total items created: " + Item.getTotalItemsCreated());
        System.out.println("Average item value: " + Item.getAverageItemValue() + " gold");
        
        // Find items by type
        System.out.println("\n=== Hero's Potions ===");
        ArrayList<Item> potions = player1.findItemsByType("potion");
        for (Item potion : potions) {
            System.out.println("- " + potion);
        }
    }
}
```

</details>

---
