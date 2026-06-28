--- 
title: "Fundamentals of Sports Business Analytics and Strategy"
author: "Justin Watkins"
date: "2023-04-03"
site: bookdown::bookdown_site
documentclass: book
link-citations: yes
url: "https://justin-watkins.github.io/"
cover-image: images/book_cover_b.png
description: A practical guide to sports business analytics for analysts, managers, and team staff
biblio-style: apalike
bibliography:
- bibliography.bib
- packages.bib
header-includes: \usepackage{amsmath}
html-document:
  theme:
    bg: '#FFFFFF'
    fg: '#212529'
    primary: '#1561ad'
    base_font:
      google: Prompt
    code_font:
      google: JetBrains Mono
---


# Abstract and foreword {-}

<img src="images/book_cover_b.png" style="float: right;" class="cover" width="262" height="350"/> This book is an instruction manual for people who want to use analytics inside a sports organization. You may be trying to get your first analytics job, move from sales or marketing into a more analytical role, manage analysts more effectively, or add better data habits to work you already do for a club. The goal is not to turn you into a statistician overnight. The goal is to help you understand the work, ask better questions, build useful analyses, and connect those analyses to business decisions.

If you want to start with applied work, begin with chapter \@ref(chapter5). The first four chapters build the foundation: how analytics fits into strategy, what the data looks like, how to explore it, and how to frame projects so the work answers a business question. The later chapters apply those ideas to segmentation, pricing, lead scoring, promotions, research, and operations.

This book was originally written for someone early in a sports business career who wants to work near analytics, strategy, business intelligence, CRM, or technology. That audience is still central. It is also written for managers and practitioners in ticketing, marketing, sponsorship, finance, research, operations, and service who need to use analytics without necessarily becoming full-time analysts. These functions overlap in practice. A good analyst needs business context, and a good manager needs enough analytical fluency to know what is possible, what is credible, and what is not worth doing.

Analytics work has also changed. Cloud data platforms, modern BI tools, machine-learning libraries, and generative AI have made many technical tasks easier to start. That does not make the work automatic. The hard parts are still defining the problem, understanding the data, choosing a reasonable method, checking whether the answer makes business sense, and communicating the result clearly. The person who can connect those pieces is valuable in any department.

This text serves four primary purposes:

1. To give you an analytically grounded toolbox that you can build upon
2. To teach you about how a sports team's business works
3. To demonstrate how to apply this knowledge to real problems to achieve desired outcomes
4. To build a reference manual of solutions to common problems

The first three items are the foundation of analytics-supported strategy. You need experience to build effective strategy, but this book should give you a practical head start. You will not become an expert by reading it once. You should, however, become more comfortable with the types of problems sports organizations face, the kinds of data used to solve them, and the tradeoffs that shape analytical work.


> If all you have is a hammer, everything looks like a nail. 

