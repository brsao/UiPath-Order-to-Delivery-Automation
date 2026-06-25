# O2D - Order-to-Delivery Automation Workflow

## Project Description
O2D is a production-ready, end-to-end order fulfillment workflow built with UiPath Maestro BPMN. It solves the problem of fragmented order processing by orchestrating the entire order lifecycle—from receipt to delivery—using real API integrations and intelligent exception handling. 

The system automates order validation, checks real-time inventory via Supabase, processes secure payments via Stripe, manages human-in-the-loop quality checks, optimizes shipping via Easyship, and sends customer notifications via Resend.

## UiPath Components Used
*   **UiPath Maestro BPMN:** Used for end-to-end process modeling, orchestration, and execution.
*   **UiPath API Workflows:** Used to build custom REST API integrations for Supabase, Stripe, Easyship, and Resend.
*   **UiPath Automation Cloud:** Used for deployment, debugging, and running the solution.
*   **UiPath Studio:** Used for designing the BPMN diagrams and API workflows.

## Agent Type
This solution utilizes **Low-code Agents (UiPath API Workflows)** orchestrated by **Maestro BPMN**. 
*(Note: While LLM-based agents were explored during development, API workflows were chosen for inventory and payment tasks to ensure deterministic, production-grade reliability. Human-in-the-loop tasks are used for quality approval and exception handling.)*

## Setup Instructions

### Prerequisites
1.  **UiPath Automation Cloud Account:** Access to UiPath Studio and Maestro.
2.  **Supabase Account:** For the inventory database.
3.  **Stripe Account:** For payment processing (Test Mode keys).
4.  **Easyship Account:** For shipping rates and label generation.
5.  **Resend Account:** For transactional email sending.

### Step 1: Database Setup (Supabase)
1. Create a new Supabase project.
2. Create a table named `inventory` with columns: `id` (uuid), `productId` (text), `productName` (text), `quantity` (int), `unitPrice` (float).
3. Insert test data (e.g., `ITEM-001`, `Widget A`, `150`, `25.99`).
4. Copy your **Supabase URL** and **Service Role Key** (or anon key with RLS policies enabled).

### Step 2: API Integrations
1. **Stripe:** Get your Publishable Key and Secret Key from the Stripe Dashboard (Test Mode).
2. **Easyship:** Get your API Token from the Easyship Developer portal.
3. **Resend:** Get your API Key from the Resend dashboard and verify your sending domain.

### Step 3: UiPath Configuration
1. Open the solution in **UiPath Studio**.
2. Navigate to the **API Workflows** (CheckInventoryAPI, ProcessPaymentAPI, ShipOrderAPI, SendNotificationAPI).
3. Update the HTTP Request activities with your respective API Keys, URLs, and Endpoints.
4. **Publish** all API workflows to UiPath Automation Cloud.

### Step 4: Running the Solution
1. Open **O2D.bpmn** in UiPath Studio.
2. Ensure the "Check Inventory", "Process Payment", etc., tasks are linked to the published API workflows.
3. **Publish** the O2D BPMN process to UiPath Automation Cloud.
4. Go to **Orchestrator** -> **Processes** and trigger the process, OR use the **Maestro** interface to start a new instance.
5. Monitor the execution trail in real-time to see the order flow through validation, inventory check, payment, and shipping.
