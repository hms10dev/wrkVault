 # Change Management

## Date: Aug 2, 2022

---

## Change Management, What is it?
- Change Management which is part of the Entity Framework provides capabilities for detecting changes to an entity and raise events.
- Developers will be able to register custom action methods to the events and execute their business logic.

### Example:
``` java
@Override
public void setFoundingYear(Integer foundingYear)
{
    DataValidationInvoker.validate(Integer.class.getName(), "FoundingYear", foundingYear, this.getEntityName(), this);
    if (this.foundingYear != null ? this.foundingYear.equals(foundingYear) : foundingYear == null)
    return;
    saveOldValue(Fields.FOUNDING_YEAR.getCode(), this.foundingYear);
    ChangeEventManager.getInstance().addChangeEvent(ChangeEventTypes.FIELD_FOUNDING_YEAR, this);
    this.foundingYear = foundingYear;
}
```



## Types of Change Events
- When an entity is created/updated, the following events are raised by default:
#### Field Events
- When a field is getting changed as a part of create/update process, the field events are raised

#### Group Events
- Developers can define multiple fields under a single group and when any of the fields within a group is changed, the group level event is raised.
	- For example, *subTotal*, *totalCharges* and *totalTaxes* in the **Order** entity can be defined under a single group called "totals" and when any of the fields change, **order** total can be recalculated.

#### Entity Events
- When child entity is added or removed, the entity level event is raised.
	- For example, Entity::[^1]OrderLine::Add event is raised at the Order level when an order line is added to Order.

[^1]: "of"

> The child entity event is raised in case of both Primary Key or Business Key based relationships. However in case of Business Key based relationship, these events are raised only when the child entity is created as part of the parent entity. If the child entity is created/removed using the child entity specific service, these events are not raised.

## Subject 3

- study of graphs began in 17366, Leonhard Euler's Sever Bridges of Konisberg
    - study: find a path that would cross every bridge only once
    - no such path could be found

### SubSubject

- four-color theorem
- GPS/maps

### SubSubject 2

- Social networks, such as facebook, twitter, and instagram
- gene/protein expression networks

## Equation Example:

$$
G = (V,E)
$$

- n vertices V ((nodes))
- m edges E (links)
- all elements are unique, aka **no repeated values**
- each edge is defined by its starting and ending edges.
    - ex: (a,b)

--- 

# REVIEW :

# Vocab:

- **undirected** graph
    
    $e =(u,v)∈ E ⇒ (v,u)∈ E$
    
    in other words, its possible to go from u to v, and vice versa
    
- **directed** graph
    
    it is not possible to go from u to v and vice versa
    
    so the 
    
    $e =(u,v)∈ E ⇒ (v,u)∈ E$
    
    equation does not hold..
    
- self loop
    
    the starting and ending vertices are the same 
    
    i.e. e=(v,v))
    
- path
    
    A path is a sequence of vertices (v1,v2,...,vk), such that vi+1 is a neighbor of vi .
    


## The notes review:

- question 1
- question 2
- question 3
- question 4

## Questions for next time

- [ ]  question 1
- [ ]  2
- [ ]  3
- [ ]  4
- [ ]  5
- [ ]  6
- [ ]  7
- [ ]  8
- [ ]  9
- [ ]  10
