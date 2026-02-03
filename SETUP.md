# 🚀 Setup Guide: Shopify-Zoho Refund Automation

Complete step-by-step guide to set up the Shopify-Zoho Inventory Refund Automation system.

## 📋 Table of Contents

- [Prerequisites](#prerequisites)
- [Part 1: Shopify Setup](#part-1-shopify-setup)
- [Part 2: Zoho Inventory Setup](#part-2-zoho-inventory-setup)
- [Part 3: Zoho Flow Setup](#part-3-zoho-flow-setup)
- [Part 4: Custom Functions](#part-4-custom-functions)
- [Part 5: Testing](#part-5-testing)
- [Part 6: Going Live](#part-6-going-live)
- [Troubleshooting](#troubleshooting)

---

## ✅ Prerequisites

### Required Accounts

| **Service** | **Plan Required** | **Sign Up Link** | **Cost** |
|-------------|-------------------|------------------|----------|
| Shopify | Basic or higher | [shopify.com](https://www.shopify.com) | From $29/month |
| Zoho Inventory | Free or higher | [zoho.com/inventory](https://www.zoho.com/inventory/) | Free up to 50 orders/month |
| Zoho Flow | Free or higher | [zoho.com/flow](https://www.zoho.com/flow/) | Free (5 flows, 1000 tasks/month) |

### Technical Requirements

- [ ] Admin access to Shopify store
- [ ] Zoho Inventory organization created
- [ ] Basic understanding of automation workflows
- [ ] Email account for notifications

### Estimated Setup Time

- **First-time setup**: 60-90 minutes
- **Experienced users**: 30-45 minutes

---

## 🛒 Part 1: Shopify Setup

### Step 1.1: Create Private App (API Access)

1. **Login to Shopify Admin**
   ```
   https://your-store.myshopify.com/admin
   ```

2. **Navigate to Settings**
   ```
   Bottom left → Settings → Apps and sales channels
   ```

3. **Develop Apps**
   ```
   Click "Develop apps" → "Create an app"
   ```

4. **App Configuration**
   ```
   App name: Zoho Flow Integration
   App developer: Your Name
   ```

5. **Configure API Scopes**
   
   Enable these permissions:
   ```
   ✅ read_orders (View orders)
   ✅ read_products (View products)
   ✅ read_customers (View customers)
   ✅ read_refunds (View refunds)
   ```

6. **Install App**
   ```
   Click "Install app" → Confirm
   ```

7. **Get API Credentials**
   ```
   API Key: [Copy and save securely]
   API Secret Key: [Copy and save securely]
   Access Token: [Copy and save securely]
   ```

   **⚠️ IMPORTANT**: Store these credentials in a password manager. You won't see them again!

### Step 1.2: Test Shopify API

Test your API access with a simple call:

```bash
curl -X GET \
  'https://your-store.myshopify.com/admin/api/2024-01/orders.json' \
  -H 'X-Shopify-Access-Token: YOUR_ACCESS_TOKEN' \
  -H 'Content-Type: application/json'
```

**Expected Response:**
```json
{
  "orders": [
    {
      "id": 1234567890,
      "name": "#1001",
      ...
    }
  ]
}
```

---

## 📦 Part 2: Zoho Inventory Setup

### Step 2.1: Create Organization

1. **Login to Zoho Inventory**
   ```
   https://inventory.zoho.in
   ```

2. **Create Organization**
   ```
   Settings → Organizations → Add Organization
   ```

3. **Organization Details**
   ```
   Name: Your Company Name
   Industry: E-commerce / Retail
   Time Zone: Select your timezone
   Currency: Your currency (e.g., INR, USD)
   ```

4. **Get Organization ID**
   ```
   Settings → Organization Profile
   Copy the Organization ID (e.g., "demo2mtabtechnology")
   ```

### Step 2.2: Add Sample Products

1. **Navigate to Items**
   ```
   Inventory → Items → + New
   ```

2. **Create Test Products**
   
   Example Product 1:
   ```
   Name: Red Tasty Strawberries
   SKU: ST-BERRIES001
   Type: Goods
   Unit: kg
   Selling Price: ₹1,000
   Stock: 100 kg
   ```

   Example Product 2:
   ```
   Name: Delicious Wild Orange for Smoothies - Frozen
   SKU: CIT-ORG0002
   Type: Goods
   Unit: kg
   Selling Price: ₹500
   Stock: 150 kg
   ```

3. **Add Products to Shopify**
   
   Sync these products to your Shopify store:
   - Use **same SKU** in both systems
   - Match product names
   - Keep pricing consistent

### Step 2.3: Create Test Customer

```
Contacts → Customers → + New
Name: Test Customer
Email: test@example.com
Phone: +91-1234567890
```

### Step 2.4: Create Test Sales Order

```
Sales → Sales Orders → + New

Customer: Test Customer
Date: Today
Reference Number: 1167 (match with Shopify order #1167)

Line Items:
  1. Red Tasty Strawberries - 45 kg @ ₹1,000 = ₹45,000

Total: ₹45,000
Status: Draft → Convert to Confirmed
```

### Step 2.5: Generate API Client

1. **Navigate to Developer Space**
   ```
   Settings → Developer Space → Zoho API Console
   ```
   Or visit: https://api-console.zoho.in

2. **Create Server-based Application**
   ```
   Add Client → Server-based Applications
   
   Client Name: Shopify Integration
   Client Domain: your-domain.com (or localhost for testing)
   Authorized Redirect URIs: https://your-domain.com/callback
   ```

3. **Note Credentials**
   ```
   Client ID: [Copy]
   Client Secret: [Copy]
   ```

4. **Generate Refresh Token**
   
   Visit:
   ```
   https://accounts.zoho.in/oauth/v2/auth?scope=ZohoInventory.salesorders.READ,ZohoInventory.salesorders.CREATE,ZohoInventory.salesreturns.READ,ZohoInventory.salesreturns.CREATE&client_id=YOUR_CLIENT_ID&response_type=code&access_type=offline&redirect_uri=YOUR_REDIRECT_URI
   ```
   
   Authorize and get the code, then exchange for refresh token:
   ```bash
   curl -X POST \
     'https://accounts.zoho.in/oauth/v2/token' \
     -d 'code=YOUR_CODE' \
     -d 'client_id=YOUR_CLIENT_ID' \
     -d 'client_secret=YOUR_CLIENT_SECRET' \
     -d 'redirect_uri=YOUR_REDIRECT_URI' \
     -d 'grant_type=authorization_code'
   ```

---

## 🔄 Part 3: Zoho Flow Setup

### Step 3.1: Create New Flow

1. **Login to Zoho Flow**
   ```
   https://flow.zoho.com
   ```

2. **Create Flow**
   ```
   Click "+ Create Flow"
   Name: Shopify Refund to Zoho Sales Return
   Description: Automates sales return creation when refunds are processed in Shopify
   Folder: Automations
   ```

### Step 3.2: Configure Trigger

1. **Add Trigger**
   ```
   Click "+" → Apps → Shopify
   ```

2. **Select Trigger**
   ```
   Trigger: Refund created
   ```

3. **Connect Shopify**
   ```
   Connection Name: Shopify API connection
   Store URL: your-store.myshopify.com
   API Key: [Your API Key]
   Password: [Your Access Token]
   
   Test Connection → Success ✓
   ```

4. **Test Trigger**
   ```
   Click "Fetch Sample Data"
   → Create a test refund in Shopify
   → Verify data received
   ```

   **Expected Fields:**
   - `order_id`
   - `refund_id`
   - `refund_line_items`
   - `customer_email`
   - `created_at`

### Step 3.3: Add Action - Fetch Order

1. **Add Action**
   ```
   Click "+" → Apps → Shopify → Fetch order
   ```

2. **Configure**
   ```
   Connection: [Same as trigger]
   Order ID: ${trigger.order_id}
   Variable Name: fetchOrder_1
   ```

3. **Test**
   ```
   Click "Fetch Sample" → Verify order details
   ```

### Step 3.4: Add Action - Search Sales Order

1. **Add Action**
   ```
   Click "+" → Apps → Zoho Inventory → Search APIs
   ```

2. **Connect Zoho Inventory**
   ```
   Connection Name: Zoho Inventory connection
   Data Center: IN (or your data center)
   
   Authorize → Allow access → Success ✓
   ```

3. **Configure Search**
   ```
   API Name: salesorders
   Organization ID: [Your Org ID]
   
   Filters:
   - Field: reference_number
   - Condition: is
   - Value: ${removeHash_2}  [We'll create this function next]
   
   Variable Name: Searchapi
   ```

### Step 3.5: Add Custom Function - removeHashFromID

1. **Create Function**
   ```
   Left sidebar → Custom Functions → + Custom Function
   ```

2. **Function Details**
   ```
   Name: removeHashFromID
   Description: Removes # from Shopify order names
   ```

3. **Add Parameter**
   ```
   Name: input_string
   Type: string
   Description: Shopify order name with #
   ```

4. **Add Code**
   ```deluge
   string removeHash(string input_string)
   {
       if(input_string.startsWith("#"))
       {
           return input_string.subString(1);
       }
       return input_string;
   }
   ```

5. **Test Function**
   ```
   Test Input: "#1167"
   Expected Output: "1167"
   Run Test → Success ✓
   ```

6. **Add to Flow**
   ```
   In your flow, before "Search Sales Order" action:
   
   Click "+" → Custom Functions → removeHashFromID
   Input: ${fetchOrder_1.name}
   Output Variable: removeHash_2
   ```

### Step 3.6: Add Action - Fetch Full Sales Order

1. **Add Action**
   ```
   Click "+" → Apps → Zoho Inventory → Fetch sales order
   ```

2. **Configure**
   ```
   Connection: [Zoho Inventory connection]
   Organization ID: [Your Org ID]
   Sales Order ID: ${Searchapi.salesorders[0].salesorder_id}
   Variable Name: fetchSalesOrder_4
   ```

### Step 3.7: Add Custom Function - prepareSalesReturnAPI

1. **Create Function**
   ```
   Custom Functions → + Custom Function
   Name: prepareSalesReturnAPI
   Description: Processes refund and creates sales return
   ```

2. **Add Parameters**
   ```
   1. salesorder_id (string) - Zoho sales order ID
   2. organization_id (string) - Zoho org ID
   3. refund_line_items (list) - Shopify refund items
   4. sales_order_line_items (list) - Zoho sales order items
   ```

3. **Add Code**
   
   Copy the entire code from:
   ```
   functions/prepareSalesReturnAPI.ds
   ```
   
   (600+ lines - available in the GitHub repository)

4. **Test Function**
   ```
   Use sample data from previous actions
   Run Test → Verify output includes:
   - status: "success"
   - return_number: "RET-00214"
   - email_message: [HTML content]
   ```

5. **Add to Flow**
   ```
   Click "+" → Custom Functions → prepareSalesReturnAPI
   
   Inputs:
   - salesorder_id: ${fetchSalesOrder_4.salesorder_id}
   - organization_id: "your_org_id"
   - refund_line_items: ${trigger.refund_line_items}
   - sales_order_line_items: ${fetchSalesOrder_4.line_items}
   
   Output Variable: prepareSalesReturnAPI_3
   ```

### Step 3.8: Add Action - Send Email

1. **Add Action**
   ```
   Click "+" → Apps → Send Email
   ```

2. **Configure Email**
   ```
   Connection: [Default email or custom SMTP]
   
   From: noreply@yourdomain.com
   To: ${fetchOrder_1.customer.email}
   CC: sales@yourdomain.com
   Subject: Sales Return Created - ${prepareSalesReturnAPI_3.return_number}
   
   Body Type: HTML
   Body: ${prepareSalesReturnAPI_3.email_message}
   ```

3. **Test Email**
   ```
   Send Test Email → Check inbox ✓
   ```

### Step 3.9: Add Decision Logic (Optional)

Add error handling:

```
After prepareSalesReturnAPI_3:

Add Decision:
  Condition: ${prepareSalesReturnAPI_3.status} equals "success"
  
  If YES:
    → Send Email (success notification)
  
  If NO:
    → Send Email (error notification to admin)
    Subject: "Sales Return Failed - Order ${fetchOrder_1.name}"
    Body: ${prepareSalesReturnAPI_3.message}
```

---

## 🧪 Part 4: Testing

### Test Scenario 1: Basic Refund

**Setup:**
1. Create a fulfilled order in Shopify
2. Add products with matching SKUs in Zoho

**Steps:**
1. Go to Shopify order
2. Click "Refund"
3. Select items and quantity
4. Submit refund

**Expected Results:**
- ✅ Zoho Flow triggers within 30 seconds
- ✅ Sales return created in Zoho Inventory
- ✅ Email sent to customer
- ✅ All quantities match

### Test Scenario 2: Partial Refund

**Setup:**
- Order: 10 items
- Already returned: 3 items
- New refund: 5 items

**Expected:**
- ✅ System allows return of 5 items (7 available)
- ✅ Sales return shows correct quantities
- ✅ Email shows remaining: 2 items

### Test Scenario 3: Full Return

**Setup:**
- Order: 10 items
- Already returned: 10 items
- New refund: 5 items (mistake)

**Expected:**
- ✅ System skips the item
- ✅ Email shows "Items That Could Not Be Returned"
- ✅ No error, graceful handling

### Test Scenario 4: SKU Not Found

**Setup:**
- Refund item SKU: "NEW-PRODUCT-001"
- Not in sales order

**Expected:**
- ✅ Item skipped
- ✅ Logged in skipped items section
- ✅ Other items processed normally

---

## 🚀 Part 5: Going Live

### Pre-Launch Checklist

- [ ] All test scenarios pass
- [ ] Error handling tested
- [ ] Email templates finalized
- [ ] Team trained on new process
- [ ] Documentation updated
- [ ] Backup plan ready

### Activation Steps

1. **Final Testing**
   ```
   Run 5-10 test refunds
   Verify 100% success rate
   Check all emails received
   ```

2. **Enable Flow**
   ```
   Zoho Flow → Your Flow
   Toggle: OFF → ON
   Status: Active ✓
   ```

3. **Monitor First Day**
   ```
   Watch execution logs
   Check for errors
   Verify sales returns in Zoho
   Collect team feedback
   ```

4. **Performance Tracking**
   ```
   Day 1: Monitor every execution
   Week 1: Daily review
   Month 1: Weekly review
   Ongoing: Monthly audit
   ```

### Rollback Plan

If issues occur:

```
1. Disable Flow (toggle OFF)
2. Process refunds manually
3. Debug the issue
4. Fix and test
5. Re-enable Flow
```

---

## 🔧 Troubleshooting

### Common Issues

#### Issue 1: "Sales Order Not Found"

**Symptoms:**
- Flow fails at Search Sales Order step
- Error: "No records found"

**Solutions:**
1. Check reference number matches:
   ```
   Shopify Order: #1167
   Zoho Reference: 1167
   ```

2. Verify removeHashFromID function works:
   ```
   Test input: "#1167"
   Expected: "1167"
   ```

3. Check sales order exists in Zoho
4. Verify organization ID is correct

#### Issue 2: "SKU Mismatch"

**Symptoms:**
- Items skipped in email
- "SKU not found in sales order"

**Solutions:**
1. Ensure SKUs match exactly:
   ```
   Shopify SKU: ST-BERRIES001
   Zoho SKU: ST-BERRIES001
   (Case-sensitive!)
   ```

2. Check for extra spaces or special characters
3. Update products in both systems

#### Issue 3: "API Rate Limit Exceeded"

**Symptoms:**
- Flow fails intermittently
- Error: "429 Too Many Requests"

**Solutions:**
1. Add delay between actions:
   ```
   Zoho Flow → Add Delay (5 seconds)
   ```

2. Batch process refunds:
   ```
   Instead of: Real-time trigger
   Use: Scheduled trigger (every 15 minutes)
   ```

3. Upgrade Zoho Flow plan (higher limits)

#### Issue 4: "Email Not Received"

**Symptoms:**
- Sales return created
- No email received

**Solutions:**
1. Check spam folder
2. Verify email address in Shopify
3. Test email action separately
4. Check email service limits
5. Verify SMTP settings (if using custom)

#### Issue 5: "Quantity Validation Failed"

**Symptoms:**
- Error: "Quantity exceeds available"
- Refund not processed

**Solutions:**
1. Check "Already Returned" quantity:
   ```
   Ordered: 45
   Returned: 40
   Available: 5
   Refund Request: 10 ❌
   ```

2. Update function to cap at available:
   ```deluge
   if(returnQty > availableToReturn)
   {
       returnQty = availableToReturn;
   }
   ```

#### Issue 6: "API Authentication Failed"

**Symptoms:**
- "Invalid credentials"
- "Token expired"

**Solutions:**
1. Regenerate access token (Shopify)
2. Refresh OAuth token (Zoho)
3. Re-authenticate connections
4. Check API scopes/permissions

---

## 📊 Performance Monitoring

### Key Metrics to Track

```
Weekly Report:
├─ Total refunds processed: X
├─ Success rate: XX%
├─ Average processing time: XX seconds
├─ Errors encountered: X
└─ Time saved: XX minutes
```

### Zoho Flow Analytics

1. **Execution History**
   ```
   Flow → History
   - View all executions
   - Filter by status (success/failed)
   - Download logs
   ```

2. **Performance Dashboard**
   ```
   Analytics → Create Dashboard
   
   Widgets:
   - Success Rate (last 30 days)
   - Execution Time Trend
   - Error Log
   - Volume Chart
   ```

---

## 💡 Best Practices

### 1. Regular Maintenance

```bash
# Weekly tasks
- Review error logs
- Test with sample data
- Update documentation
- Check API limits

# Monthly tasks
- Performance audit
- Team feedback session
- Update test cases
- Review and improve
```

### 2. Security

- [ ] Rotate API keys every 90 days
- [ ] Use environment variables for credentials
- [ ] Enable 2FA on all accounts
- [ ] Audit access logs
- [ ] Backup configurations

### 3. Optimization

- [ ] Cache frequently accessed data
- [ ] Batch similar operations
- [ ] Use webhooks instead of polling
- [ ] Minimize API calls
- [ ] Index Zoho Inventory fields

---

## 🆘 Getting Help

**Need assistance?**

1. **Documentation**: Re-read relevant sections
2. **Community**: GitHub Discussions
3. **Issues**: Report bugs on GitHub
4. **Email**: sohail@mtabtechnology.com
5. **Zoho Support**: support.zoho.com

---

## 🎉 Congratulations!

You've successfully set up the Shopify-Zoho Refund Automation!

**Next Steps:**
- Monitor first few executions
- Gather team feedback
- Document any custom changes
- Share your experience
- Star ⭐ the GitHub repository

---

<div align="center">

**Setup Guide v1.0**

Created by [Sohail (Kanishk)](https://github.com/Sohail-crdriod)

[Back to README](./README.md) • [Report Issue](https://github.com/Sohail-crdriod/shopify-zoho-refund-automation/issues)

</div>
