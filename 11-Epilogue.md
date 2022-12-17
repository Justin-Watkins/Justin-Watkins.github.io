
# Epilogue {#Chapter11}

We have covered a variety of subjects related to foundations business strategy in a sports business setting. This setting is specific to working at a club. We have been focused on how to build strategies that increase ticket sales and revenue, and strategies to benefit business operations. We have also uncovered some thought process during our time together. Additionally, you were shown a number of concepts in two different parts. Chapters 1-5 covers foundational elements that are needed in order to analyze specific problems. Chapters 5-10 looks at those specific problems and demonstrates some techniques that you can use to solve them.

1. Chapter \@ref(chapter1) introduced us to __how to think about and use data__. Using data is fundamental to business strategy
2. Chapter \@ref(chapter2) introduced us to some specific data sets and to how to create them using the __R language__. Some knowledge of programming is still critical for the analysis. 
3. Chapter \@ref(chapter3) demonstrated how to __build and interpret the foundational graphs using R__. It also covered summarizing and exploring data.
4. Chapter \@ref(chapter4) discussed how to frame and think about problems that you will face. We also got to see some basic __project management__ techniques . 
5. Chapter \@ref(chapter5) introduced us to __customer segmentation__. We look at a few different methods and discuss how to use this data.
6. Chapter \@ref(chapter6) covers some basic __pricing__ and forecasting principles.
7. Chapter \@ref(chapter7) extends segmentation with __lead scoring__.
8. Chapter \@ref(chapter8) demonstrated how to consider __promotions and covers some brand management__ concepts
9. Chapter \@ref(chapter9) introduces some formal __research principles__ including hypothesis testing and sampling.
10. Chapter \@ref(chapter10) covered a couple of techniques related to stadium operations. Understanding simulation is critical to solving a wide variety of operations problems. 

This is a lot of material, but have only scratched the surface. In fact, I struggled to even cover subjects in any real depth. Let's take a look at our four goals we discussed at the beginning of this book and discuss whether they were accomplished.

1. To give you an analytic toolbox
2. To teach you about how a sports team's business works
3. To apply this knowledge to real problems to achieve desired outcomes
4. To build a reference manual of solutions to common problems

Ultimately, this knowledge coalesces into strategic thought. You aren't born understanding strategy. The foundations of strategy are built on experience. Analytics is tightly coupled to strategy. It is something that touches every functional unit of a business and helps produce the answers to questions that the strategist devises. Let's review your analytics toolbox. 

## Your analytics toolbox

We covered a lot of code in this book and introduced a number of concepts. You definitely should have come away with a good analytics toolbox. At a high level, we covered:

- How to manipulate and summarize data with code
- regression
- How to implement machine learning algorithms 
- Formal research methods
- Simulation and its applications
- Building graphics
- Problem solving and framing projects

We also covered several techniques, the code that you can use to implement them, and how to interpret the results. However, there is a lot that we didn't cover We didn't cover. 

1. Neural Networks and A.I.
2. More exotic forms of regression
3. Bayesian methods
4. Other ensemble learning methods

This is deliberate. Once you understand how to think through a problem, applying a specific algorithm is trivial once you have your data sets in the proper place. There are also hundreds of algorithms, but they more-are less do the same things in our context:

1. Predict a numerical value
2. Predict a class
3. Demonstrate structure

We didn't cover tools such as convolutional neural networks for computer vision or speech recognition. That is because we don't really need it and specialists are going to be able to do it better than us. For instance, you might want to deploy facial recognition for entering a suite. You might also like to deploy speech recognition or natural language processing to replace your sales staff. You might want some spatial analysis of the park using something like a digital twin. Ultimately, vendors will do that work for you in a much more efficient manner. You just need to be aware of these tools and how they are leveraging them. You don't want a salesperson wowing your executives with "A.I." when it isn't even the right tool to be using. Now you know what that means. 

## Sports business 

We also discussed how to think about problems and should understand some of the distinctions between sports and other industries. Sports is unique and outcomes are often out of your control. You can't just apply techniques and analysis learned in business school because the business is constricted in many ways. There are geographic boundaries, agency agreements, labor issues, and many other unique circumstances. At their heart, many leagues are simply trade organizations. Our work revolves around a constrained optimization exercise. It's like we operate a mutual fund. Sometimes it's up, sometimes it's down. Your job is to navigate those seas and to think about problems in advance and in an abstract fashion.

