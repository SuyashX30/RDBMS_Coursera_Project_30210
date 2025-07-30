# Retail Sales Database Schema

This PostgreSQL schema defines a retail sales database designed to track customers, products, sales transactions, and staff operations across multiple sales outlets. The schema was auto-generated using pgAdmin 4's ERD tool.

## 🧱 Database Structure

The database consists of the following main entities:

### 1. `customer`
Stores information about customers.

- **Primary Key**: `customer_id`
- **Attributes**: `customer_name`, `email`, `reg_date`, `card_number`, `date_of_birth`, `gender`

---

### 2. `product`
Details of products available for sale.

- **Primary Key**: `product_id`
- **Foreign Key**: `product_type_id → product_type.product_type_id`
- **Attributes**: `product_name`, `description`, `product_price`

---

### 3. `product_type`
Defines categories and types of products.

- **Primary Key**: `product_type_id`
- **Attributes**: `product_type`, `product_category`

---

### 4. `sales_transaction`
Records sales transactions that occur at sales outlets.

- **Primary Key**: `transaction_id`
- **Foreign Keys**: 
  - `sales_outlet_id → sales_outlet.sales_outlet_id`
  - `staff_id → staff.staff_id`
  - `customer_id → customer.customer_id`
- **Attributes**: `transaction_date`, `transaction_time`

---

### 5. `sales_detail`
Line-item detail of each product sold in a transaction.

- **Primary Key**: `sales_detail_id`
- **Foreign Keys**:
  - `transaction_id → sales_transaction.transaction_id`
  - `product_id → product.product_id`
- **Attributes**: `quantity`, `price`

---

### 6. `sales_outlet`
Represents physical sales locations.

- **Primary Key**: `sales_outlet_id`
- **Attributes**: `sales_outlet_type`, `address`, `city`, `telephone`, `postal_code`, `manager`

---

### 7. `staff`
Information about store employees.

- **Primary Key**: `staff_id`
- **Attributes**: `first_name`, `last_name`, `position`, `start_date`, `location`

---

## 🔗 Relationships

- **One-to-Many**: 
  - `product_type` → `product`
  - `product` → `sales_detail`
  - `sales_transaction` → `sales_detail`
  - `customer` → `sales_transaction`
  - `sales_outlet` → `sales_transaction`
  - `staff` → `sales_transaction`

## 🛠 Installation & Usage

1. Ensure you have PostgreSQL installed.
2. Use pgAdmin 4 or psql CLI to execute the script:
   ```bash
   psql -U your_username -d your_database -f schema.sql
