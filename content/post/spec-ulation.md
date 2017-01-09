+++
description = "Rich Hickey Deconstructs Semantic Versioning"
linktitle = ""
featured = ""
featuredalt = ""
title = "Spec-ulation"
categories = [
  "programming",
  "clojure",
  "presentation"
]
featuredpath = ""
date = "2016-12-10T18:47:59-08:00"
author = "beppu"

+++

{{<youtube oyLBGkS5ICk>}}

<https://www.youtube.com/watch?v=oyLBGkS5ICk>

# tl;dw

When Rich Hickey speaks, it's a good idea to listen. He is able to see things
that many of the rest of us cannot, and he is able to analyze and explain his
thoughts with a precision that is rare even among programmers.

Little did I know that there was a problem with semantic versioning. It seemed
like a reasonable system, and I never gave it a second thought until I watched
this presentation where Rich exposed what the semantics of this system actually
were.

## Briefly, the semantics of x.y.z

* z changes - don't care.
* y changes - don't care.
* x changes - you're screwed.

That's all this system can tell you.

Furthermore, this system implicitly formalizes software breakage by saying if
you change **x**, you're allowed to make backward incompatible changes.

However, do we have to break our software?

Rich points us toward another way.

# 0:00 Spec-ulation<a id="sec-1-2" name="sec-1-2"></a>

Rich Hickey

# 0:58 This is not a talk about spec<a id="sec-1-3" name="sec-1-3"></a>

## It's a talk about what spec is about<a id="sec-1-3-1" name="sec-1-3-1"></a>

1.  Giving something to someone that they can use
2.  Making a commitment
    1.  i.e. not taking it away later

# 2:46 Change<a id="sec-1-4" name="sec-1-4"></a>

is it a thing?

# 3:35 'Change'<a id="sec-1-5" name="sec-1-5"></a>

## Origin:<a id="sec-1-5-1" name="sec-1-5-1"></a>

1.  from Latin cambire "to exchange, barter"

## You could change a cow into wheat!<a id="sec-1-5-2" name="sec-1-5-2"></a>

1.  c.f. Eurogames

## One-sided change is&#x2026; theft?<a id="sec-1-5-3" name="sec-1-5-3"></a>

1.  Anti-social at least

## Productivity and soul-crushing at worst?<a id="sec-1-5-4" name="sec-1-5-4"></a>

# 5:13<a id="sec-1-6" name="sec-1-6"></a>