Individuals are also attracted to sports for a variety of reasons and that should influence our thought. Clubs deal with public relations issues along a variety of avenues. They can be appropriated by politicians at the most inopportune times. Our brand is critical and we aren't always in control of it. This is a strategic problem that we didn't even consider covering, but should be understood. How do you proactively protect your brand through public relations and community involvement. How do these issues impact corporate sponsorship or ticket sales? These measures could be defensive or offensive in nature. How do you know that you are making the right choices? You may not know. You just do the best you can.  

## Problems faced by a club

Additionally, we covered many real-world problems.The first part of this book was concerned with a few main subjects:

1. Understanding the context of analytics and strategy within sports business (specifically at a club)
2. Building and understanding common data sets (To introduce you to R and the data)
3. Exploring data (Understanding how to build the most common graphs that you will use)
4. Framing Projects (Understanding how to think about problems in a strategic fashion)

The second half of this book covered the application of analytic techniques and the interpretation of the results. We covered:

1. Segmentation 
2. Pricing
3. Lead scoring
4. Promotions
4. Research
6. Operations


We didn't cover many subjects related to functional departments or exercises that make some of what we covered possible. Some of these functions live in I.T. or live at the Executive level. Some of thse related subjects include: 

1. Asset valuation in corporate sponsorship departments
2. Building dashboards and other business intelligence functions
3. Constructing ETLs

Additionally, we didn't cover higher-order strategic problems. These problems might involve legal rights or fundamental features of customer or asset classes. Examples of these strategic issues include:

- Media rights
- digital rights 
- Other issues with politics or legal issues
- Growing top-of-funnel audiences (looking at Gen Z or Gen Alpha)
- Business development and growth


## How do I learn more

Google it. Seriously. There are a million resources for learning R or Python online. You can take free classes or access entire books on subjects like programming for free. The same can be said for machine learning techniques. However, this comes with a warning. Techniques change rapidly. Techniques such as random forests and support vector machines may be destined for the scrap-pile as neural networks become easier to deploy. TensorFlow [@tensorflow2020] accelerated this trend several years ago.

Additionally, if you are a student take some classes and network. Contact someone at a club and ask if you can work on a project with them for school. I you already work in the industry, try to expand your horizon. Don't get locked into only working on a few narrow projects. Look to expand your influence throughout the office. The broader your work experience, the better you'll be at everything that you do.  

There are also scores of books on any number of subjects related to analytics. The subject is so broad that you will naturally gravitate toward specific components. You may prefer visualization or building databases. You might fall-in-love with modeling and statistics. Figure out what components of analytics that you like, purchase a used book on it, read it and try to duplicate what you can find. R, Python, TensorFlow, and many other technologies can be used for _free_. Download them and get started on some data. Thousands of data sets can even be found embedded in R and Python. In R you can find them with a simple command:


```r
data(package='ggplot2')
```

You can see all the available data sets by using this variation of the preceding function:


```r
data(package = .packages(all.available = TRUE))
```

Find some interesting data sets and use them. Many packages also have excellent documentation with full-scale vignettes. Take advantage of them. With a little time and focus, you'll be surprised at how much you will learn. 

## What does the future hold

Many of the examples that you saw in this book have been solved to one degree or another. The problems are well understood within and outside of sports. For instance, we only explored pricing from a very rudimentary standpoint. Dynamically pricing tickets based on variable demand levels has been happening in industry (by applying specific algorithms) for over forty years. Probably much longer. It's commoditized. This is a good thing. During the nascency of the analytics revolution the analyst may have been considered a malevolent presence in the board room. They are now a necessity and that influence will continue to grow. The skill sets need to wield an analytics team will be a prerequisite for future leadership. Working in the field is the best way to get that experience.

Over time, you will see more functions become integrated into CRM systems and skill sets will become more comoditized as students continue to flock to "analytcs" oriented degree programs funded through cheap government student loans. This is neither bad nor good. I look at analytics in a similar vein to Computer Engineering degrees. You don't need one-million people with Computer Engineering degrees. Do you know what you call a second-rate computer engineer? A bartender. They might also run a call center or do other I.T. work. The point here is that you only need a few people who are really good at building better processors. Analytics is similar to me. You don't need armies; You need a few people who are really good at it.

