# Spring boot DTO

DTO stands for Data transfer Object. It is used when you have fx an API but only want to expose specific fields to that API. So instead of just returning an original fx `Student` class you would have a modified class that fx does not have the `id` exposed. This is in order to control what the user can interact with



## Difference between DTO and original

Here is a simple example of a DTO called `OrderDTO`

```java
public class OrderDto {
    private String comments;
    private Collection<OrderItem> orderItems;
    private int customerId;
}
```

This is the original `Order` model. There are some obvious differences since this model is an entity that will be added to a database. **But** there are some more differences like the `orderDate`, `orderId`, etc are **not** part of the DTO. These are fields we don't want to expose

```java
package swc3.server.PrimaryDatasource.models;

import lombok.EqualsAndHashCode;
import lombok.Getter;
import lombok.Setter;

import javax.persistence.*;
import java.time.LocalDate;
import java.util.Collection;

@EqualsAndHashCode
@Setter
@Getter
@Entity
@Table(name = "orders", schema = "swc3_springboot")
public class Order {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "order_id", nullable = false)
    private int orderId;

    @Basic
    @Column(name = "customer_id", nullable = false)
    private int customerId;

    @Basic
    //@JsonFormat(pattern = "dd/MM/yyyy")
    @Column(name = "order_date", nullable = false)
    private LocalDate orderDate;

    @Basic
    @Column(name = "status", nullable = false)
    private byte status;

    @Basic
    @Column(name = "comments", nullable = true, length = 2000)
    private String comments;

    @Basic
    @Column(name = "shipped_date", nullable = true)
    private LocalDate shippedDate;

    @Basic
    @Column(name = "shipper_id", nullable = true)
    private Short shipperId;

    @OneToMany(mappedBy = "ordersByOrderId")
    private Collection<OrderItem> orderItems;

    //Hibernate will ignore this field
    @Transient
    public Double getTotalOrderPrice() {
        double sum = 0;
        for (OrderItem oi : getOrderItems()) {
            sum += oi.getTotalPrice();
        }
        return sum;
    }

    @Transient
    public int getProductsNumber(){
        int sum = 0;
        for (OrderItem oi : getOrderItems()){
            sum += oi.getQuantity();
        }
        return sum;
    }
```



## DTO in the controller

So now we have a new model that represents a subset of the fields in the `order` class

Now what needs to be done in the controller is that fx for the endpoint `api/orders` need to get all the orders and transform the list of orders into a list of OrderDTO's. This can be done with the fancy `.map` method. It can also be done with a normal for loop that goes through all `Order`'s and adds them to a list. 

```java
@GetMapping("/api/1.0/users")
  List<UserDTO> getUsers(){
    return userService.getOrders().map(OrderDTO::new).collect(Collectors.toList());
  }
```



