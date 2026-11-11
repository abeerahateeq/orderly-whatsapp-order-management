# &#x20;Orderly

### WhatsApp Business Order Management, Made Simple.

**Orderly** is an AI-powered WhatsApp Business Order Management platform designed to help small businesses organize customer conversations, extract order details using AI, manage order confirmations, track orders, export data to Excel, and calculate profits — all through one simple, elegant dashboard.

Turn scattered WhatsApp conversations into organized business operations.

---

## &#x20;Key Features

### 🤖 AI-Powered Order Extraction

- Automatically extract order details from customer conversations.
- Identify customer names, products, quantities, sizes, prices, and delivery information.
- Review and edit AI-generated order drafts before saving.
- Support for multiple AI providers with fallback options.

### 💬 WhatsApp Integration

- Receive customer messages through WhatsApp Business Cloud API.
- Organize conversations in one dashboard.
- Send customer welcome messages.
- Send order confirmation messages.
- Identify customer replies and classify confirmations, changes, and cancellations.

### 📦 Smart Order Management

- Track orders through different stages:
  - New
  - Confirmation Sent
  - Change Requested
  - Unclear
  - Confirmed
  - Dispatched
  - Cancelled
- Edit extracted order details.
- Manage multiple items within an order.
- Add orders received through phone calls.
- Maintain order history and audit records.

### 📊 Profit Calculation

- Upload purchase-price lists.
- Calculate order-wise profits.
- View daily profit summaries.
- Export profit reports to Excel.
- Keep profit information restricted to the owner interface.

### 📁 Excel Import & Export

- Export confirmed orders to Excel.
- Import existing spreadsheets.
- Preview and validate changes before applying them.
- Download profit reports.

### 🔐 Authentication & Security

- Secure Google Sign-In using Supabase Auth.
- Protected dashboard routes.
- Owner and staff interface roles.
- Customer phone number masking in chat lists.
- Secure backend authentication and webhook signature verification.

### 💾 Backup & Restore

- Download business data as a JSON backup.
- Restore data from previous backups.
- Keep business records stored locally in the browser.

---

## 🛠️ Tech Stack

| Category         | Technologies                |
| ---------------- | --------------------------- |
| Frontend         | React, Vite, TypeScript     |
| Styling          | Tailwind CSS                |
| Animations       | Framer Motion               |
| Routing          | React Router                |
| State Management | Zustand                     |
| Data Tables      | TanStack Table              |
| Local Database   | Dexie.js, IndexedDB         |
| Excel Processing | ExcelJS                     |
| Backend          | Python, FastAPI             |
| Authentication   | Supabase Auth               |
| Database         | Supabase PostgreSQL         |
| AI Integration   | Gemini, Groq, Mistral       |
| Messaging        | WhatsApp Business Cloud API |

---

## 🏗️ Architecture

Orderly uses a hybrid architecture to separate authentication and temporary messaging infrastructure from local business data.

```text
Customer
   |
   | WhatsApp Message
   v
Meta WhatsApp Cloud API
   |
   | Webhook
   v
FastAPI Backend
   |
   | Verify & Process
   v
Supabase
   |
   | Temporary Events
   v
Orderly Dashboard
   |
   | Save Business Data
   v
Browser IndexedDB
```

**Architecture highlights:**

- Supabase manages authentication, roles, and temporary platform data.
- IndexedDB stores business data locally in the user's browser.
- FastAPI handles AI requests, message processing, and calculations.
- AI extracts and classifies information, while the seller remains in control of business decisions.
- Excel files are generated and processed in the browser.

---

## 🚀 Getting Started

### Prerequisites

Before running Orderly, make sure you have:

- Node.js and npm
- Python 3.11+
- A Supabase project
- Google OAuth credentials
- A Meta Developer account with WhatsApp Cloud API access
- At least one supported AI provider API key

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/orderly-whatsapp-order-management.git

cd orderly-whatsapp-order-management
```

### 2. Set Up the Frontend

```bash
cd frontend

npm install
```

Create your frontend environment file:

```bash
cp .env.example .env
```

Configure the following variables:

```env
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=
VITE_API_BASE_URL=
```

Start the frontend development server using the available Vite development script:

```bash
npm run dev
```

### 3. Set Up the Backend

Open another terminal:

```bash
cd backend
```

Create and activate a Python virtual environment:

```bash
python -m venv venv
```

Activate it:

**Windows:**

```bash
venv\Scripts\activate
```

**macOS / Linux:**

```bash
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Create your backend environment file:

```bash
cp .env.example .env
```

Configure the required environment variables.

### 4. Configure Supabase

1. Create a Supabase project.
2. Configure Google OAuth under Authentication Providers.
3. Add the appropriate redirect URLs.
4. Apply the database schema and security policies from the project documentation.
5. Configure the required environment variables.

### 5. Configure WhatsApp Cloud API

1. Create a Meta Developer application.
2. Configure WhatsApp Cloud API.
3. Add the test phone number.
4. Configure the webhook URL and verification token.
5. Add the required webhook subscription.
6. Configure the WhatsApp credentials in the backend environment.

