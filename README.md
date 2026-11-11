# Orderly

**AI-Powered WhatsApp Business Order Management**

Orderly is an AI-powered WhatsApp Business Order Management platform designed to help small businesses organize customer conversations, manage orders, handle confirmations, track deliveries, export records to Excel, and calculate profits through one simple dashboard.

Orderly turns everyday WhatsApp conversations into structured, manageable business orders while keeping the seller in control.

## Key Features

### AI-Powered Order Extraction
- Extracts customer and order details from WhatsApp conversations.
- Identifies products, sizes, quantities, addresses, and agreed prices.
- Highlights missing information and unclear details.
- Generates structured order drafts for seller review.
- Allows sellers to edit and approve extracted information.
- Uses Python for calculations to ensure accurate totals.

### WhatsApp Business Integration
- Connects with WhatsApp Business through the WhatsApp Cloud API.
- Receives customer messages through webhooks.
- Organizes conversations for easier order management.
- Supports the planned Meta Embedded Signup integration.
- Aims to support WhatsApp Coexistence, allowing eligible businesses to continue using the WhatsApp Business app alongside Orderly.

### Order Management
- Organizes orders in a structured dashboard.
- Tracks order statuses:
  - New
  - Confirmation Sent
  - Change Requested
  - Unclear
  - Confirmed
  - Dispatched
  - Cancelled
- Allows sellers to review and update order information.
- Supports manual entry for orders received through phone calls.
- Keeps sellers in control of customer communication and order decisions.

### Order Confirmation
- Generates buyer confirmation messages for seller review.
- Allows sellers to edit and send confirmation messages.
- Identifies customer replies as confirmations, change requests, or cancellations.
- Updates order status based on the customer's response.

**Important:** AI prepares suggestions and drafts. It does not independently send messages or make business decisions.

### Excel Management
- Exports organized orders to Excel.
- Supports importing edited Excel files.
- Provides a preview before applying imported changes.
- Validates imported information.
- Identifies conflicts using Order IDs.
- Avoids silently overwriting existing order information.

Excel exports are snapshots of dashboard data rather than live two-way synchronization.

### Profit Management
- Supports seller-provided purchase-price lists.
- Calculates order costs and estimated profit.
- Uses structured order information for reporting.
- Keeps business calculations under the seller's control.

### Authentication
- Google Sign-In through Supabase Authentication.
- Secure account access.
- Stores account and integration-related metadata through Supabase.

### Backup and Restore
- Allows sellers to create backups of their business data.
- Supports restoring data from backup files.
- Keeps backup files under the seller's control.
- Supports saving backups locally or to the seller's own cloud storage.

---

## Product Vision

Orderly aims to provide small businesses with a complete WhatsApp-based order management experience.

The intended customer onboarding experience is:

1. The shopkeeper signs up using Google.
2. The shopkeeper selects **Connect WhatsApp Business**.
3. Meta Embedded Signup guides the shopkeeper through connecting an eligible WhatsApp Business number.
4. The shopkeeper completes the required phone number verification and connection steps.
5. With supported WhatsApp Coexistence, the shopkeeper can continue using the WhatsApp Business app while managing orders through Orderly.

The goal is to make order management easier without forcing shopkeepers to change their everyday communication habits.

## Meta Developer Integration

The Meta Developer account and WhatsApp Cloud API test environment have been set up.

### Current Meta Setup

- Meta Developer account created.
- WhatsApp product configured in the Meta app.
- WhatsApp Cloud API test environment initialized.
- Test Phone Number ID obtained.
- Test recipient phone number added and verified.
- Temporary access token generated.

### Meta Integration Requirements

The complete onboarding experience depends on Meta's platform requirements, including:

- Meta Business Portfolio setup and business verification.
- Meta App Review.
- Advanced Access for required permissions, including:
  - `business_management`
  - `whatsapp_business_management`
- Tech Provider approval.
- Access Verification.
- Embedded Signup configuration.
- WhatsApp Coexistence eligibility and support for the business's phone number.

These requirements are necessary for the intended platform-managed onboarding experience. Availability and eligibility depend on Meta's policies and supported regions.

A temporary access token is suitable for testing but is not a permanent production credential.

---

## Technology Stack

| Area | Technology |
|---|---|
| Frontend | React, Vite, TypeScript |
| Styling | Tailwind CSS |
| Animations | Framer Motion |
| Routing | React Router |
| State Management | Zustand |
| Data Tables | TanStack Table |
| Local Database | IndexedDB, Dexie.js |
| Excel Processing | ExcelJS |
| Backend | Python, FastAPI |
| Authentication | Supabase Auth |
| Platform Metadata | Supabase |
| AI Providers | Gemini, Groq, Mistral |
| Messaging | WhatsApp Business Cloud API |
| Signup Integration | Meta Embedded Signup |
| Business Messaging | WhatsApp Coexistence |

---

## System Architecture

Orderly is designed to keep business records under the seller's control while using backend services for messaging integration and temporary event delivery.

