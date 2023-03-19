--- 
title: "Fundamentals of Sports Business Analytics and Strategy"
author: "Justin Watkins"
date: "2023-03-19"
site: bookdown::bookdown_site
documentclass: book
link-citations: yes
url: "https://justin-watkins.github.io/"
cover-image: images/cover.png
description: A book to help you learn about business analytics
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


# Abstract and forward {-}

<img src="images/cover.png" style="float: right;" class="cover" width="262" height="350"/> If you want to get straight to work, skip the first few chapters and go directly chapter \@ref(chapter5). The work-content of this book is all contained in the back half. The first few chapters will get you familiar the data we'll be exploring, the tools we'll use to explore it, and how to put your projects in context. If you continue reading this chapter I am going to explain why I put this project together and explain what it contains. 

This book was primarily conceived as a resource for a young person who wants to work in sports business under an analytics group, strategy function, and to a lesser extent an I.T. team. These skill sets blend together and complement one another. However, I believe this book could be useful to almost anyone that wants to get a deeper understanding of how analytics is functionally used in a club setting. 

I was once asked by a college professor teaching an analytics course how many analyst we are going to need in the future. He was speaking in front of a group of his analytics students and my response wasn't what he wanted to hear. I believe that we are going to need fewer. I encouraged the students to apply their analytics skills to a discipline such as marketing, I.T., or finance. Technology is rapidly commoditizing analytics work. If you have these skill but work in another discipline you can be an incredibly effective manager. From that perspective, anyone working in sports business could benefit from this knowledge. It helps you understand the benefits and limitations of analytics and puts you in the driver's seat in terms of implementing the strategies that you believe will be most effective.  

Additionally, this book is at least partially inspired by a vestigial lament from my youth. When I took a math class I was always forced to show my work, but the hypocritical writers of textbooks didn't feel as though this precept applied to them. You were invariably tricked on a test through some algebraic edge-case that was entirely new to you. This stuff was formulaic. Just demonstrate to me exactly how to solve these problems and I can do the same for all similar problems. The way math used to be taught in school was less about the concept and more about calculation, but there was some modicum of conceptual learning that didn't blend well with the contemporary teaching techniques. I want to right this wrong in some limited way. I want to show you the naked truth. This book is an exposure. I want to show you everyting. To that end it serves four main purposes:

1. To give you an analytically grounded toolbox that you can build upon
2. To teach you about how a sports team's business works
3. To demonstrate how to apply this knowledge to real problems to achieve desired outcomes
4. To build a reference manual of solutions to common problems

The first three items of this list are the foundations of your core business strategy. You need experience to put together effective strategies. This text should give you a head-start working with analytically oriented tasks that help support strategy. You won't be a strategy or analytics expert, but you'll better understand how to approach many common problems. Analytics (as a field) is a great tool for understanding a wide variety of problems, but it has limits. keep this quote in mind:

> If all you have is a hammer, everything looks like a nail. 

