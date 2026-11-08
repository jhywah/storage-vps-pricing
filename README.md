# Storage VPS Server Pricing: Why 1 TB Costs $3 a Month at One Host and $125 at Another, Which Plans Cap Out Early, and What to Check Before You Order (Full Plan Tables)

A terabyte of VPS disk runs from about $3 a month to well over $100, and both ends of that range get sold under the name "storage VPS". The spread comes from what sits under the filesystem: SATA or HDD arrays priced by the terabyte, against NVMe priced as part of a general-purpose server with CPU and RAM attached.

Three tables below cover the decision: every VPS plan SpinServers publishes, the real cost per terabyte across five hosts, and the contract terms that decide whether a cheap plan stays cheap after month one.

> **Quick pick:** If all you need is the most disk per dollar and you can live in a Linux shell, the lowest cost per terabyte in this batch is InterServer at $3/TB/month. If you want one box that also carries real CPU, RAM and bandwidth, SpinServers' published VPS range runs $12 to $89 a month on RAID-10 SSD with 4–20 TB of transfer. 👉 [See SpinServers' current VPS plans and prices](https://bit.ly/Spinservers)

## Every VPS plan SpinServers publishes

SpinServers does not split its catalogue into a storage tier and an application tier. Its VPS page lists application servers with RAID-10 SSD, and the largest single VPS disk on that page is 500 GB. Here is the full lineup as printed, with nothing omitted.

| Plan | vCPU / RAM | SSD (RAID-10) | Bandwidth | Price/mo | Order |
| --- | --- | --- | --- | --- | --- |
| KVM 2 vCPU 2 GB | 2 / 2 GB DDR4 | 40 GB | 4 TB | $12.00 | [ Order](https://bit.ly/Spinservers) |
| KVM 4 vCPU 4 GB | 4 / 4 GB DDR4 | 80 GB | 8 TB | $29.00 | [ Order](https://bit.ly/Spinservers) |
| KVM 6 vCPU 8 GB | 6 / 8 GB DDR4 | 120 GB | 8 TB | $39.00 | [ Order](https://bit.ly/Spinservers) |
| KVM 8 vCPU 8 GB | 8 / 8 GB DDR4 | 160 GB | 10 TB | $45.00 | [ Order](https://bit.ly/Spinservers) |
| KVM 12 vCPU 12 GB | 12 / 12 GB DDR4 | 160 GB | 10 TB | $62.00 | [ Order](https://bit.ly/Spinservers) |
| KVM 16 vCPU 16 GB | 16 / 16 GB DDR4 | 320 GB | 15 TB | $74.00 | [ Order](https://bit.ly/Spinservers) |
| Hybrid KVM 32 vCPU 32 GB | 32 / 32 GB | 500 GB | 20 TB | $89.00 | [ Order](https://bit.ly/Spinservers) |

Every plan ships with a 1 Gbps network port and one IPv4 plus one IPv6 address. CPU, RAM and transfer grow together in a straight line: $12 buys 2 cores and 4 TB of transfer, $89 buys 32 cores and 20 TB. The 160 GB plan appears twice at different price points because the 12-core version doubles the memory and CPU rather than the disk.

One restriction applies across the whole range and appears in bold on every plan block. Port 25 is closed by default. If you need SMTP out, you file a ticket with a justification, and SpinServers reserves the right to refuse. For a backup target that sends failure alerts through its own mail relay, that is worth knowing before you migrate.

Two other things the page leaves open. There is no published trial or refund window for these VPS plans, so confirm the cancellation policy with sales before paying. Region selection is not listed on the VPS page either, so ask which datacenter you are being provisioned in if latency to your users matters.

If your dataset is already larger than half a terabyte, no plan in this table holds it on one volume. SpinServers also sells dedicated servers, which is where terabyte-scale single-machine storage sits in its catalogue. 👉 [Check what SpinServers lists for VPS and dedicated capacity](https://bit.ly/Spinservers)

## What a storage VPS is, and what it will not do

A storage VPS puts capacity ahead of CPU speed and disk IOPS. The workloads that fit are backups, archives, media libraries, file sync and log retention. Every host in this comparison describes the category the same way, and every one of them points database traffic somewhere else.

Onidel states it plainly in its own FAQ: storage VPS uses HDD, HDD has higher latency than NVMe, and databases should go on its NVMe tiers. InterServer sends the same signal from the product page, directing anyone who needs fast disk I/O or application hosting to its SSD-backed cloud VPS instead. Cloudzy sells NVMe but still warns against database workloads on its storage line.

The other surprise for first-time buyers is the interface. InterServer's storage VPS is a command-line Linux environment with root SSH and no GUI or RDP preinstalled. If you were planning to attach a remote desktop and drag files around, that plan will not do it. RamNode gives full root access and expects you to configure RAID and backups yourself. These are self-managed machines in the ordinary sense: you get a shell, an IP and a disk.

## The $/TB table

The category name is identical across hosts, so cost per terabyte is the only number that compares them. Prices below come from each provider's own product page.

| Host and plan | Disk | Price/mo | $/TB/mo | Medium |
| --- | --- | --- | --- | --- |
| InterServer, 1 slice | 1 TB | $3.00 | $3.00 | SATA, ZFS-backed |
| InterServer, 8 slices | 8 TB | $24.00 | $3.00 | SATA, ZFS-backed |
| RamNode, 1000 GB | 1 TB | $17.00 | $17.00 | HDD |
| RamNode, 4000 GB | 4 TB | $64.00 | $16.00 | HDD |
| Contabo VPS 30 | 1 TB | $13.44 (24-mo) / $16.80 | $13.44–$16.80 | SSD |
| Cloudzy, 60 GB | 60 GB | $7.48 | ~$125 | NVMe |
| SpinServers, KVM 16 | 320 GB | $74.00 | ~$231 | SSD RAID-10 |
| SpinServers, Hybrid 32 | 500 GB | $89.00 | ~$178 | SSD RAID-10 |

The 40x spread between $3 and $125 is not a pricing error on anybody's part. InterServer sells a slice as a unit: each one adds 1 TB of SATA, 2 GB of RAM, one core and 2 TB of transfer for $3, and the storage sits on ZFS arrays with special vdevs. You are buying bulk capacity with the smallest possible amount of everything else, capped at a 10 Gbps shared port.

Cloudzy's 60 GB plan costs $7.48 and includes NVMe on AMD EPYC, DDR5, a 40 Gbps uplink, a dedicated IPv4 and IPv6, and KVM with root SSH. The disk is small because the plan is priced as a fast general server, not as a bucket. SpinServers lands in the same territory from the opposite direction: at $89 you get 32 vCPU, 32 GB of RAM and 20 TB of transfer, and the 500 GB of RAID-10 SSD is the least interesting part of the purchase.

Contabo is the awkward row. Its storage VPS line uses SSD, not HDD, so the per-terabyte figure looks competitive while the hardware underneath is a different class from InterServer and RamNode. It also quotes two prices at once, which is the next problem.

## Promo pricing and the second year

Contabo's VPS 10 shows $6.60 and $5.28 on the same page. The small print explains the gap: the displayed price is the effective monthly rate for a 24-month subscription including applicable taxes. Over two years that is $126.72 at the promotional rate against $158.40 at the regular one, a difference of about $31.68. The minimum first term is one month, subsequent terms match it, and postpaid cancellations need four weeks' notice. If you are testing whether a host works for you, that structure matters more than the headline number.

Cloudzy runs the same trick in a different format, listing $3.48 next to a struck-through $6.95 and labelling the whole page 50% off. The discount is real and the original price is disclosed, which is more than most hosts bother to do. When a promotional rate ends, you renew at the second number.

InterServer goes the other way and removes the ambiguity entirely. Storage VPS has no trial period and no money-back guarantee. Billing is monthly and you can cancel whenever you like, but the first payment is not refundable. Cloudzy offers 14 days. Onidel gives 25% bonus account credit on a first invoice instead of a discount. SpinServers publishes no refund terms on its VPS page, so that is a question for support rather than an assumption.

## Four things buried in the plan pages

**Shrinking is close to impossible.** InterServer's FAQ says you can add slices at any time, then adds the line that matters: most filesystems cannot shrink without a reinstall. Buy small and grow, never the reverse. That advice holds for any host selling disk in monthly increments.

**Managed support has a threshold.** InterServer includes managed support only from four slices upward, which is $12 a month and 4 TB. The $3 single-slice plan is self-managed. Support at the higher tier covers security patches, failed services, databases and control panel issues.

**No desktop, no RDP.** InterServer states this outright for its storage line. Budget for SSH and a control panel you install yourself, or pick a different product.

**Port 25 is closed on SpinServers VPS.** Every plan block carries the same note, and opening the port requires a ticket plus a justification that can be denied.

## How the five hosts compare on paper

| Host | Entry plan | Largest disk listed | Billing and refund | Notes |
| --- | --- | --- | --- | --- |
| InterServer | $3/mo, 1 TB SATA | 32 TB | Monthly, cancel anytime; no trial, no refund | CLI only; managed support from 4 slices; 3 US regions |
| RamNode | $4/mo, 160 GB HDD | 4 TB | Hourly ($0.006–$0.095/hr) or monthly; terms not listed | Up to 150 TB bandwidth; Plex, Nextcloud, seedbox use cases |
| Contabo | $5.28–$6.60/mo, 300 GB SSD | 1.4 TB | 24-month effective pricing; refund terms not listed | 9 regions, 11 locations; unlimited traffic under fair use |
| Cloudzy | $3.48/mo, 25 GB NVMe | 240 GB in the price table | Monthly; 14-day money-back | 13 regions; copy mentions 750 GB and 1.5 TB plans the table does not show |
| Onidel | Not published | 10 TB HDD per server | Not published | Ceph triple replication; Sydney and Singapore |

Onidel's plan section renders as a loading state, so no price can be quoted from it. Its architecture notes are still useful: three replicas across separate nodes, 99.999999% durability claimed, and a line in its own FAQ stating that triple replication protects against hardware failure and does not replace backups. That distinction applies to every provider here. Replication is not a backup strategy, and no host on this list takes responsibility for your data beyond the hardware.

## FAQ

**Can I run a database on a storage VPS?**
Technically yes, and none of these hosts recommend it. HDD and SATA latency shows up directly in query times. Put the database on NVMe and keep the storage box for dumps.

**Is 1 TB enough for backups?**
For a handful of servers with deduplicated, compressed backups, a terabyte holds months of incrementals. For raw disk images of several machines, it disappears quickly. Count your full backup size, multiply by the retention window, then subtract whatever deduplication you actually get.

**Does triple replication mean I can skip backups?**
No. Onidel says so about its own Ceph cluster. Replication survives a dead disk; it does not survive a deleted file, a corrupted filesystem or a compromised server.

**Monthly or annual?**
Annual and 24-month terms buy real discounts, as Contabo's two prices show. They also lock you in for the term. If you have not run this workload on this host before, pay monthly for the first cycle.

## Which one to order

Match the workload to the plan rather than the other way round.

- 1–32 TB of archive, backup or media files, shell access is fine → InterServer, $3 per terabyte per month, add slices as the dataset grows.
- Media server or seedbox, hourly billing, up to 150 TB of transfer → RamNode's HDD line.
- European or Asian users, SSD, willing to commit to a 24-month term → Contabo.
- Small NVMe volume, a refund window, 13 regions → Cloudzy.
- One machine that needs 32 cores, 32 GB of RAM, 20 TB of transfer and up to 500 GB of fast local disk → SpinServers' Hybrid plan at $89.
- Sydney or Singapore with distributed storage → Onidel, once you have asked for pricing.

Two checks before any payment goes through. Confirm whether the plan can be downsized later without a reinstall, and confirm what the cancellation and refund terms are in writing, since several of these pages do not publish them. SpinServers' $12 entry plan is the cheapest way to see whether its network and support suit you, and the 500 GB hybrid is the sensible ceiling if the workload stays on one VPS. 👉 [Start with SpinServers' plan list and pick the size you need](https://bit.ly/Spinservers)