### 6. Configure AI Providers

Add API keys and model names for the supported providers:

- Google Gemini
- Groq
- Mistral

Orderly supports provider fallback so that extraction and classification can continue when a configured provider is unavailable.

---

## 🔑 Environment Variables

### Frontend

| Variable                 | Description                   |
| ------------------------ | ----------------------------- |
| `VITE_SUPABASE_URL`      | Supabase project URL          |
| `VITE_SUPABASE_ANON_KEY` | Supabase public/anonymous key |
| `VITE_API_BASE_URL`      | Backend API URL               |

### Backend

| Variable                    | Description                    |
| --------------------------- | ------------------------------ |
| `APP_ENV`                   | Application environment        |
| `FRONTEND_ORIGIN`           | Frontend origin for CORS       |
| `PRODUCT_NAME`              | Product name                   |
| `SUPABASE_URL`              | Supabase project URL           |
| `SUPABASE_SERVICE_ROLE_KEY` | Supabase service role key      |
| `SUPABASE_JWT_SECRET`       | JWT verification secret        |
| `WA_ACCESS_TOKEN`           | WhatsApp access token          |
| `WA_APP_SECRET`             | Meta application secret        |
| `WA_VERIFY_TOKEN`           | Webhook verification token     |
| `WA_GRAPH_API_VERSION`      | Meta Graph API version         |
| `GEMINI_API_KEY`            | Gemini API key                 |
| `GEMINI_MODEL`              | Gemini model name              |
| `GROQ_API_KEY`              | Groq API key                   |
| `GROQ_MODEL`                | Groq model name                |
| `MISTRAL_API_KEY`           | Mistral API key                |
| `MISTRAL_MODEL`             | Mistral model name             |
| `AI_PROVIDER_ORDER`         | AI provider fallback order     |
| `AI_TIMEOUT_SECONDS`        | AI request timeout             |
| `QUEUE_TTL_HOURS`           | Temporary event queue lifetime |
| `PHONE_HASH_SALT`           | Salt used for phone hashing    |

**Security:** Never commit `.env` files, API keys, access tokens, or service role credentials to GitHub.

---

## 📂 Project Structure

```text
orderly-whatsapp-order-management/
│
├── frontend/
│   ├── src/
│   │   ├── app/
│   │   ├── features/
│   │   │   ├── auth/
│   │   │   ├── chats/
│   │   │   ├── orders/
│   │   │   ├── excel/
│   │   │   ├── profit/
│   │   │   ├── data/
│   │   │   └── settings/
│   │   ├── components/
│   │   └── lib/
│   ├── .env.example
│   └── package.json
│
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── config.py
│   │   ├── auth.py
│   │   ├── routers/
│   │   ├── services/
│   │   ├── models.py
│   │   └── prompts.py
│   ├── tests/
│   ├── requirements.txt
│   └── .env.example
│
├── scripts/
│   └── send_fake_webhook.py
│
├── synthetic-data/
│
└── docs/
```

---

## 🔄 Order Workflow

```text
Customer Sends WhatsApp Message
              |
              v
       Message Received
              |
              v
       AI Extracts Details
              |
              v
      Seller Reviews Order
              |
              v
     Buyer Confirmation Sent
              |
              v
      Customer Replies
              |
       +------+------+
       |      |      |
      Yes   Change  Cancel
       |      |      |
       v      v      v
   Confirmed Update Cancelled
       |
       v
   Dispatched
```

**Important:** AI prepares drafts and classifies replies. The seller makes the final decisions about confirming and dispatching orders.

---

## 🔒 Privacy & Data Handling

Orderly is designed with a local-first business data architecture.

- Business messages, orders, purchase prices, and audit history are stored in browser IndexedDB.
- Supabase stores authentication and platform-related data.
- The backend uses a temporary event queue for incoming and outgoing message synchronization.
- Message content, phone numbers, and customer addresses must not appear in server logs.
- Business data is not automatically synchronized across multiple devices.
- Users should download regular backups to protect their local business data.

---

## ⚠️ Prototype Limitations

Orderly is initially designed as a hackathon prototype.

- WhatsApp integration uses a Meta test phone number.
- The test number can message only verified recipient numbers.
- Meta temporary access tokens need to be refreshed when they expire.
- Free-form WhatsApp replies are supported within the 24-hour customer-service window.
- WhatsApp message templates for communication outside that window are not implemented.
- Real multi-device synchronization and real multi-user staff accounts are outside the current scope.
- Business data is stored locally, so clearing browser data or losing the device can result in data loss without a backup.

---

## 🎯 Our Vision

We believe managing customer orders should be simple, organized, and stress-free.

Small business owners deserve tools that save time, reduce manual work, and help them focus on growing their businesses.

**Orderly transforms WhatsApp conversations into organized business operations.**

---

## 👩‍💻 Built With

Created with a vision to make business management smarter and more accessible for small businesses.

---

\<p align="center">
&#x20; \*\*🌿 Orderly — Bring Order to Your Business.\*\*
\</p>
