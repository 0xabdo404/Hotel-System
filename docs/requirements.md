# Requirements: inbook System

## 1. Roles

1. **Customer :**
   Unauthenticated/Authenticated user who registers, links a digital wallet, purchases and spends points, searches for hotels, compares similar hotels by location and price, and directly books rooms and add-on services/events.

2. **Hotel Admin :**
   Hotel business owner who registers hotel branches, links a bank account for point-to-cash payouts, sets room prices in points, and manages available room inventory.

3. **System Admin :**
   Platform manager who reviews and approves registered hotels, monitors points-to-cash transactions and commission deductions, and ensures system security and uptime.

---

## 2. User Stories

- **US-01:** As a **Customer**, I want to search for hotels by location, date, and number of guests so that I can find available accommodation for my trip. [Must]
- **US-02:** As a **Customer**, I want to view a list of similar hotels based on price and location so that I can compare alternative options fairly. [Must]
- **US-03:** As a **Customer**, I want to purchase points packages into my wallet so that I can use them to book room reservations. [Must]
- **US-04:** As a **Customer**, I want to book a room directly using my wallet points so that I can secure my reservation instantly without middleman fees. [Must]
- **US-05:** As a **Customer**, I want to view my active booking voucher so that I can present my reservation details at check-in. [Should]
- **US-06:** As a **Customer**, I want to book local events or trips using my points so that I can customize my travel itinerary in one place. [Could]
- **US-07:** As a **Hotel Admin**, I want to register my hotel details and branches so that customers can discover my properties. [Must]
- **US-08:** As a **Hotel Admin**, I want to manage room types, availability, and point prices so that I can keep my inventory up to date. [Must]
- **US-09:** As a **Hotel Admin**, I want to link my bank account details so that I can receive periodic cash payouts for earned points. [Must]
- **US-10:** As a **Hotel Admin**, I want to offer direct discount point rates for specific dates so that I can increase occupancy during off-peak seasons. [Should]
- **US-11:** As a **System Admin**, I want to review and approve newly registered hotels so that only verified businesses operate on the platform. [Must]
- **US-12:** As a **System Admin**, I want to generate payout reports showing total points redeemed and  platform commission so that financial settlements remain transparent. [Should]

---

## 3. Acceptance Criteria

### Feature: Search & Compare Hotels (US-01 & US-02)

**Scenario: Successful hotel search with matching results**
- **Given** the customer is on the search page
- **When** the customer enters destination "Alexandria", check-in date, and 2 guests
- **Then** the system displays a list of available hotels in Alexandria matching the criteria

**Scenario: View similar hotels for price comparison**
- **Given** the customer is viewing details of "Hotel A" priced at 500 points/night
- **When** the customer clicks "View Similar Hotels"
- **Then** the system presents alternative hotels within 5 km range priced between 400 and 600 points

---

### Feature: Purchase Wallet Points (US-03)

**Scenario: Successful points purchase**
- **Given** the customer has an active logged-in account and a linked wallet
- **When** the customer selects the "1,000 Points Package" ($200) and completes payment
- **Then** 1,000 points are added to the customer wallet balance immediately

**Scenario: Insufficient funds payment failure**
- **Given** the customer attempts to buy points
- **When** the payment gateway rejects the card due to insufficient balance
- **Then** the system displays "Payment failed" and wallet points balance remains unchanged

---

### Feature: Direct Room Booking (US-04)

**Scenario: Successful room reservation using points**
- **Given** a customer with 1,000 wallet points
- **And** a room at "Steigenberger Hotel" is available for 400 points/night
- **When** the customer confirms a 2-night booking (800 points total)
- **Then** 800 points are deducted from the customer wallet balance
- **And** room availability is decremented by 1
- **And** a confirmation voucher is generated

**Scenario: Booking attempt with insufficient points**
- **Given** a customer with 300 wallet points
- **When** the customer attempts to book a room costing 500 points
- **Then** the system rejects the booking with message "Insufficient wallet points balance"

---

### Feature: Room & Inventory Management (US-08)

**Scenario: Hotel Admin adds new room inventory**
- **Given** an authenticated Hotel Admin on the management dashboard
- **When** the admin adds 5 "Deluxe Sea View" rooms priced at 600 points/night
- **Then** the new room type appears in the hotel public catalog with 5 available units

---

### Feature: Hotel Bank Payout Setup (US-09)

**Scenario: Hotel Admin links valid IBAN**
- **Given** an authenticated Hotel Admin setting up financial details
- **When** the admin enters a valid IBAN and bank account name
- **Then** the account status changes to "Verified for Direct Payouts"

---

## 4. Non-Functional Requirements (NFRs)

- **NFR-01 (Performance):** Hotel search and similar hotel recommendation queries must return results in less than 2.0 seconds for up to 10,000 listed hotels.
- **NFR-02 (Security):** All user passwords must be hashed using bcrypt with a cost factor of 12 or higher, and bank details must be encrypted at rest.
- **NFR-03 (Usability):** A first-time customer must be able to complete a room reservation in under 3 minutes without requiring assistance or training.
- **NFR-04 (Availability):** The booking and search services must maintain an availability uptime of 99.5% during operating hours.

---

## 5. MVP Scope

The Minimum Viable Product (MVP) for the 10-week release focuses strictly on the core booking lifecycle:

- **Included Stories:** US-01, US-02, US-03, US-04, US-07, US-08, US-09, US-11.
- **Rationale:** These **Must** stories allow customers to buy points, search, compare, and book rooms directly while allowing hotel admins to list properties, manage rooms, and link bank accounts.
- **Deferred Stories (Backlog):** US-05, US-06 (event booking), US-10 (off-peak discounts), and US-12 (advanced payout reporting) remain in the backlog for future releases.
