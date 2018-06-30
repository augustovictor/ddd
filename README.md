# Domain Driven Design

## Strategic design with Bounded Contexts and the Ubiquitous Language

### Bounded context

Contextual boundary where everything about a model is inside.

E.g.: Collaboration (Forum, discussions, posts), Identity and access management (user, role, permission), Support (Support plan, incident)

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
Scenario: The product owner commits a backlog item to a print
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

![ddd-architecture](./img/ddd-architecture.png)

Event-driven Architecture (Event sourcing)

Command Query Responsibility Segregation (CQRS)

Reactive and Actor Model

Rest

Microservices and SOA