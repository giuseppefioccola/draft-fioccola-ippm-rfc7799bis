---
title: "Active and Passive Metrics and Methods (with Hybrid Types In-Between)"
abbrev: "Active, Passive, and Hybrid"
category: BCP

docname: draft-fioccola-ippm-rfc7799bis-latest
obsoletes: 7799
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Operations and Management"
workgroup: "IP Performance Measurement"
keyword:
 - active
 - passive
 - hybrid
 - metric
 - method
venue:
  group: "IP Performance Measurement"
  type: "Working Group"
  mail: "ippm@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/ippm/"
  github: "giuseppefioccola/draft-fioccola-ippm-rfc7799bis"
  latest: "https://giuseppefioccola.github.io/draft-fioccola-ippm-rfc7799bis/draft-fioccola-ippm-rfc7799bis.html"

author:
 -
    fullname: Giuseppe Fioccola
    organization: Huawei Technologies
    email: giuseppe.fioccola@huawei.com
 -
    fullname: Al Morton
    organization: AT&T Labs

normative:

informative:
  OAM: I-D.ietf-opsawg-oam-characterization
  Y.1540:
    author:
      organization: ITU-T
    title: Internet protocol data communication service - IP packet transfer and availability performance parameters
    date: March 2011
    target: https://www.itu.int/rec/T-REC-Y.1540-201103-I/en
  Y.1731:
    author:
      organization: ITU-T
    title: ITU-T, Operation, administration and management (OAM) functions and mechanisms for Ethernet-based networks
    date: August 2015
    target: https://www.itu.int/rec/T-REC-G.8013-201508-I/en


--- abstract

   This memo provides clear definitions for Active and Passive
   performance assessment.  The construction of Metrics and Methods can
   be described as either "Active" or "Passive".  Some methods may use a
   subset of both Active and Passive attributes, and we refer to these
   as "Hybrid Methods".  This memo also describes multiple dimensions to
   help evaluate new methods as they emerge.

   This memo obsoletes RFC 7799.

--- middle


# Introduction

