# **Travel Agency Management System – Domain Modeling**

## ## **1. Domain Entities**

### **Client**

```
- id
- firstname
- lastname
- phone
- email
- passportNumber
- dateOfBirth
```

### **Ticket (AirTicket)**

```
- id
- clientId
- airline
- ticketNumber
- pnr
- departure
- arrival
- departureDate
- returnDate
- type (one_way, round_trip)
- basePrice
- agencyCommission
- totalPrice
- status (issued, cancelled, refunded)
```

### **Booking**

```
- id
- clientId
- agencyUserId
- travelDate
- origin
- destination
- bookingStatus (pending, confirmed, cancelled)
- createdAt
```

### **Payment**

```
- id
- ticketId
- method (cash, mobile money, bank, card)
- amount
- paidAt
- status (paid, failed, pending)
```

### **Invoice**

```
- id
- ticketId
- invoiceNumber
- amount
- emissionDate
- pdfUrl
```

### **AirlineProvider**

```
- id
- name
- contact
- type (airline, consolidator)
- email
- commissionRate
```

### **User (Staff)**

```
- id
- name
- email
- password
- role (admin, agent, accountant)
```

---

## ## **2. Relationships (UML Text Form)**

```
Client ───< Ticket >── AirlineProvider
          |
          └──< Payment
          |
          └── Invoice

User ───< Booking >── Ticket
```

---

## ## **3. Use Cases**

### **Client Use Cases**

```
- createClient
- updateClient
- searchClient
- getClientHistory
```

### **Ticket Use Cases**

```
- createTicket
- issueTicket
- cancelTicket
- refundTicket
- listTickets
- ticketDetails
```

### **Booking Use Cases**

```
- createBooking
- confirmBooking
- cancelBooking
```

### **Payment Use Cases**

```
- receivePayment
- refundPayment
- listPayments
- calculateCommission
```

### **Accounting Use Cases**

```
- dailySalesReport
- monthlyRevenueReport
- agentCommissionReport
- providerPaymentsReport
```

### **Invoice Use Cases**

```
- generateInvoice
- downloadInvoice
- sendInvoiceByEmail
```

---

## ## **4. Real-Life Scenarios**

### **Scenario 1 — Client buys a ticket**

1. Client asks for a route
2. Agent creates a **booking**
3. Booking becomes a **ticket**
4. Client makes a **payment**
5. Ticket status → **issued**
6. System generates a **PDF invoice**
7. Accounting module stores the sale

---

### **Scenario 2 — Ticket cancellation**

1. Client requests cancellation
2. Agent cancels the **ticket**
3. System computes refund / penalties
4. Refund recorded
5. Accounting updated

---

### **Scenario 3 — Daily accounting report**

1. Accountant opens dashboard
2. System shows:

   * total tickets sold
   * revenue
   * commissions
   * provider payouts
