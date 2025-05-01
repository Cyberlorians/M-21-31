# 📘 M-21-31 PowerApp Install Guide

---

### **Required Items**
- **PowerBI Template File**
- **Excel Data File**
- **Power App Solution File**

---

### **Pre-Reqs** (Before starting the deployment)
1. **Dataverse Setup**: Ensure the Dataverse environment is correctly set up and accessible.
2. **Security Roles**: Verify security roles to ensure appropriate permissions for importing the solution.
3. **Power BI Workspace**: Ensure you have a Power BI Workspace to publish PBIX files to.
4. **Power BI Desktop App**: Install Power BI Desktop.

---

## **Power App (Part 1)**

### **1. Import Power Apps Solution**
- Navigate to the desired **Power Apps environment** where the solution will be imported.
- Go to **Solutions**, then click on **Import Solution**.
- Upload the **M2131 Solution Zip file**.

### **2. Import Data into Dataverse**
- From the same environment where the solution was imported, navigate to **Dataflows**.
- **Edit the dataflow**:
   - Click on the **EL0 Table**.
   - Click on the **Gear icon** next to the **Source Step**.
   - **Upload or browse** to the location of the `xxxxxx.xlsx` file.
   - **Configure the connection** to the file.
   - Click **Next**.
   - Click **Publish**.

---

### **3. Setup Security Roles**
There are two security roles:
- **Admin Role**: For users with full access.
- **Read-Only Role**: For users who only need to view data.
   
Any user needing access to the solution will require membership in one of these two roles.

---

### **4. Run Relationship Workflows**
- Navigate to the **Solution**.
- Click on **Flows**.
- Run both flows **once** to establish data relationships.

---

### **5. Get AppID / ORG URL and Test the App**
1. Navigate to the **Solution**.
2. Click on **Apps**.
3. **Play the M2131 App**.
   - **Note**: The initial PowerBI Report will fail to load. This is expected until the link is established.
4. **Grab the Org URL and App ID** from the URL for later use.

---

## **Power BI**

### **1. Setup PowerBI**
1. Open the **M2131-Dashboard-Template.pbit** file in **Power BI Desktop**.
2. Enter the **ORG URL** (without the `https://` and no trailing backslash). For example: `indencetest.crm9.dynamics.com`.
3. Enter the **AppID** from the URL you retrieved earlier.
4. Click **Load**.

---

### **2. Publish the Power BI File**
1. Once the data is loaded, **Publish** the file to your **Power BI Online Workspace**.
   - Click the **Publish** button.
   - Save the file to your preferred **local destination**.
   - Choose the **Workspace** to publish to.
   - Click **Select**.
   - On the success screen, click **Got It**.

---

## **Power App (Part 2)**

### **1. Setup the Dashboard**
1. Navigate to the **Solution** you imported earlier.
2. Click on **Dashboards**.
3. **Edit the M21-31 Compliance Management Dashboard**.
4. Update the **Workspace** and **Report** for the **Published M2131 Report** from the previous step.
5. Click **Save**.
6. Click **Publish**.

---

### **Summary of Key Steps**
1. **Import the Power App Solution** and **Data** into Dataverse.
2. **Set up Security Roles** and assign them to users.
3. **Run Relationship Workflows** to establish connections.
4. **Get Org URL and App ID** for Power BI integration.
5. **Configure Power BI** by opening the template, entering the details, and publishing.
6. **Set up and publish the Power App dashboard**.

---

### 🚨 **Important Notes**:
- The initial **Power BI Report** in the app will fail to load until it is linked with the correct App ID and Org URL.
- Ensure you have the **correct permissions** and **access roles** before proceeding with the deployment.

---

Let me know if you need any more adjustments!
