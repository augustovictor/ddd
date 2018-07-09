# Domain Driven Design

## Strategic design with Bounded Contexts and the Ubiquitous Language

### Bounded context

Contextual boundary where everything about a model is inside.

E.g.: <a name="collaboration-context">Collaboration</a> (Forum, discussions, posts), Identity and access management (user, role, permission), Support (Support plan, incident)

### Ubiquitous language

The meaning and definitions of terms with within a bounded context.

E.g.: French is spoken in France.

In order to develop a ubiquitous language we should develop scenarios of how specific objects/concepts work with other concepts  within the domain model to accomplish a specific scenario goal.

E.g.:

```
The product owner commits a backlog item to sprint. The backlog item may be commited only if it is already scheduled for release, and if a quorum of team members have approved commitment.

If it is already committed to a different sprint, it must be uncommitted first. When the commitment completes, notify the sprint from which it was uncommitted and the sprint to which it is now committed.
```

Given: Where our model is in a point in time and how its data is set.
When: A specific business operation occurs.
Then: We can assert that certains conditions are met.

```python
# Specification of acceptance test
Scenario: The product owner commits a backlog item to a sprint
Given a backlog item that is scheduled for release
And the product owner of the backlog item
And a sprint for commitment
And a quorum of team approval for commitment
When the product owner commits the backlog item to the sprint
Then the backlog item is committed to the sprint
And the backlog item committed event is created
```

### Domain experts

Has focus on a specific area of the business.

### Definition of bounded context and ubiquitous language

This is achieved by developers working along with domain experts.

Also what is out of a bounded context should be defined.

### Challenge and unify

We use this technique to break the Big ball of mud.

Ask if terms are part of a model.

### Architectures or Architectural patterns

Hexagonal architecture

![ddd-architecture](img/ddd-architecture.png)

Event-driven Architecture (Event sourcing)

Command Query Responsibility Segregation (CQRS)

Reactive and Actor Model

Rest

Microservices and SOA

## Strategic Design with Subdomains

### Subdomain (Area of expertise)
A portion of the business domain.

### Types of subdomain

#### Core domain
Where the organization is making strategic investment in software.

Addresses at what the organization must excel by means of software

How the organization wil distinguish from competitors.

E.g.: Scrum management application

#### Support subdomain

Necessary to support a core domain.

E.g.: [Collaboration context](#collaboration-context)

#### Generic subdomain

Necessary, but generic.

Consider purchasing to avoid heavy investment.

Consider out sourcing its development.

### Dealing with integration complexity of legacy code

![Big ball of mud broken into bounded contexts](img/big-ball-of-mud-to-bounded-contexts.png)

Strive for the ideal modeling composition of 1:1 relationships between the bounded context and subdomain.

![](img/ideal-modeling-composition.png)

## Strategic Desigh with Context Mapping

### Kinds of mapping

- Partnership: Two teams work on two different bounded contexts with a common goal.
    - Visual representation: Thick line
- Shared kernel: At leas two teams have a very similar software model. So they develop a part of the model that both are going to use.
    - Visual representation: Intersection between the two circles with crossing lines fulfilling this part.
- Customer supplier: There is a well defined upstream and downstream between two teams. It means that changes on upstream team impacts the downstream team team. These changes must be negotiated.    
    - Visual representation: Line with U (Upstream) and D (Downstream)
- Conformist: Same as `Customer supplier` but in terms of `Model` where the upstream team model impacts the downstream team model. The downstream team will basically consume the upstream team model only.
- Anti-corruption layer: There is an upstream and downstream team but the downstream team does not want to influenced by the upstream team unnecessarily. Structured as the `Conformist` but the downstream team will consume the upstream team data and translates that to its own model by using an ACL (Anti-Corruption Layer).

- Open Host Service: Well documented and well defined model to consume.
- Published Language: The upstream team produces a well defined and documented exchange format that allows the donwstream team to consume data from upstream team.
- Separate Ways: Describes what kinds of integrations could take place between two teams. But for whatever reason the other team decides to create their own solution instead of consuming what the other team has developed.
- Big ball of mud: Changes in one part of the model impacts a model in another area. In order to integrate with a ball of mud try to use an `ACL` where the ball of mud is the upstream and your model is the downstream.

### Integration patterns with Context Mappig

#### RPC with soap
![](img/rpc-with-soap.png)
![](img/rpc-with-soap-communication.png)

Disadvantage: Due to network failures tasks might not be completed.

#### RESTful HTTP
![](img/rest-http.png)
![](img/rest-http-communication.png)

We can experience the same network issues.

Let clients consume data the way they want.

#### Messaging
![](img/messaging.png)
![](img/messaging-aggregate.png)

If the message is delivered more than once the receiver should be able to deduplicate it.

![](img/message-content.png)
![](img/message-more-info.png)