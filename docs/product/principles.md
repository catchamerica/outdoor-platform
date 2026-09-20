# Product Principles

> Status: approved v1.

These principles guide product and architecture decisions across the platform.
They are durable, so they should outlast any single feature, provider, or
release. They do not describe implementation or requirements. When a decision
conflicts with a principle, raise it rather than working around it.

1. **Build for Catch America now, but do not hard-code Catch America into the
   platform core.** A real operator with real needs keeps the work honest.
   Operator-specific assumptions stay out of the core so another fishing or
   outdoor company can run on the platform later.

2. **Fishing is the first domain pack, not the platform itself.** Fishing
   vocabulary, rules, and data shapes belong to the pack. The core stays
   domain-neutral.

3. **Knowledge belongs to the platform, not to an AI model.** The platform
   stores and governs what we know. Nothing durable exists only inside a model.

4. **AI providers and models are replaceable.** Changing a model or vendor must
   not require changes to domain code.

5. **AI may propose, summarize, structure, reason, and assist. It does not own
   truth, business rules, authority, or persistent memory.** AI output is an
   input to a decision, never the decision itself.

6. **External providers are integrations and adapters, not the domain model.**
   Systems such as Shopify, Klaviyo, QuickBooks, Meta, weather providers, and AI
   providers are mapped to our own types at the edge.

7. **Knowledge must preserve source, provenance, perspective, time, evidence,
   uncertainty, corrections, invalidations, and legitimate conflicting
   viewpoints.** Two credible experts can disagree and both be worth keeping.
   The platform holds the disagreement instead of flattening it.

8. **Declared, observed, inferred, and contextual information about a
   participant must remain distinguishable.** What someone told us is not the
   same as what we watched, what we derived, or what their situation implies.
   Keeping them separate prevents an inference or a behavior from being mistaken
   for an explicit fact.

9. **Every piece of participant data we ask for should create an obvious benefit
   for that participant.** If we cannot name the benefit, we do not ask.

10. **Fresh first-party field intelligence is a central source of differentiated
    value.** It comes from experts and from people actually in the field.

11. **Create knowledge once and reuse it across experiences and channels.** A
    contributor should give us something one time, and the platform carries it
    wherever it is useful.

12. **Customer-facing experiences are designed and approved before
    implementation.** That includes screens, flows, copy, empty states, and
    error states.

13. **Do expensive intelligence ahead of the user whenever possible.**
    Interactive experiences consume prepared intelligence and stay fast.

14. **When a participant is actively fishing, the product enters Fishing Mode:
    an on-water experience focused solely on helping the participant fish.**
    Fishing Mode contains no ecommerce, promotions, campaigns, or selling.

15. **Experts and contributors should spend less time contributing than the
    value the platform creates for them.** Keep contributor effort low and make
    the return clear.

16. **People should be able to communicate naturally by voice, text, photo, or
    video.** AI does the structuring where appropriate. Natural input plus AI
    structuring should reduce unnecessary structured data entry.

17. **Automation executes approved policy. It does not invent policy.** If no
    approved policy covers a case, automation must not invent or infer the
    missing policy. The appropriate approved workflow may stop, escalate, or
    route the case for human review.

18. **Business rules must be explicit, versioned, approved, and testable.** A
    rule that lives only in someone's head, in a model, or in a conversation is
    not a rule we have.

19. **Retain source and provenance for externally acquired facts, observations,
    rules, measurements, signals, and content.** We should always be able to say
    where something came from.

20. **Historical records should not be silently rewritten.** Corrections,
    reversals, supersession, and invalidation preserve auditability, so the
    earlier state stays visible alongside what replaced it.
