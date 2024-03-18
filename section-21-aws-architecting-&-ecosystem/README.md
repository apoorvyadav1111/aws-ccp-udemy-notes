# Section 21: AWS Architecting & Ecosystem

# 257: AWS Whitepapers Well-Architected Frameworks
- AWS Cloud Best Practices:
  - Scalable
  - Disposable Resourses
  - automation
  - loose coupling:
    - monolith
    - break it down into smaller loose components
    - a change should not cascade to others
  - services, not servers
    - dont just use ec2
- 6 Pillars
  - they are synergy
 
---

# 258: Pillar 2: Operational Excellence
- includes the ability to run and monitor systems to deliver business value and to continually improve process and procedures
- design principles:
  - perform ops as a code
  - annotate documentations
  - make frequent, small, reversible changes
  - refine operations procedures freq
  - anticipate failure
  - learn from all operational failures
 
- Prepare
  - use config and CF
- operate
  - use automate,
  - track and trace
  - use CF, config and cloudtrail
  - use cloudwatch
  - use xray
- evolve
  - CF
  - use cicd tools like codebuild, code commit, codedeploy, codepipeline
  -

---
