---
title: "Our Projects"
date: 2025-09-24
draft: false
type: "projects"
layout: "single"
---


Since our founding, most of our work has gone into building the Open Source
core of our platform. Our flagship project is AMPEL, our software supply chain
policy engine.

## 🔴🟡🟢 AMPEL

AMPEL (The Amazing Multipurpose Policy Engine (and L)) is designed to harden
the software development lifecycle. It was created to insert itself at every
stage of the software creation and delivery process: From code push, repository merges,
build processes, delivery and admission control.

AMPEL is open source, released under the Apache-2.0 license, you can download
the latest binaries from its GitHub repository:

https://github.com/carabiner-dev/ampel

### Features

AMPEL is a full fledged policy engine. It ships with ready-to-use advanced features built-in
and has many extension points through drivers and extensions to add more functions.

### Composable Policy Framework

AMPEL's policies are framed in JSON with their executable bit in
a policy language (CEL by default). Several policies can be grouped together
in a PolicySet. The policy code is reusable and sets can reference existing policy files
to reuse code and leverage community knownledge.

### Native Sigstore Support

When running a policy evluation, AMPEL can natively verify attestations signed
and wrapped in sigstore bundles. Our policy framework can enforce identities 
based on Fulcio certificates.

### Plain DSSE Support

AMPEL can verify attestations wrapped in DSSE (Dead-Simple Signing Envelope)
envelopes. Key-based identities is supported by the policy framework. Carabiner
also offers tools to work with keys as well as to sign and verify attestations.

### Pluggable Runtimes

AMPEL policies are defined in a JSON frame that contains the policy code. The
policy framework is designed to support more than one language runtime. Currently,
AMPEL ships the CEL ([Common Expression Language](https://cel.dev/)) engine, but
we are experimenting with other language runtimes such as
[Cedar](https://www.cedarpolicy.com/en),
[Rego](https://www.openpolicyagent.org/docs/policy-language) and even JavaScript.

Our CEL evaluator is extendable, plugins can load data into
the runtime environment and define new functions that add capabilities to policies.
We have released some plugins to work with hashes, URLs, expose the
[Protobom](https://github.com/protobom/protobom/) SBOM Graph API, interact
with GitHub references and we are constantly developing more.

### Predicate Transformers

AMPEL has a notion of transformers. These are Go-based extensions compiled into
the ampel binary that policies can load on demand to transform predicate data.
The tranformer framework is still under development but we ship AMPEL with some
examples that can transform vulnerability reports or work with VEX data.

### Evidence Chains

One of the most powerful features in AMPEL are _Evidence Chains_. Chains are the
solution when you want to verify an artifact but the data lies in an attestation
of another subject.

For example, you need to verify a commit, but the policy should evaluate a
vulnerability scan of a binary. To solve this, you can form a chain from the
commit SHA, to the binary by applying a selector to a SLSA attestation that
returns the digest of a binary.

Chains are supported in PolicySets too! This lets AMPEL to run a policy on
multiple subjects extracted by applying a selector to attested data. For example,
you can apply a selector to an SBOM to run a policy on all its language dependencies.
