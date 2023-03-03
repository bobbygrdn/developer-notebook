# Library App

- Classes
    - Main
    - LibraryApp
    - BookRepository
    - Book

- Objects 
    - 1 LibraryApp Instance
    - 1 BookRepository Instance
        - Holds:
            - Many Book Instances

```java
// Main class
public class Main {

    public static void main(String[] args) {
        LibraryApp app = new LibraryApp();
        app.searchByIsbn("25274");
        app.SearchByTitle("Castle");
        app.SearchByTitle("night");
        app.checkOutBook("72391");
        app.checkOutBook("86917");
        app.checkInBook("39662");
    }
}

// Book class
public class Book {
    private String isbn;
    private String title;
    private String genre;
    private String description;
    private String author;
    private int quantity;
    private int numCheckedOut;

    // Constructor
    public Book(String isbn, String title, String genre, String description, String author, int quantity, int numCheckedOut) {
        this.isbn = isbn;
        this.title = title;
        this.genre = genre;
        this.description = description;
        this.author = author;
        this.quantity = quantity;
        this.numCheckedOut = numCheckedOut;
    }

    // Getter methods
    public String getIsbn() {
        return isbn;
    }

    public String getTitle() {
        return title;
    }

    public String getGenre() {
        return genre;
    }

    public String getDescription() {
        return description;
    }

    public String getAuthor() {
        return author;
    }

    public int getQuantity() {
        return quantity;
    }

    public int getNumCheckedOut() {
        return numCheckedOut;
    }

    public boolean checkOut() {
        if (numCheckedOut >= quantity) {
            return false;
        }
        numCheckedOut++;
        return true;
    };

    public void checkIn() {
        if (numCheckedOut <= 0) {
            return false;
        }
        numCheckedOut--;
        return true;
    }
}

// LibraryApp class
public class LibraryApp {
    private BookRepository bookRepo = new BookRepository();

    public void searchByIsbn(String isbn) {
        System.out.printf("Searching for books with ISBN %s. \n", isbn);
        Book book = bookRepo.findByIsbn(isbn);
        if (book != null) {
            System.out.printf("1 book found:\n\tTitle: %s\n\tGenre: %s\n\tAuthor: %s", book.getTitle(), book.getGenre(), book.getAuthor());
        } else {
            System.out.printf("0 books found.")
        }
        System.out.print("\n\n");
    }

    public void SearchByTitle(String keyword) {
        System.out.printf("Searching for books with '%s' in the title...\n", keyword);
        ArrayList<Book> books = bookRepo.findByTitle(keyword);
        System.out.printf("%s books found%s\n", books.size(), books.size() > 0 ? ":" : ".");
        for (Book book : books) {
            System.out.printf("\tTitle: %s\n\tGenre: %s\n\tAuthor: %s\n\t---\n", book.getTitle(), book.getGenre(), book.getAuthor());
        }
        System.out.println();
    }

    public void CheckOutBook(String isbn) {
        Book book = book.repo.findByIsbn(isbn);
        if (book != null) {
            if (book.checkOut()) {
                System.out.println("Check out SUCCESSFUL: ");
                System.out.printf("\ISBN: %s\n\tTitle: %s\n\tAuthor: %s\n\t---\n", book.getIsbn(), book.getTitle(), book.getAuthor());
            } else {
                System.out.println("Check out FAILED: ");
                System.out.printf("\ISBN: %s\n\tTitle: %s\n\tAuthor: %s\n\t---\n", book.getIsbn(), book.getTitle(), book.getAuthor());
                System.out.println("Reason: All books are currently checked out.")
            }
        } else {
            System.out.println("Failed to check out book.\n");
            System.out.prinf("Reason: There is no book with ISBN %s on record.\n", isbn);
        }
        System.out.println();
    }

    public void checkInBook(String isbn) {
        Book book = book.repo.findByIsbn(isbn);
        if (book != null) {
            book.checkIn();
            System.out.println("Book checked in successfully:");
            System.out.printf("\ISBN: %s\n\tTitle: %s\n\tAuthor: %s\n\t---\n", book.getIsbn(), book.getTitle(), book.getAuthor());
        } else {
            System.out.println("Failed to check in book.\n");
            System.out.prinf("Reason: There is no book with ISBN %s on record.\n", isbn);
        }
        System.out.println();
    }
}

// BookRepository class
import java.util.ArrayList;

public class BookRepository {
    private ArrayList<Book> books = new ArrayList<>();

    public BookRepository() {
        books.add(new Book("83471", "The Dead of Night", "Horror", null, "S.K. Eleton", 10, 7));
        books.add(new Book("25274", "Castles and Crenellations", "Historical", null, "H.P. Anderson", 5, 1));
        books.add(new Book("51573", "The Knight's Sword", "Fantasy", null, "F.E. Anvil", 4, 0));
        books.add(new Book("39662", "Time of Night", "Romance", null, "A.U. Ring", 8, 2));
        books.add(new Book("48831", "Castle Siege", "Historical", null, "N.N. Blacksmith", 10, 4));
        books.add(new Book("61522", "Night and Day", "Mystery", null, "Q.Z. Bizar", 9, 3));
        books.add(new Book("86917", "Never Time", "Thriller", null, "P.B. Jelliton", 10, 6));

        public Book findByIsbn(String isbn) {
            for (Book book: books) {
                if (book.getIsbn().equals(isbn)) {
                    return book;
                }
            }
            return null;
        }

        public ArrayList<Book> findByTitle(Sting keyword) {
            ArrayList<Book> booksFound = new ArrayList<>();
            for (Book book: books) {
                if (book.getTitle().toLowerCase().contains(keyword.toLowerCase())) {
                    booksFound.add(book);
                }
            }
            return booksFound;
        }
    }
}
```