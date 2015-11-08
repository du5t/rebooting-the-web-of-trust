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

Distributed, self-sovereign, or [why is this OR and not AND?] cryptographic
protocols and structures offer potential guarantees and applications that offer
significantly more robustness, portability, and versatility than centralized,
escrowed, or less-secure conventional processes. The first instantiations of
technologies to do this emerged 25 years ago and the peer-2-peer architecture
was called a Web of Trust and usage was confined to highly technical
communities. Now is the time to extend them to be usable by all who have access
to digital networks and in particular ensure that marginalized populations can
benifit.  A decentralized system engineered *not* to accumulate power as it
grows in size avoids this; web of trust networks in fact increase their
credibility as more users provide their assessments as input.



We are considering use cases with stringent demands that require such robust
systems, and a fortunate tragedy that there is no shortage of real-life examples
of those in the world today. A large spectrum of individuals, from marginalized
persons like stateless refugees, victims of human trafficking, to members of the
informal or unregulated economy, urgently need to participate in otherwise
privileged economic and political fora, but they face technical, economic, and
political barriers to entry.

The essential problem is to connect burgeoning new technological developments
with unmet consumer needs, and vice-versa. In this paper, we present five use
cases, from two relatively simple cases of selective disclosure, to the most
extreme case of establishing government-verifiable credentials from zero for a
stateless refugee.

Basic technical/implementation needs are identified for each case, and a brief
solution sketch is offered. The potential user-experience for each use case is
also outlined. It should be noted that often this "last mile" of any solution
requires intensive research and field testing to ensure the sucessful adoption
by real people and institutions. Finally, we examine common themes in
discussion, and summarize future prospects.

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

```
DRAFT--THIS SKETCH WILL BE REVISED REPEATEDLY
- [ ] Needs decentralization
- [x] define selective disclosure canonically
- [ ] also define directed disclosures
- [ ] mention BC case as needed (DPKI paper links, reference)
```
Basic technical/implementation needs / Solution

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

The systemic approach is to check first the Know Your Client and Anti-Money
Laundering regulations of the jurisdiction or country that one aims to
approach. The once the regulatory compliance idenitity criteria are established,
establish the delta between the existing quality of identity and the required
quality of identity. Then build common processes for improving idenity to a
level that passes the KYC/AML tests; which are the barriers to accessing
established financial services.

Preserving low cost of access and progressive reputation are essential to
maintaining accessibility.

    - Darla doesn't have much money, has limited credit history.

    - Darla gets access to a secure digital device.

    - Darla signs up for an account. To grant universal access, she is not
      required to prove her legal identity and the cost of the account is $0.

    - She earns money through work and is able to store these funds in a way
      that is associated with her account.

    - To increase her network reputation, she voluntarily verifies her legal
      identity to comply with anti money laundering and know your customer laws
      (AML/KYC). Note that this ideally comes after storing money in the
      account. Also, the mechanism for verification of legal identity should be
      the subject of several separate use cases.

    - She makes payments for services at local merchants and online.

    - Her balance of funds and payment history information is stored in a way
      that is associated with the account.

    - A Creditor can ask her if her account history meets certain criteria. All
      of her purchase history should not be exposed. Creditor needs to be sure
      that the relevant information is not fradulent.

    - Local thieves and internet hackers are interested in knowing who in has
      funds - but they are not able to determine who in the community has funds.

    - Creditor grants her access to use additional funds.

    - She uses the funds for purchases and makes payments.

    - No one knows what she has purchased, how much she paid, or who she
      purchased it from (e.g. all of her transaction history is not revealed to
      the merchant).

    - She misses several repayments.

    - Creditor adjusts the amount of available funds down and increases the
      interest on the credit.

    - She makes payments on her credit consistently for some period of
      time. Creditor decreases the interest rate and increases her available
      credit.

    - Creditor wants to offer credit to many individuals and needs to know the
      interest rates which will cover defaults. Creditor makes a mass query of
      loan default rates. The network gives summary information without
      revealing individual purchases or credit information of specific
      individuals who have not requested credit from Creditor.


>> XDI feature: link contracts are p2p agreements about disclosure, sharing, and
>time of data > in this particular case, user is covered by protective
>stipulations without 'right to be forgotten' > XDI (if well-implemented by bank
>and rating agencies) will enable user's ability to dispute erroneous or
>malicious financial rating or activity associated with her account--tool that
>empowers user and enables efficient detection of possibly fraudulent activity:
>sunshine+transparency

>> delete this, mention cumulative quality of this next use cases

