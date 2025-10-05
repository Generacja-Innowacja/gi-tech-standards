# Mailing solution for NGO Manager app

## Introduction

This research presents an analysis and recommendation for a transactional email service to be integrated into our apps,
which is built on a TypeScript and Nest.js stack and hosted within the AWS cloud. The primary function of this service
will be to handle all application-generated, non-marketing emails, such as user invitations, password resets, and other
notifications.

The evaluation was guided by the following key criteria:

**Cost-Effectiveness:** a strong preference for a solution with a generous free tier, aiming for a “free or nearly free”
operational cost for our current and projected transactional volume.

**Developer Experience:** the ease and efficiency of integrating the service with our Nest.js framework, and the overall
quality of the API and documentation. We work with volunteers and practitioners, we have to select a tool that is
straightforward to use and understand.

**Ecosystem Alignment:** the solution’s ability to seamlessly fit into our existing AWS infrastructure to streamline
operations, security and billing.

**Scalability and Reliability:** the capacity to handle significant future growth in email volume without incurring
significant costs, while ensuring high deliverability rates.

## Analyzed Solutions & Comparison Overview

I used Google Gemini to provide me a detailed review of four leading email service providers. The table below provides a
high-level summary of their offerings.

| Feature                    | AWS SES (Simple Email Service)                                                 | Resend                                                     | SendGrid                              | Mailgun                                           |
|:---------------------------|:-------------------------------------------------------------------------------|:-----------------------------------------------------------|:--------------------------------------|:--------------------------------------------------|
| **Free Tier**              | 62,000 emails/month (from AWS compute); 1,000/month otherwise.                 | 3,000 emails/month (with a 100/day limit).                 | 100 emails/day (recurring).           | 5,000 emails/month (for the first 3 months only). |
| **Cost Beyond Free Tier**  | ~$0.10 per 1,000 emails                                                        | ~$0.75 per 1,000 emails                                    | Starts at $19.95/month for 50k emails | Pay-as-you-go, ~$1.00 per 1,000 emails            |
| **Integration Assessment** | Straightforward via AWS SDK or Nodemailer; requires initial AWS console setup. | Excellent; modern, developer-first API and dedicated SDKs. | Mature and simple via official SDKs.  | Mature and simple via official SDKs.              |

## In-depth evaluation

### AWS Simple Email Service (SES) – primary candidate 🏆

Given our existing infrastructure, SES is the most logical and powerful choice.

**Pros:**

- **Cost structure:** the free tier of 62,000 emails per month, when sending from an EC2 instance, is
exceptionally generous and will cover our needs for the foreseeable future. The subsequent cost of $0.10 per 1,000
emails is the lowest on the market.
- **Deep ecosystem integration:** SES integrates natively with other AWS services like IAM for secure access control,
CloudWatch for monitoring sending activity, and SNS for bounce/complaint notifications.
- **High deliverability & scalability:** as a core AWS service, it is built for massive scale. AWS actively manages its
IP address reputation, ensuring reliable delivery.

**Cons:**

- **Initial configuration overhead:** the setup process is more involved than with other providers. It requires
a mandatory domain/email verification and, critically, a manual request to AWS Support to move the account out of the
"sandbox environment" to send emails to unverified addresses.
- **Less intuitive UI:** the AWS Management Console for SES is purely functional and lacks the user-friendly dashboards
and analytics provided by competitors.

### Resend – pretty good alternative ✨

Resend is a newer, highly impressive service designed specifically for developers.

**Pros:**

- **Superior developer experience:** the API is modern, clean, and incredibly simple to use. The documentation is
excellent. A unique feature is its react-email library, which allows for building email templates using React
components.
- **Rapid implementation:** integration is extremely fast. A developer can get a proof-of-concept running in minutes
using the official resend Node.js package.
- **Sufficient free tier for startups:** 3,000 emails/month is adequate for the initial phases of an application.

**Cons:**

- **Daily Sending Limit:** the free tier's cap of 100 emails per day could become a bottleneck during peak activity
(e.g., a user import or notification broadcast).
- **Higher Cost at Scale:** while competitive, its pay-as-you-go pricing is significantly higher than that of AWS SES.

### SendGrid & Mailgun – The Market Veterans

These are powerful, mature platforms with extensive feature sets beyond simple transactional email.

**Assessment:** While both services are robust and reliable, their value proposition for our specific use case is
diminished. Their free tiers have become less competitive over time. SendGrid’s 100 emails/day limit is too restrictive,
and Mailgun’s free tier is effectively a 3-month trial. They do not align with our primary requirement for a long-term,
low-cost solution and were therefore ruled out as primary candidates.

## Final recommendation

Based on the analysis, I recommend the adoption of AWS Simple Email Service (SES) as our primary solution for
transactional emails.

**Justification:**

- **Financial transparency:** SES offers an unbeatable cost model that aligns perfectly with our core requirement. It is
effectively free at our initial scale and remains the most affordable option as we eventually grow.

- **Strategic ecosystem alignment:** using SES strengthens our investment in the AWS ecosystem. It centralizes our
infrastructure, simplifying security management (via IAM), monitoring (via CloudWatch), and billing. Although this is
also a concern, we're vendor-locking our infrastructure to Amazon.

- **Long-term scalability:** the initial setup, while more complex, is a one-time investment that establishes a robust,
reliable, and infinitely scalable email infrastructure for the future.

## Alternative (Contingency) Recommendation

In a scenario where the absolute, overriding priority is speed of implementation for a proof-of-concept or MVP, I would
recommend Resend. Its excellent developer experience allows for the fastest possible integration. However, this should
be adopted with the explicit understanding that it would be a short-term solution, requiring a planned migration to AWS
SES later to optimize operational costs.

## Conclusion

In summary, AWS SES provides the optimal balance of cost, scalability, and strategic alignment with our existing
infrastructure. It is the most robust and financially sound choice for our project’s long-term success. I propose we
proceed with the initial setup and integration of AWS SES into our development environment.

## Credits

**RESEARCHED BY:** Oskar Barcz ([@oskarbarcz](https://github.com/oskarbarcz))

**DATE:** October 5, 2025
