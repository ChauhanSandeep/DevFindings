# Database Design Using Entity Relationship Model

## Introduction

An Entity Relationship Diagram (ERD) is a graphical representation of the entities, relationships, and attributes that make up a system. It is commonly used to visually explain the structure of a system, and how the entities in the system interact with each other.

In this tutorial, we will discuss how we can do database design using an Entity relationship diagram. We will use Crow Feet annotations to describe the relationship between tables.

## Crow Feet Notations

Crow's Foot Notation is an extremely useful diagrammatic representation of the relationship between various entities. Through its lines and symbols, it can provide a clear and concise explanation of how two different entities interact with each other, as well as the cardinality of that relationship. This graphical representation is invaluable in helping to quickly grasp the complexities of a system, making it an essential tool for any database administrator.

### Basics

1. Relation between two tables is displayed by connecting these tables with connector lines
    
2. A perpendicular line on the connector line depicts one mandatory entry
    
3. A circle on the connector line depicts the optional entry.
    
4. A reverse arrow on the connector line depicts many entries.
    

## Database Modelling: Relationships

1. one-to-one relationship `1 : 1`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551152017/7a4c2950-e117-4325-af16-c1d0380adf46.png align="center")
    
    A one-to-one (1:1) relationship is when two entities have exactly one relationship with each other. For example, a one-to-one relationship could exist between a customer and their account in an e-commerce app. Each person can only have one bank account, and each account can belong to only one customer.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673547107686/192a18ef-6d6c-4767-813a-aa3f9382fcce.png align="center")
    
2. one-to-zero or one relationship `1 : 0..1`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551189988/5e798e38-25f9-4573-a249-98d121056a94.png align="center")
    
    A one-to-zero or one (1:0..1) relationship is where one entity has zero or one relationship with another entity.
    
    For example, a one-to-zero or one relationship could exist between a person and their passport. A person may or may not have a passport, and a passport can only belong to one person.
    
3. One-to-many relationship `1 : N`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551592134/39c3a239-ef00-49ce-9bae-4c3a391cb8b6.png align="center")
    
    A one-to-many (1:N) relationship is when one entity has many relationships with another entity.
    
    For example, a one-to-many relationship could exist between a customer and their orders. One customer can have multiple orders, while each order can only have one customer.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551856512/724528c3-84c4-436a-9d24-8f9b0e9b21fc.png align="center")
    
4. one-to-one and more relationship `1 : 1..N`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551608093/54f1a07d-5bd5-4930-982a-4953b07bdb07.png align="center")
    
    A one-to-one and more (1:1..N) relationship is where one entity has one or more relationships with another entity.
    
    For example, a one-to-one and more relationship could exist between a programmer and their laptops. A person could have one or more laptops, while each laptop can only belong to one programmer.
    
5. one-to-zero and more relationship `1 : 0..N`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551625754/fe0a58aa-0e2c-40d2-ac3d-c7be828b03d7.png align="center")
    
    A one-to-zero and more (1:0..N) relationship is where one entity has zero or more relationships with another entity.
    
    For example, a one-to-zero or more relationship could exist between a person and their cars. A person could own 0 or more cars, while each car can only belong to one person.
    
6. one-to-many relationship `N : N`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551299103/14096bac-b005-4a60-a0f6-2c83ed11987a.png align="center")
    
    A many-to-many (N:N) relationship is when two entities have many relationships with each other.
    
    For example, a many-to-many relationship could exist between a student and their clubs. A student can be a member of multiple clubs, while each club can have multiple members.
    
7. one or more to one or more relationship `1..N : 1..N`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551346773/da3abc0a-63d1-423e-8cf5-b768e537c989.png align="center")
    
    A `one or more to one or more (1..N:1..N)` relationship is where one entity has one or more relationships with many other entities.
    
    For example, `one or more to one or more` relationships could exist between a teacher and their students. A teacher can have one or more students, while each student can have multiple teachers.
    
8. zero or more to zero or more relationship `0..N : 0..N`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673551368782/7cb222d7-715e-4ea0-b940-958b3b3bb9d5.png align="center")
    
    A zero or more to zero or more (0..N:0..N) relationship is where one entity has zero or more relationships with many other entities.
    
    A zero or more to zero or more relationship could exist between a company and its suppliers. A company could have zero or more suppliers, while each supplier can provide services to multiple companies.