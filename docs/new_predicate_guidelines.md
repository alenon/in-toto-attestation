# Guidelines for new predicates

This document provides guidelines for developing and contributing new
in-toto Attestation Framework predicate types.

## Preliminary questions

It's important to understand the _why_ for each predicate type.
Before you start developing your new predicate, make sure you can answer the
following questions. This will also help us better understand your request.

-   What's your use case?
-   Why don’t [existing predicates] cover this use case?
-   What might a new predicate type for your use case look like?
(concrete examples in JSON or CUE preferred)
-   What policy questions do you want to be able to answer with the predicate?

## Predicate conventions

We provide a set of common predicate [field types], and recommend the
following conventions for predicates:

-   [Predicates] SHOULD follow and opt-in to the general [parsing rules],
    particularly the monotonic principle, and SHOULD explain what the
    parsing rules are.

-   Field names SHOULD use lowerCamelCase.

-   Timestamps SHOULD use [RFC 3339] syntax with timezone "Z" and SHOULD
    clarify the meaning of the timestamp. For example, a field named
    `timestamp` is too ambiguous; a better name would be `builtAt` or
    `allowedAt` or `scannedAt`.

Predicate designers are free to limit what subject types are valid for a
given predicate type. For example, suppose a "Gerrit code review" predicate
only applies to git commit subjects. In that case, a producer of such
attestations should never use a subject other than a git commit.

## Contributing your new predicate to in-toto

We love to see our list of vetted predicates grow. New attestation predicates
usually undergo a short [vetting process] before they are added to our list.
To start this process, please submit a PR following the [ITE-9] formatting
guidelines.

**IMPORTANT:** Your predicate is yours. This means that in-toto Attestation
Framework maintainers can provide feedback, but will not write the
specification for you.

## Vetting process

Our vetting process is simple, and is based on the process specified in [ITE-9].

1.  Open a PR following the formatting guidelines specified in the
    [predicate template].
    -   Add the new predicate to the list of [existing predicates].
    -   To generate Go/Python/Java language bindings for the new predicate,
        include a [protobuf definition].
2.  The in-toto Attestation Framework maintainers will review the PR at the
    next maintainers meeting.
3.  If accepted, the new predicate type will be included in our directory.
4.  Finally, if the new [predicateType] URI is defined under the
    https://in-toto.io/attestation namespace, submit a PR to add the following
    line to the [URL redirects list] for the in-toto.io domain:

`attestation/<predicate name>/<version> https://github.com/in-toto/attestation/tree/main/spec/predicates/<predicate name>.md`

[ITE-9]: https://github.com/in-toto/ITE/tree/master/ITE/9#document-format
[Predicates]: ../spec/v1/predicate.md
[RFC 3339]: https://tools.ietf.org/html/rfc3339
[URL redirects list]: https://github.com/in-toto/in-toto.io/blob/main/layouts/index.redirects
[field types]: ../spec/v1/field_types.md
[existing predicates]: ../spec/predicates/README.md
[parsing rules]: ../spec/v1/README.md#parsing-rules
[predicateType]: ../spec/v1/predicate.md#fields
[protobuf definition]: ../protos/README.md
[vetting process]: #vetting-process
[predicate template]: /spec/predicates/template/template.md
