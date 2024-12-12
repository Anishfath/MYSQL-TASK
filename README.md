package GuviSeleniumWebDriver.GuviSeleniumWebDriver;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;

public class JDBCTask {
    public static void main(String[] args) {
        // SQLite database URL
        String url = "jdbc:sqlite:GuviTask1.db";

        // SQL Insert Query
        String query = "INSERT INTO employee (empcode, empname, empage, empsalary) VALUES (?, ?, ?, ?)";

        // Employee data to insert
        Object[][] employees = {
            {101, "Jenny", 25, 10000.0},
            {102, "Jacky", 30, 20000.0},
            {103, "Joe", 20, 40000.0},
            {104, "John", 40, 80000.0},
            {105, "Shameer", 25, 90000.0}
        };

        try (Connection connection = DriverManager.getConnection(url);
             PreparedStatement preparedStatement = connection.prepareStatement(query)) {

            // Loop through the employees and add them to the database
            for (Object[] employee : employees) {
                preparedStatement.setInt(1, (int) employee[0]);    // empcode
                preparedStatement.setString(2, (String) employee[1]); // empname
                preparedStatement.setInt(3, (int) employee[2]);    // empage
                preparedStatement.setDouble(4, (double) employee[3]); // empsalary

                // Execute the query
                preparedStatement.executeUpdate();
            }

            System.out.println("Data inserted successfully!");

        } catch (Exception e) {
            e.printStackTrace();
        }   
    }
}
