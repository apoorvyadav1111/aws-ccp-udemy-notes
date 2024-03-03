# Section 12: AWS Global Infra

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

# 141: CloudFront hands On

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







