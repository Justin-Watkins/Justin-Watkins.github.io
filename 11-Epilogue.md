
# Epilogue {#Chapter11}

We have covered a variety of subjects related to foundational elements of business strategy in a sports business setting. This setting is specific to working at a club. We have been focused on building strategies that increase ticket sales and revenue and benefit business operations. Additionally, you were shown several concepts in two different parts. Chapters 1-4 cover foundational elements needed to analyze data. Chapters 5-10 looks at examples of problems you will face and demonstrates some techniques you can use to solve them.

1. Chapter \@ref(chapter1) introduced us to __how to think about and use data__. Using data is fundamental to business strategy
2. Chapter \@ref(chapter2) introduced us to specific data sets and how to create them using the __R language__. Some knowledge of programming is still critical for the analysis. 
3. Chapter \@ref(chapter3) demonstrated how to __build and interpret the foundational graphs using R__. It also covered summarizing and exploring data.
4. Chapter \@ref(chapter4) discussed how to frame and think about problems that you will face. We also saw some essential __project management__ techniques. 
5. Chapter \@ref(chapter5) introduced us to __customer segmentation__. We look at several methods and discuss how to use this data.
6. Chapter \@ref(chapter6) covers some basic __pricing__ and forecasting principles.
7. Chapter \@ref(chapter7) extends segmentation with __lead scoring__.
8. Chapter \@ref(chapter8) demonstrated how to consider __promotions and covers some brand management__ concepts
9. Chapter \@ref(chapter9) introduces some formal __research principles__ including hypothesis testing and sampling.
10. Chapter \@ref(chapter10) covered some techniques related to stadium operations. Understanding simulation is critical to solving a wide variety of operations problems. 

We covered a lot of material but have yet to scratch the surface. I struggled even to cover subjects in any real depth. Let's look at the four goals we discussed at the beginning of this book and discuss whether they were accomplished.

1. To give you an analytic toolbox
2. To teach you about how a sports team's business works
3. To apply this knowledge to real problems to achieve desired outcomes
4. To build a reference manual of solutions to common problems

Ultimately, this knowledge coalesces into strategic thought. You aren't born understanding business strategy. The foundations of strategy are built on experience. Analytics is tightly coupled with strategy. It touches every functional unit of a business and helps produce the answers to questions that the strategist or manager devises. Let's review your analytics toolbox. 

## Your analytics toolbox

We covered a lot of code in this book and introduced several concepts. At a high level, we covered the following:

- How to manipulate and summarize data with code
- regression
- How to implement machine learning algorithms 
- Formal research methods
- Simulation and its applications
- Building graphics
- Problem-solving and framing projects

We also covered several techniques, the code you can use to implement those techniques, and how to interpret the results. However, there is a lot that we should have covered. 

1. Neural Networks and A.I.
2. More exotic forms of regression (mixed effects models, etc.)
3. Bayesian methods
4. Other ensemble learning methods
5. Deploying web apps for reporting and information dissemination 

We deliberately didn't cover these subjects. There is no need to cover everything. Once you understand how to think through a problem, applying a specific algorithm is trivial once you have your data sets in the proper place. There are also hundreds of algorithms, but they more-are less do the same things in our context:

1. Predict a numerical value
2. Predict a class
3. Demonstrate structure

We didn't cover tools such as convolutional neural networks for computer vision or speech recognition. That is because we don't need it, and specialists can do it better than us. For instance, you can deploy facial recognition for entering a suite. You can also deploy speech recognition or natural language processing to replace your sales staff. You might want some spatial analysis of the park using a digital twin. Ultimately, vendors will do that work for you much more efficiently. You need to know these tools and how they leverage them. You don't want a salesperson wowing your executives with "A.I." when it isn't even the right tool.

## Sports business 

We also discussed how to think about problems and should understand some distinctions between sports and other industries. Sports is unique, and outcomes are often out of your control. You can't just apply techniques and analysis learned in business school because sports business is constricted in many ways. Geographic boundaries, agency agreements, labor issues, and many other unique circumstances exist. At their heart, many leagues are simply trade organizations. Our work revolves around a constrained optimization exercise. It's similar to operating a mutual or hedge fund. Sometimes it's up, and sometimes it's down. Your job is to navigate those seas and think about problems in advance and abstractly. You have to show your team the path to success. 

