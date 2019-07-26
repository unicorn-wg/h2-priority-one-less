---
title: "Deprecation of HTTP/2 Priority Signaling Hints"
abbrev: "--PRIORITY"
docname: draft-peon-httpbis-h2-priority-one-less-latest
date: {DATE}
category: std
ipr: trust200902
area: ART
workgroup: HTTPBIS
updates: 7540

stand_alone: yes
pi: [toc, sortrefs, symrefs, docmapping]

author:
  -
    ins: R. Peon
    name: Roberto Peon
    email: grmocg@gmail.com

  -
    ins: M. Thomson
    name: Martin Thomson
    org: Mozilla
    email: mt@lowentropy.net

--- abstract

This document deprecates HTTP/2 priority signaling hints.  It updates RFC 7540
to do so.

--- middle

# Deprecation of HTTP/2 Priority Signaling Hints

An important feature of any implementation of a protocol that provides
multiplexing is the ability to prioritize the sending of information.
Prioritization is a difficult problem, so it will always
be suboptimal, particularly if one endpoint operates in ignorance of the needs
of its peer.

The significance of this problem was recognized during the design of HTTP/2
{{!HTTP2=RFC7540}} and contributed to the design of a priority signaling
scheme.  HTTP/2 introduced a complex prioritization signaling scheme that used
a combination of dependencies and weights, formed into an unbalanced tree. That
scheme also depends on in-order delivery, so it is unsuitable for use in
protocols like HTTP/3 {{?HTTP3=I-D.ietf-quic-http}}, which attempts to avoid
global ordering.

Though the scheme in HTTP/2 is rich in some ways, it has proven to be
inadequate in several others.  For instance, it is not well suited to major use
cases like live video delivery and it cannot be used to carry hints from
servers.

Critically, the HTTP/2 prioritization signaling scheme suffers from poor
deployment and interoperability.  Most server implementations do not include
support for the scheme, some favoring instead bespoke schemes based on
heuristics and other hints, like the content type of resources and the order in
which requests arrive.

Consequently, the priority hints defined in HTTP/2 cannot be used across
different HTTP versions.  So either we define richer schemes that might support
translation between versions, or we suffer information loss if multiple versions
are in use.

Retaining the HTTP/2 priority scheme increases the complexity of the entire
system without any evidence that the value it provides offsets that complexity.

This document formally deprecates the priority scheme defined in HTTP/2,
acknowledging the lack of wide interoperability and its lack of suitability for
new protocol versions and current use cases.

HTTP/2 servers were never obligated to use the information provided by clients
in HTTP/2 PRIORITY (and HEADERS) frames.  This document encourages servers to
ignore those frames.  Similarly, HTTP/2 clients are encouraged not to send
priority information in HTTP/2.


# Security and Privacy Considerations

HTTP/2 prioritization signaling was always optional.  Processing of priority
information could be used as a denial of service vector by adversaries.
Ignoring priority information removes this vector.


# IANA Considerations

This document makes no request of IANA.


--- back
