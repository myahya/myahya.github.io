---
layout: post
title: What is the User Looking For? Information Needs, Queries & Narratives
mathjax: true
---
<script type="text/javascript" async src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-MML-AM_CHTML'></script>

If you're running an Information Retrieval (IR) system (aka a search system), then one important aspect you have to reason about is: how good are the results the IR system returns to the user in response to their query? This is known as result **relevance**.

$$Relevance: \text{Query}, \text{Result} \rightarrow \{\text{Perfect} = 2, \text{Good} = 1, \text{Bad} = 0\}$$

A major complication when judging relevance is that the IR system (and those running it) only get to observe the user's query. However, the query is typically ambiguous and open to interpretation. Relevance should instead be judged with respect to the user's **information need** underlying the query.

$$Relevance: \text{Information Need}, \text{Result} \rightarrow \{\text{Perfect} = 2, \text{Good} = 1, \text{Bad} = 0\}$$

There's now another complication: most IR systems don't have the ability to interrogate the user about their information need. When was the last time Google sent you an email to ask you about what you were after when you issued a query? Instead, an IR system has to craft a narrative, which is a proxy for the user's information need. The narrative is constructed by considering information we know about the user, the search session, the world, etc.

$$Relevance: \text{Narrative}, \text{Result} \rightarrow \{\text{Perfect} = 2, \text{Good} = 1, \text{Bad} = 0\}$$

![](/assets/2025-01-05-information-needs-queries-narratives/user-and-ir-system_reduced.png)
## An Example
Let's say you magically got access to Google's search logs and saw someone posed the query: 

> *uk sim card jordan roaming inclusive*

Two questions arise:
1. **Information Need**: what is the user trying to do, or what information are they after?
2. **Relevance**: what constitutes a *relevant* web page for them?

Possible information needs behind the above query might be:

> 1. Buying a sim card in the UK that allows roaming in Jordan.
> 2. Buying a sim card from a UK mobile service provider with the ability to use the sim card in Jordan without extra roaming charges.
> 3. Buying a sim card for roaming in the UK, with the ability to also roam in Jordan.
> 4. Something else ...?

Google is probably not going to ring the user and ask them about their information need. However, it can use what it knows about the user to build a proxy for that information need:

> - They are logged in with their Google account.
> - Their profile indicates that they live in the UK.
> - In the days preceding the above query, they searched for "heathrow amman flights", "amman car rental", etc.
With the above, information needs 1 and 2 seem more likely than 3.

Now, let's say that looking further at the logs over an extended period: 

> * this user logs in from Jordan 2-3 times a year for the past 10 years, each time for a period of 1 week.

With this extra information, information need 2 seems more likely than 1. The "narrative" we have now built is something along the following lines:

> The user lives in the UK and travels to Amman, Jordan 2-3 times a year, each time staying there for around 1 week. They are looking for to buy a sim card from a UK mobile service provider with the ability to use the sim card in Jordan without extra roaming charges.

