https://www.codewars.com/kata/ipv4-to-int32/train/python

## Task
Take the following IPv4 address: 128.32.10.1 This address has 4 octets where each octet is a single byte (or 8 bits).

* 1st octet 128 has the binary representation: 10000000
* 2nd octet 32 has the binary representation: 00100000
* 3rd octet 10 has the binary representation: 00001010
* 4th octet 1 has the binary representation: 00000001

So 128.32.10.1 == 10000000.00100000.00001010.00000001

Because the above IP address has 32 bits, we can represent it as the 32 bit number: 2149583361.

Write a function ip_to_int32(ip) ( JS: ipToInt32(ip) ) that takes an IPv4 address and returns a 32 bit number.

~~~
  ip_to_int32("128.32.10.1") => 2149583361
~~~

## Best Practices

**Py First:**
~~~py
def ip_to_int32(ip):
    """
    Take the following IPv4 address: 128.32.10.1 This address has 4 octets
    where each octet is a single byte (or 8 bits).

    1st octet 128 has the binary representation: 10000000
    2nd octet 32 has the binary representation: 00100000
    3rd octet 10 has the binary representation: 00001010
    4th octet 1 has the binary representation: 00000001
    So 128.32.10.1 == 10000000.00100000.00001010.00000001

    Because the above IP address has 32 bits, we can represent it as
    the 32 bit number: 2149583361.

    Write a function ip_to_int32(ip) ( JS: ipToInt32(ip) ) that takes
    an IPv4 address and returns a 32 bit number.

    ip_to_int32("128.32.10.1") => 2149583361

    """
    addr = ip.split(".")
    res = int(addr[0]) << 24
    res += int(addr[1]) << 16
    res += int(addr[2]) << 8
    res += int(addr[3])
    return res

~~~

**Py Second:**
~~~py
def ip_to_int32(ip):
    return reduce(lambda acc, x: acc << 8 | x, (int(x) for x in ip.split('.')))

~~~

**Py Third:**
~~~py
def ip_to_int32(ip):
  return int(''.join([(bin(int(x))[2:]).zfill(8) for x in ip.split('.')]),2)
~~~
