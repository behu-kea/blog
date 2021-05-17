# Java testing



To use testing in Java, add the following to your `pom-xml` file



```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>5.7.0</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.7.0</version>
    <scope>test</scope>
</dependency>
```



Now add a new test class under the folder `src/test/java/wishlistTest.java`



```java
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;

import static org.springframework.test.util.AssertionErrors.assertEquals;

public class wishlistTest {
    @Test
    @DisplayName("Simple multiplication should work")
    public void testMultiply() {
        assertEquals("should work", 20, getNumber());
    }

    public int getNumber() {
        return 20;
    }
}
```



`@test` - is used to tell Java that we are creating a new test

`@DisplayName` - is a way to tell what name the test will have