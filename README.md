# ER-Diagrams

# 📦 Instagram Thrift Creator Store

## 🧾 Project Overview
This project represents the database design of a small Instagram-based thrift and handmade product store. Initially, orders are managed through DMs and WhatsApp, but as the business grows, a structured system is required to manage:

- Customers  
- Products (Thrift & Handmade)  
- Inventory  
- Orders  
- Payments  
- Shipping  

This ER model provides a scalable backend structure to handle all these operations efficiently.

---

## 🧑‍💻 Entities & Tables Explanation

### 👤 Customers
Stores user-related information.

**Fields:**
- `id` (Primary Key)
- `username`, `email`, `password`
- `address`, `phone_number`
- `access_token`, `refresh_token`, `reset_token`
- `createdAt`, `updatedAt`

👉 Used for authentication and order placement.

---

### 🛍️ Products
Stores all product details.

**Fields:**
- `id` (Primary Key)
- `name`, `price`, `size`, `color`
- `condition`
- `rating`
- `type` → `thrift` or `handmade`
- `createdAt`

---

### 📦 Inventory
Tracks stock of each product.

**Fields:**
- `id` (Primary Key)
- `product_id` (Foreign Key → Products)
- `quantity`

👉 Helps avoid overselling.

---

### 🛒 Orders
Stores customer orders.

**Fields:**
- `id` (Primary Key)
- `customer_id` (Foreign Key → Customers)
- `status` → `pending`, `shipped`, `delivered`, `cancelled`
- `total_amount`
- `createdAt`

---

### 📋 Ordered Items
Stores products inside each order.

**Fields:**
- `id` (Primary Key)
- `customer_id` (FK)
- `order_id` (FK → Orders)
- `product_id` (FK → Products)
- `quantity`, `price`

👉 Resolves **many-to-many relationship** between Orders and Products.

---

### 💳 Payments
Handles payment information.

**Fields:**
- `id` (Primary Key)
- `order_id` (Foreign Key → Orders)
- `amount`
- `payment_method`
- `transaction_id`
- `status` → `pending`, `completed`, `failed`
- `createdAt`

---

### 🚚 Shipping
Tracks delivery details.

**Fields:**
- `id` (Primary Key)
- `order_id` (Foreign Key → Orders)
- `shipping_status` → `processing`, `shipped`, `delivered`
- `delivery_date`

---

### 🎨 Handmade Products
Stores extra info for handmade items.

**Fields:**
- `id` (Primary Key)
- `product_id` (FK → Products)
- `quantity`

---

### ♻️ Thrift Products
Stores extra info for thrift items.

**Fields:**
- `id` (Primary Key)
- `product_id` (FK → Products)
- `quantity`

---

## 🔗 Relationships Explanation

### 1. Customer → Orders (1:N)
- One customer can place multiple orders  
- `customers.id < orders.customer_id`

---

### 2. Orders → OrderedItems (1:N)
- One order can have multiple orderedItems  
- `orders.id < orderedItems.order_id`

---

### 3. Products → OrderedItems (1:N)
- One product can be part of many orderedItems  
- `products.id < orderedItems.product_id`

👉 This creates a **many-to-many relationship** between Orders and Products.

---

### 4. Orders → Payments (1:1)
- Each order has one payment  
- `orders.id - payments.order_id`

---

### 5. Orders → Shipping (1:1)
- Each order has shipping details  
- `orders.id - shipping.order_id`

---

### 6. Products → Inventory (1:1)
- Each product has stock information  
- `inventory.product_id < products.id`

---

### 7. Products → Type-Based Tables
- If `type = handmade` → data goes to `handmade_product`
- If `type = thrift` → data goes to `thrift_product`

---

## 🧠 Key Design Concepts Used

- ✅ Normalization  
- ✅ Foreign Keys  
- ✅ ENUMs for controlled values  
- ✅ Many-to-Many relationship handling  
- ✅ Scalable design  

---

## 🚀 Real-World Flow

1. Customer signs up  
2. Browses products  
3. Places an order  
4. Order items stored in `orderedItems`  
5. Payment processed  
6. Shipping tracked  
7. Inventory updated  

---

## 📌 Conclusion
This ER design transforms a small Instagram-based store into a structured and scalable e-commerce system. It ensures proper handling of orders, payments, inventory, and customer data.
