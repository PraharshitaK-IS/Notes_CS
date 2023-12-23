### Praharshita Krishna
### Notes on 'Designing data intensive applications - Martin Kleppmann'

# Chapter 1
- reliability (tolerating hardware, software faults and human error)
- scalability (Measuring load and performance latency, percentile throughput)
- maintainability (operability, simplicity and evolvability)


" Applications need to:
• Store data so that they, or another application, can find it again later (databases)
• Remember the result of an expensive operation, to speed up reads (caches)
• Allow users to search data by keyword or filter it in various ways (search indexes)
• Send a message to another process, to be handled asynchronously (stream processing)
• Periodically crunch a large amount of accumulated data (batch processing)"

Fault: One component deviating from spec
Failure: System as a whole stops providing required service to the user
#### (Netflix Chaos Monkey - Check)

### Hardware Faults
### Software Errors
### Human Error

Twitter - Home timeline 
The problem: How to create a timeline for twitter users that reduces number of fetches.
Solution: Create a timeline cache for each user that has the tweets of everyone they follow. 
Offload read-time problems to write time by updating these caches everytimne a lead-user tweets.
- Subproblem - How to handle popular users?
Solution: Handle popular users as a special case and fetch them separately. 

## Describind Performance
- what happens when load increases?
- how is system performance affected?
- if you increase load parameter - how do you need to increase resources to keep performance unchanged?

### Response time != Latency
  Response time : What the client sees
  Response time = Service time + Network Delays + Queueing delays
  Latency - Duration that a request is waiting to be handled

High percentiles of response times = Tail latencies
Handling customers with a lot of data in the account - who have the worst response times - p99.9 is important because they are valuable customers (more usage = valuable)
"""Amazon has also observed that a 100 ms increase in response time reduces
sales by 1% [20], and others report that a 1-second slowdown reduces a customer satisfaction
metric by 16%"""

SLO (Service level objectives) , SLA (Service level agreements)

Head-of-line blocking - When a small number of slow requests hold up the processing of subsequent requests
Tail-latency-amplification - Multiple calls to slow backend service - leads to higher proportion of slower responses. 
Efficient wats of approximating percentiles - Forward Decay, t-digest, HdrHistogram

## Approaches for coping with load
Distributing load across multiple machines = Shared-nothing architecture




