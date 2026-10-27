## AWS Is Not One Place

It is easy to think of the cloud as a single system somewhere. In practice, AWS runs physical data centers in locations around the world, and that geography is exposed directly to anyone using it. Almost every decision made when creating a resource involves choosing where it lives.

Understanding this structure early explains a set of behaviors that otherwise seem arbitrary, and it prevents a category of mistakes that are awkward to undo.

---

## Regions

A region is a separate geographic area containing its own AWS infrastructure. Examples include one in Northern Virginia, one in Ireland, one in Mumbai, and one in Sydney. Each region has a code used in commands and configuration, such as `us-east-1`, `eu-west-1`, or `ap-south-1`.

The important property is that regions are independent of one another. Three consequences follow directly:

- **Resources belong to a region.** A storage bucket created in Ireland does not appear when looking at the Mumbai region. This is why almost every command and console screen involves a region, and why a resource can seem to have disappeared when the region has been switched by accident.
- **Pricing varies by region.** The same service can cost different amounts depending on where it runs, sometimes noticeably.
- **Service availability varies.** Newer services often launch in a small number of regions and expand later, so a service available in one region may not yet exist in another.

---

## Choosing a Region

Three considerations usually drive the decision.

**Latency.** Data travels at a finite speed, so physical distance matters. An application serving users in Europe will respond faster from a European region than from one in North America. The usual guidance is to run close to whoever or whatever is using the service.

**Compliance and data residency.** Some data is legally required to remain within a particular country or jurisdiction. Where regulations require personal data to stay within a specific area, the region choice is not a preference but a requirement, and it is often the deciding factor regardless of cost or latency.

**Cost.** Regions are priced differently. A more distant region may be cheaper, which can be worth it for workloads where nobody is waiting on a response, such as overnight batch processing or long term archival.

These can conflict. A cheaper region may be the wrong one for compliance, or the compliant region may not be the closest. Naming which of the three is the constraint usually settles the decision quickly.

---

## Availability Zones

Within a region, infrastructure is divided further into availability zones. An availability zone is one or more physically separate data centers with independent power, cooling, and networking.

```text
Region: us-east-1
    |
    +-- Availability Zone us-east-1a     independent power and networking
    +-- Availability Zone us-east-1b     independent power and networking
    +-- Availability Zone us-east-1c     independent power and networking
```

The separation is deliberate and carefully balanced. Zones are far enough apart that a localized problem, such as a power failure, a fire, or a flood, is unlikely to affect more than one at a time. They are close enough together that the network links between them are fast, so an application spread across zones does not pay a meaningful latency penalty for the arrangement.

Most regions contain at least three availability zones.

---

## Why Availability Zones Exist

Hardware fails. Data centers occasionally lose power. Availability zones exist so that those events do not have to take an application down with them.

An application running in a single zone has a single point of failure. The same application running across two or more zones can keep serving from the remaining zones when one becomes unreachable.

This is the reasoning behind patterns that appear repeatedly across AWS services:

- A database configured for high availability maintains a standby copy in a second availability zone and switches to it automatically if the primary becomes unreachable.
- A group of servers behind a load balancer is normally distributed across zones, so the load balancer can route around a zone that stops responding.
- Storage services replicate data across multiple zones by default, which is why an object put into storage survives the loss of a data center without anything being configured.

The cost of designing this way at the outset is usually small. The cost of retrofitting it after an outage is considerably higher.

---

## Edge Locations

A third type of location is worth knowing about, though it is used differently. Edge locations are a much larger number of smaller sites, placed close to end users, that cache content rather than run applications. Their purpose is to serve frequently requested content from somewhere physically near the person requesting it, rather than fetching it from the region each time.

Regions and availability zones are where infrastructure runs. Edge locations are where content is cached for speed.

---

## Why the Choice Matters Early

Region and availability zone decisions are made at the moment a resource is created, and some are difficult to reverse. Moving a database to a different region is a migration involving planning and downtime, not a setting to be changed. Choosing deliberately at the start avoids that work later.