# Actors

> Status: approved v1.

## Modeling Principles

- Person and Organization are the foundational entities.
- Customer, Participant, Expert, Guide, Contributor, Collaborator, Employee,
  Provider, and Subscriber are contextual roles or relationships. They are not
  mutually exclusive Person types.
- A Person may hold multiple roles at the same time, and roles may vary by
  Organization, Activity, Location, or other context.
- An Organization may also hold multiple relationships and roles.
- A guide service is an Organization. Individual guides are People related to
  that Organization.
- Subscriber is a relationship and state created by a Subscription, not a Person
  type.

## People and Roles

**Participant**

- A Person participating in an outdoor Activity.
- In the Fishing domain, Participant may be presented to users as an angler.
- May learn, follow, plan, express Trip Intent, create Watches, check in, use Fishing Mode, record outcomes/catches, contribute content/reports, participate in community, book services, subscribe, and earn/use rewards where applicable.

**Customer**

- A Person or Organization with a commercial relationship to an Organization.
- May purchase products, book services, hold orders, receive offers where permitted, participate in subscriptions, use rewards, or otherwise engage commercially.
- Customer status does not imply participation in the outdoor Activity, product ownership, product use, or expertise.

A Person may simultaneously be both a Participant and Customer.

**Expert**

- A contextual role representing recognized expertise.
- Expertise may apply to specific Activities, Locations, species or targets,
  methods, techniques, or subjects.
- Expertise is contextual and is not universal authority.
- Experts may contribute, verify knowledge, review and correct Max, provide
  Catch Therapy, create content, and earn cash and/or reward currency.

**Guide**

- A Fishing-domain and service-provider role held by a Person.
- May operate independently or through a guide-service Organization.
- Can maintain their profile, expertise, availability, services, schedule, field
  reports, bookings, customer context, and contributions.

**Contributor**

- A Person or Organization supplying content, observations, reports, research,
  verification, feedback, product testing, corrections, or other useful
  contributions.
- A Participant, Expert, Guide, Collaborator, or employee may also be a
  Contributor.

**Collaborator**

- A Person or Organization working with another Organization on content
  creation, promotion, research, product testing, photography and video,
  influencing, ambassador work, or another project.
- Does not need to be an Expert or an employee.

**Internal Team Member**

- A Person working within an Organization.
- Responsibilities may include leadership, marketing, content, community and
  customer service, operations and fulfillment, finance, product, or other
  business functions.
- Job responsibility and platform permissions are related but not identical
  concepts.

**Provider**

- A Person or Organization offering a Service.
- Guide is one fishing-specific Provider role. Future domain packs may introduce
  other provider roles.

**Platform Administrator**

- A Person operating the underlying platform rather than one outdoor
  Organization.
- Platform administration stays distinct from Organization-level administration.

## Organizations and Relationships

**Guide Service / Provider Organization**

- An Organization that offers services through one or more Providers or Guides.
- May have owners and admins plus multiple individual guides.
- Can manage organization-level services, team membership, availability,
  bookings, business information, and approved customer communications.

**Organization in Partnership**

- An Organization taking part in an organization-to-organization partnership.
- Partnership context can include joint campaigns, products, content, research,
  referrals, bookings, services, or other approved collaboration.
- The underlying entity is an Organization.
- Partner describes the relationship between organizations.
- Being in a partnership does not create a permanent Organization type.

**Retailer / Dealer**

- An Organization taking part in wholesale and resale relationships.
- May purchase products, receive dealer pricing, access product education and
  assets, take part in launches or marketing, and interact through approved B2B
  capabilities.

### Relationship Examples

- Person works_for Organization
- Person owns Organization
- Person guides_for Organization
- Person or Organization contributes_to Organization
- Organization partners_with Organization
- Organization supplies Organization
- Person or Organization provides Service
- Person participates_in Activity

These are conceptual vocabulary only. They are not implementation enums, and the
list is not exhaustive.

## Important Boundaries

- Role is not identity.
- Account is not Person.
- Customer is not the same as Participant.
- Expert is not the same as Guide.
- Guide is not the same as a guide-service Organization.
- Contributor is not the same as creator, rights owner, or subject of a
  contribution.
- Partner is a relationship, not an Organization type.
- Subscription status does not define Person identity.