This is the famous _Law of the Instrument_.^[https://en.wikipedia.org/wiki/Law_of_the_instrument] Analytics and data are not the answer to every question. Sometimes the right answer is a conversation with a sales manager, a better operating procedure, a cleaner customer record, a clearer offer, or a decision to stop measuring something that does not matter. Since this book shows how to do the work, it includes granular material. The details are intentional. They help you see how an analysis is built instead of only seeing the final chart.

Analytics is still a black box to many managers. It should not be. Consider this quote: "Expert Power is influence wielded as a result of expertise, special skill, or knowledge." [@Robbins2012] Understanding analytical tools and techniques gives you a degree of expert power. If you manage analytical work without understanding the basics, you may struggle to evaluate recommendations, scope projects, or explain why a decision was made. You do not need to know every algorithm. You do need enough fluency to participate intelligently.

You do not need to be a software engineer to benefit from this book, but you will get more from it if you are willing to learn basic scripting. The examples are written in R [@R-base]. R remains a strong language for statistics, visualization, and teaching data analysis. Python, SQL, spreadsheet tools, and BI platforms are also common in sports organizations. The specific tool matters less than the habit: structure the data, write reproducible work when possible, check the output, and explain the decision.

R is excellent in some ways and unusual in others. It has idiosyncrasies that make it operate differently than many programming languages. If a concept is unfamiliar, do not stop. Keep moving, run the examples, and return to the details as needed. The point is not to memorize syntax. The point is to understand the workflow well enough to adapt it.

This book also points you toward concepts and references that are useful in practice. Analytics is too large for any one person to know completely. A durable skill is knowing what to search for, how to evaluate whether an answer applies to your situation, and when to ask for help from a specialist. The references are meant to make that search easier.

The book also teaches a little bit about the business of a professional sports team. Sports is unusual because many outcomes are outside the control of business staff. Wins, injuries, star players, weather, schedule quality, local competition, media attention, and brand history all affect demand. Your strategies need to account for that reality. If your team is rebuilding, if the schedule is weak, or if the market is changing, your sales and marketing strategy should change too.

We will frame strategy around goals. A club may care about ticket revenue, renewal rate, attendance, sponsorship value, fan experience, operating efficiency, media reach, or franchise valuation. These goals interact. A decision that helps short-term revenue may hurt long-term loyalty. A decision that improves fan experience may require operational investment. Analytics should help clarify those tradeoffs.

We are not going to cover every form of corporate _strategy_. We will not spend much time on ownership structures, media-rights entities, league governance, legal arrangements, or every possible business-development opportunity. Instead, we will focus on the practical strategy that connects the club to its fans and customers: selling, marketing, pricing, researching, servicing, and operating better.

From that perspective, we can create a provisional definition of strategy in this context:

> Strategy is the discipline of coordinating decisions, systems, and resources so the organization can achieve its business goals more effectively.

That definition is intentionally practical. If you are skeptical of anything you find here, that is good. Analysts should demand to be convinced. You do not need to understand every mathematical detail before using a technique, but you do need to know what the technique is for, what assumptions it makes, and how it can mislead you. Think of an analyst or strategist as a mechanic for the business systems of a club. If everything always worked, you would not need them.

Chapter \@ref(chapter1) covers the relationship between analytics, strategy, and technology. It also explains the distinction between _Business Intelligence_ and _Analytics_ and introduces a maturity model for building analytical capability.

Chapter \@ref(chapter2) introduces the data used throughout the book by creating it. The formats resemble data you may encounter in the wild: customer records, ticketing data, demographic data, secondary-market data, and sales activity. The examples use an imaginary professional baseball team, but the lessons apply across sports and many other businesses.

Chapter \@ref(chapter3) covers data exploration. You will build common graphs, summarize data, and learn how to look for structure before jumping to conclusions. BI tools such as Tableau, Power BI, Looker, and Qlik are useful, but code gives you reproducibility and flexibility that point-and-click tools often cannot match.

Chapter \@ref(chapter4) explains how to frame projects. This is one of the most important skills in the book. A well-framed question saves time, reduces confusion, and gives the analysis a better chance of influencing a decision.

Chapter \@ref(chapter5) demonstrates several methods for building customer segmentation schemes. Segmentation is central to integrated sales, marketing, service, and research strategy. You will also confront one of the most common analytical problems: missing data.

Chapter \@ref(chapter6) covers pricing and forecasting. Pricing is complex, and many pricing systems are now vendor-supported or automated. You still need to understand the logic behind price recommendations, demand estimates, and forecasts. This chapter also goes deeper into regression.

Chapter \@ref(chapter7) demonstrates methods for _Lead Scoring_. Lead scoring extends segmentation and helps sales and marketing teams prioritize effort. The chapter discusses common techniques and demonstrates a machine-learning model.

Chapter \@ref(chapter8) looks at promotions. Promotions are a critical marketing tool, but they are easy to misread. This chapter discusses marketing strategy, offer design, and the difficulty of attributing sales to marketing activity.

Chapter \@ref(chapter9) covers research methods. Research can be tedious, but it is fundamental to strategy. This chapter introduces concepts such as survey design, hypothesis testing, and sampling. If you take one idea from the chapter, take this one: sampling matters, and it is easy to do poorly.

Chapter \@ref(chapter10) covers operations. Simulation and queuing are introduced through stadium and ballpark problems. These methods are useful because operations problems often involve systems with many moving parts.

This book cannot be comprehensive. It is heavily concerned with sales and marketing because those functions sit close to the fan relationship and to several major revenue streams: tickets, concessions, retail, media, and sponsorship. If you do not understand how the club attracts, serves, retains, and monetizes fans, higher-order analytics projects will have a weak foundation.

Many related topics receive only limited attention: social data, marketing mix, retail, media, staffing, food and beverage pricing, sponsorship valuation, CRM strategy, gate entry, parking, digital rights, and league-level technology constraints. Those topics matter. They are also large enough to deserve their own treatments. The aim here is to give you a strong foundation that transfers across roles.

Finally, this book will age. Some tools, vendors, and workflows will change. That is unavoidable. The durable lessons are more basic: define the problem, understand the data, choose a method that fits, validate the result, communicate clearly, and connect the work to a decision. If you learn those habits, you will be able to adapt as the analytics space changes.

I hope this text gives you a deeper understanding of sports business analytics and enough practical confidence to improve the work around you.

## Book License

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a>.

Just give credit where it is due. Nothing is new, everything is built on those that came before you. We aren't trying to advance theory here, just to show you how to do some of these things.
 

## Code License


<p xmlns:dct="http://purl.org/dc/terms/" xmlns:vcard="http://www.w3.org/2001/vcard-rdf/3.0#">
  <a rel="license"
     href="http://creativecommons.org/publicdomain/zero/1.0/">
    <img src="http://i.creativecommons.org/p/zero/1.0/88x31.png" style="border-style: none;" alt="CC0" />
  </a>
  <br />
  To the extent possible under law,
  <span resource="[_:publisher]" rel="dct:publisher">
    <span property="dct:title">Justin Watkins</span></span>
  has waived all copyright and related or neighboring rights to
  this work.
This work is published from:
<span property="vcard:Country" datatype="dct:ISO3166"
      content="US" about="[_:publisher]">
  United States</span>.
</p>


Do whatever you want with it.

## Contact Information

Justin Watkins: watkinsjudo@gmail.com








