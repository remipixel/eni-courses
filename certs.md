# RDS certificate with san 

```
New-SelfSignedCertificate -Subject "rds.remy.tssr.eni" -TextExtension @("2.5.29.17={text}DNS=rds.remy.tssr.eni&DNS=rds&IPAddress=192.168.1.2")
```