We want our software (esp.
libraries/services to be
different/better tomorrow.

What will that mean for our consumers?

# 5:42 Dependencies<a id="sec-1-7" name="sec-1-7"></a>

[image of versioned library dependency tree]

# 6:59 But&#x2026;<a id="sec-1-8" name="sec-1-8"></a>

## Artifacts don't actually use other artifacts<a id="sec-1-8-1" name="sec-1-8-1"></a>

## There is nothing in the code about artifacts<a id="sec-1-8-2" name="sec-1-8-2"></a>

# 7:45 Dependencies Redux<a id="sec-1-9" name="sec-1-9"></a>

[image of versioned library dependency tree broken down by namespace]
[exposes opportunity for dead code elimination; don't need library z]

# 9:46 But&#x2026;<a id="sec-1-10" name="sec-1-10"></a>

## Namespaces/packages don't actually use other namespaces/packages<a id="sec-1-10-1" name="sec-1-10-1"></a>

## At least require/import appear in the code<a id="sec-1-10-2" name="sec-1-10-2"></a>

## Where is the mapping to artifacts? [no mapping of artifact to namespaces]<a id="sec-1-10-3" name="sec-1-10-3"></a>

# 10:48 Dependency Truth (code)<a id="sec-1-11" name="sec-1-11"></a>

[image of namespaces further broken down by function dependencies]
[shows hat lib X is not a true dependency]

# 13:45 Do deps Force Versioning?<a id="sec-1-12" name="sec-1-12"></a>

"What you can do is let Semantic Versioning provide you
with a sane way to release and upgrade packages without
having to roll new versions of dependent packages"
<http://semver.org/spec/v2.0.0.html>

## Is that what happens?<a id="sec-1-12-1" name="sec-1-12-1"></a>

## Often, no, cascading version bumps<a id="sec-1-12-2" name="sec-1-12-2"></a>

1.  to let root 'know' about improvements to leaves, even if path nodes' code unchanged

2.  level violation

# 15:27 Names, Levels, Scopes, Contexts<a id="sec-1-13" name="sec-1-13"></a>

## fns depend on (call) fns by name<a id="sec-1-13-1" name="sec-1-13-1"></a>

## ns/packages requires/includes set up a context in which those calls can succeed<a id="sec-1-13-2" name="sec-1-13-2"></a>

## Artifact deps/poms set up a context in which those requires can succeed<a id="sec-1-13-3" name="sec-1-13-3"></a>

## fn name scopes include ns but not artifact<a id="sec-1-13-4" name="sec-1-13-4"></a>

1.  artifact context is MAGIC

# 17:19 Basis<a id="sec-1-14" name="sec-1-14"></a>

## Why do we put things in our deps?<a id="sec-1-14-1" name="sec-1-14-1"></a>

1.  We need access to libs while developing

2.  Maven chases transitive deps

3.  Incorporated in artifact to communicate needs to our consumers

4.  "we tested against x,y,z"

## But, course-grained, implies too much<a id="sec-1-14-2" name="sec-1-14-2"></a>

1.  doesn't capture actual deps, just context

# 19:49 (Ex)changes in Software     :important:declarations:<a id="sec-1-15" name="sec-1-15"></a>

## What is required?<a id="sec-1-15-1" name="sec-1-15-1"></a>

1.  fn - args

2.  ns - var names

3.  artifact  ns/package names/paths

## What is provided?<a id="sec-1-15-2" name="sec-1-15-2"></a>

1.  fn - ret (proc/service effect)

2.  ns - vars/fns

3.  artifact - namespaces/packages

# 22:11 Growing Your Software<a id="sec-1-16" name="sec-1-16"></a>

## Accretion<a id="sec-1-16-1" name="sec-1-16-1"></a>

1.  provide more

## Relaxation<a id="sec-1-16-2" name="sec-1-16-2"></a>

1.  require less

## Fixation<a id="sec-1-16-3" name="sec-1-16-3"></a>

1.  bash bugs

# 24:14 Breaking Your Software<a id="sec-1-17" name="sec-1-17"></a>

## Require more<a id="sec-1-17-1" name="sec-1-17-1"></a>

## Provide less<a id="sec-1-17-2" name="sec-1-17-2"></a>

## Unrelated stuff under same name<a id="sec-1-17-3" name="sec-1-17-3"></a>

# 25:55 Change is Not a Thing<a id="sec-1-18" name="sec-1-18"></a>

## It's one of two things<a id="sec-1-18-1" name="sec-1-18-1"></a>

1.  Growth

2.  Breakage

## In the small (fns), spec can help us determine which, prevent breaking specs<a id="sec-1-18-2" name="sec-1-18-2"></a>

## As long as we don't try to do something silly like versioning specs!<a id="sec-1-18-3" name="sec-1-18-3"></a>

# 27:56 Recognizing Collections<a id="sec-1-19" name="sec-1-19"></a>

## You only 'change' a collection by adding/removing members<a id="sec-1-19-1" name="sec-1-19-1"></a>

## Adding = growth, removing = breakage<a id="sec-1-19-2" name="sec-1-19-2"></a>

## Namespaces - collections of vars/fns<a id="sec-1-19-3" name="sec-1-19-3"></a>

## Artifacts - collections of namespaces/packages<a id="sec-1-19-4" name="sec-1-19-4"></a>

## Don't conflate levels!<a id="sec-1-19-5" name="sec-1-19-5"></a>

1.  My family doesn't change when I put on a hat

## (Everything intersting happens at the leaves.)<a id="sec-1-19-6" name="sec-1-19-6"></a>

# 29:52 "Semantic" Versioning "Semantics"<a id="sec-1-20" name="sec-1-20"></a>

## 1.2.changed<a id="sec-1-20-1" name="sec-1-20-1"></a>

1.  "you don't care"

## 1.changed.0<a id="sec-1-20-2" name="sec-1-20-2"></a>

1.  "you don't care"

## changed.0.0<a id="sec-1-20-3" name="sec-1-20-3"></a>

1.  "you're screwed"

# 31:18 Even worse&#x2026;<a id="sec-1-21" name="sec-1-21"></a>

## "you might be screwed"<a id="sec-1-21-1" name="sec-1-21-1"></a>

## Considered covering of change at all levels<a id="sec-1-21-2" name="sec-1-21-2"></a>

1.  Good luck determining where

## Might just as well change the name<a id="sec-1-21-3" name="sec-1-21-3"></a>

# 32:26 Might as well change the name<a id="sec-1-22" name="sec-1-22"></a>

# 32:28 MIGHT AS WELL CHANGE THE NAME<a id="sec-1-23" name="sec-1-23"></a>

# 32:52 But&#x2026;<a id="sec-1-24" name="sec-1-24"></a>

that's not change,
That's a new thing!
Right.

# 33:09 Which name?<a id="sec-1-25" name="sec-1-25"></a>

Levels again

# 33:39 Requiring More args?  Providing Less on return?<a id="sec-1-26" name="sec-1-26"></a>

## i.e. incompatible spec<a id="sec-1-26-1" name="sec-1-26-1"></a>

## new function<a id="sec-1-26-2" name="sec-1-26-2"></a>

old-ns/foo-2 or new-ns/foo

## N.B - the namespace is port of the name<a id="sec-1-26-3" name="sec-1-26-3"></a>

1.  ns aliases can ease transition

# 36:14 Providing Fewer fns/vars?<a id="sec-1-27" name="sec-1-27"></a>

## New namespace/package<a id="sec-1-27-1" name="sec-1-27-1"></a>

# 37:20 Providing Fewer namespaces/packages?<a id="sec-1-28" name="sec-1-28"></a>

## New artifactId?<a id="sec-1-28-1" name="sec-1-28-1"></a>

## but&#x2026; that's what MAJOR segment is for?<a id="sec-1-28-2" name="sec-1-28-2"></a>

1.  no, "any backwards incompatible changes"

    i.e. too-broad "semantic"

2.  The problem is artifact->namespaces magic means possibility of collision

    1.  No 'scope' implicitly renaming children

## [Rich was not sure what the right strategy for this situaion is.]<a id="sec-1-28-3" name="sec-1-28-3"></a>

# 40:33 Doesn't Doing the Right Thing Name-wise Make You Reluctant to Remove Things?<a id="sec-1-29" name="sec-1-29"></a>

Yes. Good.

# 41:02 Breaking Changes are Broken<a id="sec-1-30" name="sec-1-30"></a>

## Full Stop<a id="sec-1-30-1" name="sec-1-30-1"></a>

## Don't do it<a id="sec-1-30-2" name="sec-1-30-2"></a>

## Don't try to figure out the best way to do it<a id="sec-1-30-3" name="sec-1-30-3"></a>

## Avoid breakage by turning it into accretion<a id="sec-1-30-4" name="sec-1-30-4"></a>

1.  old and new can co-exist

# 42:25 So Maven is Broken?<a id="sec-1-31" name="sec-1-31"></a>

## Not really - how we use it may be broken<a id="sec-1-31-1" name="sec-1-31-1"></a>

## Maven central doesn't let you 'change' artifacts<a id="sec-1-31-2" name="sec-1-31-2"></a>

1.  and never 'breaks', is not versioned!!

    1.  no "I'm using maven central 1234567.0.0"

## You're always hapy to use latest maven central<a id="sec-1-31-3" name="sec-1-31-3"></a>

1.  Why?

2.  it's an accreting collection of immutable things

# 44:27 (insert rotten sandwich image here)<a id="sec-1-32" name="sec-1-32"></a>

# 46:29 So SemVer is Broken?<a id="sec-1-33" name="sec-1-33"></a>

## Yes<a id="sec-1-33-1" name="sec-1-33-1"></a>

1.  It is, in part, about how to ship breakage

2.  and the other 'semantics' are of little utility

## What instead?<a id="sec-1-33-2" name="sec-1-33-2"></a>

1.  Maybe chronological versioning?

    1.  YYYYMMDD.HHMMSS

2.  Conveys more and supports some forms of relativism

# 48:47 What about Git?<a id="sec-1-34" name="sec-1-34"></a>

## Wonderful, immutable, truth-of-the-code system, widely adopted<a id="sec-1-34-1" name="sec-1-34-1"></a>

## Content-based addressing<a id="sec-1-34-2" name="sec-1-34-2"></a>

## Almost completely ignored by artifacts/versioning, even though code basis<a id="sec-1-34-3" name="sec-1-34-3"></a>

## Deserves a role<a id="sec-1-34-4" name="sec-1-34-4"></a>

1.  but, SHAs vs order/causality/readability

# 50:37 It's a Social Thing<a id="sec-1-35" name="sec-1-35"></a>

## We won't be albe to tech ourselves out of this<a id="sec-1-35-1" name="sec-1-35-1"></a>

## We need to agree that treating each other well is important<a id="sec-1-35-2" name="sec-1-35-2"></a>

# 51:18 Local dev vs Open dev<a id="sec-1-36" name="sec-1-36"></a>

## Incompatible churn acceptable in private<a id="sec-1-36-1" name="sec-1-36-1"></a>

## Slack is not standup<a id="sec-1-36-2" name="sec-1-36-2"></a>

## OS user base is open and unknown<a id="sec-1-36-3" name="sec-1-36-3"></a>

# 54:18 Coding for Growth<a id="sec-1-37" name="sec-1-37"></a>

## Open specs and data formats are key<a id="sec-1-37-1" name="sec-1-37-1"></a>

## Specs are about what you can do, not about what you can't<a id="sec-1-37-2" name="sec-1-37-2"></a>

## Prohibition turns growth into breakage, cascades<a id="sec-1-37-3" name="sec-1-37-3"></a>

## Always presume you might be handed more than what you need or know about<a id="sec-1-37-4" name="sec-1-37-4"></a>

1.  ignore, or have policy for it

# 58:31 What about Iterative Development?<a id="sec-1-38" name="sec-1-38"></a>

## Alphas are OK<a id="sec-1-38-1" name="sec-1-38-1"></a>

## But maybe should be in artifactId<a id="sec-1-38-2" name="sec-1-38-2"></a>

## Or - incremental API 'publishing'<a id="sec-1-38-3" name="sec-1-38-3"></a>

## Open source is not an excuse for indefinite public thrashing around<a id="sec-1-38-4" name="sec-1-38-4"></a>

# 1:00:14 The Only Truth is Runtime<a id="sec-1-39" name="sec-1-39"></a>

## Deps/POMs are just suggestions<a id="sec-1-39-1" name="sec-1-39-1"></a>

1.  can be full of 'conflicts'

## Someone needs to build a classpath<a id="sec-1-39-2" name="sec-1-39-2"></a>

1.  that alone determines runtime context

## Possibly a lib set that none of the components have ever run against<a id="sec-1-39-3" name="sec-1-39-3"></a>

# 1:01:59 Testing is Runtime Dependent<a id="sec-1-40" name="sec-1-40"></a>

## And runtimes are independent (if related) of dev- and build-time deps<a id="sec-1-40-1" name="sec-1-40-1"></a>

## Plus, you can't test against an open set of consumers<a id="sec-1-40-2" name="sec-1-40-2"></a>

## Artifact release testing is inherently limited<a id="sec-1-40-3" name="sec-1-40-3"></a>

## We could be reifying artifact sets at a macro (e.g. app or multi-app) level<a id="sec-1-40-4" name="sec-1-40-4"></a>

# 1:03:47 (Live Coding Demo)<a id="sec-1-41" name="sec-1-41"></a>

# 1:04:00 What about Web Services?<a id="sec-1-42" name="sec-1-42"></a>

## Same problems, same mistakes<a id="sec-1-42-1" name="sec-1-42-1"></a>

1.  'versioning' non-answer

2.  conflating collections w/contents

## Web service is collection of ops<a id="sec-1-42-2" name="sec-1-42-2"></a>

## ops require/provide<a id="sec-1-42-3" name="sec-1-42-3"></a>

## Accretion could prevent a lot of client/service version hell<a id="sec-1-42-4" name="sec-1-42-4"></a>

# 1:07:04 We Need to Bring FP to the Library Ecosystem<a id="sec-1-43" name="sec-1-43"></a>

## Currently update-in-place, excused but not corrected by versioning<a id="sec-1-43-1" name="sec-1-43-1"></a>

1.  dependency hell == mutability hell

## Makes programming fragile<a id="sec-1-43-2" name="sec-1-43-2"></a>

## Libraries less useful<a id="sec-1-43-3" name="sec-1-43-3"></a>

1.  Even undesirable, whatever their features

# 1:08:19 "This is Impossible/Impractical"<a id="sec-1-44" name="sec-1-44"></a>

## Nope<a id="sec-1-44-1" name="sec-1-44-1"></a>

## Many examples of decade+ compatibility<a id="sec-1-44-2" name="sec-1-44-2"></a>

1.  Unix APIs

2.  Java

3.  HTML

4.  Clojure?

## Compatibility a prerequisite of success?<a id="sec-1-44-3" name="sec-1-44-3"></a>

# 1:09:47 What If We Never Broke Anything?<a id="sec-1-45" name="sec-1-45"></a>

## names become enduringly meaningful<a id="sec-1-45-1" name="sec-1-45-1"></a>

## orthogonal compatibility checking becomes possible<a id="sec-1-45-2" name="sec-1-45-2"></a>

## find-grained deps can be explored<a id="sec-1-45-3" name="sec-1-45-3"></a>

## use the latest with impunity<a id="sec-1-45-4" name="sec-1-45-4"></a>

## compose with impunity<a id="sec-1-45-5" name="sec-1-45-5"></a>

# 1:10:54 Open Challenges<a id="sec-1-46" name="sec-1-46"></a>

## We can't 'see' some changes<a id="sec-1-46-1" name="sec-1-46-1"></a>

1.  collection adds are easy

2.  fn args/ret not visible in source

    1.  specs can help

## spec compatibility context-dependent<a id="sec-1-46-2" name="sec-1-46-2"></a>

1.  provide vs require

## repo->artifact->namespaces not first class<a id="sec-1-46-3" name="sec-1-46-3"></a>

## tooling that reinforces the status quo<a id="sec-1-46-4" name="sec-1-46-4"></a>

# 1:12:40 Opportunities for Clojure<a id="sec-1-47" name="sec-1-47"></a>

## spec<a id="sec-1-47-1" name="sec-1-47-1"></a>

## Flexible (vs fragile/brittle) dep awareness<a id="sec-1-47-2" name="sec-1-47-2"></a>

## Explicit code->artifact/repo support<a id="sec-1-47-3" name="sec-1-47-3"></a>

## First-class, fine-grained 'publish' for APIs<a id="sec-1-47-4" name="sec-1-47-4"></a>

1.  ditto deprecation

## Testing based on fine-grained deps<a id="sec-1-47-5" name="sec-1-47-5"></a>

1.  generative testing needs this

# 1:14:23 Exchange > Change<a id="sec-1-48" name="sec-1-48"></a>

## Grow your software<a id="sec-1-48-1" name="sec-1-48-1"></a>

## Give birth to variation<a id="sec-1-48-2" name="sec-1-48-2"></a>

1.  Don't break, accrete

## Think of the -children- consumers<a id="sec-1-48-3" name="sec-1-48-3"></a>

## Move forward without burning bridges<a id="sec-1-48-4" name="sec-1-48-4"></a>

## Create a lib/service ecosystem of which we can all be proud<a id="sec-1-48-5" name="sec-1-48-5"></a>


<style>
#content h1 {
  margin-top: 1em;
  border-top: 1px solid #888;
}

#content h2 {
  font-size: 13px;
}
</style>