```text
Customer
   |
   v
WhatsApp Business
   |
   v
Meta WhatsApp Cloud API
   |
   v
FastAPI Backend
   |
   v
Webhook Verification
   |
   v
Temporary Event Queue
   |
   v
Orderly Dashboard
   |
   v
IndexedDB
   |
   v
AI Order Extraction
   |
   v
Seller Review and Approval
   |
   v
Order Management
   |
   v
Excel Export and Profit Reports
```

### Data Storage

**IndexedDB**
- Stores the seller's business orders and related operational records locally in the browser.
- Keeps customer and order information under the seller's control.

**Supabase**
- Handles authentication and account-related metadata.
- Supports the temporary event queue used for message delivery.

**FastAPI**
- Handles WhatsApp webhook verification and incoming events.
- Processes integration requests.
- Coordinates temporary event delivery to the dashboard.

Temporary events are removed when acknowledged by the dashboard. Undelivered events are subject to expiration, so the system does not promise complete recovery of every message.

---

## Order Management Workflow

1. A customer sends a message through WhatsApp.
2. Meta delivers the message to the configured webhook.
3. The backend verifies and queues the incoming event.
4. The dashboard receives the message.
5. The seller selects a conversation for order extraction.
6. AI prepares a structured order draft.
7. The seller reviews and edits the extracted details.
8. The seller sends the buyer confirmation.
9. The customer's reply is classified.
10. The seller manages the order through confirmation and dispatch.
11. Orders can be exported to Excel.
12. Profit reports can be calculated using the seller's purchase-price information.

---

## AI Processing

Orderly is designed to use AI to reduce manual work while keeping the seller responsible for business decisions.

The AI can help identify:

- Customer name and contact information.
- Product details.
- Size and quantity.
- Delivery address.
- Agreed price.
- Missing information.
- Unclear order details.
- Suggested dispatch notes.

The planned AI provider fallback order is:

1. Gemini
2. Groq
3. Mistral

AI-generated information must be reviewed by the seller before it is used for order confirmation or other business actions.

---

## Privacy and Data Handling

Orderly is designed around seller-controlled business data.

- Business orders and operational records are intended to remain in the seller's browser storage.
- Supabase is used for authentication, account metadata, and temporary event delivery.
- Backup files are saved under the seller's control rather than passing through Orderly's server.
- AI processing should use platform-managed credentials.
- Synthetic data should be used for demonstrations and testing.
- Real customer information should not be sent through free AI services during prototype demonstrations.

Browser storage can be lost if browser data or the device is lost. Sellers should maintain backups of important business records.

---

## Project Setup

### Prerequisites

- Node.js
- Python
- Supabase account
- Meta Developer account
- WhatsApp Cloud API test configuration

### Environment Configuration

The exact environment variable names should match the application's implementation.

Typical configuration may include:

```env
# Supabase
SUPABASE_URL=
SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
SUPABASE_JWT_SECRET=

# WhatsApp Cloud API
WHATSAPP_ACCESS_TOKEN=
WHATSAPP_PHONE_NUMBER_ID=
WHATSAPP_BUSINESS_ACCOUNT_ID=
WHATSAPP_APP_SECRET=
WHATSAPP_VERIFY_TOKEN=

# AI Providers
GEMINI_API_KEY=
GROQ_API_KEY=
MISTRAL_API_KEY=
```

Keep secret keys private. Never commit access tokens, service-role keys, or other credentials to a public repository.

### Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/orderly-whatsapp-order-management.git
cd orderly-whatsapp-order-management
```

Install dependencies and configure the frontend and backend according to their respective project configuration files.

---

## Project Structure

The intended project organization is:

```text
orderly/
|
|-- frontend/
|   |-- src/
|   |-- public/
|   |-- package.json
|
|-- backend/
|   |-- app/
|   |-- requirements.txt
|
|-- docs/
|
|-- scripts/
|
|-- synthetic-data/
|
|-- README.md
```

Actual folders and filenames may vary according to the repository implementation.

---

## Excel Data Handling

Orderly uses Excel as a convenient way for sellers to manage and review their order records.

The import process is designed to:

- Validate uploaded data.
- Preview changes before applying them.
- Match existing orders using Order IDs.
- Identify conflicting information.
- Prevent silent overwrites.

The dashboard remains the primary source of truth.

---

## Demonstration and Testing

The demonstration environment can use Meta's WhatsApp test number and synthetic customer/order information.

The test environment is intended to demonstrate the messaging workflow, webhook processing, AI-assisted order extraction, order management, Excel export, and profit calculations.

Meta test numbers have restrictions, including recipient verification requirements. Temporary access tokens also expire and need to be renewed.

---

## About Orderly

Orderly is designed to help small businesses spend less time organizing messages and more time managing their business.

By bringing WhatsApp conversations, AI-assisted order extraction, confirmations, order tracking, Excel management, and profit calculations into one dashboard, Orderly aims to make everyday business operations simpler and more organized.

**Orderly — Bring Order to Your Business.**
