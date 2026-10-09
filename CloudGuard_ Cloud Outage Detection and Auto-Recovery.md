[Skip to content](#main)

[CloudGuard](#top)

- [Simulator](#simulator)
- [The problem](#problem)
- [How it works](#how)
- [Architecture](#architecture)
- [Tech stack](#stack)
- [Outcome](#outcome)

# When a cloud region fails, CloudGuard moves the traffic.

A prototype that detects outages in an e-commerce platform, scales it under heavy load, sends customers to a healthy region, and tells the administrator what happened.

[Run the live simulation](#simulator) [Read the case study](#problem)

## ShopSphere, mid-sale

A health check during the outage

- Website ✓ Up
- Login ✓ Up
- Product search ✓ Up
- Shopping cart ✓ Up
- Checkout ✕ Down
- Payment ✕ Down

The homepage loads, but customers cannot pay. A simple “is the website online?” check would call this a success.

## Run the outage yourself

Pick a scenario and watch CloudGuard detect the problem, decide what to do, and recover. This is a browser simulation with made-up numbers, not a real cloud.

Normal operation. CloudGuard is monitoring.

### Platform metrics

Active users0

### Regions and traffic

### Service health checks

### What CloudGuard is doing

Numbers in the simulation follow the case study: normal CPU near 40%, a spike pushing CPU to about 95%, and a 3-server to 6-server scale-out. In a real build, these values would come from live monitoring tools.

## What went wrong at ShopSphere

ShopSphere is an e-commerce company serving millions of customers, with its whole platform on cloud infrastructure. During a major sale, most critical services depended on a single cloud region.

1. High traffic
2. Server and resource overload
3. Application failures
4. Database and API problems
5. Orders fail
6. Website partly unavailable

### Root causes

- **Single-region dependency**Most critical services run in one cloud region.
- **Traffic spike**A sudden jump in users overwhelms resources.
- **Insufficient auto-scaling**Resources cannot grow quickly enough.
- **Service dependency**One failing service drags others down with it.
- **Database bottleneck**Too many requests arrive at the database at once.
- **Poor failure detection**Problems are not noticed quickly.
- **Weak disaster recovery**Backup systems cannot take over immediately.
- **No effective failover**Traffic cannot move to healthy infrastructure on its own.

### Business impact

- Lost orders
- Failed payments
- Revenue loss
- Customer dissatisfaction
- Inventory inconsistencies
- More customer-support work
- Damage to the company’s reputation
- Possible data inconsistency

“Unable to place order” “Payment failed” “Service temporarily unavailable”

### Partial failure is the hardest to catch

The website may still open while checkout is broken. Checking only whether the site is “online” is not enough, so CloudGuard tests each service the customer actually needs.

## How CloudGuard works

The core idea is five actions in a row: detect, decide, redirect, recover, report. Behind them are five building blocks.

1. 1

   ### Monitor continuously

   CloudGuard watches the health of the whole platform. When CPU hits 92%, error rate hits 17% and response time hits 4.8 seconds, it knows the environment is getting unhealthy.

   CPUMemoryNetwork trafficResponse timeError rateDatabase loadActive usersFailed transactionsService availability
2. 2

   ### Check each service

   Instead of asking only whether a server is running, CloudGuard runs application-level health checks on login, search, cart, checkout and payment. This is how it catches partial outages.
3. 3

   ### Scale automatically

   When traffic grows, CloudGuard starts more application instances. When traffic falls, it removes the extra ones to save cost.

   Normal: 3 servers

   High: 6 servers

   Extreme: 10 servers
4. 4

   ### Fail over automatically

   If Region A becomes unhealthy, CloudGuard sends new requests to Region B. The platform no longer depends on a single location.
5. 5

   ### Keep the data replicated

   The database is copied between the primary and backup environments. If the primary becomes unavailable, the backup can be promoted. A real system would need careful design for consistency and transactions, especially for payments and inventory.

## Prototype architecture

Users reach a load balancer, which sends traffic to the primary region. A backup region is ready to take over, and CloudGuard watches everything.

Users

Load balancer

### Cloud Region A (primary)

App servers

### Cloud Region B (backup)

App servers

Database replicationprimary and backup copies stay in sync

CloudGuard monitoring

Alert systemtells the administrator

Auto recoveryscales and fails over

## Technology for a student prototype

You do not need a huge production cloud. A simulation is enough to demonstrate the idea, and you can grow it in three levels.

- **Frontend**HTML, CSS, JavaScript. React for a more advanced interface.
- **Backend**Python with Flask or FastAPI, or Node.js.
- **Monitoring**Prometheus and Grafana.
- **Cloud simulation**AWS, Microsoft Azure or Google Cloud. For a simpler project, simulate two regions with two local or server instances.
- **Database**MySQL, PostgreSQL or MongoDB.
- **Containers**Docker.
- **Optional advanced**Kubernetes for automatic scaling and service recovery.

Level 1

### Simulated prototype

A dashboard and two simulated regions. Enough for a clear college demo.

Level 2

### Docker-based version

Each region and service runs in its own container for a stronger project.

Level 3

### Real multi-service deployment

Services deployed across real cloud infrastructure.

## The idea: act without waiting for a human

The strongest part of CloudGuard is the combination of monitoring, prediction and automatic recovery.

### Without CloudGuard

1. Problem happens
2. A human notices
3. A human fixes it

### With CloudGuard

1. Problem is detected
2. System analyzes it
3. System responds
4. Service recovers
5. Administrator receives an alert

You could also add a simple machine-learning model that predicts an upcoming outage from CPU, memory, traffic, latency and error rate.

## What the prototype proves

A cloud-based e-commerce application protected by CloudGuard can:

- ✓Detect abnormal conditions
- ✓Identify which service is failing
- ✓Scale resources during traffic spikes
- ✓Redirect users to a healthy region
- ✓Keep data replicated
- ✓Alert administrators
- ✓Record each incident for later analysis
- ✓Reduce downtime and improve availability

CloudGuard: A Fault-Tolerant Cloud Architecture for Automatic Detection and Recovery from E-Commerce Service Outages

### CloudGuard

Intelligent cloud outage detection and auto-recovery. A college project prototype.

### Jump to

- [Simulator](#simulator)
- [The problem](#problem)
- [How it works](#how)
- [Architecture](#architecture)
- [Tech stack](#stack)
- [Outcome](#outcome)

© CloudGuard project. ShopSphere is a fictional company, and the simulator uses made-up numbers for demonstration only.