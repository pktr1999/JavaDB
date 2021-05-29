# JavaDB
# Create a blank database & DB path will be used in database URL
# Write a java program that uses UCanAccess JDBC driver to connect database
package net.codejava.jdbc;
import java.sql.*;
public class JdbcAccessTest {
    public static void main(String[] args) {  
        String databaseURL = "jdbc:ucanaccess://e://Java//JavaSE//MsAccess//Contacts.accdb";  
        try (Connection connection = DriverManager.getConnection(databaseURL)) {    
            String sql = "INSERT INTO Contacts (Full_Name, Email, Phone) VALUES (?, ?, ?)";
            PreparedStatement preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setString(1, "prasanna");
            preparedStatement.setString(2, "prasanna@gmail.com");
            preparedStatement.setString(3, "1234567890");   
            int row = preparedStatement.executeUpdate(); 
            if (row > 0) {
                System.out.println("A row has been inserted successfully.");
            }
             
            sql = "SELECT * FROM Contacts";
             
            Statement statement = connection.createStatement();
            ResultSet result = statement.executeQuery(sql);
             
            while (result.next()) {
                int id = result.getInt("Contact_ID");
                String fullname = result.getString("Full_Name");
                String email = result.getString("Email");
                String phone = result.getString("Phone");
                 
                System.out.println(id + ", " + fullname + ", " + email + ", " + phone);
            }
             
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
    }
}
