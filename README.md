Part A: Connecting to MySQL and Fetching Data
1. Database Setup
CREATE DATABASE companydb;

USE companydb;

CREATE TABLE Employee (
  EmpID INT PRIMARY KEY,
  Name VARCHAR(50),
  Salary DOUBLE
);

INSERT INTO Employee VALUES
(101, 'John Doe', 50000),
(102, 'Alice Smith', 60000),
(103, 'Bob Johnson', 55000);

2. Java Program (FetchEmployee.java)
import java.sql.*;

public class FetchEmployee {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/companydb";
        String user = "root";
        String pass = "password";

        try {
            // 1. Load JDBC driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // 2. Establish connection
            Connection con = DriverManager.getConnection(url, user, pass);

            // 3. Create Statement and execute query
            Statement stmt = con.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM Employee");

            // 4. Display data
            System.out.println("EmpID\tName\t\tSalary");
            System.out.println("--------------------------------");
            while (rs.next()) {
                System.out.println(rs.getInt("EmpID") + "\t" + rs.getString("Name") + "\t" + rs.getDouble("Salary"));
            }

            // 5. Close connection
            con.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
