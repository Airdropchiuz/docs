---
sidebar_position: 99
title: Aquarium Pricing
description: Aquarium service plans 
---

# Aquarium Pricing

The Aquarium hosted service offers a forever-free development plan. For production-ready squids, one should use the Premium or an individual Enterprise plan.

- The dev free plan includes:
  -  One collocated squid (API + processor + Postgres)
  -  10GB of database storage
  -  500k monthly RPC requests
  -  Community support
- The premium plan costs `40$/mo` and enables:
  - Configurable dedicated squids
  - Pay-as-you-go collocated squids
  - 2M RPC requests monthly
  - Direct support in a personal Telegram chat
  - `$40` monthly rebate (i.e. the subscription fee is deducted from the final bill)
- The Enterprise plan includes individual SLAs and discounts. [Book a demo](https://calendly.com/d/yzj-48g-bf7/subsquid-demo) to get a personal quote.

## Pricing

The pricing is based solely on the resources consumed by the squid, as the archive data is provided free of charge. 
The total squid price is the total of compute and database storage resources.

### Storage

Database storage is billed at `0.5$/mo` per Gigabyte, both for dedicated and collocated squids.

### Compute for dedicated squids

Dedicated squids have separate [compute profiles](/deploy-squid/scale/#services) for the Postgres database and API/processor services:

#### API/Processor

- `small`: `0.04$/hr` 
- `medium`: `0.08$/hr`
- `large`: `0.15$/hr`

API and processor are configured and billed separately. For example, running a small processor plus a small API costs `0.08$/hr`.

#### Database

- `small`: `0.08$/hr`
- `medium`: `0.16$/hr`
- `large`: `0.33$/hr`

### Collocated (development) squids

Collocated squids share compute resources and thus their performance is NOT guaranteed. We do not recommend using
collocated squids in production, but it's a good fit for development and testing.
Compute is billed at a flat rate of `$0.02/hr` (`~$15/mo`) per each collocated squid (API + processor + DB).
It is not possible to additionally configure a collocated squid except for the storage.

### RPC requests

The premium plan already includes a generous package of 2M requests per month. Above that, it is `$5/1M` requests. 

## SLAs

We align with the [SLAs of the Google Cloud Platform](https://cloud.google.com/compute/sla) and will reduce the bill based on the following schedule:

| Uptime | Rebate |
|-----------------|-----------------|
| 95.00% - < 99.50%     | 10%        |
| 90.00% - < 95.00%       | 25%         |
| < 90.00%          | 100%       |

Note that the SLA applies only to the provisioning the Aquarium services (API availability, provisioning of compute resources) and DOES NOT apply to client code. In particular, if a squid is stuck due to a bug or an upstream Archive/RPC issue, the SLA discounts don't apply. Similarly, the client is responsible for provisioning compute profiles adequate to the expected traffic.

For Enterprise plan customers, individual SLA terms may be negotiated. 

## Examples

### Small dedicated squid

- 1x API service (small)
- 1x processor (small)
- 1x DB (small)
- 50GB storage

Runs 24/7 (720 hours a month). 

| Service | `$/hr` | `$/mo`          |
|-----------------|-----------------|-----------------|
| Compute total  |  `$0.16`    | `$115.2` |
| Storage      |          | `$25` |
| Premium subscription       |      | `$40` |
| Rebate       |      | `-$40` |
| **Total**       |      | **`$140.2`** |


### Processor-only squid

A squid writing parquet files to an external s3 bucket. No database or API is provisioned.

- 1x processor (small)

| Service | `$/hr` | `$/mo`          |
|-----------------|-----------------|-----------------|
| Compute total  |  `$0.04`    | `$28.8` |
| Premium subscription       |      | `$40` |
| Rebate       |      | `-$28.8` |
| **Total**       |      | **`$40`** |


### Large production squid

- 2x API service (medium)
- 1x processor (small)
- 1x DB (large)
- 500GB storage

| Service | `$/hr` | `$/mo`          |
|-----------------|-----------------|-----------------|
| Compute total   |  `$0.53`    | `$381.6` |
| Storage      |          | `$250` |
| Premium subscription       |      | `$40` |
| Rebate       |      | `-$40` |
| **Total**       |      | **`$631.6`** |


### Test collocated squid:

- API + processor + DB (collocated)
- 50GB storage

| Service | `$/hr` | `$/mo`          |
|-----------------|-----------------|-----------------|
| Compute total  | `0.02`    | `$15` |
| Storage      |          | `$25` |
| Premium subscription       |      | `$40` |
| Rebate       |      | `-$40` |
| **Total**       |      | **`$40`** |

## FAQ

**Q**: What happens if I am on a free plan now and have more than one squid?

**A**: Only a single collocated squid is included in the free plan. Please apply for Premium or some of your squids will be at risk of hibernation.

**Q**: What is the difference between collocated and dedicated squids? Why are collocated squids much cheaper?

**A**: Collocated squids share compute resources which means that it may be unresponsive if the neighbour squid is under high load. 
While we do our best to ensure that the resources are shared fairly, we strongly recommend dedicated services for production use.

**Q**: I deployed my squid yesterday, will it be billed for the whole month ?

**A**: No, only the actual hours the squid has been running will be billed.

**Q**: How do I configure the profiles for my squid? 

**A**: Use the [manifest-based deployments](/deploy-squid/deploy-manifest/) and [the profile reference](/deploy-squid/scale/).

**Q**: How can I use the provided RPC package? How do I set the rate limits for it?
 
**A**: Please look at the [RPC proxy docs](/deploy-squid/rpc-proxy/).

