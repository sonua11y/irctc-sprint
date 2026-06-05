# IRCTC Problem Discovery — Part A

## Summary

* Total problems documented: 6 (3 Given + 3 Self-Discovered)
* Platform explored: IRCTC Web Platform
* Devices used:

  * Desktop Chrome
  * Mobile Chrome
* Objective: Identify high-impact usability, performance, and reliability issues affecting train booking users and document them in a structured format for Part B solution design.

---

# Problem 1: Tatkal Booking Crashes at 10:00 AM [Given]

## What is broken

The IRCTC server becomes unresponsive when Tatkal booking opens at 10:00 AM. Users experience page freezes, session drops, delayed OTPs, and failed payments during the most critical booking window.

## Affected users

* Tatkal passengers
* Daily commuters
* Emergency travelers
* Users from Tier 2 and Tier 3 cities

Estimated affected users: 20–40 lakh users during the 9:58–10:05 AM booking window.

## Frequency

Occurs daily at 10:00 AM during Tatkal booking.

## Current Flow — Step by Step

1. User logs into IRCTC around 9:50 AM.
2. User searches and selects a train.
3. User chooses Tatkal quota.
4. User enters passenger details.
5. User clicks Book Now at 10:00 AM.
6. Page freezes and loading spinner appears.
7. User waits 15–45 seconds.
8. Session times out or shows HTTP 502 error.
9. User refreshes page.
10. User discovers quota is already exhausted.

## Where Exactly It Breaks

Steps 6–8.

The booking request overloads backend systems. Users receive no queue status or progress feedback, causing repeated clicks that further increase server load.

---

# Problem 2: Search Filters Do Not Work Reliably [Given]

## What is broken

Filters such as class, quota, availability, and departure time frequently reset or display inconsistent results.

## Affected users

* All train search users
* Senior citizens
* First-time users
* Users comparing multiple trains

Estimated affected users: Most of the 8 crore registered users who search trains.

## Frequency

Intermittent. Observed more frequently during peak traffic periods.

## Current Flow — Step by Step

1. User enters source, destination, and travel date.
2. User clicks Search Trains.
3. Results display 20–40 trains.
4. User selects Sleeper and Available filters.
5. Results refresh.
6. Waitlisted trains still appear.
7. User opens train details.
8. Availability does not match selected filter.
9. User navigates back.
10. Filter settings reset.

## Where Exactly It Breaks

Steps 5–10.

Filter state is not consistently preserved, and refreshed availability data can invalidate previously applied filters.

---

# Problem 3: Seat Selection Resets Randomly [Given]

## What is broken

Selected seats or berth preferences are lost while moving between booking screens.

## Affected users

* Families
* Senior citizens
* Users requiring lower berths
* Divyang passengers

Estimated impact: 30–40% of bookings involve seat preferences.

## Frequency

Approximately 15–25% of booking sessions. Higher on mobile devices.

## Current Flow — Step by Step

1. User selects train and class.
2. User opens seat selection map.
3. User selects a preferred lower berth.
4. Seat is highlighted as selected.
5. User clicks Proceed.
6. Passenger details page loads.
7. Seat preference changes to Auto or another berth.
8. User returns to seat map.
9. Previously selected berth appears unavailable.
10. User completes booking without preferred seat.

## Where Exactly It Breaks

Steps 5–7.

Seat selection state is not consistently transferred between booking components.

---

# Problem 4: Refund Tracking Is Opaque [Self-Discovered]

## How I Found It

Explored ticket cancellation and refund information after reviewing booking history.

## What is broken

Users cannot clearly track refund progress after cancelling tickets. Refund information is scattered across multiple pages.

## Affected users

* Users cancelling tickets
* Frequent travelers
* Business travelers
* Students making schedule changes

Estimated impact: 2–4 lakh users daily.

## Frequency

Occurs every time a refund is pending.

## Current Flow — Step by Step

1. User opens Booked Ticket History.
2. User selects a booked ticket.
3. User clicks Cancel Ticket.
4. Cancellation confirmation appears.
5. User expects refund tracking details.
6. Only basic refund information is shown.
7. User checks transaction history.
8. User still cannot determine refund stage.
9. User searches FAQs or support pages.
10. User waits without clarity.

## Where Exactly It Breaks

Steps 5–8.

The platform confirms cancellation but does not provide a detailed refund timeline or progress tracker.

## Screenshot / Description

Cancellation page displays ticket cancellation status but lacks refund progress information such as processing, bank transfer, or completion stage.

---

# Problem 5: PNR Status Provides Data but Not Guidance [Self-Discovered]

## How I Found It

Explored the PNR enquiry section using waitlisted ticket scenarios.

## What is broken

Users can view current PNR status but receive no guidance regarding confirmation chances or recommended actions.

## Affected users

* Waitlisted passengers
* Students
* Migrant workers
* Last-minute travelers

Estimated impact: Several lakh passengers daily.

## Frequency

Occurs for every waitlisted booking.

## Current Flow — Step by Step

1. User books a waitlisted ticket.
2. User receives PNR number.
3. User opens PNR Status page.
4. Current WL or RAC position appears.
5. User wants to know confirmation probability.
6. No prediction or explanation is provided.
7. User searches external websites.
8. User compares information from third-party apps.
9. User remains uncertain about travel plans.

## Where Exactly It Breaks

Steps 5–7.

The platform provides raw status information but lacks decision-support information.

## Screenshot / Description

PNR page displays current status only without prediction, trend, or recommendation.

---

# Problem 6: Mobile Booking Forms Are Difficult to Complete [Self-Discovered]

## How I Found It

Attempted a complete booking flow using a mobile browser.

## What is broken

Passenger forms are lengthy, require excessive scrolling, and become difficult to complete on smaller screens.

## Affected users

* Mobile-only users
* Elderly passengers
* Users with slower devices
* Rural users relying on mobile internet

Estimated impact: More than half of booking sessions.

## Frequency

Occurs during most mobile booking attempts.

## Current Flow — Step by Step

1. User searches for trains on mobile.
2. User selects train and class.
3. Passenger details form opens.
4. User starts entering passenger information.
5. Multiple dropdown menus require scrolling.
6. Mobile keyboard covers important fields.
7. Validation errors appear after submission.
8. User scrolls to locate missing fields.
9. Form requires repeated corrections.
10. Booking takes significantly longer.

## Where Exactly It Breaks

Steps 5–8.

The form layout is not optimized for mobile usage and increases user effort and error rates.

## Screenshot / Description

Long passenger information form requiring frequent scrolling and repeated interaction with dropdown menus.

---

# Conclusion

The six documented problems reveal three major categories of failure across the IRCTC ecosystem:

1. Performance and Reliability Issues

   * Tatkal Crash
   * Seat Selection Reset

2. Search and Information Architecture Issues

   * Filter Reliability
   * PNR Guidance Gap

3. User Experience and Transparency Issues

   * Refund Tracking
   * Mobile Booking Friction

These findings will be used in Part B to propose feature specifications, AI-powered improvements, wireframes, prioritization matrices, and implementation recommendations.
