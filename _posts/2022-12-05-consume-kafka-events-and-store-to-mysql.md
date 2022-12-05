# Java program that consumes orders as events from Kafka and stores them in a MySQL database

Here is an example of a Java program that consumes order-related events from Kafka and stores them in a MySQL database:


```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.util.Properties;

import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.KafkaConsumer;

public class OrderEventConsumer {
    public static void main(String[] args) {
        // Set up MySQL connection and prepared statement
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "username";
        String password = "password";
        Connection conn = null;
        PreparedStatement stmt = null;

        // Set up Kafka consumer
        Properties props = new Properties();
        props.put("bootstrap.servers", "localhost:9092");
        props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
        props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
        props.put("group.id", "my-group");
        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
        consumer.subscribe(Collections.singletonList("orders"));

        // Consume and process events
        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(100);
            for (ConsumerRecord<String, String> record : records) {
                // Connect to MySQL
                try {
                    conn = DriverManager.getConnection(url, user, password);

                    // Insert event into database
                    stmt = conn.prepareStatement("INSERT INTO orders (order_id, product, quantity, price) VALUES (?, ?, ?, ?)");
                    stmt.setString(1, record.key());
                    stmt.setString(2, record.value().split(",")[0]);
                    stmt.setInt(3, Integer.parseInt(record.value().split(",")[1]));
                    stmt.setDouble(4, Double.parseDouble(record.value().split(",")[2]));
                    stmt.executeUpdate();
                } catch (SQLException e) {
                    e.printStackTrace();
                } finally {
                    // Close the connection and statement
                    if (stmt != null) stmt.close();
                    if (conn != null) conn.close();
                }
            }
        }
    }
}

```

