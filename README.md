# octets

What percent of IP addresses are unambiguously specifiable without octet delimiters?



def valid(ip):
    return all(map(lambda n: int(n) in range(256), ip.split(".")))

valid = lambda ip: all(map(lambda n: int(n) in range(256), ip.split(".")))


import math
def nCr(n,r):
    f = math.factorial
    return f(n) / f(r) / f(n-r)
nCr(3*4-1, 4-1) == 165
# we will have to check at most 165 combinations


ip = "12345"
for i in range(0, len(ip)+1):
    for j in range(i, len(ip)+1):
        for k in range(j, len(ip)+1):
            r = ip[:i], ip[i:j], ip[j:k], ip[k:]
            if all(r): print '.'.join(r)
1.2.3.45
1.2.34.5
1.23.4.5
12.3.4.5



ip = "654321"
l = len(ip)+1
for i in range(0, l):
    for j in range(i, l):
        for k in range(j, l):
            r = ip[:i], ip[i:j], ip[j:k], ip[k:]
            if all(r): print '.'.join(r)
6.5.4.321
6.5.43.21
6.5.432.1
6.54.3.21
6.54.32.1
6.543.2.1
65.4.3.21
65.4.32.1
65.43.2.1
654.3.2.1



ip = "654321"
l = len(ip)+1
for i in range(1, l-3):
    for j in range(i, l-2):
        for k in range(j, l-1):
            r = ip[:i], ip[i:j], ip[j:k], ip[k:]
            if all(r):
                myip = '.'.join(r)
                if valid(myip):
                    print myip
6.5.43.21
6.54.3.21
6.54.32.1
65.4.3.21
65.4.32.1
65.43.2.1


ip = "654321"
for i in range(1, len(ip)-2):
    for j in range(i+1, len(ip)-1):
        for k in range(j+1, len(ip)):
            r = ip[:i], ip[i:j], ip[j:k], ip[k:]
            print '.'.join(r)
6.5.4.321
6.5.43.21
6.5.432.1
6.54.3.21
6.54.32.1
6.543.2.1
65.4.3.21
65.4.32.1
65.43.2.1
654.3.2.1


ip = "1234567"
for i in range(1, len(ip)-2):
    for j in range(i+1, min(len(ip)-1, i+4)):
        for k in range(j+1, min(len(ip), j+4)):
            r = ip[:i], ip[i:j], ip[j:k], ip[k:]
            print '.'.join(r)
1.2.3.4567
1.2.34.567
1.2.345.67
1.23.4.567
1.23.45.67
1.23.456.7
1.234.5.67
1.234.56.7
12.3.4.567
12.3.45.67
12.3.456.7
12.34.5.67
12.34.56.7
12.345.6.7
123.4.5.67
123.4.56.7
123.45.6.7
1234.5.6.7



ip = "7654321"
for i in range(1, 4):
    for j in range(i+1, min(len(ip)-1, i+4)):
        for k in range(j+1, min(len(ip), j+4)):
            r = '.'.join([ ip[:i], ip[i:j], ip[j:k], ip[k:] ])
            if valid(r): print r
7.65.43.21
76.5.43.21
76.54.3.21
76.54.32.1


ip = "123456789012"
def comb(ip):
    r = []
    for i in range(1, 4):
        for j in range(i+1, min(len(ip)-1, i+4)):
            for k in range(max(j+1, len(ip)-3), len(ip)):
                r.append('.'.join([ ip[:i], ip[i:j], ip[j:k], ip[k:] ]))
                if not valid(r[-1]): r.pop()
    return r

