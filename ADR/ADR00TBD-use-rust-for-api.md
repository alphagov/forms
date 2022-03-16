# ADR00TBD: Use Rust for our core API

Date: 2022-03-15

## Status

`Proposed`

## Context

> Rust bills itself as _A language empowering everyone to build reliable and efficient software_. It was first released in 2010, 8 months after Go. 
It is designed to build provablly correct software, with an emphasis on zero runtime failures, and high-quality developer ergonomics.

Our core API is (or will be) a vital piece of government infrastructure. It is important that it is both reliable and fast, without being complicated to develop. Further, the carbon cost of this infrastructure needs to be low.
In alpha testing, we wrote a prototype api, powering the X-Gov form builder UI in three languages:
 1. Ruby
 2. Rust
 3. Python

The source code for these three prototypes are available in branches of [alphagov/forms-api-prototype](https://github.com/alphagov/forms-api-prototype) 

In our prototyping, we saw that rust was a much better match for the project we planned on building, despite it being a new language to the GDS.
Notable benefits are:
- An 80x decrease in API response times, and a consummate reduction in power requirement (and therefore carbon cost)
- An aproximate 10x reduction in memory overhead.
- Faster development due to instant compiler feedback (instead of waiting for logs)
- Faster development due to less unit testing burden: Many errors that would require unit testing are instead compile-time errors.
- 100% compiled coverage by definition (all compiled code is valid). Allowing the team great confidence that no API responses are invalid, no inputs cause errors, and whole categories of bugs are provably impossible.
- A focus in the wider Rust community on correctness and security. Contrast with NPM, which requires so much work to control supply chain attacks that most teams give up the attempt.

## Decision

We will build our core API in Rust.

## Consequences

The concequences are, as ever, mostly human:
- Hiring: though we will still hire based on Ruby, Python, and Javascript, we must advertise that rust is a language we use.
- Training: Rust has earlier requirements for learning; Whereas most languages wait until scale-up to require tuning, the Rust compiler requires much to be done ahead-of-time. The team can not expect new starters to be expert. 
