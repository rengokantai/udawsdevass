### udawsdevass

36.
- ECR: consistency across all aopies of data is usually reached within a second,repeating a read after a shoer time should return the updated data.(best)
- SCR: Returns a result that reflects all writes the received as sucessful response prior to the read

37.
- Local secondary index (5 max) has the same hash key, different range key
  - can only be created when creating a table. They can not be removed or modified later.

- Global secondary index (5 max)
  -has diff hash key and diff range key.can be created later

38.
- Query: finds item in a table using only primary key attribute values. Must provide a hash key attribute name and a distinct value to search for.
- Optionally provide a range key attribute and value, and use a comparison operator to refine the searvch results.
- set the ScanIndexForward to false if want to descending.(by default is evetually consistent but can be changed to be strongly consistent)
- Use projectExpression param so that the Scan only returns some of the attributes, rather than all of then.

39.
- Unit of read provisioned throughput
  - All reads are 4kb
  - Eventually consistent reads(default) consist 2 reads per second
  - Strongly consistent reads consist 1 reads per second
- Unit of write provisioned throughput
  - All writes are 1kb
  - All writes consist of 1 write per second
- (Read calculation problems)
- Ex: 7kb, 8items, stronglyconsistent. Read throughput= ceil(7/4)*8/1=16.
- Ex: 10kb,5items, write consistent=5*10=50
- API Error code: 400: ProvisionedThroughtExceededException( you exceeded your max allowed pro thou for a table or for one or more global sec indexes)

40
- AssumeRoleWithWebIdentity API
- copy ARN from any table, IAM->select role type->role for identity provider access->Grant access to web identity access->select facebook, type in applicationID->next step->policy generator->allow dynamodb(all action),paste ARN. ->Add statement

41
- Idempotent
- Atomic counter(not idempotent), This means that the counter will increment each time you call updateItem 
- BatchGetItem API, retrieve 1MB of data as many as 100 items
43
SQS
- Does not offer FIFO
- 30second min, 12 hours max visibility time out(when you receive a message from a queue and begin processing it, you may find the visibility timeout for the queue is insufficient to fully process and delete that message. You can change hte itmeout by using ChangeMessageViibility action
- long polling max =20sec
- 256kb message size
- billed at 64kb chunks

46
- Create new topic>

48
- The decider is a program that controls the coordination of tasks. their ordering, concurrency, and scheduling according to applicaion logic
- Your workflow and activity flows and age workflow execution itself are all scoped to a domain
- Maximum workflow can be 1 year and the value is always measured in seconds
- SWF task is assigned and is never duplicated.

50
- environment tier(webserver)->create an RDS, Create this a VPC->
52
- create a subnet(CIDR:10.0.1.0/24)
- create second subnet(CIDR:10.0.2.0/24)
- create third subnet(CIDR:10.0.3.0/24)
- Edit route table, by default, the route table can access to vpc itself
- create a new igw, attach to vpc, create a new route table, add target=igw, destination=0.0.0.0/0.
- Attach subnet to route table.
- one subnet can only assoc to one route table.