This is the famous _Law of the Instrument_^[https://en.wikipedia.org/wiki/Law_of_the_instrument]. Analytics and data are not the answer to every question. I assume that many people seem to think this way since it is something that you tend to hear often. Since I am trying to show you how to do this work, we are going to be traversing a lot of very granular material. Due to the more technical nature of that material, it is better suited for people that want to develop technical skill sets. It is less-well suited for people that want to understand the application of the theory.

While technology has democratized analytics, analytics is still a black-box to many managers. These people should depend on these tools. Instead, they will often retreat from them. Consider this quote: "Expert Power is influence wielded as a result of expertise, special skill, or knowledge." [@Robbins2012] Understanding these tools and techniques gives you a degree of expert power. However, as a manager without this knowledge the idiom "the tail wags the dog" applies. If you don't understand these concepts, but want to use them you can lose credibility from your employees or look less competent than the people you are managing. 

While you don't need to know how script or code to leverage this book, some programming/scripting knowledge will an enormous benefit. You will want to understand some basic scripting to make full use of this text. You are going to be heavily exposed to it and I need you to learn to have a working knowledge of it. If you want to work implementing solutions in this field, it is still a necessary prerequisite. The code that you'll find in this book is written in R [@R-base]. In fact, this entire book was written using R libraries using free software. We'll mostly follow best practices as defined in "Advanced R" [@Wickham2014]. While Python has become more popular in recent years, I find R to be more suitable for non-programmers. 

R is great in some ways and unusal in others. It has some idiosyncrasies that make it operate a little differently than many programming languages. The most noticeable difference is in flow control, where _for_ and _while_ loops are avoided in favor of a suite of vectorized functions. These functions have also been expanded and improved by generous developers. If you don't know what this means, you are going to learn it so don't worry. In our examples we'll use common constructs when we won't be penalized on run-time. From a data-science perspective, python makes use of many packages that essentially duplicate R's advantages (Pandas and Numpy). You'll come away with an appreciation for the language whether you want that appreciation or not.   

Additionally, I hope to expose you to a lot of reading material and concepts. In fact, I believe that all an undergraduate education really does is give you a broad cursory knowledge base consisting of facile concepts. You probably didn't put a lot of the concepts to use in practice, but you will know things like "If I want to find the area under a curve I can probably use the Integral." This is great. It means you can Google-through most problems really quickly. The books I mention in the text are ones I have stumbled across while trying to solve problems. I mention them to make your life a little easier. Analytics is too large of a field to know everything. You just need to know how to find the answers and other people have probably done this for you. Hopefully, you will be introduced to enough concepts to be able to speak to the most important subjects in these verticals. I'll make simple references to Wikipedia pages whenever I talk about specific subjects that don't require in-depth information or are out-of-scope. That will be enough to get you started.

Furthermore, I would like to teach you a little bit about the main business functions of a professional sports team. Sports is a unique business. It's fortunes are often outside of the control of most of the employees. Your strategies need to reflect this fact. If you don't think your efforts to sell tickets are going to be effective, why do them? This is where strategy comes into play. If you know that the team is going to be dismantled in a year, how does that change your strategy?  

We'll also frame strategy around goals. This means all kinds of different things. To a club it could mean your plan to achieve a goal of \$x valuation. Sports clubs act a little differently than other assets. Additionally, there has been a rapid proliferation of SPACs designed to invest directly into teams. Valuations are beginning to reach such levels that a single owner may soon be a dinosaur. That will change the way these clubs are ran. A club is worth whatever some tech oligarch, hedge-fund managing pirate, or real-state heir, company, or consortium wants to pay and there are thousands of these groups. They are not necessarily worth a discounted cash flow based on revenue. 

We aren't going to cover corporate _strategy_. We aren't going to talk about setting up shell companies, owning different parts of the value chain, human resources structure, shady finance and accounting, new business opportunities and extensions, or the agency agreements that make these businesses function. We are going to take a close look at the strategy that makes the wheels turn where dollars are exchanged between the club and its fans.

From that perspective we can create a provisional definition of strategy in this context:

> Strategy is the discipline of amplifying revenue generating efforts, operationalizing improved procedures, consultation on how decisions interact to build cohesive business systems, and longer and shorter-term planning through coordinated and informed decision making. 

That is a mouthful and is deconstructable, but we don't want to be too narrow or broad. We also don't want to extend platitudes. A definition serves to explain how to think about these problems in this specific context. If you are skeptical of anything that you find here, that is a good thing. Please don't take me at my word. As an analyst, you should demand to be convinced. You'll have to think actively to do it. This type of work isn't for the intellectually lazy. You don't have to understand that the Atkinson cycle ^[Your car may use something different: https://en.wikipedia.org/wiki/Atkinson_cycle] makes your car work to be able to drive it. Many analytic techniques can be thought of the same way. You don't need to understand the underlying mechanisms, you just need to understand how to appropriately wield them. This is the gas pedal, here is the brake. An analyst or a strategist is a mechanic for the business systems of a club. If everything always worked you wouldn't need them. 

The first chapter \@ref(chapter1) will cover some important elements of analytics such as the intersection of information technology. It will also look at the distinction between disciplines such as _Business Intelligence_ and _Analytics_. We'll also discuss some technologies that are integrating these disciplines at scale and discuss how these functions will continue to evolve in the future. This chapter helps frame a foundation for the rest of the book. 

The ability to leverage analytic techniques is predicated on access to quality data. The second chapter  \@ref(chapter2) will familiarize you with the data that we will be using by going through the exercise of creating it. The formats will closely resemble data that we have found _in-the-wild_. This includes customer data along with common demographic data formats. We'll also build a database of ticketing data from the primary and secondary market to be used in a pricing exercise. We'll also build some activity data to demonstrate some common pitfalls we've seen when building sales and marketing plans. This data will be constructed based on an imaginary professional baseball team. Baseball operates a little differently than other sports because of the high number of games. However, the lessons learned here can be applied to almost any sport. In fact, lessons contained in this book can be applied to business problems in a variety of industries. It is a boring chapter. This book isn't really about coding, but we will demonstrate exactly how we do everything we show you. In this way we will pay off a debt my old math teachers owe me. 

In chapter \@ref(chapter3) we will cover how to explore your data. While B.I. technologies such as Tableau make performing _ad hoc_ analysis relatively easy, writing your analysis in code has huge advantages. This chapter covers many of the common graphs that you encounter and shows you how to build and understand them. It will also demonstrate how to summarize and consolidate data. This is such an incredibly common task that it would be easy to ignore it. Using a programming language to manipulate data is so much better than using excel that I can't express it well enough. R is excel on military-grade performance enhancing drugs. While excel and other spreadsheet programs have their place, after you begin using paradigms found in R you will avoid them whenever it is convenient. Point-and-click tools sometimes make finding solutions to problems more difficult if you know the hard way to accomplish the same task.

In chapter \@ref(chapter4) we will take a look at how to frame projects. Some basic project management knowledge is useful and we'll cover a little bit of it. This would also be an easy chapter to avoid, but I thought it was important to include it. It includes some good examples on how to frame a project by asking the right questions. It tries to avoid pedantic MBA speak, but definitely covers some of that arena. 

In chapter \@ref(chapter5) we will demonstrate a couple of different methods for building customer segmentation schemes. Consumer segmentation is a crucial ingredient to an integrated sales, marketing, and research strategy. There are myriad ways to accomplish an effective and useful segmentation scheme. It is as much an art as it is a science. We will cover some very important concepts in this chapter through a working example to demonstrate one way segmentation might be performed. One of the most important skills an analyst has in the toolbox is understanding how to deal with missing data. You'll cover it first hand here.

In chapter \@ref(chapter6) we will cover pricing and forecasting. Pricing is a complex exercise, but we will cover the basics of how they are computed. Increasingly, pricing exercises are becoming a commodity. This means you may not be working much on it directly, but it is critical that you understand a few methods prices are decided upon in practice. This chapter also goes a little deeper into another critical tool that you will use, regression. Regression is the gold standard for estimating numerical data and understanding some of its complexity is important. We'll also cover forecasting in this chapter. Forecasting is also an art and a science. We will cover what forecasts are useful and discuss how to think about them. 

Chapter \@ref(chapter7) will demonstrate a couple of methods of _Lead Scoring_. Lead scoring is also fundamental to an integrated sales and marketing strategy. I consider it an extension of segmentation. Lead scoring can also be slightly controversial. It is a different way to think about going after sales. This chapter will discuss a few commonly used techniques and demonstrate how to build a machine learning model. It will also demonstrate some important concepts endemic to the sports marketing world.  

As an extension of pricing, we'll take a look at promotions in chapter \@ref(chapter8). Promotions are a critical component of marketing, and there are good and bad ways of looking at them. You also have to make many assumptions when working with marketing. Economics is referred to as "The dismal science." If Economics is dismal, Marketing is just as dismal but tends to lack the science in both thought and practice. We will also walk through the basic components of a marketing strategy in this chapter and discuss some of the problems with attributing sales to marketing functions. 

Methods for conducting research will be covered in chapter \@ref(chapter9). Conducting research is a tedious, time consuming, and often a thankless task, but it is fundamental to business strategy. Research is also an enormous subject. We'll examine some useful techniques that go beyond examining facile attitudinal questions. This chapter will introduce you to some critical concepts if you haven't conducted formal research. This chapter isn't nearly long enough. It simply glances at enormous subjects such as hypothesis testing and sampling. If you can only take one thing away from this chapter, I want you to know that sampling is critical to do correctly and is always a problem. 

Chapter \@ref(chapter10) will cover Operations. Operations is a broad topic and we will discuss some important concepts. Simulation and queuing will be discussed in the context of real problems that are faced in stadium and ballpark operations. Simulations are the bread-and-butter of operations problems and you need to understand how they work. They are often the best way to understand a system. If you don't have an operations background and like mathy subjects, you'll enjoy this chapter.   

This book can't be comprehensive. As you might have gathered from the preceding paragraphs, this book is heavily concerned with sales and marketing. That is for good reason. Professional sports teams have high fixed and variable costs and an enormous amount of operational leverage stuck in payroll. They have a few main sources of revenue (Ticket sales, Concessions, Retail sales, Media, and Sponsorship). All of these sources are derivative of having fans attend games or watching the games through media outlets. If you are concerned with the fundamentals of your strategy, it has to start with getting your approach to selling and marketing to fans correct. Get the structural parts right. If you or the executives don't think you are maximizing your opportunities around sales and marketing, you won't be able to focus on higher-order projects that might prove more valuable in the long or short term.    

In addition to what we will cover, Social data, Marketing mix, Retail, Media, staffing, F&B pricing, corporate sponsorship, and operational components of the experience such as gate entry and parking all impact revenue and strategy. Furthermore, there could be structural issues throughout the value-chain that we aren't considering. For instance, a league could have an out-sized influence on your technology stack or even own the digital rights to fans. ^[This has been the case in MLB since at least 2003] Your strategy must to take all of these factors into consideration. Your CRM and technology strategy also has a direct influence on success. From a CRM perspective, we will only touch it tangentially. If we covered every one of these subjects or even went into detail on the ones that we do cover, this book would be many times longer. I believe that you will come away from it with a great foundation for working in a variety of positions throughout a sports organization.   

Finally, this book will quickly become outdated. In many ways, it is already outdated. The field of analytics has progressed rapidly over the past decade. New technologies (upgrades in hardware and software) make performing certain tasks easier. Amazon web Services and the Google Cloud Platform offer sophisticated tools for analytics and I expect much of the low-hanging analytics fruit in sports and other industries to be harvested by these platforms in the coming years. Research uncovers new methods for approaching problems and higher-order skill-sets make certain tasks commodities. Additionally, consumer behavior makes performing other tasks obsolete. Other factors are completely out of our control. My hope is that this text will give you a deeper understanding of the sports industry and you'll quickly be able to eclipse what you find here to push our discipline and industry further along. 

## Book Liscense 

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a>.

Just give credit where it is due. Nothing is new, everything is built on those that came before you. We aren't trying to advance theory here, just to show you how to do some of these things.
 

## Code Liscense


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









