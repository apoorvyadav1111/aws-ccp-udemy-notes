# Section 12: AWS Global Infra

[🏠 Go to Home](https://apoorvyadav1111.github.io/aws-ccp-udemy-notes/)

---

# 138: Why?
- app deployed in multiple geographies
- could be regions or edge locations
- low latency
- better experience
- disaster recovery, failover to another region
- attack protection, distributed app is harder to attack
- checkout infrastructure.aws
- global DNS: Route 53
- global CDN: Cloudfront
- s3 transer accelleration
- aws global accelerator

---

# 139: Route 53 Overview
- managed DNS
- collection of rules and records which help clients understand how to reach a server via urls

```
              (myapp.domain.com)
[computer]------------------------------->[DNS Route 53]
    ^ |     <-----------------------------
    | |          (IP: 32.45.67.85)
    \ \
      \ \ HTTP Req to IP___>[  App ]
        _HTTP resp ________ [Server]

```

### Routing Policies:
- simple, no health checks
- weighted: distributed traffic to different servers, some kind of load balancing
- latency routing: looks at the user's location and redirects to the closest server
- failover routing: in failover, the dns will do a health check on the primary and then failover

---

# 140: Route 53 Hands On
- Go to route 53
- go to registered domains> choose a domain name > complete the contain form
- Go to EC2 > Launch with User data change the from text to actual country name
- Create another instance in another region
- Go to route 53
- create records
- record type A
- value will be ip address of the first instance
- latency based policy
- Do the same for another instance

---

# 141: CloudFront Overview
- CDN
- improves read performance
- improves UX
- 216 point of presence
- DDoS protection

### Cloudfront origins
- S3 Bucket
  - for distributing file and caching them at the edge
  - enhanced security with CF OAC
  - OAC is replacing OAI
  - CF can be used as  in ingress( to upload files to S3)

- Custom Origin (HTTP)
 - ALB
 - EC2
 - S3 website
 
### CF at high level
```

    💻 <===============> [CF edge location] <-------------------------> 🪣 or 🖥️
            Get                                fwd to the origin
```

### S3 as an origin
- moves data from s3 bucket (origin) to the edge location via private AWS

### Diff between CF vs Cross Reg Replication
- CF:
  - Global edge n/w
  - files are cached for a TTL (maybe a day)
  - great for static content that must be available everywhere
 
- S3 Cross Region Replication
  - must be setup for each region
  - files updated in real time
  - read only
  - great for dynamic content with low latency in few regions
 
---

# 142: CloudFront hands On

- Create a s3 bucket > upload the files
- using cloudfront without making the objects public
- go to cloudfront
  - new distribution
  - select origin as bucket
  - origin access > OAC
  - create OAC
    - give name
  - update the s3 bucket policy
    - under permissions
  - skip all and disable security protection
  - copy the policy to update
  - go to s3 bucket permissions > edit > paste
  - if missed copying, go to origins > edit > copy the policy from the page
- wait until deployed
- copy and open in new tab


---

# 143: S3 Transfer Acceleration
- increase transfer speed by transferring file to edge location which will forward the data to the s3 bucket in target region
- you test it for all regions

---

# 144: AWS Global Accelerator:
- improve global app and performance using aws global network
- gives up to 60% improvement
- 2 anycast IP are created for your app and traffic is sent through edge locations
- the edge location will send the traffic to your location
- CF vs GA:
  - both use global network and edge locations
  - both use AWS Sheild for DDoS protection
  - but CF caches content at the edge
  - in GA
    - requests are passed to the app via the internal network
    - no caching
    - good for HTTP cases

---

# 145: AWS Outposts
- dealing with hybrid cloud
  - one for the AWS Cloud
  - one for the on premis infra
 
- outposts are server racks that offers same aws infra , services, API, tools to build you app but on on-premise
- aws will setup and manage outposts racks within your on premise infra and you can start leveraging AWS services on premise
- Benefits:
  - low latency
  - local data processing
  - data residency
  - easy migration
  - fully managed service
  - most services work on outposts
 
 ---

 # 146: AWS Wavelengths:

 - wavelength zones are infra deployments embedded within the telecom providers datacenters at the edge of 5g n/w
 - bring aws to the edges of the 5g n/w
 - ex: ec2, ebs, vpc
 - ultra low latency
 - traffic doesnt leave the telecom providers space
 - high bandwidth & secure connection to the parent AWS Region
 - no fees or service agreements
 - use cases: smart cities, ML assisted diagnostic, connected vehicles

---

# 147: AWS Local Zone
- places aws compute storage dbs and other services to end users to run latency sensitive apps
- extend your vpc to more locations
- compatible with ec2, rd, ecs, ebs, elasticache, direct connect
- basically you create a vpc that  spans across regions to provide better connectivity
- Click Zones > Click a region > Click a local zone and enable it
- Now when u create a resource, you can create a subnet with the local zone


---

# 148: Global APP Arch

- single region single az
  - no high av, bad global latency, easy to setup
- single region, multi az
  - high av, bad global latency, easy to medium
 
- multiregion, active passive
  - users can actively read and write in one region, while the other region is passive, data replication is happening, can read but not write
  - global read latency is better
  - global write latency is high
  - high av
  - medium diff

- multi region active active
  - both region active
  - high difficulty to setup
  - low global r/w latency
 
---







