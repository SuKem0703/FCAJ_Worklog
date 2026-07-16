---
title: "Blog 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---
### Building a Safer Multi-tenant AI System with Amazon Bedrock

Hi everyone, today I'd like to share an interesting article from AWS about how PAR Technology built an AI system using Amazon Bedrock while ensuring that each user can only access the data they are authorized to see.

PAR is a company that provides technology solutions for restaurant chains. They developed a system that lets users ask questions in natural language, and the AI automatically generates SQL queries to retrieve data and respond. The idea sounds simple, but in practice, a critical challenge emerged: data security.

![](https://scontent.fsgn2-8.fna.fbcdn.net/v/t39.30808-6/739699246_1520665259811084_3979309470280326443_n.jpg?stp=dst-jpg_tt6&cstp=mx853x497&ctp=s853x497&_nc_cat=102&ccb=1-7&_nc_sid=aa7b47&_nc_eui2=AeGN4VpncdwfE0TYbKBi_HNoU0D3pXbypQRTQPeldvKlBBizMZPvCbF7IAWQw1XtrqEIXNncD3mSiJcTmmWhoAbR&_nc_ohc=zX7azuzigUoQ7kNvwEuuE9m&_nc_oc=Adowc2XcccTmhpEkOLjW_qMnTrdTBAZTtNr4hkMUv37wo7xelVUzan6F4CbdzRjH_dg5sgHKWKf-JkQj2GUhTh6r&_nc_zt=23&_nc_ht=scontent.fsgn2-8.fna&_nc_gid=a6DHMTKRpeUham_BJUritA&_nc_ss=7b2a8&oh=00_AQDtaOshej61mUQGDMSSUm9fvsou8L3jHxnbkEFnU6hnjQ&oe=6A5AC9DB)

![Architecture diagram](https://scontent.fsgn2-4.fna.fbcdn.net/v/t39.30808-6/739620942_1520665423144401_5066396045548758978_n.jpg?stp=dst-jpg_tt6&cstp=mx857x430&ctp=s857x430&_nc_cat=101&ccb=1-7&_nc_sid=aa7b47&_nc_eui2=AeEluZTeMDzHbgzfhVKc-dQU-VE6hT63A935UTqFPrcD3eXcLd2NsSV6Z7hMj-71X7cj_5lSLMPVmG1Q-CX0B6VJ&_nc_ohc=8auVoYRlI0wQ7kNvwHkKmsp&_nc_oc=AdpgLJJoxLplOtNLxST0lkp4eUExr8z-Spt3XRtuRCak5qals8lF00pP9cKyaZ9DEWcGP63B6Ju3U3YC8Of32Jhr&_nc_zt=23&_nc_ht=scontent.fsgn2-4.fna&_nc_gid=a6DHMTKRpeUham_BJUritA&_nc_ss=7b2a8&oh=00_AQDCNDWhlp5cSXe5kyXqqAP5TBg45K-Ht7l2BpYGKOELsg&oe=6A5AE51A)

#### 3.3.1 The Problem

In PAR's system, many customers share the same platform. For instance, a store owner should only see their own store's revenue, while a senior manager can view revenue across the entire chain.

If the AI generates incorrect queries or pulls the wrong data, users could see information they are not permitted to access. This is a critical issue for enterprise systems.

#### 3.3.2 PAR's Solution

Instead of letting the AI make all decisions, PAR built a system with multiple layers of protection.

First, every request is authenticated to ensure the sender is legitimate. Then, the system validates whether the user's question is clear and appropriate before passing it to the AI.

Most importantly, data is filtered based on each user's access permissions before the AI generates SQL queries. This ensures the AI only works with authorized data rather than the entire database.

#### 3.3.3 Why This Approach Works

What I found impressive is that AWS and PAR do not place complete trust in the LLM. The AI is only responsible for understanding the question and helping generate SQL — access control is still handled by the system.

This way, even if the AI generates an inaccurate query or is affected by unexpected prompts, data outside the permitted scope remains inaccessible.

#### 3.3.4 Results

According to the article, this architecture has been used in production, handling over 50,000 queries with zero data leaks between users.

Beyond improved security, this design also gives enterprises more confidence when deploying AI applications on sensitive data.

#### 3.3.5 My Thoughts

I found this to be a valuable lesson in building AI applications. I used to think choosing a good LLM model was enough, but in reality, architectural design and access control are even more important.

Amazon Bedrock makes building AI applications convenient, but for a system to operate safely, you still need to combine it with authentication, authorization, and data filtering mechanisms from the start.

#### 3.3.6 Conclusion

Through this article, I believe AI should not be the sole component deciding data access. By combining Amazon Bedrock with proper security layers, enterprises can build AI systems that are both intelligent and trustworthy.

Reference: https://aws.amazon.com/vi/blogs/machine-learning/multi-tenant-llm-analytics-with-row-level-security-how-we-built-a-secure-agent-on-aws/
