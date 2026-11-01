# Security Policy

## Reporting a vulnerability

**Do not open a public issue for a security vulnerability.**

Report it privately by email to **<security@ethereumclassic.net>**. Include
"SECURITY" in the subject line, and use PGP encryption if possible; the key is
available on request.

For this repository, that covers anything that would let someone put an endpoint
into the public RPC pool or keep one out by means other than its admission rules,
stop the public endpoints from being served, get around their rate limits, or
reach a credential, including an API key committed inside an endpoint URL. Include
what you can: what is affected, what an attacker gains, and a reproduction if you
have one. A report without a reproduction is still worth sending.

A vulnerability in the client belongs to
[Core-Geth's security policy](https://github.com/ethereumclassic/core-geth/blob/main/SECURITY.md),
which uses the same address.

With the ETC Cooperative's dissolution, Ethereum Classic stakeholders such as
mining pools, exchanges and service providers should use
<security@ethereumclassic.net> as their point of contact. A person answers it:
one of the core developers who maintain this repository and have been with the
network since its inception.

### What to expect

Reports are acknowledged and triaged privately. Where a fix is warranted, it is
prepared privately and disclosed once it is in place. Reporters are credited
unless they ask not to be.

## Automated and AI-assisted review

Findings from automated or agent-assisted review go through the same private
channel as any other. They do not go in a public issue, or in a pull request
whose diff describes the defect before a fix exists.
