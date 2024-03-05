# DBMS - Concepts & Terminology

## A.C.I.D
**ACID** is a set of properties that ensure database transactions are processed reliably. It stands for Atomicity, Consistency, Isolation, and Durability:

- **Atomicity** ensures that each transaction is treated as a single unit, which either completes in its entirety or is rolled back (i.e., it does not occur at all), ensuring no partial transactions.
- **Consistency** guarantees that database transactions move the database from one valid state to another, maintaining all predefined rules, such as unique keys, foreign keys, and constraints.
- **Isolation** ensures that concurrently executed transactions do not affect each other’s execution. This property ensures that transactions are securely isolated until they are completed, preventing concurrent transactions from interfering with each other.
- **Durability** guarantees that once a transaction has been committed, it will remain so, even in the event of power loss, crashes, or errors. This means the changes made by the transaction are permanently stored in the database.

These properties are crucial for the reliability of database systems, ensuring data integrity and consistency despite errors, crashes, or concurrent transactions.

# 