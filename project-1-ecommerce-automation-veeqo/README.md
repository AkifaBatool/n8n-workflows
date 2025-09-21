# 📦 Project 1: Veeqo → Google Sheets Order Sync

## 🧩 The Business Problem
E-commerce teams often manage multiple stores and sales channels. Exporting orders and shipment data manually from Veeqo and maintaining monthly reports in spreadsheets is tedious, error-prone, and wastes valuable time.

---

## 🚀 The Automated Solution
This workflow fully automates the process:
- Fetches **store names and channels** from the Veeqo API
- Iterates through each store to pull **orders & shipment tracking data**
- Cleans and formats the raw API response using Code nodes
- Checks if the **monthly Google Sheet** already exists
  - If yes → update existing rows, avoid duplicates, and append new data
  - If no → create a new monthly sheet automatically

---

## 🔄 Workflow Flow
1. **Trigger**: Scheduled daily with Cron  
2. **Fetch Stores**: Call Veeqo API → list all stores & channels  
3. **Loop Stores**: For each store, fetch order & shipment data  
4. **Transform Data**: Code node → extract key fields (order ID, store name, customer, date, shipment status)  
5. **Check Sheet**: Google Sheets node → ensure monthly sheet exists  
6. **Upsert Data**: Append new rows, update existing ones  

---

## 🛠 Tools & Nodes
- **Cron** – automation schedule  
- **HTTP Request** – connect to Veeqo API  
- **Code** – transform API response  
- **Google Sheets** – data storage & reporting  

---

## 💻 Pseudocode Example
```js
// Transformation logic (simplified pseudocode)
for each order in orders:
    record = {
        id: order.id,
        store: order.store_name,
        customer: order.customer.name,
        date: format(order.created_at),
        status: order.shipment.status
    }
    add record to results
return results
