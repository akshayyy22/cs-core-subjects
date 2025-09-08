# Scalability and Performance Optimization

## Vertical vs Horizontal Scaling

### **Vertical Scaling (Scale Up)**
Upgrading hardware resources of existing machines - increasing CPU, RAM, storage capacity on a single server.[1][2][3]

**Characteristics**:[2][3][1]
- **Same number of nodes** with enhanced capabilities
- **Simpler management** - single machine to maintain
- **Data migration required** when upgrading hardware
- **Limited by hardware constraints** - finite scalability ceiling

**Example**: Upgrading database server from 8GB to 32GB RAM, 4 to 16 CPU cores.

### **Advantages of Vertical Scaling**[1][2]
- **Cost-effective initially** - upgrading existing hardware cheaper than buying new servers
- **Simpler architecture** - no need for load balancing or distributed coordination
- **Easier maintenance** - single point of management and updates
- **No application changes** - existing applications work without modification

### **Disadvantages of Vertical Scaling**[3][4][1]
- **Single point of failure** - if server fails, entire system goes down
- **Diminishing returns** - exponentially expensive at higher tiers
- **Hardware limits** - cannot scale beyond physical machine capabilities
- **Downtime required** - system offline during hardware upgrades

### **Horizontal Scaling (Scale Out)**
Adding more servers/nodes to distribute load across multiple machines.[2][3][1]

**Characteristics**:[1][2]
- **Increased number of nodes** handling requests in parallel
- **Linear performance scaling** - adding nodes directly improves capacity
- **Data partitioning required** - data distributed across machines
- **Complex coordination** - requires load balancing and distributed management

**Example**: Expanding from 1 database server to 4 servers with sharded data.

### **Advantages of Horizontal Scaling**[4][2][1]
- **High availability** - failure of one node doesn't affect entire system
- **Unlimited scaling** - theoretically no limit to nodes you can add
- **Cost-effective at scale** - commodity hardware less expensive than high-end servers
- **Fault tolerance** - system resilient to individual node failures
- **Regional expansion** - can place nodes geographically closer to users

### **Disadvantages of Horizontal Scaling**[3][1]
- **Increased complexity** - requires distributed system design patterns
- **Higher initial costs** - need multiple machines upfront
- **Application changes** - may require code modifications for distribution
- **Data consistency challenges** - maintaining consistency across nodes is complex

### **Interview Questions - Scaling**
**Q: When would you choose vertical over horizontal scaling?**
**A: For smaller applications with predictable load, tight consistency requirements, or when application architecture cannot easily support distribution. Also when operational simplicity is prioritized.**

**Q: What are the main challenges with horizontal scaling?**
**A: Data consistency across nodes, increased operational complexity, load balancing, potential network partitions, and ensuring fault tolerance while maintaining performance.**

***

## Sharding

### **What is Sharding?**
Database architecture pattern that splits large datasets horizontally across multiple database instances (shards), where each shard contains subset of total data.[5][6][7][8]

**Key Concepts**:[6][5]
- **Shard**: Individual database instance holding portion of data
- **Shard Key**: Column/attribute used to determine data distribution
- **Routing Logic**: Mechanism to direct queries to correct shard

### **Why Sharding?**[7][6]
Traditional monolithic databases face scalability challenges:
- **Performance bottlenecks** from single database server
- **Storage limitations** of individual machines
- **Expensive vertical scaling** with diminishing returns
- **Management complexity** of extremely large datasets

**Benefits of Sharding**:[8][6]
- **Improved performance** through parallel processing across shards
- **Infinite scalability** by adding new shards as needed
- **Cost-effective** using commodity hardware
- **High availability** - failure affects only one shard

### **Sharding Methods**[9][10][5][7][8]

### **1. Range-Based Sharding**[10][5][7][8]
Divides data based on value ranges of shard key.

**Example**: Customer database sharded by name ranges
- Shard A: Names A-I
- Shard B: Names J-S  
- Shard C: Names T-Z

```sql
-- Application logic determines shard
if (customer_name >= 'A' && customer_name <= 'I') {
    route_to_shard_A();
}
```

