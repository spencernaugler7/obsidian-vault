---
title: ActivityPub Won by Being Boring
source: https://o.ee/blog/activitypub-won-by-being-boring/
author:
  - "[[Owl Owl OÜ]]"
published: 2026-07-05
created: 2026-08-16
description: At FediForum 2026, ActivityPub co-author Evan Prodromou explained why the protocol succeeded by staying deliberately ordinary and why the W3C's Q3 2026 revision needs to keep it that way.
tags:
  - clippings
  - activitypub
---
At FediForum 2026, [Evan Prodromou](https://evanp.me/ "Evan Prodromou") gave a talk with the kind of title only a protocol co-author can get away with: “How To Bullshit Your Way Through a Conversation about ActivityPub.”

The joke worked because the speaker had no need to bluff. Prodromou is one of the five authors listed on the [W3C ActivityPub Recommendation](https://www.w3.org/TR/activitypub/ "W3C ActivityPub Recommendation") and the author of O’Reilly’s [ActivityPub](https://www.oreilly.com/library/view/activitypub/9781098162733/ "ActivityPub") book. The self-deprecating frame covered an honest architecture talk about why the Fediverse works at all.

His running gag was that every term could be treated as a portmanteau. Fediverse is federated plus universe. ActivityPub is activity plus publishing. RESTful, in his groaner version, is rest plus full. Fine. Protocol people deserve hobbies too.

Behind the jokes was a serious claim: ActivityPub works because its core is intentionally ordinary. It is impressive in the way a good loading dock is impressive. Trucks arrive. Boxes move. Nobody writes a poem about the forklift.

Any competent Web engineer from the mid-2010s could look at ActivityPub and think, yes, this is roughly how I would have done it.

If you want the primer before the argument, start with [What Is ActivityPub?](https://o.ee/blog/what-is-activitypub/ "What Is ActivityPub?"). This piece is about why those familiar parts mattered.

## The protocol part is deliberately dull

Federation starts with a modest agreement. Independent networks agree to exchange activity data. They do not agree on a database, a moderation model, an admission policy, a user interface, a ranking system, or a product category.

That minimum agreement is the important part. [Mastodon](https://o.ee/blog/what-is-mastodon/ "Mastodon"), PeerTube, Lemmy, WriteFreely, Pixelfed, WordPress, and small single-user servers keep their own shape. It is why our [Mastodon](https://o.ee/services/mastodon/ "Mastodon") service on C.IM, [PeerTube](https://o.ee/services/peertube/ "PeerTube") service on P.LU, and [Lemmy](https://o.ee/services/lemmy/ "Lemmy") service on R.NF can share a social graph without becoming one product.

The [ActivityPub specification](https://www.w3.org/TR/activitypub/ "ActivityPub specification") describes two layers: a client-to-server API and a server-to-server federation protocol. In practice, the server-to-server part is where most Fediverse operators feel the machinery. Actors have inboxes and outboxes. Servers deliver activities to remote inboxes. Other servers fetch actor documents, objects, and collections by URL.

The model is almost aggressively plain. An activity is a sentence: subject, verb, object. Alice liked the article. Bob followed Alice. A server created a note. Someone announced a post. The thing crossing the wire is often the sentence about the content, not merely the content itself.

That distinction makes ActivityPub social. A content-sync protocol can move articles and images. A social protocol also has to move reactions, follows, blocks, shares, undo operations, and the context that makes those actions meaningful.

Prodromou’s funniest historical aside was that the activity concept traces back to 1930s Soviet activity theory, associated with psychologist Alexei Leontiev, and then wandered through user-experience research before landing in Activity Streams. The Fediverse running on repurposed Marxist psychology sounds like satire written by committee. Protocol concepts rarely arrive cleanly from first principles; they get dragged in from wherever the previous generation left useful tools.

The transport is even less exotic. ActivityPub uses HTTP. Fetch an actor’s URL to learn about the actor. POST an activity to an inbox to deliver it. The [spec’s overview](https://www.w3.org/TR/activitypub/#Overview "spec’s overview") says the quiet part directly: inboxes and outboxes are URLs, and federation usually happens by servers posting messages to other servers’ inboxes.

Even the familiar `user@domain` handle is not fundamental to ActivityPub. It comes through WebFinger, a modernization of older Internet identity lookup habits. The protocol needs identifiers. Humans like handles because `@alice@example.org` fits in a search box better than a full actor URL.

This is why ActivityPub spread. JSON-ish objects, HTTP GET, HTTP POST, URLs, collections, actors, inboxes, outboxes. None of this is dazzling. Boring is implementable.

## The technical debt is less charming

Boring protocols still accumulate weird debt. ActivityPub has a good example sitting in authentication.

The Fediverse commonly uses HTTP Signatures for server-to-server request authentication. The awkward part is which HTTP Signatures. The deployed Fediverse grew around the older [draft-cavage-http-signatures-12](https://datatracker.ietf.org/doc/html/draft-cavage-http-signatures-12 "draft-cavage-http-signatures-12"), an Internet-Draft that is now expired and archived. The IETF work later produced [RFC 9421, HTTP Message Signatures](https://www.rfc-editor.org/rfc/rfc9421.html "RFC 9421, HTTP Message Signatures"), published in February 2024, with a different design.

Minimum-consensus evolution looks like this in practice: a draft is useful enough, implementers ship, the network grows, and the official standard arrives later with a different shape. Nobody can fix that by saying “the spec says” loudly at a server log.

Security has another blunt edge. ActivityPub has addressing. A `to` field can say which actor or collection an activity is intended for. Servers can deliver only to addressed recipients, and they can check authorization when someone fetches a private object. The ActivityPub spec explicitly allows servers to require authorization and return 403 or 404 when a request should not see a target object.

That gives the Fediverse an access-control model. It does not give it end-to-end encryption.

Content usually sits in cleartext on the instance that hosts it. Admins with database or filesystem access can read what their server stores. Backups, object storage, logs, full-text indexes, and search pipelines can widen the practical trust surface if an operator is careless.

For instance admins and self-hosters, this is the operational truth worth writing on the wall: the instance is the trust boundary.

Running your own server can shrink that boundary to infrastructure you control. Choosing someone else’s server means choosing an operator, their security practices, their backup habits, their incident response, and their judgment. That is the direct consequence of a federated publishing system without built-in end-to-end encryption.

## Governance is a protocol surface

Open by default sounds clean until abuse arrives with a working DNS record.

ActivityPub lets anyone put a compatible server on the network. There is no department of the Fediverse where a new instance asks for a license. That openness is essential. It is also why defederation exists.

Defederation is the rough defense mechanism for a rough world: one server blocks another server. There is no president of the Fediverse. Blocks happen locally, sometimes coordinated through shared blocklists, public warnings, private admin channels, and community memory. Obvious abuse can trigger a fast cascade. Ambiguous cases become slow, political, and deeply human.

This is where the minimum viable agreement stops being enough. A protocol can define how to deliver a `Create` activity. It cannot decide which community should accept a server that has weak moderation, hostile users, a spam problem, or a different theory of speech.

The standards process has its own version of this tension. W3C consensus moves slowly because it is supposed to move together. That works when the goal is interoperability rather than speed. It becomes harder once the installed base is real.

Prodromou framed the problem clearly in the Q&A. ActivityPub still has room to be invented, but it already has more than a hundred implementations and tens of millions of users whose social graph should not be broken by a clean-sheet rewrite. Every improvement has to negotiate with existing software.

Even the language around the network carries governance history. “Social web” and “Fediverse” are technically close relatives, sometimes near-synonyms. “Fediverse” also carries the identity of the 2017 to 2022 wave: free software, open standards, LGBTQ communities, safety-conscious communities, left politics, anarchist politics, and a strong sense of “us” developed against large platforms that had already failed them.

That cultural memory affects protocol adoption. Bluesky can be bridged through Bridgy Fed. From one side, bridged Bluesky accounts may look like part of the Fediverse. From the other, the same bridge may look like ActivityPub accounts appearing in the Atmosphere.

## The win condition is uncomfortable

Prodromou’s answer to “when has ActivityPub won?” was intentionally uncomfortable for some parts of the Fediverse.

Victory is not merely a thousand cozy instances, each with good local norms and a donation page that almost covers the object-storage bill. That world is valuable, but it does not change the default assumptions of the Internet.

His win condition was two or more hundred-million-user commercial networks federating over ActivityPub. Think Threads plus another large network such as LinkedIn or Snap. At that point, small independent servers could still participate as peers in the same network as the giants.

A huge commercial platform joining ActivityPub is both a validation of the standard and a threat to the culture that kept the standard alive. If the open protocol is strong enough, large platforms become participants. If it is weak, they become gravity wells.

Prodromou also pointed to large Chinese social networks as an opportunity: hundreds of millions of users, mostly disconnected from the global social web, potentially able to interconnect on their own terms through an open protocol. ActivityPub’s ambition is not to be a nicer microblogging club. It is connective tissue for social software.

The historical warning came from the late 1990s web. Dynamic web content could have gone through Java applets, controlled by Sun, or ActiveX, controlled by Microsoft. The boring outsider path was JavaScript. It took years, a lot of pain, and standards work for the open option to become the default.

The Fediverse should not assume it gets the same happy ending automatically. Large platforms can arrive with proprietary “solutions” for identity, portability, search, ranking, payments, moderation, trust, or quote posts, then try to turn deployment scale into standards authority. The open answers have to ship first.

## ActivityPub’s next revision should feel anticlimactic

On January 15, 2026, W3C chartered a new [Social Web Working Group](https://www.w3.org/groups/wg/social/ "Social Web Working Group") chaired by Darius Kazemi. The [active charter](https://www.w3.org/2026/01/social-web-wg-charter.html "active charter") runs through January 31, 2028 and covers maintenance for ActivityPub, Activity Streams, Activity Vocabulary, WebSub, Micropub, Linked Data Notifications, Webmention, and related notes.

For ActivityPub operators, the most immediate milestones are deliberately modest. The charter lists expected completion in Q3 2026 for updated ActivityPub, Activity Streams, and Activity Vocabulary documents. Prodromou described the ActivityPub work as backward-compatible and largely editorial: clarify underspecified areas, document what existing implementations already depend on, and make the standard easier to implement without breaking the network that exists.

The current ActivityPub Recommendation is stable, but it is also a 2018 document carrying the assumptions and omissions of that moment. Common Fediverse content types and behaviors often live across ActivityStreams vocabulary, implementation practice, FEPs, project-specific extensions, and admin folklore. A maintenance revision that turns some of that into clearer text is exactly the sort of work operators notice only after fewer things fail strangely.

The same charter names [LOLA](https://swicg.github.io/activitypub-data-portability/lola "LOLA") as a tentative deliverable that the Working Group may adopt as a Recommendation-track specification, depending on incubation progress, implementer interest, and group consensus. LOLA is a proposal for live online account portability between ActivityPub servers at a user’s request. Its draft covers copying content, moving following relationships, notifying followers, redirects, and the trust decisions involved when one server asks another for a user’s account data.

Portability is where the boring protocol has to protect users from boring lock-in. If leaving a server means losing posts, followers, reactions, media, and social context, the Fediverse has recreated the trap with more domains in it.

After the maintenance revision, the conversation can move toward an eventual ActivityPub 2. The right model may look less like a flag day and more like HTTP evolution: old versions keep working while capable peers negotiate better behavior. Backward compatibility is how a social network avoids cutting its own graph in half.

The hard engineering ahead is not making ActivityPub cleverer. Clever protocols are easy to admire and hard to deploy. ActivityPub won because it made federation feel like ordinary Web plumbing. Now the network is growing into the parts that are less ordinary: signatures, privacy, moderation, portability, commercial scale, and standards governance under load.

The next phase should keep the machinery boring while the politics, economics, and user counts stop being small.

## Watch the talk

The FediForum recording is worth watching because the jokes make the architecture easier to remember.

<iframe title="FediForum Talk: How To Bullshit Your Way Through a Conversation about ActivityPub" width="100%" height="100%" src="https://spectra.video/videos/embed/s8DKnnaPFw2b1JS8zD5VE8" allow="fullscreen" sandbox="allow-same-origin allow-scripts allow-popups allow-forms" allowfullscreen=""></iframe>