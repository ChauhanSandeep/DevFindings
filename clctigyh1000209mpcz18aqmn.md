---
title: "How to Design a Database with ERD: A Beginner’s Guide"
seoTitle: "Database Design Using Entity Relationship Model | Dev Findings"
seoDescription: "Learn how to create an Entity Relationship Diagram (ERD) to visually explain the structure of a system and how the entities in the system interact with each"
datePublished: Thu Jan 12 2023 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: clctigyh1000209mpcz18aqmn
slug: how-to-design-a-database-with-erd-a-beginners-guide
tags: databases, system-design

---

Database design is a crucial step in developing any software system that involves storing and manipulating data. In this article, we will learn how to use Entity Relationship Diagrams (ERDs) to visually represent the structure and relationships of a database.

## What is ERD?

An Entity Relationship Diagram (ERD) is a graphical representation of the entities, relationships, and attributes that make up a system. It is commonly used to visually explain the structure of a system, and how the entities in the system interact with each other.

For instance, consider an e-commerce application. In this system, entities could include customers, products, and orders. The relationships between these entities, such as a customer placing an order for a product, can be effectively illustrated using an ERD

In this article, we will discuss how we can do database design using an ERD. We will use Crow Foot notation to describe the relationship between tables.

## Crow Foot Notation

Crow's Foot Notation is an extremely useful diagrammatic representation of the relationship between various entities. Through its lines and symbols, it can provide a clear and concise explanation of how two different entities interact with each other, as well as the cardinality of that relationship.

This graphical representation is invaluable in helping to quickly understand the complexities of a system, making it an essential tool for designing well structured, efficient and reliable system.

### Basics

1. Relation between two tables is displayed by connecting these tables with connector lines
    
2. A perpendicular line on the connector line depicts one mandatory entry
    
3. A circle on the connector line depicts the optional entry.
    
4. A reverse arrow on the connector line depicts many entries.
    

## Understanding Various Relationship Types in ERD

Now that we have understood the basics of the Crow foot notation, let's see how it is used to create different types of relationships between entities.

1. One-to-one relationship (`1 : 1`)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551152017/7a4c2950-e117-4325-af16-c1d0380adf46.png align="center")
    
    **A one-to-one (1:1)** relationship is when two entities share exactly one connection with each other.
    
    **Scenario:** A one-to-one relationship could exist between a *customer* and their *account* in an e-commerce app.
    
    * Each person can only have one bank account
        
    
    * each account can belong to only one customer.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673547107686/192a18ef-6d6c-4767-813a-aa3f9382fcce.png align="center")
    
2. One-to-zero-or-one relationship (`1 : 0..1`)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551189988/5e798e38-25f9-4573-a249-98d121056a94.png align="center")
    
    **A one-to-zero-or-one (1:0..1)** relationship is where one entity has zero or one connection with another entity.
    
    **Scenario:** Consider a relationship between a *person* and their *passport*.
    
    * A person may or may not have a passport
        
    * A passport can only belong to one person.
        
3. One-to-many relationship (`1 : N`)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551592134/39c3a239-ef00-49ce-9bae-4c3a391cb8b6.png align="center")
    
    **A one-to-many (1:N)** relationship is when one entity has many relationships with another entity.
    
    **Scenario:** Consider the relationship between a *customer* and their *orders*.
    
    * One customer can have multiple orders.
        
    * Each order can only have only one customer.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551856512/724528c3-84c4-436a-9d24-8f9b0e9b21fc.png align="center")
    
4. One-to-one-or-more relationship (`1 : 1..N`)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551608093/54f1a07d-5bd5-4930-982a-4953b07bdb07.png align="center")
    
    **A one-to-one-or-more (1:1..N)** relationship is where one entity has one or more relationships with another entity.
    
    **Scenario:** Consider the relationship between a *programmer* and their *laptops*.
    
    * A programmer could have one or more laptops.
        
    * Each laptop can only belong to one programmer.
        
5. One-to-zero-or-more relationship (`1 : 0..N`)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551625754/fe0a58aa-0e2c-40d2-ac3d-c7be828b03d7.png align="center")
    
    A **one-to-zero-or-more (1:0..N)** relationship is where one entity has zero or more relationships with another entity.
    
    **Scenario:** Consider the relationship between a person and their cars.
    
    * A person could own zero or more cars.
        
    * Each car can only belong to one person.
        
6. Many-to-many relationship (`N : N`)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551299103/14096bac-b005-4a60-a0f6-2c83ed11987a.png align="center")
    
    A **many-to-many (N:N)** relationship is when two entities have many relationships with each other.
    
    **Scenario:** Consider the relationship between *programmers* and the *programming languages* they know.
    
    * A programmer can know multiple programming languages.
        
    * A programming language can be known by multiple programmers.
        
7. One-or-more-to-one-or-more relationship (`1..N : 1..N`)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551346773/da3abc0a-63d1-423e-8cf5-b768e537c989.png align="center")
    
    A **one-or-more-to-one-or-more relationship (**`1..N : 1..N`**)** relationship signifies that one entity is connected to one or more instances of another entity, and vice versa.
    
    **Scenario:** Consider the relationship between a *seller* and *products* in an online marketplace
    
    * A *seller* can offer *one or more products*
        
    * Each *product* may be sold by one or *multiple sellers*.
        
8. Zero-or-more-to-zero-or-more relationship (`0..N : 0..N`)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551368782/7cb222d7-715e-4ea0-b940-958b3b3bb9d5.png align="center")
    
    A **zero-or-more-to-zero-or-more (0..N:0..N)** relationship is where one entity has zero or more relationships with many other entities and vice versa.
    
    **Scenario:** Consider the relationship between a *product* and *category* in an e-commerce application.
    
    * A *product* can belong to *zero or more categories*.
        
    * Each *category* can contain *zero or more products.*
        

## Conclusion

In this article, we have learned how to do database design using ERD. We have discussed the basics of ERD, the Crow Foot Notation, and the different types of relationships that can exist between entities. We have also seen some examples of how to represent these relationships graphically using ERD symbols.

We hope you have enjoyed this article and learned something new. If you have any questions or feedback, please feel free to leave a comment below. Thank you for reading!