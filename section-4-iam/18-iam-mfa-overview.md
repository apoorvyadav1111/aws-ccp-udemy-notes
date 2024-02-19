# IAM - MFA

**Password Policy**
- can setup a pwd policy: length, specific char type
- allow or not to change their pwd
- pwd expiry dates
- prevent reuse

**Multi Factor Authentication - MFA**
- want to protect root and IAM users
- MFA = pwd + security device
- unauthorized individual with a pwd will not be able to do until they have the device
- Device Options
  - Virtual: Google Authenticator (phone only), Authy (multi-device)
  - Universal: U2F security Key example: YubiKey
  - Hardware Key Fob MFA Device,ex Gemalto, SurePassID
  
