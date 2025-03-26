# Inventory Management System - SQL Project 
![image_fka6zlUH_1742971548687_raw](https://github.com/user-attachments/assets/08e90558-cc5c-4b31-b5c9-b5b45c38d2e0)

## 1. Introduction
The Inventory Management System is a database-driven solution designed to efficiently manage product inventory, supplier details, customer orders, and stock levels. This system ensures seamless tracking of products, suppliers, customers, and orders while automating stock updates and purchase order generation.
## Key Features:
- Supplier Management – Store and retrieve supplier details.

- Product Management – Track product details, categories, and pricing.

- Customer Management – Maintain customer records.

- Order Processing – Handle customer orders and update stock.

- Stock Management – Monitor stock levels and generate purchase orders when stock falls below reorder levels.

- Automated Triggers & Procedures – Ensure data consistency and automate workflows.

## 2. Database Schema
The system consists of 5 main tables:

**1. SUPPLIER Table**
     - Stores supplier details.

     - Fields: SID (PK), SNAME, SADD, SCITY, SPHONE, EMAIL.

**2. PRODUCT Table**
     - Contains product information.

     - Fields: PID (PK), PDESC, PRICE, CATEGORY, SID (FK).

**3. STOCK Table**
    - Tracks stock levels.
    
    - Fields: PID (FK), SQTY, ROL (Reorder Level), MOQ (Minimum Order Quantity).

**4. CUST Table**
    - Stores customer details.
    
    - Fields: CID (PK), CNAME, ADDRESS, CITY, PHONE, EMAIL, DOB.

**5. ORDERS Table**
    - Records customer orders.
    
    - Fields: OID (PK), ODATE, CID (FK), PID (FK), OQTY.

**6. PURCHASE Table** 
    - Automatically generates purchase orders when stock is low.
    
    - Fields: PID, SID, PQTY, DOP (Date of Purchase).

 ## 3. Key Functionalities
**A. Auto-Generated IDs** 

A function fn1() generates 5-character alphanumeric IDs (e.g., S0001, P0002).

**B. Stored Procedures**

1.ADDSUPPLIER – Adds a new supplier.

2.ADDPRO – Adds a new product.

3.ADDCUST – Adds a new customer.

4.ADDORDER – Places an order with auto-generated OID and current date.

**C. Triggers**

1.TR_IN_ORD – Updates stock when an order is placed.

- Rejects orders if stock is insufficient.

2.TR_UP_ORD – Adjusts stock when order quantity is modified.

3.TR_UP_STK – Automatically generates a purchase order in the PURCHASE table if stock falls below the reorder level (ROL).

**D. Reports**

1.Daily Report – Shows transactions for the current day.

2.Bill Generation – Generates a bill for a given order.

3.Customer Ledger – Lists all transactions by a customer.

4.Supplier Report – Displays products supplied by a given supplier.

**4. Workflow**

**Order Placement & Stock Management**

1.A customer places an order.

2.The system checks stock availability.

- If stock is sufficient:

    - Order is accepted.
  
    - Stock is reduced.

- If stock is insufficient:

   - Order is rejected.

3.If stock falls below the reorder level (ROL), a purchase order is automatically generated in the PURCHASE table.  

**Automatic Purchase Order Generation**
- When stock (SQTY) ≤ reorder level (ROL), the system:

    - Fetches MOQ (Minimum Order Quantity).
    
    - Records PID, SID, PQTY, and current date (DOP) in the PURCHASE table.

## 5. Sample Queries & Outputs

**1. Display Product & Supplier Details**

```
SELECT P.PID, P.PDESC, P.CATEGORY, S.SNAME, S.SCITY
FROM PRODUCT P
INNER JOIN SUPPLIER S ON P.SID = S.SID;
```

**2. Generate a Bill for Order O0001**
```
EXEC pc_BILL 'O0001';
```
- The created Stored Procedure on Bill Table i.e pc_BILL generates the bill for any given Order ID.

**3. Daily Transaction Report**
```
EXEC pc_Daily_report;
```
- The created Stored Procedure pc_Daily_report shows all transactions on daily basis.

**4. Supplier Report (S0001)**
```
EXEC pc_supplier_report 'S0001';
```
- The created Stored Procedure pc_supplier_report shows the details of all the suppliers and the their products that they supply.

## 6. Conclusion

This Inventory Management System efficiently handles:

✔ Supplier & Product Management

✔ Customer Order Processing

✔ Automated Stock Updates

✔ Purchase Order Generation

✔ Reporting & Analytics

The use of triggers, stored procedures, and auto-generated IDs ensures data integrity and workflow automation, making it a robust solution for businesses.


 
     