The adjectives "Active" and "Passive" have been used for many years
to distinguish between two different classes of Internet performance
assessment. The first Passive and Active Measurement (PAM)
Conference was held in 2000, but the earliest proceedings available
online are from the second PAM conference in 2001
(https://www.ripe.net/ripe/meetings/pam-2001).

The notions of "Active", "Passive", and "Hybrid" are well-established.
In general:

- An Active Metric or Method depends on a dedicated measurement
  packet stream and observations of the stream.

- A Passive Metric or Method depends "solely" on observation of one
  or more existing packet streams. The streams only serve
  measurement when they are observed for that purpose, and are
  present whether or not measurements take place.

- A Hybrid Metric or Method uses a subset of both Active and Passive
  attributes.

As new techniques for assessment emerge, it is helpful to have clear
definitions of these notions. This memo provides more-detailed
definitions, defines a new category for combinations of traditional
Active and Passive techniques, and discusses dimensions to evaluate
new techniques as they emerge.

This memo provides definitions for Active and Passive Metrics and
Methods based on long usage in the Internet measurement community,
and especially the Internet Engineering Task Force (IETF). This memo
also describes the combination of fundamental Active and Passive
categories that are called Hybrid Methods and Metrics.

The classification guidelines set in {{?RFC7799}} are used as a
reference to position measurement methods and establish a structured approach
to capture measurement method characteristics. Typically, a measurement method
is first presented by indicating whether it belongs to Active/Passive/Hybrid
category defined in {{?RFC7799}}.

This memo obsoletes {{?RFC7799}}. The description of Metrics
and Methods as "Active" or "Passive" and "Hybrid" is unchanged compared
to {{?RFC7799}}, while the discussion about the existing methods has been
updated. Main changes are listed in {{sec-changes}}.

## Conventions and Definitions

{::boilerplate bcp14-tagged}


# Purpose and Scope

The scope of this memo is to define and describe Active and Passive
versions of metrics and methods that are consistent with the long-
time usage of these adjectives in the Internet measurement community
and especially the IETF. Since the science of measurement is
expanding, we provide a category for combinations of the traditional
extremes, treating Active and Passive as a continuum and designating
combinations of their attributes as Hybrid Methods.

Further, this memo's purpose includes describing multiple dimensions
to evaluate new methods as they emerge.

# Terms and Definitions

This section defines the key terms of the memo. Some definitions use
the notion of "stream of interest", which is synonymous with
"population of interest" defined in clause 6.1.1 of ITU-T
Recommendation {{Y.1540}}. These definitions will be useful for
any work in progress.

## Performance Metric

The standard definition of a quantity, produced in an assessment of
performance and/or reliability of the network, which has an intended
utility and is carefully specified to convey the exact meaning of a
measured value. (This definition is consistent with that of
Performance Metric in {{!RFC2330}} and {{!RFC6390}}).

## Method of Measurement

The procedure or set of operations having the object of determining a
Measured Value or Measurement Result.

## Observation Point

See {{Section 2 of !RFC7011}} for the definition of Observation Point (a
location in the network where packets can be observed), and related
definitions. The comparable term defined in IETF literature on
Active measurement is "Measurement Point" (see {{Section 4.1 of !RFC5835}}).
Both of these terms have come into use describing
similar actions at the identified point in the network path.

## Active Methods

Active Methods of Measurement have the following attributes:

- Active Methods generate packet streams. Commonly, the packet
  stream of interest is generated as the basis of measurement.
  Sometimes, the adjective "synthetic" is used to categorize Active
  measurement streams {{Y.1731}}. An accompanying packet stream or
  streams may be generated to increase overall traffic load, though
  the loading stream(s) may not be measured.

- The packets in the stream of interest have fields or field values
  (or are augmented or modified to include fields or field values)
  that are dedicated to measurement. Since measurement usually
  requires determining the corresponding packets at multiple
  measurement points, a sequence number is the most common
  information dedicated to measurement, and it is often combined
  with a timestamp.

- The Source and Destination of the packet stream of interest are
  usually known a priori.

- The characteristics of the packet stream of interest are known at
  the Source (at least), and may be communicated to the Destination
  as part of the method. Note that some packet characteristics will
  normally change during packet forwarding. Other changes along the
  path are possible, see {{?RFC8468}}.

When adding traffic to the network for measurement, Active Methods
influence the quantities measured to some degree, and those
performing tests should take steps to quantify the effect(s) and/or
minimize such effects.

## Active Metric

An Active Metric incorporates one or more of the aspects of Active
Methods in the metric definition.

For example, IETF metrics for IP performance (developed according to
the framework described in {{!RFC2330}}) include the Source-packet
stream characteristics as metric-input parameters, and also specify
the packet characteristics (Type-P) and Source and Destination IP
addresses (with their implications on both stream treatment and
interfaces associated with measurement points).

## Passive Methods

Passive Methods of Measurement are:

- based solely on observations of an undisturbed and unmodified
  packet stream of interest (in other words, the method of
  measurement MUST NOT add, change, or remove packets or fields or
  change field values anywhere along the path).

- dependent on the existence of one or more packet streams to supply
  the stream of interest.

- dependent on the presence of the packet stream of interest at one
  or more designated Observation Points.

Some Passive Methods simply observe and collect information on all
packets that pass Observation Point(s), while others filter the
packets as a first step and only collect information on packets that
match the filter criteria, and thereby narrow the stream of interest.

It is common that Passive Methods are conducted at one or more
Observation Points. Passive Methods to assess Performance Metrics
often require multiple Observation Points, e.g., to assess the
latency of packet transfer across a network path between two
Observation Points. In this case, the observed packets must include
enough information to determine the corresponding packets at
different Observation Points.

Communication of the observations (in some form) to a collector is an
essential aspect of Passive Methods. In some configurations, the
traffic load generated when communicating (or exporting) the Passive
Method results to a collector may itself influence the measured
network's performance. However, the collection of results is not
unique to Passive Methods, and the load from management and
operations of measurement systems must always be considered for
potential effects on the measured values.

## Passive Metric

Passive Metrics apply to observations of packet traffic (traffic
flows in {{!RFC7011}}).

Passive performance metrics are assessed independently of the packets
or traffic flows, and solely through observation. Some refer to such
assessments as "out of band".

One example of Passive Performance Metrics for IP packet transfer can
be found in ITU-T Recommendation {{Y.1540}}, where the metrics
are defined on the basis of reference events generated as packets
pass reference points. The metrics are agnostic to the distinction
between Active and Passive when the necessary packet correspondence
can be derived from the observed stream of interest as required.

## Hybrid Methods and Metrics

Hybrid Methods are Methods of Measurement that use a combination of
Active Methods and Passive Methods, to assess Active Metrics, Passive
Metrics, or new metrics derived from the a priori knowledge and
observations of the stream of interest. ITU-T Recommendation {{Y.1540}}
defines metrics that are also applicable to the hybrid
categories, since packet correspondence at different observation/
reference points could be derived from "fields or field values which
are dedicated to measurement", but otherwise the methods are Passive.

There are several types of Hybrid Methods, as categorized below.

With respect to a *single* stream of interest, Hybrid Type I methods
fit in the continuum as follows, in terms of what happens at the
Source (or Observation Point nearby):

- Generation of the stream of interest => Active

- Augmentation or modification of the stream of interest, or
  employment of methods that modify the treatment of the stream =>
  Hybrid Type I

- Observation of a stream of interest => Passive

As an example, consider the case where the method generates traffic
load stream(s), and observes an existing stream of interest according
to the criteria for Passive Methods. Since loading streams are an
aspect of Active Methods, the stream of interest is not "solely
observed", and the measurements involve a single stream of interest
whose treatment has been modified by the presence of the load.
Therefore, this is a Hybrid Type I method.

Hybrid Type II is defined as follows: Methods that employ two or more
different streams of interest with some degree of mutual coordination
(e.g., one or more Active streams and one or more undisturbed and
unmodified packet streams) to collect both Active and Passive Metrics
and enable enhanced characterization from additional joint analysis.
Note that one or more Hybrid Type I streams could be substituted for
the Active streams or undisturbed streams in the mutually coordinated
set. It is the Type II Methods where unique Hybrid Metrics are
anticipated to emerge.

Methods based on a combination of a single (generated) Active stream
and Passive observations applied to the stream of interest at
intermediate Observation Points are also Hybrid Methods. However,
{{!RFC5644}} already defines these as Spatial Metrics and Methods. It
is possible to replace the Active stream of {{!RFC5644}} with a Hybrid
Type I stream and measure Spatial Metrics (but this was unanticipated
when {{!RFC5644}} was developed).

The table below illustrates the categorization of methods (where
"Synthesis" refers to a combination of Active and Passive Method
attributes).

~~~
                    | Single Stream          | Multiple Simultaneous
                    | of Interest            | Streams of Interest
                    |                        | from Different Methods
====================================================================
Single Fundamental  | Active or Passive      |
Method              |                        |

Synthesis of        | Hybrid Type I          |
Fundamental Methods |                        |

Multiple Methods    | Spatial Metrics        | Hybrid Type II
                    | (RFC5644)              |
~~~

There may be circumstances where results measured with Hybrid Methods
can be considered equivalent to those measured with Passive Methods.
This notion references the possibility of a "class C" where packets
of different Type-P are treated equally in network implementation, as
described in {{Section 13 of !RFC2330}} and using the terminology for
paths from {{Section 5 of !RFC2330}}:

  > Hybrid Methods of measurement that augment or modify packets of a
  "class C" in a host should produce results equivalent to Passive
  Methods of Measurement when hosts accessing and links transporting
  these packets along the path (other than those performing
  augmentation/modification) treat packets from both categories of
  methods (with and without the augmentation/modification) as the
  same "class C". The Passive Methods of Measurement represent the
  Ground Truth when comparing results between Passive and Hybrid
  Methods, and this comparison should be conducted to confirm the
  "class C" treatment.


# Graphical Representation

If we compare the Active and Passive Methods, there are at least two
dimensions on which methods can be evaluated. This evaluation space
may be useful when a method is a combination of the two alternative
methods.

The two dimensions (initially chosen) are:

  > Y-Axis: "Effect of the measured stream on network conditions". The
  degree to which the stream of interest biases overall network
  conditions experienced by that stream and other streams. This is
  a key dimension for Active measurement error analysis. (Comment:
  There is also the notion of time averages -- a measurement stream
  may have significant effect while it is present, but the stream is
  only generated 0.1% of the time. On the other hand, observations
  alone have no effect on network performance. To keep these
  dimensions simple, we consider the stream effect only when it is
  present, but note that reactive networks defined in {{!RFC7312}} may
  exhibit bias for some time beyond the life of a stream.)

  > X-Axis: "a priori Stream Knowledge". The degree to which stream
  characteristics are known a priori. There are methodological
  advantages of knowing the source stream characteristics, and
  having complete control of the stream characteristics. For
  example, knowing the number of packets in a stream allows more-
  efficient operation of the measurement receiver, and so is an
  asset for Active Methods of Measurement. Passive Methods (with no
  sample filter) have few clues available to anticipate what
  protocol the first packet observed will use or how many packets
  will comprise the flow; once the standard protocol of a flow is
  known, the possibilities narrow (for some compliant flows).
  Therefore, this is a key dimension for Passive measurement error
  analysis.

There are a few examples we can plot on a two-dimensional space. We
can anchor the dimensions with reference point descriptions.

~~~
Y-Axis:Effect of the measured stream on network conditions
^ Max
|* Active using max capacity stream
|
|
|
|
|* Active using stream with load of typical user
|
|
|
|* Active using extremely sparse, randomized stream
|                                                          Passive
| Min                                                            *
+----------------------------------------------------------------|
|                                                                |
Stream          X-Axis: a priori Stream Knowledge        No Stream
Characteristics                                    Characteristics
Completely                                                   Known
Known
~~~

We recognize that method categorization could be based on additional
dimensions, but this would require a different graphical approach.

For example, "effect of stream of interest on network conditions"
could easily be further qualified into:

1. effect on the performance of the stream of interest itself: for
   example, choosing a packet marking or Differentiated Services
   Code Point (DSCP) resulting in domain treatment as a real-time
   stream (as opposed to default/best-effort marking).

2. effect on unmeasured streams that share the path and/or
   bottlenecks: for example, an extremely sparse measured stream of
   minimal size packets typically has little effect on other flows
   (and itself), while a stream designed to characterize path
   capacity may affect all other flows passing through the capacity
   bottleneck (including itself).

3. effect on network conditions resulting in network adaptation: for
   example, a network monitoring load and congestion conditions
   might change routing, placing some flows on alternate paths to
   mitigate the congestion.

We have combined 1 and 2 on the Y-axis, as examination of examples
indicates strong correlation of the effects in this pair, and network
adaptation is not addressed.

It is apparent that different methods of IP network measurement can
produce different results, even when measuring the same path at the
same time. The two dimensions of the graph help us to understand how
the results might change with the method chosen. For example, an
Active Method to assess throughput adds some amount of traffic to the
network, which might result in lower throughput for all streams.
However, a Passive Method to assess throughput can also err on the
low side due to unknown limitations of the hosts providing traffic,
competition for host resources, limitations of the network interface,
or private sub-networks that are not an intentional part of the path,
etc. Hybrid Methods could easily suffer from both forms of error.
Another example of potential errors stems from the pitfalls of using
an Active stream with known a bias, such as a periodic stream defined
in {{!RFC3432}}. The strength of modeling periodic streams (like Voice
over IP (VoIP)) is a potential weakness when extending the measured
results to other application whose streams are non-periodic. The
solutions are to model the application streams more exactly with an
Active Method or to accept the risks and potential errors with the
Passive Method discussed above.


# Examples

This section presents some examples.

## OWAMP, TWAMP, and STAMP

One-Way Active Measurement Protocol (OWAMP) {{?RFC4656}}, Two-Way
Active Measurement Protocol (TWAMP) {{?RFC5357}}, Simple Two-way
Active Measurement Protocol (STAMP) {{?RFC8762}} are standardized
networking protocols that enable the measurements of IP network
performance, such as packet loss, delay, and jitter. These protocols
allow the calculation of these metrics by actively sending test packets
between two endpoints.

Since "the stream of interest is generated as the basis of
measurement", OWAMP, TWAMP and STAMP can be classified
as Active Methods.

## Alternate-Marking

{{?RFC9341}} defines a performance monitoring technique, called
Alternate-Marking, that consists of marking the packets in order to divide
the packet flow into batches, that are used to get coherent counters
and timestamps in every marking period to measure the performance. It
can be implemented by using reserved bits in the protocol header, and
the change in value of these marking bits at the domain edges (and not
along the path) is formally considered a modification of the stream
of interest.

This method processes a user traffic stream and inserts "fields or
values which are dedicated to measurement". Thus:

- The method intends to have a minor effect on the measured stream
  and other streams in the network. There are conditions where this
  intent may not be realized.

- The measured stream has unknown characteristics until it is
  processed to add the marking in the header, and the stream could
  be measured and time-stamped during that process.

Alternate-Marking is a Hybrid Type I method, having at least one
characteristic of both Active and Passive Methods for a single stream
of interest.

## IOAM

In situ Operations, Administration, and Maintenance (IOAM), described
in {{?RFC9197}}, consists of collecting operational and telemetry
information in the packet while the packet traverses a path between two
points in the network. The term "in situ" refers to the fact that the
OAM data is added to the data packets rather than being sent within
packets specifically dedicated to OAM.

This method processes a user traffic stream and inserts "fields or
values which are dedicated to measurement". Similarly to
Alternate-Marking, IOAM also intends to have a minor effect in the
network and the measured stream has unknown characteristics until it is
processed. IOAM can thus be portrayed as Hybrid Type I.

## PDM

In {{?RFC8250}}, an IPv6 Option Header for Performance and Diagnostic
Measurements (PDM) is described which, when added to the stream of
interest at strategic interfaces, supports performance measurements.

This method processes a user traffic stream and adds "fields which
are dedicated to measurement" (the measurement intent is made clear
in the title of this option). PDM also intends to have a minor effect
in the network and the measured stream has unknown characteristics
until it is processed. Note that if the packet MTU is exceeded after
adding the header, the intent to have a minor effect will not be
realized. PDM is classified as a Hybrid Type I method, having at
least one characteristic of both Active and Passive Methods for a
single stream of interest.


