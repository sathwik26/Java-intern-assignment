# Java-intern-assignment
import java.util.*;

// Class representing a Book with attributes like ID, Title, Author, Genre, and Availability
class Book {
    private String bookID;
    private String title;
    private String author;
    private String genre;
    private String availability;

    // Constructor to initialize book details
    public Book(String bookID, String title, String author, String genre, String availability) {
        this.bookID = bookID;
        this.title = title;
        this.author = author;
        this.genre = genre;
        this.availability = availability;
    }

    // Getters and Setters
    public String getBookID() {
        return bookID;
    }

    public String getTitle() {
        return title;
    }
    
    public void setTitle(String title) {
        this.title = title;
    }
    
    public String getAuthor() {
        return author;
    }
    
    public void setAuthor(String author) {
        this.author = author;
    }
    
    public String getGenre() {
        return genre;
    }

    public String getAvailability() {
        return availability;
    }

    public void setAvailability(String availability) {
        this.availability = availability;
    }

    // Override toString method for better readability when printing book details
    @Override
    public String toString() {
        return "Book ID: " + bookID + ", Title: " + title + ", Author: " + author + ", Genre: " + genre + ", Availability: " + availability;
    }
}

// Class representing the Library, which manages book records
class Library {
    private Map<String, Book> books = new HashMap<>(); // Stores books using a HashMap

    // Method to add a new book to the collection
    public void addBook(Book book) {
        if (!books.containsKey(book.getBookID())) {
            books.put(book.getBookID(), book);
            System.out.println("Book added successfully.");
        } else {
            System.out.println("Book ID already exists.");
        }
    }

    // Method to display all books in the library
    public void viewAllBooks() {
        if (books.isEmpty()) {
            System.out.println("No books available.");
        } else {
            for (Book book : books.values()) {
                System.out.println(book);
            }
        }
    }

    // Method to search for a book by ID or title
    public Book searchBook(String keyword) {
        return books.values().stream()
                .filter(book -> book.getBookID().equalsIgnoreCase(keyword) || book.getTitle().equalsIgnoreCase(keyword))
                .findFirst().orElse(null);
    }

    // Method to update book details
    public void updateBook(String bookID, String title, String author, String availability) {
        Book book = books.get(bookID);
        if (book != null) {
            book.setTitle(title);
            book.setAuthor(author);
            book.setAvailability(availability);
            System.out.println("Book details updated successfully.");
        } else {
            System.out.println("Book not found.");
        }
    }

    // Method to delete a book from the catalog
    public void deleteBook(String bookID) {
        if (books.remove(bookID) != null) {
            System.out.println("Book deleted successfully.");
        } else {
            System.out.println("Book not found.");
        }
    }
}

// Main class to interact with the library system
public class DigitalLibrarySystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Library library = new Library();
        
        while (true) {
            // Display menu options
            System.out.println("\n1. Add Book\n2. View All Books\n3. Search Book\n4. Update Book\n5. Delete Book\n6. Exit");
            System.out.print("Enter choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline
            
            switch (choice) {
                case 1:
                    // Add book details
                    System.out.print("Enter Book ID: ");
                    String bookID = scanner.nextLine();
                    System.out.print("Enter Title: ");
                    String title = scanner.nextLine();
                    System.out.print("Enter Author: ");
                    String author = scanner.nextLine();
                    System.out.print("Enter Genre: ");
                    String genre = scanner.nextLine();
                    System.out.print("Enter Availability (Available/Checked Out): ");
                    String availability = scanner.nextLine();
                    library.addBook(new Book(bookID, title, author, genre, availability));
                    break;
                case 2:
                    // View all books
                    library.viewAllBooks();
                    break;
                case 3:
                    // Search for a book
                    System.out.print("Enter Book ID or Title: ");
                    String keyword = scanner.nextLine();
                    Book book = library.searchBook(keyword);
                    System.out.println(book != null ? book : "Book not found.");
                    break;
                case 4:
                    // Update book details
                    System.out.print("Enter Book ID to update: ");
                    bookID = scanner.nextLine();
                    System.out.print("Enter New Title: ");
                    title = scanner.nextLine();
                    System.out.print("Enter New Author: ");
                    author = scanner.nextLine();
                    System.out.print("Enter New Availability: ");
                    availability = scanner.nextLine();
                    library.updateBook(bookID, title, author, availability);
                    break;
                case 5:
                    // Delete a book
                    System.out.print("Enter Book ID to delete: ");
                    bookID = scanner.nextLine();
                    library.deleteBook(bookID);
                    break;
                case 6:
                    // Exit the program
                    System.out.println("Exiting... Goodbye!");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice. Try again.");
            }
        }
    }
}
