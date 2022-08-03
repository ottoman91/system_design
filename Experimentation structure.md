# Experimentation question structure

1. Understand what is the feature

* What is the core feature?
* Who are the target customers?
* What behaviour are we planning on impacting with the feature?
* How is the feature aligned with the core goal of the business?

2. Identify the core hypothesis

H0 and H1

3. Identify at max two target metrics, and 2-3 guardrail metrics.

4. What is the core user group to expose the experiment to?

5. Where would the feature be exposed? make sure to expose it at the correct
entry point in order to prevent dilution from happenig.

6. decide statistical power, significance and MDE. use it to do power analysis for investigating sample size.

7.instrument the experiment

8. scale it to 1% of users to see that exposres are being logged correctly

9. if no sample size imbalance, then launch the experiment and scale it to 100% of users.

10. track users and carry out t test with unequal variance to check whtehr there is stat sig impact in metrics.
