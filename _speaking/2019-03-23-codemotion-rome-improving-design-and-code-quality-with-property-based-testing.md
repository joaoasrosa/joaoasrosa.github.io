---
title: 'Improving design and code quality with Property-based testing'
description: >
 A suite of traditional unit tests will only be as strong as the possible arguments or parameters tested against your code. Quoting Romeu Moura: If you take a String as an argument, then the works of Shakespeare in Japanese & Korean are ONE valid input. Obviously, this can be achieved with parameterized testing. However, this makes the unit tests so big that it is harder to understand which behaviour it is validating. We want our unit tests to also serve as living documentation so they should be comprehensible and to the point.
 <br />
 <br />
 Enter Property-Based Testing. In Property-Based Testing, we randomly generate data points within the boundary of a property to verify the property’s behaviour. This not only lets us test edge cases that could expose unwanted and unexpected errors in the code but also enables us to make small tests that are readable and clear. Making these tests will also force you to think harder about the problem at hand and improve your design and code quality.
 <br />
 <br />
 In this technical session, Kenny & João demonstrates and explains what property-based testing is, and how to implement it in C# with FsCheck and Java with JUnit-Quickcheck. If you are interested in improving your unit testing, so you don’t have to worry much about test data anymore, but more about the problem your code is solving, this talk is for you!
conference: 'Codemotion Rome'
type: 'talk'
location: 'Rome, Italy'
website: 'https://events.codemotion.com/conferences/rome/2019/'
slides: 'https://speakerdeck.com/player/47adc00a65a74edaae10e15aa83ef2fb'
date: 2019-03-23 00:00:00
featured_image: 'images/speaking/2019-03-23-codemotion-rome-improving-design-and-code-quality-with-property-based-testing.webp'
---