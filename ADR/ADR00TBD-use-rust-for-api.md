# ADR00TBD: Try Rust for an API

Date: 2022-03-15

## Status

`Proposed`

## Context
> The scope of this ADR is to evaluate the technilogical viability of Rust. Out of scope is if the GDS adopts it widely, that is a decision for another report, or perhaps an RFC.

Our core API is (or will be) a vital piece of government infrastructure (to be clear, it may or may not be Critical National Infrastructure). It is important that it is both reliable and fast, without being complicated to develop. Further, the carbon cost of this infrastructure needs to be low.

### Rust Advantages
> Rust bills itself as _"A language empowering everyone to build reliable and efficient software"_. It was first released in 2010, 8 months after Go. 

It is designed to build provablly correct software, with an emphasis on zero runtime failures, and high-quality developer ergonomics.

In alpha testing, we wrote a prototype api, powering the X-Gov form builder UI in three languages, the source code for these three prototypes are available in branches of [alphagov/forms-api-prototype](https://github.com/alphagov/forms-api-prototype) :
 1. [Ruby](https://github.com/alphagov/forms-api-prototype/pull/1)
 2. [Rust](https://github.com/alphagov/forms-api-prototype/pull/2)
 3. [Python](https://github.com/alphagov/forms-api-prototype/pull/3)

In our prototyping, we saw that rust was a much better match for the project we planned on building, despite it being a new language to the GDS.

Notable benefits are:
- An [76x decrease](https://github.com/drujensen/fib#results) in simple execution times (against Python, 32x decrease against Ruby), and a consummate reduction in power requirement (and therefore carbon cost)
	- (Request round-trip times are also faster, the slowest rust web frameworks [are faster](https://web-frameworks-benchmark.netlify.app/result?asc=0&l=rust,ruby,python]) than the fastest Python and Ruby frameworks. Ruby is 1.45x slower, Python, 1.85x)
- A potential order of magnatude reduction in memory overhead compared to python and ruby (depending on application) due to no runtime overhead.
- Faster development due to instant compiler feedback (instead of waiting for logs)
- Faster development due to less unit testing burden: Many errors that would require unit testing are instead compile-time errors. This is not just simple type errors, but whole categories of invalid states are unrepresentable due to careful language and library design.
- 100% compiled coverage by definition (all compiled code is valid). Allowing the team great confidence that no API responses are invalid, no inputs cause errors, etc.
- A focus in the wider Rust community on correctness and security. Contrast with NPM, which requires so much work to control supply chain attacks that most teams give up the attempt.

### Rust Disadvantages

## Decision

We will build an API in Rust.

## Consequences

The consequences are, as ever, mostly human:
- Hiring: though we will still hire based on Ruby, Python, and Javascript, we must advertise that rust is a language we use.
- Training: Rust has earlier requirements for learning; Whereas most languages wait until scale-up to require tuning, the Rust compiler requires much to be done ahead-of-time. The team can not expect new starters to be expert. 
