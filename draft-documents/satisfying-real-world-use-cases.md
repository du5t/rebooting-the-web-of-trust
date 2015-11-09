Rebooting the Web of Trust

# Opportunities Created by WoT to Control and Leverage Personal Data

## Overview

This month (Nov 2015), Facebook's share price broke 100USD/share, for a total
valuation of 290 billion USD. This is evidence that both Facebook and the market
understand the value of controlling and leveraging personal data. On the other
hand, the now-conventional, absorb-everything design of Facebook in which users
are a passive producer to be milked, with no control of their data, is a blunt
one that only scratches the surface of what is possible with networks of
information and identity.

Over the long term, there are limits to the amount of 'trust' (in almost any
sense of the word) a centralized authority can garner: democracies come with the
expectation that citizens be forever watchful of their government, and the
imbalance of power between consumers and corporations is offset by class action
suits and regulatory bureaus--both punitive postures. A decentralized system
engineered *not* to accumulate power as it grows in size avoids this; web of
trust networks in fact increase their credibility as more users provide their
assessments as input. A decentralized system engineered *not* to concentrate
power as it grows in size avoids this; web of trust networks in fact increase
their credibility as more users provide their assessments as input.

Distributed, self-sovereign, cryptographic protocols and structures offer
potential guarantees and applications that offer significantly more robustness,
portability, and versatility than centralized, escrowed, or less-secure
conventional processes.

One of the first technologies to offer this kind of promise emerged 25 years
ago: the "Web of Trust" that grew out of the decentralized, cryptographically
verified attestations of PGP users. Due to failures of UX design, the spread of
PGP was was confined to highly technical communities. Now is the time to extend
them to be usable by all who have access to digital networks and in particular
ensure that marginalized populations can benefit.

In light of light, we consider use cases with stringent demands that require
such robust systems. It is a fortunate tragedy that there is no shortage of
real-life examples of those in the world today. A large spectrum of individuals,
from marginalized persons like stateless refugees, victims of human trafficking,
to members of the informal or unregulated economy, urgently need to participate
in otherwise privileged economic and political fora, but they face technical,
economic, and political barriers to entry.

The essential problem is to connect burgeoning new technological developments
with unmet consumer needs, and vice-versa. In this paper, we present five use
cases, from two relatively simple cases of selective disclosure, to the most
extreme case of establishing government-verifiable credentials from zero for a
stateless refugee.

Basic technical/implementation needs are identified for each case, and a brief
solution sketch is offered. The potential user-experience for each use case is
also outlined. Finally, we examine common themes in discussion, and summarize
future prospects.

## Use Cases

1. Selective Disclosure: Proof of Age
2. Short-term Contracts with Memory: Distributed AirBnB
3. Bootstrapping Long-Term Identity: Creating A Record of Credit
    4. Concerns in Non-G20 Nations
5. Starting From Zero: Refugee
6. Human Trafficking: Exiting Safe Houses

``` below: Each use case should include "why WoT" ```

### Use Case 1 - Selective Disclosure: Proof of Age ###

Beth wants to go to the club with her friends, but lately they've been
photographing all IDs at entry for 'reasons of liability.' Both club owners and
privacy-minded individuals like Beth are understandably concerned about how that
data will be stored and used. The current system requires that the individual
share an ID that gives not only their exact age but their name, address and
additional information unneeded in that context. Beth would like to provide the
minimum information needed to get in (proof that she is over 21 years of
age). The club owner would like to be able to prove later that all attendees
were over 21 years of age if needed, without incurring the liability of securing
the irrelevant personally identifying information (PII). The local government
would like to establish a minimum degree of verifiability of the club's records
without creating an undue liability issue for the club owner.