**Advantages**:[8][10]
- **Efficient range queries** - data naturally ordered
- **Simple implementation** - straightforward range logic
- **Good for time-series data** - chronological ordering

**Disadvantages**:[7][10][8]
- **Uneven distribution** - some ranges may have more data
- **Hotspots** - popular ranges get more traffic
- **Limited flexibility** - difficult to rebalance

### **2. Hash-Based Sharding**[5][9][10][7]
Uses hash function to determine shard assignment based on shard key.

**Example**: User ID sharding
```sql
shard_id = hash(user_id) % number_of_shards
```

**Advantages**:[10][7]
- **Even data distribution** - hash function spreads data uniformly
- **Prevents hotspots** - random distribution avoids concentrated load
- **Scalable** - easy to implement and maintain

**Disadvantages**:[9][10]
- **Complex range queries** - data for ranges scattered across shards
- **Resharding challenges** - adding/removing shards requires data movement
- **No data locality** - related records may be on different shards

### **3. Directory-Based Sharding**[5][9][7]
Uses lookup table to map shard keys to specific shards.

**Example**: Geographic sharding with lookup table
```
Region -> Shard Mapping:
US-East -> Shard-1
US-West -> Shard-2  
Europe -> Shard-3
Asia -> Shard-4
```

**Advantages**:[9][7]
- **Flexible assignment** - can optimize data placement
- **Easy shard addition** - update lookup table only
- **Custom distribution logic** - handle business-specific requirements

**Disadvantages**:[7][9]
- **Extra query overhead** - must consult lookup table first
- **Single point of failure** - lookup table becomes critical dependency
- **Caching complexity** - need to cache lookup table for performance

### **4. Geo-Based Sharding**[5]
Distributes data based on geographical location for latency optimization.

**Example**: Social media platform with regional shards
- Users in US -> US shard
- Users in Europe -> European shard
- Users in Asia -> Asian shard

### **Interview Questions - Sharding**
**Q: How do you handle transactions that span multiple shards?**
**A: Use distributed transactions with two-phase commit, or redesign to avoid cross-shard transactions through denormalization or application-level coordination.**

**Q: What happens when you need to add more shards to existing system?**
**A: Requires resharding - redistributing existing data across new shard configuration, which can be complex and require downtime or sophisticated migration strategies.**

***

## Tricky Edge Cases & FAANG Interview Insights

### **Sharding Edge Cases**

### **1. Cross-Shard Queries**[6]
**Problem**: Queries requiring data from multiple shards become complex and slow.

**Example**: 
```sql
-- This query might need to check all shards
SELECT COUNT(*) FROM users WHERE registration_date > '2024-01-01';
```

**Solutions**:
- **Denormalization** - duplicate frequently queried data
- **Application-level aggregation** - query shards in parallel and combine results
- **Materialized views** - pre-compute cross-shard aggregations

### **2. Hotspotting**[9][7]
**Problem**: Uneven data distribution causing some shards to handle disproportionate load.

**Common Causes**:
- **Celebrity users** generating massive traffic
- **Time-based sharding** with recent data getting more access
- **Geographic concentration** in directory-based sharding

**Solutions**:
- **Hybrid sharding** strategies combining multiple methods
- **Auto-rebalancing** mechanisms to redistribute data
- **Read replicas** for heavily accessed shards

### **3. Rebalancing Complexity**[10]
**Problem**: Adding/removing shards requires data migration which can be disruptive.

**Challenges**:
- **Consistency** during migration
- **Performance impact** while rebalancing
- **Application downtime** requirements

### **Scaling Pattern Edge Cases**

### **4. Split-Brain Scenarios**[4]
**Problem**: In horizontally scaled systems, network partitions can cause multiple nodes to think they're the primary.

**Solutions**:
- **Consensus algorithms** (Raft, PBFT)
- **Quorum-based decisions**
- **Circuit breakers** for partition detection

### **5. Thundering Herd**[1]
**Problem**: After vertical scaling upgrades, sudden traffic spikes can overwhelm newly upgraded systems.

