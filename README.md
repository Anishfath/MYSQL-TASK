package GuviSeleniumWebDriver.GuviSeleniumWebDriver;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class JDBCTask
{
    // JDBC URL, username, and password
    private static String url = "jdbc:mysql://localhost:3306/GuviTask1.db";
    private static Connection connection;
    
 
    public static void main(String args[])
    {
        // SQL query to insert data into the table
        String insertQuery = "INSERT INTO Employee (empcode, empname, empage, empsalary) VALUES (?, ?, ?, ?)";

        try {
            // Establishing connection
            connection = DriverManager.getConnection(url);
            // Creating PreparedStatement
            PreparedStatement pst = connection.prepareStatement(insertQuery);

            // Inserting data
            insertEmployee(pst, 101, "Jenny", 25, 10000);
            insertEmployee(pst, 102, "Jacky", 30, 20000);
            insertEmployee(pst, 103, "Joe", 20, 40000);
            insertEmployee(pst, 104, "John", 40, 80000);
            insertEmployee(pst, 105, "Shameer", 25, 90000);

            System.out.println(" Data successfully inserted ");
        }
        catch (SQLException e)
        {
            e.getMessage();
        }
        //finally block used to close connection
        finally
        {
            try
            {
                if (connection != null)
                {
                    connection.close();
                }
            }
            catch (SQLException e)
            {
                e.printStackTrace();
            }
        }

    }

    // Method to insert employee data into the database
    private static void insertEmployee(PreparedStatement pst, int empcode, String empname, int empage, int empsalary) throws SQLException
    {
        pst.setInt(1, empcode);
        pst.setString(2, empname);
        pst.setInt(3, empage);
        pst.setInt(4, empsalary);

        // Executing the insert statement
        pst.executeUpdate();
    }
}
