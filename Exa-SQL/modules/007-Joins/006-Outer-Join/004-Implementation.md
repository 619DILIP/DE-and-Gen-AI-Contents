<br>

Table: PartyGuests

|guestid|guestname|
-------|---------|
| 1|Alice    |
| 2|Bob      |
| 3|Charlie  |
| 4|David    |

Table: PartyAttendees

|attendeeid|attendeename|
----------|------------|
| 1|Alice       |
| 3|Charlie     |
| 5|Eve         |

Let's consider a scenario where you have two tables: one containing a list of people invited to a party `PartyGuests` and another containing a list of people who actually attended the party `PartyAttendees`. We'll use a `FULL OUTER JOIN` to combine these tables and see the complete picture, including guests who didn't attend and attendees who were not on the original guest list.

```sql
SELECT PartyGuests.GuestID, PartyAttendees.AttendeeID, PartyGuests.GuestName,
    PartyAttendees.AttendeeName  
FROM PartyGuests  
FULL OUTER JOIN PartyAttendees ON PartyGuests.GuestID = PartyAttendees.AttendeeID;
```

This could also be written omitting OUTER and yield the same result.

```sql
SELECT PartyGuests.GuestID, PartyAttendees.AttendeeID, PartyGuests.GuestName,
    PartyAttendees.AttendeeName
FROM PartyGuests
FULL JOIN PartyAttendees ON PartyGuests.GuestID = PartyAttendees.AttendeeID;
```
OUTPUT:
|guestid|attendeeid|guestname|attendeename|
-------|----------|---------|------------|
| 1|         1|Alice    |Alice       |
| 2|        NULL  |Bob      |    NULL        |
| 3|         3|Charlie  |Charlie     |
| 4|      NULL    |David    |     NULL       |
| NULL|         5|   NULL      |Eve         |

This example demonstrates how a `FULL OUTER JOIN` helps you see the complete picture of guests and attendees at a party, including those who were on the guest list but didn't attend and those who attended but were not on the guest list.