Furthermore, analytics will begin to change the workforce in sports. Chat-bots will increasingly take over for sales and service personnel. Accountants are similarly doomed. If what you do is formulaic, you aren't going to be doing it long. These workforce changes aren't limited to sports. We all better be voting for universal basic income.  

Media will continue to rapidly change. GenZ and GenAlpha (All born after 2000) will continue to shape media consumption and content strategy. Both of these factors impact sports consumption through media and even more critically, in-person. What is trick? Nobody knows yet, but most literature says something like this [@Fromm2018]:

> "Start by humanizing your brand. This means giving your brand a personality that consumers can engage with."

Apparently, communication rules have changed. Interactions with hardware seem almost silly:

> "Pivitols learned to swipe before they could speak. Attempting to swipe the unswipable--like TV screens or the pages of a magazine--they assumed the image in front of them was broken."

I admit that I have swiped a magazine page. Gen Z interacts with social media and technology in a much more intuitive way than older generations. Sports is adapting, but will have to continue to adapt. We don't know what the answer is here, but interfacing with young people is a huge strategic problem that has to be thought of as an investment. At the club level, it is difficult to think about marketing initiatives in the context of investment. However, we have to do it. 

Stadium operation will also continue to change. New venues will be more purposefully constructed to provide more convenient and more immersive experiences for fans. I've been concerned for years that a terrorist attack on a large public sporting event would revolutionize how we approach ticketing, ingress, and egress. The same thing happened in 2001 when attacks on the World Trade Center permanently altered air travel ^[https://www.pbs.org/newshour/nation/how-911-changed-air-travel]. You'll see massive changes here. Whether these changes improve the experience will be up for debate. However, the proliferation of gaming and gambling will definetly have an impact. 


Additionally, everything is incremental. Nothing is new about any of the concepts in this book. Neural Networks have been around for decades. Looking back at an old textbook from college "Decision Support Systems and Intelligent Systems" published in 2001 [@Aronson2001] I reviewed the chapter on Neural Networks. Fundamentally, nothing has changed. Incremental improvements in hardware, software, and mathematics have simply pushed these technologies further. In the final chapter of the book there is a section entitled "The future of Management Support SYstems. A couple of predictions stood out to me:

> Groupware technologies for collaboratoin and communication will become easier to use, more powerful, and less expensive. They will make electronic group support a viable initiative even in small organizations. 

Thank you COVID19. Zoom, Slack, Microsoft Teams, and a host of other technologies are now ubiquitous and necessary. Let's look at another excellent prediction:

> The use of voice technologies and natural language processing will further facilitate the usage of MSS. 

Bingo. Amazon Alexa, Apple's Siri, and many others have dramatically expanded the use of NLP. Thank you neural networks. I'd like to share one more:

> Frontline decision support technologies that mostly support CRM will become an integral part of IT in most medium-sized and large corportations.

This is the most accurate quote from this section. Salesforce has become a dominant player and is continuing to expand it's capabilities through acquisition (in 2019 Tableau and in 2020 Slack) ^[https://investor.salesforce.com/press-releases/press-release-details/2019/Salesforce-Signs-Definitive-Agreement-to-Acquire-Tableau/default.aspx, https://investor.salesforce.com/press-releases/press-release-details/2020/Salesforce-Signs-Definitive-Agreement-to-Acquire-Slack/default.aspx]. CRM platforms are increasingly using NLP to enable conversational intelligence. These developments take a long time. Almost 20 years after this quote was written development is still proceeding at a rapid pace. 

Ultimately, we aren't in chaos, but there are a lot of disruptive and chaotic problems that we face. Littlefinger in Game of Thrones called chaos a ladder. ^[https://www.quora.com/What-is-the-meaning-of-the-Chaos-is-a-ladder-quote-from-Game-of-Thrones] He was correct. Uncertainty creates innovation and the problems faced by clubs are more complex than ever. If your core business isn't efficient, it prohibits you from working on potentially much more rewarding projects. Hopefully, this book give you a good idea of how to implement basic analytical tasks to serve the strategic initiatives of managers throughout your organization. 