#### Concerns in Non-G20 Nations

    Farhad is a migrant worker at a mine in, with no fixed address, yet receives
    a regular wage in cash, which he would like to store in a bank account. He
    has no recurring bills or credit bureau profile; yet turns up for work on
    time over day, 6 days a week, 50 weeks a year, is known by multiple
    locations by the same name and travels in the same geographies. He needs to
    be able to turn this accumulated consistency into a (nearly) completely
    self-portable record of this economic reliability that others can assess and
    verify, so he can store government currency, pay bills, and gain access to
    credit. Farhad creates a self-sovereign identity, and begins migrating his
    past claims into verifiable records attached to that identity with his
    employer. He submits these to a traditional financial institution, which
    verifies them for their own records. The institution is able to satisfy
    regulatory requirements (such as KYC-AML *equivalents* in global south) with
    the supplied information, and can give Farhad an insured account and good
    credit rating. Farhad reaches parity with conventional account holders.


>> needs *much* more detail about global south banking issues > obvious
>application of microloans > 8 global priorities of gates foundation:
>http://www.gatesfoundation.org/What-We-Do/Global-Development/Financial-Services-for-the-Poor
>reference and write in > empowers unbanked person, beginning with 'secure
>kernel' of identity that is taken for granted by holders of state-issued
>identity documents > basic social needs like health insurance, credit a
>privilege in the global north--consider even more dire needs of global south
>citizens

Basic need: Accumulation (i.e. bootstrapping) of sufficient identity attributes
to satisfy financial regulatory burdens in the user's locality.

>> key need: interoperability of credentials

### Use Case 4 - Starting From Zero: Refugee ###

Yevgeni is a member of a persecuted or targeted class in his nation of
citizenship and residence. He cannot guarantee that he can transport identity
documents or corroborating information about his situation when he flees the
country. He needs a self-sovereign identity for initiating the asylum/refugee
process in a foreign nation. His newly registered identity

>> verb usage: registered::established::declared (verifiably?)::registered WoT
>identity(?)

 information asserting his grounds for asylum must bypass local centralized data
 stores, as it could be exploited to harm him (i.e., records identifying or
 locating individuals could be seized by a new hostile regime). In order to meet
 this need, an identity exchange
 
 >> explain 'identity exchange': mere infrastructure supporting WoT transactions
 >and electronic function
 
 supported in a legal jurisdiction that will take responsibility for WoT service
 availability *over a given period*, is implemented. The 'accepting' government
 polls the exchange, obtaining identity attributes that satisfy the host
 government's documentation requirements. Yevgeni is able to leave his country
 on the accepting government's terms without excessive risk, and at immigration
 uses his self-sovereign identity to enter.

>> double-check government terms-labels > explain self-sovereign identity

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
instantiated in a technical system? For example, Deloitte has a document that
outlines the enrollment processes needed to comply with HSPD-12:


    - Person presents - doesn't have an ID in ID2020 system

    - What are they asked for? name etc...

    - How is this record in a database/digital system linked to "them"

     - Is a biometric captured to alow them to present themselves again in the
       future and be authenticated. could this be voice?

    - The digital root of this ID is rooted in a decentralized network - The
      identifiers are "validated" by workers at the NGO and potentially also
      family members enrolled in the same system.


>> make sure definition of WoT and identities registered to it are clear
>> consider using Kaliya's topologies of identity models
>> explain threat models at each point of refugee's journey
>> make sure biometrics can be later disabled or deleted as desired (ask christopher)
>> explain how motes of refugee's identity can be maintained (while respecting privacy) by NGOs and governments

>> technical: blockchain(-like) structure, XDI for semantic interoperability, provable claims, biometric-type identification, attestations (by refugee workers for example)

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

Although the demands illustrated by the use cases we present are quite serious,
we note that there have never been so many legally unencumbered technical and
expert resources for this application as there are at present. We believe that
the main challenges ahead are those of systems integration and widespread
adoption, for which the prospects are good. Given adequate funding, we are
certain that the challenges illustrated above can be met, >> come up with nice
wording here later.

>> unprecedented historical opportunity--evolution not only of internet as
>infrastructure but turning point of human culture: first time in history
>identity can be represented and communicated in a fashion that transcends any
>centralized authority, empowering every actor in the system to be a unique
>person, community, company or government, obtaining the assurances they need to
>operate and engage in trusted interactions, including the underprivileged and
>marginalized to realize an incredibly economically and socially beneficial
>improvement for humankind.

Privacy-respecting, secure (in the senses defined above) distributed systems
areuniquely able to both accurately chart this experience, as well as empower us
to foster or develop identities that have never been possible before. While this
is great news from a technological standpoint, the same systems can certainly
also be employed in a coercive manner. At worst, large-scale information
systems,whether centralized databases with essentially unlimited storage
ordecentralized append-only structures, could near-permanently foreclose the
disjoint, varied, and possibly contradictory nascent identities of masses
ofpeople going forward. (Imagine if a government ID system was coupled with an
undeniable append-only log, fed by a ubiquitous surveillance system--then
placeit at different points in history.)

