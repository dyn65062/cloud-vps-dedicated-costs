# Cloud hosting services: what month three really costs, which tier fits your site, and when a flat-rate VPS is the better buy (full specs and decision rules)

Almost every cloud hosting price you see first is a temporary one. Cloudways, one of the better-known managed platforms, currently advertises its Growth plan at $10/month and returns to $50/month from month three; the same page charges $0.033/GB for offsite backup and $0.02/GB for CDN traffic beyond your allocation. Those three numbers decide most of your bill: the list price, the contract term, and the extras. This guide works from the numbers rather than the marketing, then narrows down to which configuration to buy if you go with Spin Servers, whose KVM VPS line runs from 2 vCPU/2GB to 32 vCPU/32GB on a 1Gbps port with up to 20TB of monthly transfer.

> **The short answer for most readers:** a KVM VPS with a fixed monthly transfer allowance covers one site, a handful of client sites, or a small app stack without metered billing. Price the entry Simple Application Server first (2 vCPU, 2GB DDR4, 40GB RAID-10 SSD, 4TB/month on a 1Gbps port). Move up to 6 vCPU/8GB when several sites or an app plus its database share the box. 👉 [Check the current Spin Servers VPS lineup and pricing](https://bit.ly/Spinservers)

## Spin Servers VPS configurations, side by side

Spin Servers publishes six KVM configurations across two product lines. Everything below ships with 1 IPv4 and 1 IPv6 address, a 1Gbps network port, and RAID-10 SSD storage on the Simple line.

| Configuration | vCPU / RAM | Storage | Monthly transfer (1Gbps port) | Price and order |
| --- | --- | --- | --- | --- |
| Simple Application Server | 2 vCPU / 2GB DDR4 | 40GB RAID-10 SSD | 4TB | [See current price](https://bit.ly/Spinservers) |
| Simple Application Server | 6 vCPU / 8GB DDR4 | 120GB RAID-10 SSD | 8TB | [See current price](https://bit.ly/Spinservers) |
| Simple Application Server | 8 vCPU / 8GB DDR4 | 160GB RAID-10 SSD | 10TB | [See current price](https://bit.ly/Spinservers) |
| Simple Application Server | 12 vCPU / 12GB DDR4 | 160GB RAID-10 SSD | 10TB | [See current price](https://bit.ly/Spinservers) |
| Simple Application Server (Xeon) | 16 vCPU / 16GB DDR4 | 320GB RAID-10 SSD | 15TB | [See current price](https://bit.ly/Spinservers) |
| Advanced Application Server (Xeon) | 32 vCPU / 32GB | 500GB SSD | 20TB | [See current price](https://bit.ly/Spinservers) |

Two things worth knowing before you pick a row.

**Pricing is quoted per configuration at the order step, not in the spec text.** Spin Servers doesn't print a single flat rate table on the VPS page, so open the configuration you want and read the number there, along with the billing cycle it's quoted on. Do that before comparing it against anything else on this page, because a $6 VPS and a $60 VPS both look cheap until you know which one you're looking at.

**Port 25 is closed by default on every VPS.** If you plan to send mail from the server itself, you have to open a ticket with a justification, and Spin Servers reserves the right to refuse. Route transactional mail through a dedicated email provider instead of budgeting for a fight.

## Cloud hosting, VPS, and dedicated servers: where the line actually falls

Cloud hosting pools virtual and physical servers and lets you scale on demand, usually with usage-based billing. Google's own definition of the category describes exactly that: shared underlying resources, elastic scaling, pay-for-what-you-use in most cases. A KVM VPS is virtualized too, but it's sold as a fixed slice at a flat monthly rate with a fixed transfer allowance. You get predictability instead of elasticity.

That distinction matters more than any brand comparison, because it decides which bill you can forecast.

**Buy elastic cloud when:**
- Traffic is spiky and you want capacity to appear without a migration.
- You need adjacent services: object storage, managed databases, a CDN, multi-region failover.
- You want per-hour billing for a short-lived project. OVHcloud bills hourly or monthly; that flexibility is the point of the model.

**Buy a flat-rate VPS when:**
- Load is steady and you can size the box once.
- Bandwidth is the constraint. 4TB to 20TB included on a 1Gbps port covers image-heavy sites, media delivery, and backup traffic that would otherwise generate overage charges elsewhere.
- You want the whole machine to yourself at a known monthly cost, with root access and no metering surprises.

**Go dedicated when CPU is pinned.** Hetzner draws the same line on its own cloud page: shared plans fit test environments, personal sites, small databases, and low-to-medium traffic; dedicated vCPU plans exist for high-traffic sites, large databases, game servers, and machine learning. If your CPU graph sits above roughly 50% for most of the day, shared vCPU is the wrong purchase regardless of provider.

One caveat that applies across the category: ZDNET's 2026 comparison notes that cloud hosting generally requires signing up for a year. The sticker price is often monthly and the commitment is annual. Spin Servers' own offerings span VPS and dedicated servers rather than metered auto-scaling infrastructure, so if you need a platform that provisions capacity automatically at 3am, this isn't that purchase.

## What the second year costs, worked through

Discounts on managed cloud hosting usually cover the first two months. Cloudways currently runs 80% off for two months across its plans, so the arithmetic on its Growth tier looks like this, using the list prices published on its pricing page:

| Item | Promo period (months 1–2) | List price (months 3–12) | Year one total |
| --- | --- | --- | --- |
| Growth plan ($10 → $50/month) | $20 | $500 | $520 |
| 50GB offsite backup at $0.033/GB | $3.30 | $16.50 | $19.80 |
| 200GB CDN overage at $0.02/GB | $8 | $40 | $48 |
| **Total** | **$31.30** | **$556.50** | **$587.80** |

The headline discount saves $80 across the year, not the $480 the banner implies. Nothing improper is happening; the promo is exactly what it says. The point is that a two-month discount barely moves a twelve-month cost, and it moves it less once backups and CDN traffic sit on top of the base plan. Cloudways also charges $1 per 10GB of extra disk and excludes applicable taxes from listed prices, both of which are easy to miss when you're comparing $10 against $50.

Flat-rate VPS pricing removes most of that uncertainty. You still pay for the configuration you chose and whatever the billing term is, but the transfer allowance is stated up front, so the 4TB or 10TB line on the spec sheet is the number that governs your month.

## Picking a Spin Servers configuration by workload

Match the workload, not the spec sheet's best column.

**One site, a staging environment, a VPN endpoint, a small API.** The 2 vCPU / 2GB / 40GB plan with 4TB is enough. A LEMP stack plus a single WordPress install fits comfortably in 2GB; a heavy page builder plus several plugins will start swapping, at which point move up rather than tune.

**Three to ten client sites, or an application with its database on the same box.** The 6 vCPU / 8GB / 120GB plan with 8TB. The RAM jump matters more than the CPU jump here, because MySQL and PHP workers compete for memory long before they compete for cores.

**WooCommerce catalogs, membership sites, image-heavy publishing.** Either the 8 vCPU / 8GB or the 12 vCPU / 12GB, both with 160GB storage and 10TB transfer. The 12 vCPU version buys headroom for concurrent PHP workers during traffic peaks.

**Build servers, game servers, video processing, large databases.** The 16 vCPU / 16GB with 15TB, or the Advanced 32 vCPU / 32GB with 20TB. Below this tier, sustained compilation or transcoding will queue.

If your needs cross into wanting several machines, hourly billing, or managed scaling, look at the elastic providers instead. 👉 [Compare Spin Servers' VPS configurations against your workload](https://bit.ly/Spinservers)

## How the mainstream cloud providers compare

These are the platforms most buyers weigh against a VPS. Positions and limitations below are drawn from ZDNET's January 2026 comparison and providers' own product pages; no pricing is quoted because none of it was verifiable at the configuration level.

| Provider | Where it fits | Billing and plan notes | Known limitation |
| --- | --- | --- | --- |
| AWS | Widest service range and global footprint; the publication's overall pick for 2026 | Pay-as-you-go, free tier to start; EC2, S3, RDS, Lambda, CloudFront, VPC; a European Sovereign Cloud for EU data-residency needs | Steep learning curve; spend climbs with heavy use |
| DigitalOcean | Small projects that want a preconfigured droplet running in minutes | Transparent per-droplet pricing, no complicated tiers | Limited advanced features; fewer data center locations |
| Microsoft Azure | Teams already standardized on Microsoft tooling | Consumption-based, deep integration with Microsoft products, strong compliance tooling | Pricing structure is hard to predict; steep for newcomers |
| Google Cloud | Kubernetes, analytics, and AI workloads that need to scale | Per-use pricing with sustained-use discounts; GKE, BigQuery, Vertex AI | Complex platform; support level depends on your plan |
| OVHcloud | Custom configurations and GDPR-sensitive European projects | Hourly or monthly billing; bare metal, VPS, and network services alongside cloud | Wide product range means specifying exactly what you need |
| Hetzner | EU-based projects that also need Singapore or US capacity | Shared and dedicated vCPU lines; one shared tier currently listed as unavailable; SLA 99.9% with defined credits, 24/7 email support, ISO/IEC 27001 in Germany and Finland, BSI C5 | Shared plans are for test and low-to-medium traffic, not sustained load |

A managed layer like Cloudways sits on top of the first four, which solves server administration but adds its own constraints: it doesn't register domains, and you don't get direct control over the underlying cloud infrastructure. Each layer you add moves you further from the raw machine and closer to a fixed monthly bill you can't tune below the platform's floor.

## Questions that come up before checkout

**Is a KVM VPS the same thing as cloud hosting?** Both are virtualized. The difference is commercial: cloud hosting meters usage and scales on demand, a VPS sells you a fixed slice at a flat rate with a stated transfer allowance. For steady workloads the VPS bill is easier to forecast; for spiky ones the cloud bill is easier to survive.

**How much transfer do I actually need?** 4TB a month works out to roughly 130GB a day, which is far more than a brochure site or a small store consumes. Bandwidth becomes the deciding factor for media hosting, backups, and downloads, which is where the 10TB and 20TB tiers earn their price.

**Can I run email on the server?** Port 25 is closed by default and opening it requires a ticket plus justification, with no guarantee of approval. Plan on a third-party mail service.

**What happens when I outgrow the plan?** With a VPS you migrate to the next configuration, which is a scheduled move rather than an automatic one. If unscheduled scaling is a requirement, the elastic providers in the table above are the correct category.

## Before you order

Two checks decide whether the price you saw is the price you'll pay. First, the billing term: confirm whether the quoted rate is monthly or annual, and what the renewal rate is once any introductory period ends. Second, the extras: transfer overage, backup storage, extra disk, and whether tax is included.

Then size the machine to your actual load. A single site on the 2 vCPU plan costs less and performs the same as a single site on the 8 vCPU plan; the difference only shows up when concurrency does. 👉 [Start with the entry configuration and confirm the current price at checkout](https://bit.ly/Spinservers)
