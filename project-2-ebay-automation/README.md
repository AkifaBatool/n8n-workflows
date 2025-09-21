# 🛒 Project 2: eBay Store Management Automation

## 🧩 The Business Problem
Managing multiple eBay stores requires juggling:
- Expiring API tokens
- Large volumes of orders
- Inventory tracking
- Financial payout records

Doing this manually is overwhelming and risky — one missed token refresh can break the entire reporting pipeline.

---

## 🚀 The Automated Solution
This workflow handles **complete eBay store management**:
- Refreshes and manages tokens in a dedicated **sub-workflow**
- Iterates through all connected eBay stores
- Fetches:
  - **Orders**
  - **Inventory**
  - **Payouts**
- Cleans & transforms data using Code nodes
- Stores results in **monthly segregated sheets/folders**
- Updates existing data, appends new data when needed

---

## 🔄 Workflow Flow
1. **Trigger**: Cron (daily or weekly)  
2. **Sub-workflow**: Refresh access tokens automatically  
3. **Loop Stores**: For each store → fetch orders, inventory, payouts  
4. **Transform Data**: Use Code nodes to structure the response  
5. **Store Data**: Save in separate files/folders by month  

---

## 🛠 Tools & Nodes
- **Sub-workflow** – token refresh  
- **HTTP Request** – eBay API calls (orders, inventory, payouts)  
- **Code** – data transformation  
- **Google Sheets / File Node** – monthly storage  

---

## 💻 Pseudocode Example
```js
// Token refresh logic
if (now > access_token_expiry) {
    access_token = refreshAccessToken(refresh_token)
}
return access_token
