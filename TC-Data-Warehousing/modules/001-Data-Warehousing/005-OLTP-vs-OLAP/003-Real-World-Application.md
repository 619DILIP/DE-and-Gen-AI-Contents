## An Airline Example

An airline's booking system is a clear example of OLTP. When a passenger books a flight, the system needs to instantly check seat availability, reserve the seat, and process payment, all as one fast, reliable transaction. Millions of these small transactions happen across the system every day.

Separately, the airline's business analysts want to know which routes were most profitable last quarter, or how booking patterns shift around holidays. Running that kind of query directly against the live booking system risks slowing it down during a busy travel period. Instead, booking data is regularly copied into a data warehouse, an OLAP system, where these large scale analytical queries can run without touching the live booking system at all.