Individuals are also attracted to sports for a variety of reasons, and that should influence our thought. Clubs deal with public relations issues along a variety of avenues. Politicians can appropriate them at the most inopportune times. Our brand is critical, and we aren't always in control. What do you do if you have a public relations scandal? We didn't consider covering this strategic problem, but it should be understood. How do you proactively protect your brand through public relations and corporate communication? How do these issues impact corporate sponsorship or ticket sales? These measures could be defensive or offensive. How do you know that you are making the right choices? You may not know. You do the best you can.  

## Problems faced by a club

Additionally, we covered many real-world problems. The first part of this book was concerned with a few main subjects:

1. Understanding the context of analytics and strategy within sports business (specifically at a club)
2. Building and understanding standard data sets (To introduce you to R and the data)
3. Exploring data (Understanding how to build the most common graphs that you will use)
4. Framing Projects (Understanding how to think about problems in a strategic fashion)

The second half of this book covered the application of analytic techniques and the interpretation of the results. We covered:

1. Segmentation 
2. Pricing
3. Lead scoring
4. Promotions
4. Research
6. Operations


We only covered a few subjects related to functional departments or exercises that make some of what we covered possible. Some of these functions live in I.T. or live at the Executive level. Some of these related subjects include: 

1. Asset valuation in corporate sponsorship departments
2. Building dashboards and other business intelligence functions
3. Constructing ETLs

Additionally, we didn't cover higher-order strategic problems. These problems might involve customers, asset classes, or the legal environment. Examples of these strategic issues include:

- Media rights
- digital rights 
- Other issues with politics or legal issues
- Growing top-of-funnel audiences (looking at Gen Z or Gen Alpha)
- Business development and growth
- Mergers or aquisitions


## How do I learn more

Google it. Seriously. There are a million resources for learning R or Python online. You can take free classes or access entire books on subjects like programming for free. The same can be said for machine learning techniques. However, this comes with a warning. Techniques change rapidly. Techniques such as random forests and support vector machines may be destined for the scrap pile as neural networks become easier to deploy. TensorFlow [@tensorflow2020] accelerated this trend several years ago.

Additionally, if you are a student, take some classes and network. Contact someone at a club and ask if you can work on a project with them for school. Finally, if you already work in the industry, expand your horizons. Don't get locked into only working on a few narrow projects. Look to expand your influence throughout the office. The broader your work experience, the better you'll be at everything you do.  

There are also scores of books on various subjects related to analytics. The topic is so broad that you will naturally gravitate toward specific components. You may prefer visualization or building databases. You might fall in love with modeling and statistics. Figure out what parts of analytics you like and are good at, purchase a used book, read it, and try to duplicate what you can find. R, Python, TensorFlow, and many other technologies can be used for _free_. Download them and get started on some data. Thousands of data sets can even be found embedded in R and Python. In R, you can find them with a simple command:


```r
data(package='ggplot2')
```

You can see all the available data sets by using this variation of the preceding function:


```r
data(package = .packages(all.available = TRUE))
```

Find some interesting data sets and use them. Many packages also have excellent documentation with full-scale vignettes. Please take advantage of them. You'll be surprised at how much you will learn with time and focus. 

## What does the future hold

Many examples in this book have been solved to one degree or another. The problems are well understood within and outside of sports. For instance, we only explored pricing from a very rudimentary standpoint. Dynamically pricing tickets based on variable demand levels has been happening in the industry (applying specific algorithms) for over forty years. Probably much longer. The technique is a commodity, and this is a good thing. During the nascency of the analytics revolution, the analyst may have been considered a malevolent presence in the board room. They are now a necessity, and that influence will continue to grow. The skills needed to wield an analytics team will be a prerequisite for future leadership. Working in the field is the best way to get that experience. However, it might be even more helpful to use those skill sets directly by specializing in another vertical such as finance. Your life is a winding path and isn't linear. 

Over time, you will see more functions integrated into CRM systems, and skill sets will become more commoditized as students continue to flock to _analytcs_ oriented degree programs. This is neither bad nor good. I look at analytics in a similar vein to Computer Engineering degrees. You don't need one-million people with Computer Engineering degrees. Do you know what you call a second-rate computer engineer? A bartender. They might also run a call center or do other I.T. work. The point is that you only need a few good people to build better processors. Analytics is similar. You don't need armies; You need a few people who are good at it.

