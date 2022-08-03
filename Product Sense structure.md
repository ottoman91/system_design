Diagnose A Problem:
1. Clarification question - do you really understand the problem accurately? Is your definition of the problem accurate? How exactly is the metric being measured?
    1. Is it a one-time event or a recurring event?
        1. If its a one-time event, then, explore the possible causes of this event. E.g.
            1. A new product feature that is cannibalizing the effect from this feature
            2. A bug in the tracking of the metrics that is causing a drop
            3. A more global event that has caused the metric to go down, e.g. internet outage.
            4. Is it affecting users in one specific geographical area, or users using one specific platform ?
        2. If its a recurrent event,
            1. Has the metric gone down after the introduction of a new feature? Maybe the new feature is cannibalizing the impact of this feature
            2. Has the metric been going down in specific user funnels? Maybe there’s a specific bug in one of the user funnels that is causing the drop in the metric.
            3. Is the metric down in specific geographical areas?
            4. Start creating hypothesis on what could be the cause of this change.
2. Start creating hypothesis for all of the possible scenarios:
    1. Discuss what are the different segmentations of users.
        1. Segment the users by specific categories, based on the question itself, e.g.
            1. Join date
            2. Demographic information
            3. Acquisition channel
            4. geofraphi
            5. Platform
            6. Total users vs active users
            7. DAU/WAU/MAU
            8. New vs existing users
            9. Time spent
    2. Discuss what are the differnet channels through which users might be using the feature that has been affected.
3. Think about how to visualize the different metrics, and once that’s done, think about what to measure and how to report it. ie. Propose and validate hypothesis.

Fractional Metrics:
Investigative metrics with fractional metrics. Look at both numerator and denominator.
* Structure is same
    * clarification
        * This is more important in this step. Consider teh following more:
            * Is it a one time or progressive event?
            * Is the metric unique or total?
            * Is the change from numerator or denominator?
            * How big is the change? This would help us determine what direction to go in, in terms of numerator or denominator.
    * Gathering context
        * Quote the impact from both numerator and denominator and try to get more context on which part to focus more on.
    * Hypothesis
    * Experiment and validate with user data
Measuring success:
* Clarify and ask questions
    * What is the product/feature?
    * What is the business’ objective?
    * What objective does the product serve?
    * How does the product serve the business’ overall purpose?
    * Who uses the product/feature?
* Understand the product and set goals
    * Why does this product exist?
    * What are the goals of this product?
    * How does this product/feature help the business?
    * What type of a business is it? B2B, B2C etc.
* Define success metrics (max 3, 2 success metrics and 1 guardrail metric)
    * Define objects of the problem, to think deeply about what success metrics define the relationships between all these objects.
    * Map out following user journeys to understand which metrics to track
        * acquisition, activation, engagement, retention, referral
        * Funnels and conversions
        * Product engagement
    * Three main categories of metrics: engagement, growth, revenue
* Test hypothesis
* Correlate behavior
* Different types of metrics:
    * Lifetime value (LTV)
    * Customer Acquisition Cost (CAC)
    * Conversions
    * Monthly Active Users
    * Session duration
    * Retention rate
    * Net Promoter Score (NPS)
Feature change:
* Clarify and ask questions
    * Point out different ways in which product could be implemented, and ask the interviewer clarifying question on which method we would be considering.
* Understand feature change
    * List down goals of business.
    * List down goals of the product.
    * Find connections between how the goals of the product tie in with the goals of the business

Metric trade off:
* Clarify and ask questions

Improving Product
Video link: https://www.youtube.com/watch?v=JCNsI0TtNGw
* First, ask whether the purpose of the improvement is to improve engagement, retention or revenue?
* Ask clarifying questions
    * Narrow down to specific product/feature to really understand what’s the purpose of the change.
* Brainstorm ideas
    * Analysis user journey maps
        * Map out different ways in which users use the product/feature. And then identify areas of reducing friction
    * Segment users into differnet groups
        * Analyze how the different groups use the product, and ways in which the usage of these groups can be improved
    * Note _ if talking to a product manager, focus on user journeys and don’t focus on ML improvements. If talking to data scientist, focus on analyzing user behavior and turning inactive users into active users
* Prioritise what ideas to implement
    * Prioritise based on the business impact - which user groups would have the most impact(in terms of revenue and total users being engaged)
    * Prioritise based on cost-benefit analysis.
* How to design experiments - choose 1/2 success metrics.
* Summarise - goals, different ideas of implementation, which idea we would choose, how to set up experiments to measure the success of this idea.

Choosing metric: GAME
G :identify goals of the change
A :list all actions that user wouod be performing ,And identify the core actions
M: metrics - for each of the actions, what metrics are needed
E: evaluation - how would we evaluate the metrics

Evaluation change in metrics:
* Extract definition of metric - really understand how that metric is calculated
* Duration of change - is it a one-time, or recurrent event
Characteristics of user samples that have change a change in the metric
* Use MESE technique to isolate internal and external reasons, and write reasons for each of these
* Write hypothesis to explore these reasons
