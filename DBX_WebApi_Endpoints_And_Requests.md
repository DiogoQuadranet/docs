# DBX WebApi Controller - Endpoints & Requests

**Base URL:** `/api/DBXWebApi/{Action}`  
**Method:** POST  
**Content-Type:** application/json

---

## 1. Test
**Endpoint:** `/api/DBXWebApi/Test`
```json
{}
```

---

## 2. KeepBookingAlive
**Endpoint:** `/api/DBXWebApi/KeepBookingAlive`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "pending_booking_guid": "00000000-0000-0000-0000-000000000000",
  "keep_alive_minutes": 15
}
```

---

## 3. DeleteBooking
**Endpoint:** `/api/DBXWebApi/DeleteBooking`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "suppress_email": false,
  "suppress_sms": false
}
```

---

## 4. GetPromotions
**Endpoint:** `/api/DBXWebApi/GetPromotions`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "date": "2026-05-15",
  "covers": 4,
  "session_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## 5. GetBooking
**Endpoint:** `/api/DBXWebApi/GetBooking`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## 6. GetLocations
**Endpoint:** `/api/DBXWebApi/GetLocations`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "site_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## 7. GetPreAuthDetails
**Endpoint:** `/api/DBXWebApi/GetPreAuthDetails`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "site_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## 8. GetSites
**Endpoint:** `/api/DBXWebApi/GetSites`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## 9. GetSessions
**Endpoint:** `/api/DBXWebApi/GetSessions`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "date": "2026-05-15"
}
```

---

## 10. GetSessionsRange
**Endpoint:** `/api/DBXWebApi/GetSessionsRange`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "date_from": "2026-05-15",
  "date_to": "2026-05-22"
}
```

---

## 11. GetAvailability
**Endpoint:** `/api/DBXWebApi/GetAvailability`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "date": "2026-05-15",
  "covers": 4,
  "return_totals": false,
  "booking_guid": null,
  "table_ids": [],
  "override_duration": null
}
```

---

## 12. MakeBooking
**Endpoint:** `/api/DBXWebApi/MakeBooking`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "booking_datetime": "2026-05-15T19:00:00",
  "covers": 4,
  "booking_source": "Website",
  "promotion_guid": null,
  "override_duration": null,
  "booking_guid_list": []
}
```

---

## 13. AddCustomer
**Endpoint:** `/api/DBXWebApi/AddCustomer`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "pending_booking_guid": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "booking_datetime": "2026-05-15T19:00:00",
  "covers": 4,
  "customer_details": {
    "forename": "John",
    "surname": "Doe",
    "email": "john@example.com",
    "phone": "07700900000",
    "consent": 1,
    "customer_message": "Birthday celebration",
    "member_id": null,
    "swipe_id": null,
    "booking_guid": null,
    "customer_tag_guids": [
      "00000000-0000-0000-0000-000000000000"
    ]
  },
  "booking_message": "Special occasion",
  "guest_request": "Window table if possible",
  "booking_source": "Website",
  "promotion_guid": null,
  "booking_tags": [
    {
      "booking_tag_guid": "00000000-0000-0000-0000-000000000000",
      "guest_name": "John Doe"
    }
  ],
  "deposit_amount": 0,
  "deposit_reference": null,
  "deposit_processor": null,
  "advert": null,
  "referrer": null,
  "promotion": null,
  "suppress_email": false,
  "suppress_sms": false,
  "preauth_token": null
}
```

---

## 14. UpdateCustomer
**Endpoint:** `/api/DBXWebApi/UpdateCustomer`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "customer_guid": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "consent": 1,
  "forename": "Jane",
  "surname": "Doe",
  "email": "jane@example.com",
  "phone": "07700900001"
}
```

---

## 15. UpdateBooking
**Endpoint:** `/api/DBXWebApi/UpdateBooking`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "booking_datetime": "2026-05-15T20:00:00",
  "covers": 5,
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "booking_message": "Updated note",
  "replace_booking_message": false,
  "booking_source": "Website",
  "promotion_guid": null,
  "guest_request": "Early seating preferred",
  "replace_guest_request": false,
  "booking_tags": [],
  "customer_tags": [],
  "deposit_amount": 25.0,
  "deposit_reference": "DEP123",
  "deposit_processor": "Stripe",
  "preauth_token": "token123",
  "suppress_email": false,
  "suppress_sms": false
}
```

---

## 16. UpdateBooking2
**Endpoint:** `/api/DBXWebApi/UpdateBooking2`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "booking_datetime": "2026-05-15T20:00:00",
  "covers": 5,
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "booking_message": "Updated note",
  "replace_booking_message": false,
  "booking_source": "Website",
  "promotion_guid": null,
  "guest_request": "Early seating preferred",
  "replace_guest_request": false,
  "booking_tags": [],
  "customer_tags": [],
  "deposit_amount": 25.0,
  "deposit_reference": "DEP123",
  "deposit_processor": "Stripe",
  "preauth_token": "token123",
  "suppress_email": false,
  "suppress_sms": false
}
```

---

## 17. UpdateBookingConfirmationStatus
**Endpoint:** `/api/DBXWebApi/UpdateBookingConfirmationStatus`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "confirmation_status": 1,
  "suppress_email": false,
  "suppress_sms": false
}
```

---

## 18. AddDeposit
**Endpoint:** `/api/DBXWebApi/AddDeposit`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "deposit_amount": 50.0,
  "deposit_reference": "DEP123456",
  "deposit_processor": "Stripe",
  "suppress_email": false,
  "suppress_sms": false
}
```

---

## 19. GetBookingTags
**Endpoint:** `/api/DBXWebApi/GetBookingTags`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## 20. GetCustomerTags
**Endpoint:** `/api/DBXWebApi/GetCustomerTags`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## 21. GetBookingSources
**Endpoint:** `/api/DBXWebApi/GetBookingSources`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## 22. DeliverectOrder
**Endpoint:** `/api/DBXWebApi/DeliverectOrder`
```json
{
  "type": "OrderSync",
  "siteId": 123,
  "clientId": 456,
  "recordId": 789
}
```

Or for ProductSync:
```json
{
  "type": "ProductSync",
  "siteId": 123,
  "clientId": 456,
  "recordId": 789
}
```