## From Information Need to Query
The term "information need" was introduced by [Robert S. Taylor](https://en.wikipedia.org/wiki/Robert_Saxton_Taylor) in his 1962 paper "[The Process of Asking Questions](https://doi.org/10.1002/asi.5090130405)". In the same paper, queries issued to an IR system are called *compromised information needs*. They are an expression of the information need dumbed down to fit (1) what the IR system can understand and (2) what kinds of results it can surface.

Think of the sim card example and Google:
1. You're unlikely to invest in crafting a perfectly grammatical long-form description of what you're after because often a simple keyword query will give you results of the same quality. Actually, you might get better results from a succinct keyword query. 
   Try:
    > *produce a list of the sim cards I should be considering if for someone living in the UK and who travels to Jordan 2-3 times a year for a week at a time. I want to pay as little as possible, but at the same time I want something reliable*
   
   vs. 
    
    > *uk sim card jordan roaming inclusive*

   The screenshot below (December 2024) shows the results I get for each of the two.
   ![alt text](/assets/2025-01-05-information-needs-queries-narratives/google-keywords-vs-longform-question_reduced.png)
2. You write your query with the expectation that Google is not capable of giving you a report comparing various sim cards. You're really just looking for it to give you back a link to a web page that will be useful. In the above screenshots, Google triggers its "AI Overview" answer for the short keyword query, but not for the long-form question that's explicitly asking for a list. Moreover, the "AI Overview" answer is very generic, it is essentially saying the the UK's three biggest mobile providers offer roaming, 😒.


Note that compared to Google, other IR systems such as [Perplexity](https://www.perplexity.ai/search/produce-a-list-of-the-sim-card-rPc43wniQPWEMyIMKXnL8w#0) might offer better answers that warrant more elaborate queries, see the screenshot below.
   ![alt text](/assets/2025-01-05-information-needs-queries-narratives/perplexity-result-longform-question_reduced.png)

The point here is not to pick on Google but instead to demonstrate that humans tailor how they query IR systems to what they know about the capabilities of these systems.

A few words about queries and information needs:
- The same information need can be expressed through different queries.

  ```   
  information need 1 ─┬─user 1──►  query a 
                      │               
                      └─user 2──►  query b 
  ```

- The same query can correspond to different information needs. 
  Think of the query "sim cards", the information needs might be:
    - learning about the technicalities of sim cards
    - learning about the different types of sim cards (full, micro, nano, embedded, etc.)
    - finding sim card offers online
    - finding nearby stores that sell sim cards

  ```   
  information need 1 ─────────┐
                              ▼
                            query a
                              ▲
  information need 2 ─────────┘             
  ```

- Satisfying a single information need might require multiple queries. Possible reasons for this:
    - The information need is too complex to express as a single query for a given IR system.
  ```   
  information need 1 ───►  query a ───► query b  ───► query c     
  ```
    - As the user observes answers to queries, their information need might shift.
  ```   
  information need 1 ───►  query a ───► query b  ───► information need 1' ───► query c ───► query d 
  ```

## Reusable Test Collections for Offline Evaluations -- The Cranfield Paradigm
If you need to rapidly iterate on building an IR system for a given corpus (i.e. a set of documents), then you want a **reusable test collection** that allows you to conduct **offline evaluation**. Your test collection has three components:
1. the document corpus
2. a set of evaluation queries
3. for each query, relevance judgments of documents in the corpus with respect to the query

The above is called the [**Cranfield Paradigm**](https://en.wikipedia.org/wiki/Cranfield_experiments). Crucially, there are no users and in this setting. This helps iterate faster. The most popular instantiation of this paradigm is TREC adhoc retrieval tracks, so we'll explain reusable test collections for IR evaluation as by explaining how TREC adhoc retrieval evaluation works.
### TREC Adhoc Retrieval

First, what is TREC? 

TREC (Text REtrieval Conference) is an annual forum for "[coopetitions](https://en.wikipedia.org/wiki/Coopetition)" in the area of information retrieval. It has been running since 1992. Each year, there are a [bunch of tracks](https://trec.nist.gov/pubs/call2024.html), each of which is focused on a specific problem in IR (e.g. video search, podcast IR and content understanding). By far, the most established flavour of tracks is "adhoc retrieval", which is the one we'll explain here.

<center>
<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Many are unfamiliar with TREC, so I&#39;ll share an explanation from 20+ years of experience both as an organizer and a participant. A good starting point is William Thomson (aka Lord Kelvin): &quot;If you cannot measure it, you cannot improve it&quot;.</p>&mdash; Jimmy Lin (@lintool) <a href="https://twitter.com/lintool/status/1857506950952403228?ref_src=twsrc%5Etfw">November 15, 2024</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
</center>

### Information Needs & Queries in TREC Adhoc Retrieval
Information needs in TREC are called **topics**. Each topic typically has:
- `num`: a unique number for reference.
- `title`: this is the short-form query.
- `desc`: a description, think of this as a long-form query or a question.
- `narr`: a narrative. Relevance judgements are done against narratives, which capture the actual information need behind the topic.

```xml
<top>

<num>402 </num>
<title> behavioral genetics </title>

<desc> Description: 
What is happening in the field of behavioral genetics,
the study of the relative influence of genetic
and environmental factors on an individual's behavior
or personality?
</desc>
<narr> Narrative: 
Documents describing genetic or environmental factors relating
to understanding and preventing substance abuse and addictions
are relevant.  Documents pertaining to attention deficit disorders
tied in with genetics are also relevant, as are genetic disorders 
affecting hearing or muscles.  The genome project is relevant
when tied in with behavior disorders (i.e., mood disorders,
Alzheimer's disease). 
</narr>
</top>
```

The query sent to an IR system is either the title in the case of a simple keyword-querying based IR system or the description in the case of something more powerful such as a question answering system.
![](/assets/2025-01-05-information-needs-queries-narratives/generating-retrieval-results-for-eval_reduced.png)
![](/assets/2025-01-05-information-needs-queries-narratives/evaluating-retrieved-result-relevance_reduced.png)

## References & Further Reading
- Article: [The Process of Asking Questions](https://onlinelibrary.wiley.com/doi/10.1002/asi.5090130405) by [Robert S. Taylor](https://en.wikipedia.org/wiki/Robert_Saxton_Taylor)
- Book: [Search User Interfaces](https://searchuserinterfaces.com/#) by [Marti Hearst](https://en.wikipedia.org/wiki/Marti_Hearst)
- Book: [User Simulation for Evaluating Information Access Systems](https://arxiv.org/abs/2306.08550) by Krisztian Balog and [ChengXiang Zhai](https://en.wikipedia.org/wiki/Cheng_Xiang_Zhai)
- Book: [Online Evaluation for Information Retrieval](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/06/ftir-online-evaluation-final-journal.pdf) by Katja Hofmann, Lihong Li and Filip Radlinski
- Video: [Cranfield paradigm](https://www.youtube.com/watch?v=5PqSn_ZOggQ)  by Victor Lavrenko