


Example Config 

```
!
class-map match-all HTTPS_MAP
match protocol https
class-map match-all HTTP_MAP
match protocol http
class-map match-all ICMP_MAP
match protocol icmp
!
policy-map G0/0/0_OUT
class HTTPS_MAP
priority percent 10
set ip dscp af31
class HTTP_MAP
bandwidth percent 10
set ip dscp af32
class ICMP_MAP
bandwidth percent 5
set ip dscp cs2
!
int g0/0/0
 service-policy output G0/0/0_OUT
!
```

