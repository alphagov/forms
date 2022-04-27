# ADR00TBD: Try Rust for an API

Date: 2022-03-15

## Status

`Proposed`

## Context

> The scope of this ADR is to evaluate the technological viability of Rust for use in the GOV.UK Forms API. Out of scope is if the GDS should adopt it widely, that is a decision for another report, or perhaps an RFC.

Our core API is (or will be) a vital piece of government infrastructure running on GOV.UK PaaS or AWS Lambda. (to be clear, it may or may not be Critical National Infrastructure in the official sense). Though not user-facing, It is important that this API be both reliable and fast, without being complicated to develop. Further, the carbon cost of this infrastructure needs to be considered (in terms of power usage).

Alongside this, we also have to consider the supportability and maintainability of this API with respect to the tech team who will need to develop and support this API. This must consider the cost of hiring or training developers in Rust, as well as what support is available more widely should it be necessary in the future. As Rust is still a relatively new language (and not one officially adopted within the GDS) these aspects to our decision making are similarly important to the technological choice.

### Rust Advantages
Rust bills itself as _"A language empowering everyone to build reliable and efficient software"_. It was first released in 2010, 8 months after Go. In terms of adoption there are [about the same number](https://redmonk.com/sogrady/files/2021/08/lang.rank_.0621.png) of github projects written in Rust as there are in Go.

Rust is designed to quickly build provably correct software, with an emphasis on zero runtime failures, and high-quality developer ergonomics.

In alpha testing, we wrote a prototype API, powering the X-Gov form builder UI in three languages, the source code for these three prototypes are available in branches of [alphagov/forms-api-prototype](https://github.com/alphagov/forms-api-prototype):
 1. [Ruby](https://github.com/alphagov/forms-api-prototype/pull/1)
 2. [Rust](https://github.com/alphagov/forms-api-prototype/pull/2)
 3. [Python](https://github.com/alphagov/forms-api-prototype/pull/3)

In our prototyping, we saw that Rust is a very good match for the project we planned on building, despite it being a new language to the GDS.

Notable benefits are:
- An [76x decrease](https://github.com/drujensen/fib#results) in execution times (compared to Python, 32x decrease compared to Ruby), and a consummate reduction in power requirement (and therefore carbon cost)
	- Request round-trip times are also faster: The slowest Rust web frameworks [are faster](https://web-frameworks-benchmark.netlify.app/result?asc=0&l=rust,ruby,python]) than the fastest Python and Ruby frameworks. Ruby is 1.45x slower, Python, 1.85x. (only the [sifrr](https://sifrr.github.io/sifrr/#/./packages/server/sifrr-server/) framework is faster in JS land)
- A up to an order of magnitude reduction in memory overhead compared to python and ruby (depending on application) due to lack of runtime overhead.
- Faster development due to instant compiler feedback (instead of waiting for logs)
- Being a compiled language, we felt much more confident in the code we were writing. Rust encodes so much logic into the rich type system that very high level logic can be compile-time validated, not just "is this a number"
	- Many errors that would require unit testing are instead compile-time errors.
	- 100% compiled coverage by definition
	- There is a focus in the wider Rust community on compile-time correctness and compile-timesecurity.

### Rust Disadvantages

- Less organisational knowledge. Though PaaS has an [experimental buildpack](https://github.com/alphagov/cf-buildpack-rust) for Rust, and Cyber Security have used it in the past (with one production service operational at time of writing) there are not many projects within GDS. This means that we run the risk of operating with slightly more risk as the decisions we'll be making are not yet proven within GDS, which could cause unforeseen consequences down the line.
- Training: Rust has earlier requirements for learning; Whereas most languages wait until scale-up to require tuning, the Rust compiler requires much to be done ahead-of-time creating a steep initial learning curve. The team can not expect new starters to have any knowledge of Rust. This would mean that until existing and future team members were able to be trained in Rust and able to effectively read and write Rust code our team would have an incredibly low number of people able to contribute and understand this part of the platform. When coupled with the prior lack of organisational knowledge, it would put an unreasonable burden on these team members to help train, develop, and support the API with a potential lack of support from team members or wider GDS.
- Hiring: though we will still hire based on Ruby, Python, and JavaScript, we would advertise that Rust is a language we use. However we still cannot guarantee that new hires are knowledgable in Rust even if listed, and run the risk of every new hire still requiring training before being able to productively join our team. This would make hiring directly into our team more costly and difficult, at the time to be productive would be much larger than other teams - leaving us at risk of being unable to scale our team as required.

## Decision

We will not build this API using Rust and have instead opted for Ruby. However, given the technical benefits that have been demonstrated above, we will look at working on some of the mitigations required for the organisational disadvantages and consider Rust again in the future for small slices of our project where the risk of those issues has much less impact (For example writing an AWS Lambda in Rust).

## Consequences

- To mitigate the disadvantages mentioned above, we will work in the wider GDS community to raise awareness and educate, including:
	- Lunch & Learn sessions on introductions to Rust
	- Q&A sessions on where it would make sense to use Rust in the GDS
	- If interest is strong, mentoring options to bring people up to speed. 
- In our team, we will also re-assess the organisational knowledge and support for this again when looking at options for languages for future aspects of our service.

