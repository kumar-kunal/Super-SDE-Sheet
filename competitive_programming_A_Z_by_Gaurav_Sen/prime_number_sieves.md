### Resource Link
https://www.youtube.com/watch?v=Xxu95iiVcPI&list=PLMCXHnjXnTnucEu8lYMatA23OOi_De3Zp&index=2

### Summary
1. Find all the prime numbers upto 100?

```
import math
def findAllPrimeUpto(n):
    touched = [False]*(n+1)
    sqrtOfN = int(math.sqrt(n))+1
    primes = []
    
    primes.append(2)
    
    for i in range(2, n, 2):
        touched[i] = True
    
    for i in range(3,sqrtOfN):
        if not touched[i]:
            for j in range(i*i, n+1, i*2):
                touched[j]=True
    
    for i in range(2,n+1):
        if not touched[i]:
            primes.append(i)
    
    print(primes)
    
findAllPrimeUpto(100)
```

2. find all the prime numbers in range 999999999140 to 1000000000000? (if range is small i.e. B-A <<< B)


method-1: find all the prime numbers upto 1000000000000 and then filter out which are less than 999999999140.

complexity: O(B*log(B)) approx
It is not suitable for above constraints.


method-2: find all prime numbers upto sqrt(B) using above sieve then use those prime numbers to sieve through range A to B.

```
import math
def findAllPrimeBetween(a,b):
    n = int(math.sqrt(b))+1
    touched = [False]*(n+1)
    sqrtOfN = int(math.sqrt(n))+1
    primes = []
    
    primes.append(2)
    
    for i in range(2, n, 2):
        touched[i] = True
    
    for i in range(3,sqrtOfN):
        if not touched[i]:
            for j in range(i*i, n+1, i*2):
                touched[j]=True
    
    for i in range(2,n+1):
        if not touched[i]:
            primes.append(i)
    
    # print(primes)
    
    range_touched = [False]*(b-a+1)
    range_primes=[]
    
    for prime in primes:
        for i in range(a,b+1):
            if i%prime ==0:
                range_touched[i-a]=True
    for i in range(len(range_touched)):
        if not range_touched[i]:
            range_primes.append(a+i)
    # print(range_primes)
    print("Number of prime between ",a," and ",b," is ", len(range_primes))
        
        
    
findAllPrimeBetween(999999999140,1000000000000)
```

complexity: sqrt(B)*log(sqrt(B)) approx