**Solutions**:
- **Gradual traffic ramping**
- **Circuit breakers** and rate limiting
- **Load testing** before full deployment

### **FAANG Interview Patterns**[11][12][13][14]

### **System Design Questions**
- **"Design Instagram/Twitter feed"** - tests sharding user data and content
- **"Design Uber/Lyft"** - geographic sharding and real-time scaling
- **"Design WhatsApp"** - horizontal scaling for messaging systems
- **"Design YouTube"** - video storage sharding and CDN scaling

### **Trade-off Questions**[12][11]
Companies test understanding of:
- **CAP Theorem implications** in distributed systems
- **Consistency vs Performance** trade-offs in sharding
- **Cost vs Reliability** in scaling decisions
- **Complexity vs Simplicity** in architecture choices

### **Real-World Scenarios**[14][11]
- **Black Friday traffic spikes** - when to scale horizontally vs vertically
- **Global expansion** - geographic sharding strategies
- **Regulatory compliance** - data residency requirements affecting sharding
- **Cost optimization** - right-sizing resources and auto-scaling

### **Performance Optimization Insights**

### **6. Connection Pooling**[2]
In horizontally scaled databases, managing connections across shards becomes critical:
```sql
-- Poor: Opening new connections for each shard query
-- Better: Reusing pooled connections across shard operations
```

### **7. Caching Strategies**[9]
- **Local caches** per shard for frequently accessed data
- **Distributed caches** (Redis) for cross-shard data
- **Application-level caching** to reduce database load

### **8. Monitoring and Observability**[1]
- **Per-shard metrics** to identify hotspots
- **Cross-shard query tracking** for performance analysis
- **Rebalancing automation** based on usage patterns

### **Interview Success Tips**[11][12][14]
- **Start simple** - begin with monolithic design, then explain scaling needs
- **Ask clarifying questions** - understand scale, consistency, and latency requirements
- **Consider trade-offs** - discuss pros/cons of each scaling approach
- **Think about operations** - monitoring, deployment, and maintenance complexity
- **Draw diagrams** - visual representation helps explain distributed concepts
- **Mention real examples** - reference how major companies solve similar problems



## References

1. [Vertical Scaling vs Horizontal Scaling – Cockroach Labs](https://www.cockroachlabs.com/blog/vertical-scaling-vs-horizontal-scaling/)  
2. [Horizontal vs Vertical Scaling – Yugabyte Docs](https://docs.yugabyte.com/preview/explore/linear-scalability/horizontal-vs-vertical-scaling/)  
3. [Horizontal vs Vertical Scaling – CloudZero](https://www.cloudzero.com/blog/horizontal-vs-vertical-scaling/)  
4. [Horizontal vs Vertical Scaling in Databases – freeCodeCamp](https://www.freecodecamp.org/news/horizontal-vs-vertical-scaling-in-database/)  
5. [What is Database Sharding – NebulaGraph](https://www.nebula-graph.io/posts/what-is-database-sharding)  
6. [Database Sharding for System Design Interviews – Dev.to](https://dev.to/somadevtoo/database-sharding-for-system-design-interview-1k6b)  
7. [Database Sharding: Everything You Need to Know – Nitor Infotech](https://www.nitorinfotech.com/blog/database-sharding-everything-you-need-to-know/)  
8. [Database Sharding – AWS](https://aws.amazon.com/what-is/database-sharding/)  
9. [Types of Sharding – PlanetScale](https://planetscale.com/blog/types-of-sharding)  
10. [Sharding in Distributed Computing – Hazelcast](https://hazelcast.com/foundations/distributed-computing/sharding/)  
11. [FAANG-Level System Design Interview Questions – DesignGurus](https://www.designgurus.io/answers/detail/faang-level-system-design-interview-questions)  
12. [System Design Interview Guide – Exponent](https://www.tryexponent.com/blog/system-design-interview-guide)  
13. [System Design Interviews – IGotAnOffer](https://igotanoffer.com/blogs/tech/system-design-interviews)  
14. [System Design Interviews (FAANG) – GeeksforGeeks](https://www.geeksforgeeks.org/system-design/system-design-interviews-faang/)  
