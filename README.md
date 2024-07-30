# JavaMySQLConnector

A comprehensive example demonstrating the connection between Java and MySQL, detailing common issues, solutions, and best practices for database operations using the MySQL Connector/J.

## Description

This project provides a detailed example of how to connect a Java application to a MySQL database using the MySQL Connector/J. It covers the setup process, common issues and solutions, and includes best practices for managing database connections in Java.

## Prerequisites

- Java Development Kit (JDK) 17 or later
- MySQL Server
- MySQL Connector/J (included in this project)

## Installation

1. **Clone the repository:**
   ```bash
   git clone git@github.com:josivantarcio/JavaMySQLConnector.git
   cd JavaMySQLConnector
   ```

2. **Set up the MySQL database:**
   - Ensure MySQL server is running.
   - Create a database named `coursejdbc`.
   - Update the `db.properties` file with your MySQL server credentials.

3. **Build and run the project:**
   - Compile the Java files:
     ```bash
     javac -cp .:mysql-connector-java-9.0.0.jar db/DB.java
     ```
   - Run the application:
     ```bash
     java -cp .:mysql-connector-java-9.0.0.jar db.DB
     ```

## Usage

- Ensure the MySQL server is running and the database `coursejdbc` is created.
- The `db.properties` file should be configured with your database credentials:
  ```properties
  user=root
  password=12345678
  dburl=jdbc:mysql://localhost:3306/coursejdbc
  useSSL=false
  ```

## Code Example

Here is a simple example of a Java class that connects to a MySQL database:

```java
package db;

import java.io.FileInputStream;
import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.util.Properties;

public class DB {

    private static Connection conn = null;

    public static Connection getConnection() {
        if (conn == null) {
            try {
                Properties props = loadProperties();
                String url = props.getProperty("dburl");
                conn = DriverManager.getConnection(url, props);
            } catch (SQLException e) {
                throw new db.DbException(e.getMessage());
            }
        }
        return conn;
    }

    private static Properties loadProperties() {
        try (FileInputStream fs = new FileInputStream("db.properties")) {
            Properties props = new Properties();
            props.load(fs);
            return props;
        } catch (IOException e) {
            throw new DbException(e.getMessage());
        }
    }
}
```

## Troubleshooting

If you encounter issues with importing `java.sql` libraries or connecting to the database, consider the following steps:

1. **Check your JDK installation:**
   Ensure that you have the correct version of JDK installed and configured.

2. **Verify your MySQL Connector/J installation:**
   Make sure the MySQL Connector/J jar file is correctly added to your project's classpath.

3. **Module system issues:**
   If you're using Java modules, ensure your `module-info.java` is correctly configured or remove it if not needed.

## Alternatives

While using MySQL Connector/J is a common approach, other alternatives for connecting Java applications to databases include:

- **JDBC connection pooling libraries** like HikariCP or Apache DBCP for better performance and resource management.
- **ORM frameworks** like Hibernate or JPA for more complex database interactions.

## Conclusion

Using the MySQL Connector/J to connect Java applications to MySQL databases remains a relevant and powerful method. This project aims to simplify the process and provide a clear, humanized guide for developers encountering common issues and seeking best practices.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

- **Josivan Tárcio** - [LinkedIn](https://www.linkedin.com/in/josevanoliveirati/)

## Acknowledgments

- Thanks to the online communities and AI tools that assisted in troubleshooting and resolving issues throughout this project.

## Tags

#Java #MySQL #Database #JDBC #JavaMySQLConnector #DatabaseConnection #Programming #SoftwareDevelopment