Furthermore, analytics will begin to change the workforce in sports. Chatbots will increasingly take over for sales and service personnel. Accountants are similarly doomed. If what you do is formulaic, you will be doing it only for a short time. These workforce changes aren't limited to sports. We all better be voting for universal basic income because the machines are coming for white-collar jobs next, and they are already here.  

Media will continue to change rapidly. GenZ and GenAlpha (All born after 2000) will continue to shape media consumption and content strategy. Both factors impact sports consumption through media and, even more critically, in-person. So what is the trick to attracting these attention-deficit-disordered youths? Nobody knows yet, but most literature says something like this [@Fromm2018]:

> "Start by humanizing your brand. This means giving your brand a personality that consumers can engage with."

Communication rules have changed. Interactions with hardware seem almost silly:

> "Pivitols learned to swipe before they could speak. Attempting to swipe the unswipable--like T.V. screens or the pages of a magazine--they assumed the image in front of them was broken."

I admit that I have swiped a magazine page. Gen Z interacts with social media and technology much more intuitively than older generations. Sports is adapting but will have to continue to adapt. We are still trying to figure out the answer, but interfacing with young people is a huge strategic problem that must be considered an investment. At the club level, it isn't easy to think about marketing initiatives in the context of investment. But, if we don't, we might find ourselves the media equivalent of professional fishing or the code equivalent of FoxPro. Remember FoxPro?  

Stadium operations will also continue to change. New venues will be more purposefully constructed to provide fans with more convenient and immersive experiences. I've been concerned for years that a terrorist attack on a large public sporting event would revolutionize how we approach ticketing, ingress, and egress. The same thing happened in 2001 when attacks on the World Trade Center permanently altered air travel ^[https://www.pbs.org/newshour/nation/how-911-changed-air-travel]. You'll see massive changes here. Whether these changes improve the experience will be up for debate.

Additionally, everything is incremental. Nothing is new about any of the concepts in this book. Neural Networks have been around for decades. Looking back at an old textbook from college, "Decision Support Systems and Intelligent Systems," published in 2001 [@Aronson2001], I reviewed the chapter on Neural Networks. Fundamentally, everything has stayed the same. Incremental hardware, software, and mathematics improvements have pushed these technologies further. In the final chapter of the book, there is a section entitled "The future of Management Support Systems." A couple of predictions stood out to me:

> Groupware technologies for collaboration and communication will become easier to use, more powerful, and less expensive. They will make electronic group support a viable initiative even in small organizations. 

Thank you, COVID-19. Zoom, Slack, Microsoft Teams, and many other technologies are now ubiquitous and necessary. The magical Metaverse might take this concept even further, where you interact with a digital version of yourself in a 3D environment. Let's have a meeting on the top of Denali. I don't know if that is cool. Let's look at another prediction:

> Using voice technologies and natural language processing will further facilitate the usage of MSS. 

Bingo. Amazon Alexa, Apple's Siri, and many others have dramatically expanded the use of NLP. Thank you, neural networks. These technologies may supplant keyboard-based search and unpredictably alter the companies that created them. I want to share one more:

> Frontline decision support technologies mainly supporting CRM will become integral to I.T. in most medium-sized and large corporations.

This is the most accurate quote from this section. Salesforce has become a dominant player and continues expanding its capabilities through acquisition (in 2019 Tableau and in 2020 Slack) ^[https://investor.salesforce.com/press-releases/press-release-details/2019/Salesforce-Signs-Definitive-Agreement-to-Acquire-Tableau/default.aspx, https://investor.salesforce.com/press-releases/press-release-details/2020/Salesforce-Signs-Definitive-Agreement-to-Acquire-Slack/default.aspx]. CRM platforms are increasingly using NLP to enable conversational intelligence. However, these developments take a long time to mature. Almost 20 years after this quote was written, growth is still progressing rapidly. 

Uncertainty, egos, intelligence, and luck breed innovation, and the problems clubs face are more complex than ever. If your core business isn't efficient, it prohibits you from working on potentially more rewarding projects. This book gives you a good idea of how to implement basic analytical tasks to serve the strategic initiatives of you and the managers throughout your organization. Please take what you learn here and improve on it.