# Discussion of OAM Methods

{{OAM}} considers some common qualifiers and modifiers that are prepended,
within the context of packet networks, to the OAM abbreviation and lays out
guidelines for their use in IETF documents.

Many Operations, Administration, and Management (OAM) methods exist
beyond the IP layer. For example, {{Y.1731}} defines several different
measurement methods that we would classify as follows:

- Loss Measurement (LM) occasionally injects frames with a count of
  previous frames since the last LM message. Therefore, LM is classified as
  Hybrid Type I, because this method processes a user traffic stream
  and augments the stream of interest with frames having "fields
  which are dedicated to measurement".

- Synthetic Loss Measurement (SLM) and Delay Measurement (DM)
  methods both inject dedicated measurement frames, so the "stream
  of interest is generated as the basis of measurement". Thus,
  SLM and DM methods are classified as Active Methods.

There are other alternate terminology used in OAM
at layers other than IP. Readers may refer to {{?RFC6374}}
for MPLS Loss and Delay measurement terminology, for example.

# Operational Considerations

TBC.

# Security Considerations

When considering the security and privacy of those involved in
measurement or those whose traffic is measured, there is sensitive
information communicated and observed at observation and measurement
points described above, and protocol issues to consider. We refer
the reader to the security and privacy considerations described in
the Large-Scale Measurement of Broadband Performance (LMAP) Framework
{{!RFC7594}}, which covers Active and Passive measurement techniques and
supporting material on measurement context.


# IANA Considerations

This document has no IANA actions.


--- back

# Changes Since RFC 7799 {#sec-changes}

The main changes since {{?RFC799}} are as follows:

* Change the intended status
* Update the discussion section

# Acknowledgments
{:numbered="false"}

Thanks to Al Morton for working on {{!RFC7799}}.

Acknowledgements from RFC 7799:
Thanks to Mike Ackermann for asking the right question, and for
several suggestions on terminology.  Brian Trammell provided key
terms and references for the Passive category, and suggested ways to
expand the Hybrid description and types.  Phil Eardley suggested some
hybrid scenarios for categorization as part of his review.  Tiziano
Ionta reviewed the document and suggested the classification for the
"coloring" Method of Measurement.  Nalini Elkins identified several
areas for clarification following her review.  Bill Jouris, Stenio
Fernandes, and Spencer Dawkins suggested several editorial
improvements.  Tal Mizrahi, Joachim Fabini, Greg Mirsky, and Mike
Ackermann raised many key considerations in their Working Group Last
Call (WGLC) reviews, based on their broad measurement experience.

{{?RFC7799}} Author's:
: Al Morton
: AT&T Labs