*Selective disclosure* refers to the process by which a credential holder like
Beth offers *only* the information actually needed by a service provider, for
only the scope (i.e., the amount of time) required for that information to serve
its purpose. Typically, this involves the substitution of a *verifiable claim*
for the actual credential itself; in the case of "proof of age", Beth could
submit a one-time claim responding to a request from the club that her age is in
fact over 21. The club owner need only check that the claim is valid.

A simple sketch of one process satisfying this requirement works as follows:

1. Beth receives a request from the club owner, containing a random unique
   number generated only for this purpose (a 'nonce').
2. Beth signs this number with a private key associated with her driver's
   license as well as a description of the claim she wants to make (i.e.,
   "birthdate earlier than 21 years prior to now"), creating a 'digest'.
3. Beth submits the resulting digest through secure channels to a decentralized
   store whose record of truth (and therefore credibility) is out of the control
   of any one actor, whether government or business. The only guarantee the
   store needs externally provisioned is availability (i.e., uptime).
4. The state checks the request from its end (perhaps by polling for requests)
   to see if it is valid (that it came from Beth and makes sense as a request),
   then signs the result and the nonce, inserting them both into the data store
   as a new digest available to Beth.
5. Beth provides the new digest to the club owner, who can then verify that the
   result was signed by the right authority.

Of course, the actual user experience of this is simple: Beth could scan a QR
code provided by the club owner, and approve the verification request through an
app on her phone. The result is then a different QR code the club owner can scan
to verify. All of the above technical back and forth happens in the background.

Note that at the end of this process, each of the third parties involved know
very little about Beth:

- The state agency storing Beth's driver's license data only knows that Beth
  needed to claim she was older than 21--not where that request came from
  (assuming communications metadata has been dealt with).
- The club owner only knows that the state agency agrees or disagrees with
  Beth's claim, and perhaps which state agency it is.

Expiry dates can be added to the data during each of the steps, ensuring that
data generated at any step is only meaningful in a certain time-limited context,
subject to the regulatory and social needs of stakeholders. Beth may make
adjustments to the request to ensure that the club owner and government are not
in collusion to deanonymize her from either direction. In this way, each of the
mechanisms that provide 'ground truth' or 'trust' are located in different parts
of the system, making it highly resistant to malicious action at any single
point or even a collection of points.

Variations on this theme have been published in academic literature for decades,
beginning with the "blind signatures" of David Chaum et al. (1983) and the "zero
knowledge proofs" of Goldwasser et al. (1985).



### Use Case 2 - Short-term Contracts with Memory: Distributed AirBnB ###

Tisha wants to rent an apartment from Joe for 2 weeks. They each need enough
validated information (such as a home address) about each other, to establish
identity, credit status, legal accountability, and some sort of letters of
reference that are relevant to the proposed transaction. They do not belong to
AirBnB, but would like to be able to create a similar level of assurance.

Tisha generates proof of:
    - Name
    - Legal residence
    - Good credit
    
...as well as (possibly anonymous or otherwise opaquely identified) letters of
reference that Joe can judge.

If Joe accepts Tisha's proofs, they establish a contract (possibly private
between them, at least initially) that sets out the terms of Tisha's stay. The
result of that contract (fulfilled or broken) can later be used in a similar
fashion for subsequent stays with others.

A simple sketch of a system that could satisfy these requirements is as follows:

1. Tisha maintains basic demographic identifiers securely as in Use Case 1, in a
   distributed, cryptographically verifiable, append-only repository.
2. Tisha and other users can 'bootstrap' some limited degree of reputability by
   having friends issue 'letters of reference' on her behalf, which could be as
   simple as ratings or actual letters submitted to the repository attached to
   their accounts.
3. Anytime Tisha arranges a short-term contract herself and relative strangers,
   she invites them to submit proof of the contract and its result, with a
   rating or comment, to the same repository. Contracts created in this fashion
   are linked in the data repository by incorporating signatures (or signature
   transactions) of all parties, once at establishment, and (optionally) once on
   fulfillment.

Technology Possibilities

