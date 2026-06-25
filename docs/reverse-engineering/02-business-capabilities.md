# Business Capabilities

This project implements the following business capabilities (source: README.md and JSP/servlet flow):

- Role-based booking workflow: Admin, Manager, Customer
- Admin: create/update seat features and set seat pricing and inventory (`ChangeFeatures`, `SetSeats` servlets/JSPs)
- Manager: review and approve/disapprove features and seat updates (`ApproveFeatures`, `ApproveSeats`, `DisapproveFeatures`, `DisapproveSeats`)
- Customer: search flights, choose flights, book seats, view current bookings and itinerary (`SearchFlights`, `ChooseFlight`, `BookFlight`, `CurrentBooking`)
- Real-time seat inventory enforcement: prohibits purchases when seats are sold out (application-managed stock in `FBS` model loaded at context startup)
- Email notification: sends itinerary on successful booking (implementation point — see code paths for email triggers)

Notes:
- Payment is simulated: pressing the pay button is treated as a completed transaction (see README: "When the customer presses the pay button consider the transaction done").
