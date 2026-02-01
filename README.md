import java.util.ArrayList;

public class LibraryUtility {
    public static int countTotalBooks(ArrayList<LibraryBook> books) {
        return books.size();
    }
    public static void displaySystemMessage() {
        System.out.println("📚 Welcome to the Library Management System");
        System.out.println("-------------------------------------------");
    }
    public static void main(String[] args) {
        displaySystemMessage();
        LibraryBook book1 = new LibraryBook(
                "Java Programming", "B101", "James Gosling");
        LibraryBook book2 = new LibraryBook(
                "Data Structures", "B102", "Mark Allen", "DSA fundamentals");
        ReferenceBook refBook = new ReferenceBook(
                "Encyclopedia", "R201", "Britannica");
        book1.issueBook("Sonam", 10);
        book2.issueBook("Robin");
        refBook.issueBook();
        book1.displayBookDetails();
        book2.displayBookDetails();
        refBook.displayBookDetails();
        book1.returnBook();
        ArrayList<LibraryBook> books = new ArrayList<>();
        books.add(book1);
        books.add(book2);
        books.add(refBook);
        System.out.println("Total Books in System: " +
                countTotalBooks(books));
    }
}
public class ReferenceBook extends LibraryBook {
    public ReferenceBook(String title, String bookId, String author) {
        super(title, bookId, author);
    }
    public ReferenceBook(String title, String bookId, String author, String description) {
        super(title, bookId, author, description);
    }
    @Override
    public void issueBook() {
        System.out.println(
                "Reference books cannot be issued, only viewed in the library."
        );
    }
}
  public class LibraryBook extends BookItem {
    private boolean isAvailable = true;
    private String issuedTo = "None";
    public LibraryBook(String title, String bookId, String author) {
        super(title, bookId, author, "No description provided");
    }
    public LibraryBook(String title, String bookId, String author, String description) {
        super(title, bookId, author, description);
    }
    public boolean isAvailable() {
        return isAvailable;
    }
    public String getIssuedTo() {
        return issuedTo;
    }
    @Override
    public void displayBookDetails() {
        System.out.println("Title: " + title);
        System.out.println("Book ID: " + bookId);
        System.out.println("Author: " + author);
        System.out.println("Description: " + description);
        System.out.println("Available: " + isAvailable);
        System.out.println("Issued To: " + issuedTo);
        System.out.println("---------------------------");
    }
    public void issueBook() {
        if (isAvailable) {
            isAvailable = false;
            issuedTo = "Unknown Student";
            System.out.println("Book issued successfully.");
        } else {
            System.out.println("Book is already issued.");
        }
    }
    public void issueBook(String studentName) {
        if (isAvailable) {
            isAvailable = false;
            issuedTo = studentName;
            System.out.println("Book issued to " + studentName);
        } else {
            System.out.println("Book is already issued.");
        }
    }
    public void issueBook(String studentName, int issueDurationDays) {
        if (isAvailable) {
            isAvailable = false;
            issuedTo = studentName;
            System.out.println("Book issued to " + studentName +
                    " for " + issueDurationDays + " days.");
            if (issueDurationDays > MAX_ISSUE_DAYS) {
                System.out.println("⚠ Warning: Issue duration exceeds MAX_ISSUE_DAYS.");
            }
        } else {
            System.out.println("Book is already issued.");
        }
    }
    public void returnBook() {
        isAvailable = true;
        issuedTo = "None";
        System.out.println("Book returned successfully.");
    }
}
public abstract class BookItem {
    protected String title;
    protected String bookId;
    protected String author;
    protected String description;
    public static final int MAX_ISSUE_DAYS = 7;
    public BookItem(String title, String bookId, String author, String description) {
        this.title = title;
        this.bookId = bookId;
        this.author = author;
        this.description = description;
    }
    public abstract void displayBookDetails();
}




# Library-Management-System