Contracts as mentioned above are a common application for decentralized
verifiable data stores: implementations targeting this area include the 'smart'
contracts of [Eris Industries](https://erisindustries.com/) and
[Ethereum](https://www.ethereum.org/), and the 'link' contracts of
[XDI](http://xdi.org/). Both of these types of offerings include expirable
permissions, and context-limited pseudonyms.

Users are both ready and willing to protect their identities in this fashion
during short-term arrangements: the AirBnB app collects an
[inordinate](http://www.theguardian.com/money/blog/2014/nov/14/airbnb-wont-let-book-room-facebook-friends)
and
[unacceptable amount](http://www.huffingtonpost.ca/kris-constable/airbnb-privacy-security-id-jumio_b_4887509.html)
of
[personally identifying information](http://www.smh.com.au/business/turbulence-for-airbnb-over-privacy-concerns-20150216-13g8tm.html)
from its users. On the other hand, craigslist has included per-listing email
obfuscation for years now, and the Berkman Center for Internet & Society at
Harvard maintains
[a massive list of services and frameworks](http://blogs.law.harvard.edu/vrm/development/)
that regard the user as the initial and final arbiter of information exchange.


### Use Case 3 - Bootstrapping Long-Term Identity: Creating a Record of Credit

Darla is a citizen of a G20 nation, but lacks a deposit account, extensive
credit history or reputable documentation of local residence. She can afford a
secure digital device however, and through it, she can sign up for an account
(whose marginal cost is close to zero). She would like to be able to store money
with a bank or other institution (credit union, etc.) and build a credit rating,
but can't meet current minimum requirements set by the bank through conventional
channels. In other words, she needs to cross a
['gap' of credibility](https://en.wikipedia.org/wiki/100_point_check) needed to
enter the conventional world of credentials.

In this case, the technical solution is similar to previous cases, excepting
that the desired result is a private credential, a reusable link to a
conventional financial record, held by the account holder, of validity (in this
context) equal to a fixed address. A sketch:

1. An independent organization sets up a data store for storing verifiable
   claims submitted either by the state or Darla.
2. The independent organization onboards Darla and ensures she understands the
   guarantees of privacy offered, and that her credentials do not fundamentally
   depend on the state.
3. The state, in concert with the independent organization, signs Darla's
   initial claim, deeming it to be of sufficient strength to accomplish tasks
   like the above.
4. Darla submits proof of the state's approval of her established identity and
   any attributes (cf. use case 1) additionally required by the bank, and
   establishes a conventional account.


The systemic approach in this case is to check first the Know Your Client and
Anti-Money Laundering regulations of the jurisdiction or country that one aims
to approach. The once the regulatory compliance identity criteria are
established, establish the delta between the existing quality of identity and
the required quality of identity. Then build common processes for improving
identity to a level that passes the KYC/AML tests; which are the barriers to
accessing established financial services.

Preserving low cost of access and progressive establishment of reputation are
essential to maintaining accessibility.

Technology Possibilities

>> XDI feature: link contracts are p2p agreements about disclosure, sharing, and
>time of data > in this particular case, user is covered by protective
>stipulations without 'right to be forgotten' > XDI (if well-implemented by bank
>and rating agencies) will enable user's ability to dispute erroneous or
>malicious financial rating or activity associated with her account--tool that
>empowers user and enables efficient detection of possibly fraudulent activity:
>sunshine+transparency

#### Concerns in Non-G20 Nations

In the The Mystery of Capital: Why Capitalism Triumphs in the West and Fails
Everywhere Else, Peruvian economist Hernando de Soto highlights a fundamental
difference between Western liberal democracies and other regions: such
democracies have functioning systems that enable the abstract representation of
value. For example, land is not simply owned territory--it is private property
registered with the state and represented by land deeds; the representation
having the force of law in disputes.

Millions of individuals do not have such representative records (birth
certificates etc.) registered with government entities, and such entities may
not be reliable enough to serve this role. Worse, many marginalized people may
either be prohibited from creating records that might enfranchise them, either
through legal exclusion or threats of violence. The Gates Foundation considers
this issue
[one of their 8 global priorities](http://www.gatesfoundation.org/What-We-Do/Global-Development/Financial-Services-for-the-Poor):

> Worldwide, more than 2.5 billion adults do not have an account at a financial
> institution, according to the World Bank's Global Financial Inclusion
> Database. Only 41 percent of adults in developing economies have an
> account—and that number drops to just over 20 percent among adults living in
> extreme poverty. Women, in particular, are largely excluded from the formal
> financial system. In developing countries, only 37 percent of women have
> accounts, compared to 46 percent of men.

They also highlight research showing that "the most effective way to
significantly expand poor people's access to formal financial services is
through digital means."

With that in mind, consider the following use case:

Farhad is a migrant worker at a mine in, with no fixed address, yet receives a
regular wage in cash, which he would like to store in a secure account. He has
no recurring bills or credit bureau profile; yet turns up for work on time over
day, 6 days a week, 50 weeks a year, is known by multiple locations by the same
name and travels in the same geographies. He needs to be able to turn this
accumulated consistency into a portable, self-sovereign record of this economic
reliability that others can assess and verify, so he can store fiat currency,
pay bills, and gain access to credit.

Farhad is without state or financial institutional support, which changes the
dynamic from the previous case. On the other hand, the regulatory burden is
expected to be lower by the same token. What Farhad needs is a way to take the
same semi-informal exchanges mentioned in previous use cases and bundle them up
into a highly-available, privacy-respecting, verifiable record of credible
activity--the basic information required for a consumer-facing financial market.

A sketch of this is as follows:

1. An independent organization sets up a distributed store of data that can be
   reached by users like Farhad with minimal equipment (say, a low-grade
   smartphone with data).
2. Farhad bootstraps his financial record with verifiable records of work and
   other met commitments, in conjunction with clients, employers, and other
   financial actors in his sphere (cf. use case 2).
3. With this record (and possibly an associated cryptocurrency where needed),
   Farhad can now make both local and electronic purchases with increased
   leverage.
4. Financial service companies can now make anonymous queries a la Craigslist,
   sending offers to users who meet a raft of criteria. Farhad can choose to
   submit anonymous claims that he meets different criteria, allowing him to
   receive these offers or apply directly for loans and other financial
   aggreements directly.

With the rise of distributed computing, it is possible to use it to support
individuals like Farhad in representing themselves--allowing them at last a
self-sovereign identity that they create and control. Through it, they can link
together their interactions/transactions and leverage it to create an abstract
representation of themselves. This type of identity can empower unbanked people,
beginning with a 'secure kernel' of identity that is taken for granted by
holders of state-issued identity documents. Such a 'secure kernel' can allow the
accounting of, and provision for, basic social needs like health insurance and
credit--privileges in the Global North that are considered dire needs of
citizens in the Global South.

Under such a system, Farhad's records are not exposed to surveillance, nor to
(financial) corruption. At the same time, claims issued in that space, whether
negatively or positively affecting his reputation, are as verifiable as any
other transaction, preferably by any user. Transaction history is not revealed
to merchants or financial service providers, nor is activity. What is available
is a verifiable record of commitments--contracts and their fulfillment
status. NB: Mechanisms of
[differential privacy](http://research.microsoft.com/pubs/64346/dwork.pdf) may
be needed in this case, to prevent semi-aggregated queries from permanently
reducing the privacy of users whose data is contained in the store.

```[FOOTNOTE]: It is critical to understand the difference between this type of
self-sovereign identity is different then just anchoring transactions to a phone
number. Individuals DO NOT have control over phone number in the same
manner. Phone numbers are rented from the phone companies and are re-assigned
(given to someone new) when one stops paying one's bill.)```

### Use Case 4 - Starting From Zero: Refugee ###

Yevgeni is a member of a persecuted or targeted class in his nation of
citizenship and residence. He does not feel safe carrying identity documents
with him when he flees--information asserting his grounds for asylum must bypass
local centralized data stores, as it could be used to harm him (i.e., records
identifying or locating individuals could be seized by a new hostile regime).

In order to meet this need, a secure, privacy-respecting data store must be made
available to the legal jurisdiction of the host government. Since refugees often
move through multiple state territories, and would prefer to avoid setting out
new permanent personal records in a new nation under complete surveillance, said
data store should be maintained independently (as in the previous use cases)
from the states themselves.
 
Such a technology can empower Yevgeni to create a self-sovereign 'anchor' of
identity--whatever documentation or information he has can be stored as
statements or photographs to be used for claims later. A prospective host
government can poll the store, obtaining proof of identity attributes that only
he can access directly, satisfying the host government's documentation
requirements. Yevgeni is able to leave his country on the accepting government's
terms without excessive risk, and at immigration uses his self-sovereign
identity to enter.




Commentary


Despite what is sometimes assumed the identity of people does not from
states. People get identity documents from the state that enable/empower them to
iteract with states over their life cycles. States issue to/provide for the
citizen identifiers that is for that context. One way to "prove" an identity is
to present identity documents from a state but what happens when there isn't a
functioning state to issue such documents or an individual is not privileged
enough to get access getting these documents.


People share social contexts the are in community with each other and through
social relations we create webs of human connection. It is possible with
self-sovereign identities for different people - each with their own
self-soverign identities.  It is possible for this web of connection to be
documented digitally by people vouching for each other and establishing this web
of connection digitally.  Creating this type of network to socially validate an
identity is why this aspect of the technology is called a Web of Trust.

This network of connection that can be documented securely between individual's
sovereign source identities could serve as another seed to bootstrap an identity
with a new jurisdiction and document circumstance.

 
 

>> double-check government terms-labels > explain self-sovereign identity



>> make sure definition of WoT and identities registered to it are clear >
>consider using Kaliya's topologies of identity models > explain threat models
>at each point of refugee's journey > make sure biometrics can be later disabled
>or deleted as desired (ask christopher) > explain how motes of refugee's
>identity can be maintained (while respecting privacy) by NGOs and governments

>> technical: blockchain(-like) structure, XDI for semantic interoperability,
>provable claims, biometric-type identification, attestations (by refugee
>workers for example)



### Use Case 5 - Trafficking / Safe Houses ###

Marsha is a victim of human trafficking who has been rescued by a local group
and conveyed to a safe house. She may have an identity card/identifier issued to
her by the state - however she does not trust the local state actors/office
enough to present to them using it to access benefits (she may be re-victimized
by them if she does). An aid organization and/or government is willing to
provide resources (financial, food, education) to her and others like her, so
that she can re-normalize her life.

>> reference MVC article:
>https://modelviewculture.com/pieces/sex-work-and-surveillance quote or
>explicitly reference reality

A caseworker provides Marsha with portable, manageable equipment for storing and
protecting identity attributes, and assists her with setting up core
attributes. Marsha then submits repeated proofs of her identity and (changing)
status for compliance purposes to the aid organization or government, which is
then able to account for the aid provided. When Marsha finally leaves the safe
house and resumes independent life, she is sure that her private information
leaves with her.



Basic needs:
    - A protocol for establishing a set of 'core' initial attributes
    - Strong guarantees of selective-only disclosure
    - Desirable: A way to 'reconstruct' still-valued components of a previously
      poisoned or toxic identity (i.e. friends or relatives prior to event)
      without risking attack or subsequent victimization
    - Clear threat models at every step of the process


The key to meeting these needs is to provide an individual services across time
and space, in a way that avoids duplication and provides for continuity of care
(medically)--in other words, persistent correlatable claims.  An independent
organization can issue these with the consent of the individual client,
achieving this result for the client without compromising her privacy. Thus
avoiding touching the formal state systems that she mistrusts.

In other words, the independent organization is dis-intermediating the state
issuance of identity documents/identifiers. This is useful when a local state
actor/office is mistrusted by Marsha. She is willing to have the independent
organization mediate the provision of support services to her via government aid
from a different department of level of government.

>> issues to explain
- DELEGATION (in initiating record, obtaining attestations)
- STEWARDSHIP (of vulnerable or short identity record)
- Limited Liability Persona
  - http://bgidps.typepad.com/bgidps/2007/10/llp-in-the-new-.html
  - https://www.youtube.com/watch?v=Lazg31TN8FE
  - http://www.slideshare.net/Kaliya/identification-and-social-justice-

>> issues: possible spouse with financial access to old accounts > not just a
>"fresh" identity; selectively expunging old identity > avoiding "stepping on
>land mines" by reconnecting old identity components > technical: code
>establishing new identity needs to provide *extremely* robust bridge to old
>identity attributes as desired

## Discussion


Unsolved problems and (technical) edge cases: >> human, policy, technical
divisions: add remaining issues from above

- Bootstrapping from self-affirmed identity attributes
- Swapping in 'proof of X' for 'X' in (all) transactions where someone's
  identity is read
- Manageable and portable equipment for storing identity information and making
  strong (yet opaque) claims with precise scope

>> list unsolved problems


Basic needs:
    - Public-facing interfaces for initial identity creation (no hardware
      requirements imposed on refugee)
    - No storage/infrastructure requirements imposed on refugee (cost of
      storage/transactions subsidized)
    - No risk creation by a central data store that could be comprimised
      creating physical risk (Citizens religion identified through hospital
      records, to then be traced and exterminated due to clash with dominant
      powers religion)
    - Concordance between amount of information provided by refugee and amount
      initially required by accepting government

Implementations that meet these needs center around the process of
enrollment. In other words, how does an identity for a person become
instantiated in a technical system?

    - Person presents - doesn't have an ID in ID2020 system
    - What are they asked for? name etc...
    - How is this record in a database/digital system linked to "them"
     - Is a biometric captured to alow them to present themselves again in the
       future and be authenticated. could this be voice?
    - The digital root of this ID is rooted in a decentralized network - The
      identifiers are "validated" by workers at the NGO and potentially also
      family members enrolled in the same system.


Although the demands illustrated by the use cases we present are quite serious,
we note that there have never been so many legally unencumbered technical and
expert resources for this application as there are at present. We believe that
the main challenges ahead are those of systems integration and widespread
adoption, for which the prospects are good. Given adequate funding, we are
certain that the challenges illustrated above can be met, >> come up with nice
wording here later.

>> unprecedented historical opportunity--evolution not only of internet as
>infrastructure but turning point of human culture: first time in history
>identities can be represented and communicated in a fashion that transcends any
>centralized authority, empowering every actor in the system to be a unique
>person, community, company or government, obtaining the assurances they need to
>operate and engage in interactions that require peristance across time and
>space - a trust of sameness, including the underprivileged and marginalized to
>realize an incredibly economically and socially beneficial improvement for
>humankind.

Privacy-respecting, secure (in the senses defined above) distributed systems are
uniquely able to both accurately chart this experience, as well as empower us to
foster or develop identities that have never been possible before. While this is
great news from a technological standpoint, the same systems can certainly also
be employed in a coercive manner. At worst, large-scale information
systems,whether centralized databases with essentially unlimited storage
ordecentralized append-only structures, could near-permanently foreclose the
disjoint, varied, and possibly contradictory nascent identities of masses
ofpeople going forward. (Imagine if a government ID system was coupled with an
undeniable append-only log, fed by a ubiquitous surveillance system--then
placeit at different points in history.)
