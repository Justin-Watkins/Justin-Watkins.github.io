
# Consumer Research {#chapter9}



This chapter will discuss different research techniques within the context of a sports team looking to leverage that research to better understand their customers. Most people hate research yet they claim that they love it. Normal people should hate research. If you don't, I hope you do after you read this chapter. It is tedious, painful, is typically repetitive in nature, and opens you up to scrutiny. Research is difficult and unless you have a PhD or worked in the research industry, it is unlikely that you have extensive experience with it. Unfortunately, you need to understand it. 

One of the main issues that you will face with it is that results from research projects are often only considered in a cursory fashion. The person who understands the results the best will be the designer and analyst. This is partly because many of the internal consumers will only be interested in a narrow band of concerns. This can be discouraging.

Furthermore, proper research is an enormous topic. In chapters \@ref(chapter5) and \@ref(chapter6) we mention that it would be easy to write an entire book on pricing and segmentation. It would be easy to fill multiple volumes on consumer research. You can find any number of these tomes on _ebay_ or on other market sites being traded at a significant discount. It would be wise to purchase a few of them to add to your library. We'll discuss a few of the books I have used over the years if you continue to read through this chapter. Basic research techniques haven't changed very much in a long time and having a few references is advised. This chapter will discuss two main topics:

1. The basics of experiment design and hypothesis testing
2. Planning and designing surveys

We'll only be able to cover a sliver of topics and techniques that you will likely face at some point in your career. We have already discussed `ANOVA` and other mechanisms to analyze experiments, but we didn't discuss how those experiments need to be designed in order to validate our techniques. This is where the term _statistical significance_ gets thrown around. The concept of statistical significance is often not well understood. It is used in a narrow context around hypothesis testing and is a mathematical artifact. It doesn't mean that a survey isn't good or useful. We'll discuss it in some detail a little later. 

I included experiment design here because it is a topic where most people lack any experience. Indeed, many business leaders aren't well versed in research in any practical way and have a difficult time navigating and consuming it. I'd like you to come away from this chapter with a few key pieces of knowledge that will help you grasp research. This might read a little cynically, but here is some food for thought. 

- You can't always trust research
- Different techniques can lead to more practical outcomes
- Sampling is difficult and involved
- Analyzing results takes some special care
- Conflicting outcomes can confound application
- It isn't always worth conducting

One of the main difficulties with consumer research in sports is that _stated_ and _observed_ behavior can often be different. This is always true, but it can be more true for sports. For instance, season-ticket-holders may not respond well to a survey that might indicate price increases, yet still renew at high rates. People try to _game_ surveys hoping that their responses can tilt Fortuna's wheel ^[See Boethius: https://en.wikipedia.org/wiki/Fortuna] in their favor. 

Additionally, research methods may be combined with more advanced discovery like purchasing data from a data-broker such as Acxiom. We've spoken about the problems with third party data quite a bit. Research conducted by fellows at Deloitte found serious inaccuracies with data purchased from a well known data broker [@Lucker2017].

> "Our survey findings suggest that the data that brokers sell not only has serious accuracy problems, but may be less current or complete than data buyers expect or need.

Accurate data is an enormous problem. Garbage-in, garbage-out. I've seen this in practice when conducting surveys by comparing stated responses to questions on gender, ethnicity, and age to data purchased on the market. Whenever practical, "Trust, but verify." 

Despite the issues that you will encounter, research should be a fundamental component of business strategy. The bigger the problem, the more important conducting worthwhile research becomes. Understanding how to frame questions that can be answered by some form of research is an overlooked skill set. Getting good at it takes experience. Hopefully, this chapter will get you thinking about this at a high level and give you the rudiments of a toolbox you can use to be more effective and confident at conducting and analyzing research. 

For the most part, you will probably conduct rather simplistic satisfaction surveys through email and deployed after games or periodically throughout the season. Conducting surveys follows a distinct process. We'll loosely frame this chapter around a process for designing a survey borrowed from "Designing Surveys, a guide to decisions and procedures." [@Blair2014] These steps include:

- Planning and survey design
- Questionnaire design and pretesting
- Final design and planning
- Sample selection and data collection
- data coding, analysis and reporting

Since the most common research method that you will likely employ will be the emailed survey, this is where we will focus. This chapter will demonstrate the basics of survey design, data preparation, and analysis. We'll also discuss our philosophies for creating them and applying the results. Since we have already demonstrated some of the techniques that we would use for analysis, we are going to put most of our focus on planning and survey design. 

## Designing experiments and hypothesis testing

There are many ways to design an experiment and this is also an extremely deep subject. Additionally, nothing will give you a case of _impostor syndrome_ faster than trying to become an expert on clinical experiment design. This stuff is full of confusing statistics jargon and combines multiple knowledge bases. Since putting together specific designs (say a fractional factorial design) is fairly mechanical, you can follow a recipe and do it correctly. Making sure the underlying assumptions regarding your analysis plan are fulfilled can be much more challenging. Luckily, you aren't going to subject to some peer review mechanism by people who conduct research as a profession. We'll try to hit the high points and demonstrate a couple of practical examples. In terms of a framework for discussion, we used "Designing experiments and analyzing data" [@Maxwell1990] by Maxwell and Delaney and "Applied Survey Data Analysis" [@Heeringa2014] by Heeringa, West, and Berglund as a high level reference. 

Experiment design is really about validity. You are concerned about your results having merit in real-world applications. There are also multiple types of validity such as _statistical conclusion validity_^[https://en.wikipedia.org/wiki/Statistical_conclusion_validity] and _construct validity_^[https://en.wikipedia.org/wiki/Construct_validity]. Much of the analysis we have covered to date has been on _statistical conclusion validity_. That is, do your results meet specific criteria related to testing your hypothesis. _Construct validity_ refers to drawing the correct conclusions from that analysis. There are many other potential problems with the validity of an experiment. Always keep this in the back of your mind. 

You'll also hear a lot of common terminology when designing an experiment. The most common terms you will hear are likely calls for a _Treatment_ and _Control_ group. This is the basic structure you will need for an _A/B_ ^ [https://en.wikipedia.org/wiki/A/B_testing] test.  This sounds straight-forward enough. One group receives a stimulus (perhaps a specific advertising mechanism) and another group doesn't. You use this fact to test whether the stimulus had a measurable impact on a specific outcome such as a purchase intent. The designs of these tests can be simple such as in the case of an A/B test or very complex. Ultimately, you hope to subject the findings on your tested groups to some statistical tests.You are looking for some level of assuredness in answering the question as to whether there are valid differences between individuals in two or more populations. Afterward, you simply have to interpret everything correctly. With any luck, you'll be able to build some causal models using the results. 

### Hypothesis testing

Hypothesis testing is confusing just because of the sentence structure that you will encounter. If you don't have a statistics background, you need to take some time to understand hypothesis testing. The next couple of paragraphs are simply going to touch the high points. There are a few steps and a few statistics that you will want to consider. You start by pecifying _an hypothesis_. Let's use an example. 

I want to understand if season ticket holders spend more money on concessions than non season ticket holders. My _Null hypothesis_ is that the mean spend of season ticket holders - the mean spend of non season ticket holders = 0. If I reject the null hypotheses it implies that the mean spend between these two populations is not equal to 0. Go ahead and reread that sentence. I know it doesn't make any sense. Don't blame me. I didn't create this stuff. 

Let's take a sample from both groups. We'll create some fake data here for this exercise.


```r
#-----------------------------------------------------------------
# Create spend data
#-----------------------------------------------------------------
sth <- as.data.frame(matrix(nrow=1000,ncol = 2))
fan <- as.data.frame(matrix(nrow=1000,ncol = 2))

names(sth) <- c('spend','type')
names(fan) <- c('spend','type')

set.seed(715)
sth$spend <- rnorm(1000,25,7)
fan$spend <- rnorm(1000,18,7)
sth$type <- 'sth'
fan$type <- 'fan'

# Sample data
set.seed(354)
sth_samp <- sth[sample(nrow(sth), 400), ]
fan_samp <- fan[sample(nrow(fan), 400), ]
```



Table: (\#tab:chninespenddataviewtwo)Sample spend data

          spend  type 
----  ---------  -----
278    16.34787  sth  
699    23.83900  sth  
581    16.23701  sth  
611    32.08364  sth  
943    36.39058  sth  
761    39.41891  sth  

We are going to use the sample to make an inference about the general population. There are four possible outcomes for a hypothesis test:

1. The null hypothesis is false. You reject it. The means are not equal to zero and season ticket holders spend differently than regular fans.
2. The null hypothesis is true. You do not reject it. season ticket holders do not spend more on average than regular fans.
3. The null hypothesis is true, but you do not reject it. This is called a type I error. 
4. The null hypothesis is false and you fail to reject it. This is called a type II error. 

The basic way to test an hypothesis is by using a student's t test. Let's apply it here and take a look at the output. 


```r
#-----------------------------------------------------------------
# T Test
#-----------------------------------------------------------------
t_test <- t.test(sth_samp$spend,fan_samp$spend)
```


Table: (\#tab:chninespenddataview)t.test results

|            |t.test_results          |
|:-----------|:-----------------------|
|estimate    |6.560613                |
|estimate1   |25.0236                 |
|estimate2   |18.46299                |
|statistic   |13.24688                |
|p.value     |2.573968e-36            |
|parameter   |789.8377                |
|conf.low    |5.588437                |
|conf.high   |7.532789                |
|method      |Welch Two Sample t-test |
|alternative |two.sided               |


In this case we _reject the null hypothesis_ that the differences in means are zero. The alternative hypothesis is true. There are also alternatives to the base `t.test`. You also need to consider if the sample sizes are equal and that other assumptions that you are making are actually true. 

### Sampling

This brings up another major consideration in experiment design. The validity of your experiment will depend heavily on your _sampling_ methodology. What questions should you be asking about your sample? Many of these questions are related to how your sample could potentially bias your results:

- Is my sample representative of the population I am trying to test?
- Is the sample large enough to apply to the broader population?
- Does the sample need to be _random?_

As you can imagine, this could get complex. 

From the preceding example, how do we know how many people to sample? We can use a _power analysis_^[https://en.wikipedia.org/wiki/Power_of_a_test] to give us an idea. We'll use the `pwr` [@R-pwr] package to evaluate our data. The following example is adapted from Kabacoff [@Kabacoff2011].


```r
#-----------------------------------------------------------------
# Power analysis
#-----------------------------------------------------------------
effect_size <- 3/sd(sth_samp$spend)
signif_lvl  <- .05
certainty   <- .9 

pwr_test <- pwr::pwr.t.test(d         = effect_size,
                            sig.level = signif_lvl,
                            power     = certainty,
                            type      = 'two.sample')
```

The results of this test are in table \@ref(tab:chninepwrresults).


Table: (\#tab:chninepwrresults)t.test results

|          | pwr_t_test_results|
|:---------|------------------:|
|n         |           127.1571|
|sig.level |             0.0500|
|power     |             0.9000|


According to our test, we need 127 participants in each group in order to calculate an effect size of .4 with 90% certainty with no more than a five percent chance of concluding that there is a difference when there isn't. Again, reread that sentence. 

This is an extremely simplistic example. There are a number of potential issues such as the underlying normality of the data, whether the values are independent, if the samples are correlated, and many more. We aren't going to go through this in any more detail. You just need to understand that getting a good sample takes a little rigor. Use a reference and follow a process. You'll be able to explain yourself later (You might just be explaining yourself to yourself).  

### Experimental design

One common experiment design is called a factorial design. ^[https://en.wikipedia.org/wiki/Factorial_experiment]. Factorial designs are common and similar to everything else, can spiral into complexity. The goal here is to make sure that you are testing each possible combination of factors against each test subject. As a note, a full factorial design isn't always feasible because it comes with cost trade-offs. It may not be possible to deploy as many surveys as you would like. In this case a fractional factorial design may be used.  ^[https://en.wikipedia.org/wiki/Fractional_factorial_design] This section is going to cover a very simplified example. Honestly, you wouldn't really use something like this in sports unless you were designing a conjoint or other formal experiment. There are also many other designs such as a _combinatorial design_^[https://en.wikipedia.org/wiki/Combinatorial_design]. If you are interested in them, you'll have to research these methods on your own. I just want you to be aware of them. If nothing else, you can impress a third party researcher that you are likely to encounter in the future.  

Let's take a look at a basic factorial design for an experiment. We will use the `AlgDesign` [@R-AlgDesign] library to build our design. Let's assume that we have two sections that we want to look at: _Dugout Seats_ and _Homeplate seats_. We want to understand consumer preferences for each section based on a high, low, and medium price. Let's say that we had three potential prices.

|Price Level|Dugout|Home Plate|
|:-:|:-:|:-:|
| High | 95 | 95 |   
| Medium| 85 | 85 | 
| Low | 75 |  75 |
|...| ... | ... |

Use the `gen.factorial` function to produce a factorial design based on the preceding options. 


```r
#-----------------------------------------------------------------
# Factorial Design
#-----------------------------------------------------------------
library(AlgDesign)

fd <- gen.factorial(levels   = 3,
                    nVars    = 2,
                    center   = TRUE,
                    factors  = FALSE,
                    varNames = c("Dugout Seats",
                                 "Homeplate Seats"))
#> Warning in xtfrm.data.frame(x): cannot xtfrm data frames
```


Table: (\#tab:chninefacdesign)Factorial design for survey

|Dugout Seats|Homeplate Seats|
|:----------:|:-------------:|
|     -1     |      -1       |
|     0      |      -1       |
|     1      |      -1       |
|     -1     |       0       |
|     0      |       0       |
|     1      |       0       |
|     -1     |       1       |
|     0      |       1       |
|     1      |       1       |


In this case we have nine different combinations that we will need to put in front of our survey recipients. The numbers represent which factor is to be tested. The first three rows indicate that the high, medium, and low prices for dugout seats are to be tested against the low price for home plate seats:

|Price Level|Dugout|Home Plate|
|:-:|:-:|:-:|
| High | 75 | 85 |   
| Medium| 85 | 85 | 
| Low | 95 |  85 |
|...| ... | ... |

The survey would give the respondent the option to purchase either seat at each level:

> Which seat would you prefer at the indicated prices?

In this case we would show a picture of the view from the seats. We are testing how fans value the view from these specific seats relative to one another. There may also be _mixed effects_^[https://en.wikipedia.org/wiki/Mixed_model] here. You have to be careful with these sorts of experiments. How would you analyze the results? There are a few ways. Let's create some data to see what we would do. 


```r
#-----------------------------------------------------------------
# Survey Responses
#-----------------------------------------------------------------
survey_responses <- 
  tibble::tibble(dugout    = factor(unlist(rep(fd[1],1000))),
                 homePlate = factor(unlist(rep(fd[2],1000))),
                 selection = NA)

survey_responses$dugout <- sapply(survey_responses$dugout, 
                                  function(x) switch(x,'-1' = '75',
                                                        '0' = '85',
                                                        '1' = '95'))

survey_responses$homePlate <- sapply(survey_responses$homePlate, 
                              function(x) switch(x,'-1' = '75',
                                                    '0' = '85',
                                                    '1' = '95'))

survey_responses$respondent <- c(rep('sth',4500), rep('sin',4500))

selection <- list()
x         <- 1
set.seed(755)

while(x <= nrow(survey_responses)){
  
  s1 <- survey_responses[x,1] 
  s2 <- survey_responses[x,2]
  
  selection_list <- c(s1,s2)
  
selection[x] <- sample(selection_list, 
                       size = 1, 
                       prob = c(.2,.8))
x <- x + 1
  
}

survey_responses$selection <- unlist(selection)
survey_responses$section  <- 
  ifelse(survey_responses$selection == survey_responses$dugout,
         'dugout',
         'homePlate')
```

Our survey responses look like this:


Table: (\#tab:chninesurveyresponse)Factorial design for survey

|dugout|homePlate|selection|respondent|section|
|:----:|:-------:|:-------:|:--------:|:-----:|
|  75  |   75    |   75    |   sth    |dugout |
|  85  |   75    |   85    |   sth    |dugout |
|  95  |   75    |   95    |   sth    |dugout |
|  75  |   85    |   75    |   sth    |dugout |
|  85  |   85    |   85    |   sth    |dugout |
|  95  |   85    |   95    |   sth    |dugout |


We can create an interaction plot with the following code.


```r
#-----------------------------------------------------------------
# Interaction Plot
#-----------------------------------------------------------------
ip_data <- survey_responses             %>%
           group_by(respondent,section) %>%
           summarise(meanSelection = mean(as.numeric(selection)))

g_xlab  <- 'Respondent Type'                     
g_ylab  <- 'Mean Price'                         
g_title <- 'Interaction Plot, respondents and location'

ip_plot <- 
ggplot(ip_data, aes(x = respondent,
                y = meanSelection,
                color = section,
                group = section))                 +
       geom_point(shape=2, size=3)                +
       geom_line(size = 1.1)                      +
       scale_y_continuous(label = scales::dollar) +
       scale_color_manual(values = palette)       +
       xlab(g_xlab)                               + 
       ylab(g_ylab)                               + 
       ggtitle(g_title)                           +
       graphics_theme_1
```




<div class="figure">
<img src="images/ch9_interaction_plot.png" alt="Interaction plot of survey results" width="100%" />
<p class="caption">(\#fig:chnineintplot)Interaction plot of survey results</p>
</div>


This plot suggest that the effect of the _view_ based on seating location is not consistent between single game ticket buyers and season ticket holders. While season ticket holders tend to value the views as equivalent, single game buyers may be willing to pay more for home plate seats when given the choice between home plate and dugout seats. You can see how complex these designs could potentially become. This is a very simple example, but it gives you the basics of how to design an experiment and produce a basic analysis. 

## Planning and design

Since we covered segmentation in chapter \@ref(chapter4) we'll base our example around gathering information related to building some pyscographic segments. This is a useful example because you could be doing one of many things. There are opportunities to:

- Hypothesis test. For instance, do certain segments tend to spend more than others?
- Look for causal links between attitudinal data and long term purchase behavior. 
- Discover groups within our population that follow specific behavioral patterns.
- To look look for correlations between behavior and specific activities.

The best way to illustrate this process is by creating a specific scenario. 

> The markeing department of the Nashville Game Hens is interested in approaching marketing efforts in a more sophisticated fashion. We want to understand a couple of different things about our fanbase: 

> 1. To understand our market structure. Who is coming to games and how does this compare to the general population of the region? We want to break that market structure into logical segments that can be discovered through multiple channels to use in marketing campaigns.

> 2. To understand something about our brand affinity and what it means. How is our brand percieved in the market? 

These are two very broad problem statements. We can see that these topics might cover multiple facets such as price sensitivity, media consumption, general interests, or financial status. We can also see that question two won't allow us to use any internal data. We are forced to collect it. We'll clearly need to carefully structure a plan in order to make sure that we actually answer the questions we are asking. In fact, these two statements didn't really ask the questions we need at all. We are going to have to contextually interpret them for our internal client. 

We need to structure how we plan on attacking this effort so that we can be sure that we address the request. What are we actually concerned with? Let's interpret the questions:

Question one is concerned with a generalization of a fan. We basically need to create a specific number of groups of people that are more alike each other than to other groups and compare them to a broader population sample that includes our fan base and the regional or national population. I can already tell you that this will be difficult. If you have one-hundred-thousand people in a sample you really have one-hundred-thousand segments. Attempting to generalize them into an arbitrary number of boxes that can be well understood will be difficult.

Question two is concerned with how an individual feels about our brand. Our competitive set may need to be uncovered. Are there other sports teams in our region that we could measure ourselves against in order to evaluate our brand? Is there a broader competitive set we should consider? How does our in-park experience impact our brand? This isn't a run-of-the-mill satisfaction survey. This is going to require some work.

Another of the main concerns we face in this example that influences our decision-making-process is the tension between _discoverability_, _accuracy_, and _utility_. Will this analysis be used to target specific individuals? Is the analysis something that we can cast on broader segments of people to understand where they fit in our segmentation scheme? How accurate will the results be? If they aren't very accurate the utility of what promises to be an expensive project may be significantly reduced. Make sure everyone clearly understands expectations and trade-offs. 

### Understanding the makeup of a clubs fans

From a brand perspective, sports is special. You don't typically see someone walking around a city with a hat advertising their favorite shampoo. Sports crosses an incredibly wide swath of individuals and has major cyclical components. Endemic concerns might include:

- There are several ticket classes with relatively small populations that have an out-sized revenue contribution
- Responses may be different during the season or at different times during the season
- There are multiple levels and forms of consumption

Referencing the first point, corporations may make a up a large portion of season tickets. Do we think demographic information is of any use here? Is there a distinction between someone who purchases tickets for their business versus a fan that purchases specifically to enjoy the game? What does enjoying the game actually mean? Individuals may consume through any number of formats and channels controlled by the club or not controlled by the club. There are many implicit and explicit signals that might imply fandom. Are we mainly concerned about ticket sales for this segmentation project? 

In our case, we will be concerned with ticket sales. We have seen some of these techniques. The factor analysis we conducted in section \@ref(factoranalysis) is an example of a potentially useful technique. The data here would have come from a survey asking why someone attends a game and what they do when they attend a game. The point here is that we had a plan for the data that we were collecting. We knew we were going to use a factor analysis to derive insight from the survey and we designed the survey to accommodate this fact. 

Ticket sales are typically public information with teams tending to announce sales ^[http://www.espn.com/mlb/attendance/_/year/2019]. Let's take a moment to analyze some data from MLB in 2019.

|Club|Sales|
|:-:|:-:|
| Dodgers | 3,974,309 |   
| Cardinals | 3,480,393 |   
| Yankees | 3,304,404 |  
|...| ... |

These teams all had a high number of ticket sales. How many individuals do we think this represents? We have to make some assumptions.

- Average of 20,000 FSEs in season tickets
- Season ticket holders buy an average of 4 tickets
- Single game buyers come to an average of 1.5 games and buy 3 tickets per game
- Groups of larger than 20 make up 10% of sales

There are many more assumptions that we would have to make, but the point is clear. If we are looking at purchasers as opposed to people who attended games, the results may look different. Additionally, we aren't considering fans that only watch on TV or follow through some other media. What about default-fans? Fans that identify with the team, but don't exhibit explicit signals that they are a fan. What about people that purchase merchandise, but don't consume the primary product? Market structure is complex in this industry.

The question remains. How large is our actual market and who precisely are we attempting to segment? The answer to this question might be the dreaded "Yes." The real answer, like everything in analytics is that it depends. The project forks in different directions depending on that answer. Let's refer back to our question. We have two objectives: 

1. To understand our market structure. Who is coming to games and how does this compare to the general population of the region? 
2. To understand something about how are brand is perceived and to interpret this perception in a may that it is useful for making decisions. 

How might we obtain the information in question 1? At least part of this data probably already exists.

- Is there governmental data that we access like census data?
- Observational research
- Emailed surveys
- Third party research

Observational research could be as simple as walking onto the concourse during the game and writing down what you see. Technologies could also be deployed here. Facial recognition technologies ^[https://aws.amazon.com/rekognition] can even automate this procedure to a large extent. 

How would we get the information in number 2? Number two also looks like a combination of techniques: 

- Emailed surveys
- Third party data

What features are we interested in looking at? At this stage we won't know what could matter. For instance, if you are looking for people that might purchase season tickets, wealth factors like _household income_ might be important. At a minimum you'll want basic demographic features such as:

- Age
- Number of children
- Marriage status
- Gender
- Ethnicity

Why do you want a feature such as ethnicity? Why does it matter what ethnic group an individual belongs to? This could be useful to your advertising department in terms of channel or the location of particular OOH efforts. Additionally, the data could be used longitudinally for a variety of purposes.

Look carefully at potential questionnaire and data quality issues. Carefully considering the question at hand is the best way to fetter out issues that may manifest at a later stage. The more time you spend considering the question, the better your final results will be. 

### Selecting the right research method

A sports team may have several needs from a consumer or brand-equity perspective. However, sports fandom can be a fickle thing. As we have discussed, fandom exists for many reasons. Switching teams isn't as easy as switching to a different hair treatment. Fans tend to be sticky, which is one of the main reasons that research often takes a back-seat in the decision making process. However, sports clubs are facing headwinds along several dimensions regarding consumer behavior such as brand loyalty and media consumption [@Fromm2018]. Properly developed and deployed research is the only method we have to confront these issues in an informed way. In sports, we have slightly different needs for research relative to other industries because of our unique brand positioning with our fans and the fashionability that ebbs and flows along with team fortunes. These questions might include:

- What is our competitive set? 
- What do consumers like about the product?
- What are our consumer's constraints (financial, monetary)?
- What are our fan's awareness levels with sponsors?
- What do fan's think about our prices?
- How are we perceived in the market relative to other properties?
- Should we introduce a loyalty program?

Different needs have different requirements in terms of research. There are also multiple types of surveys that are designed for specific tasks. These specialty surveys must be designed in a particular way and require some knowledge to interpret. Examples include:

- Conjoint experiments^[https://en.wikipedia.org/wiki/Conjoint_analysis]
- Van Westendorp^[https://en.wikipedia.org/wiki/Van_Westendorp%27s_Price_Sensitivity_Meter]
- Max-Diff^[https://en.wikipedia.org/wiki/MaxDiff]
- Predictive market studies^[https://en.wikipedia.org/wiki/Prediction_market]

While there is significant variation within techniques, relatively few techniques are commonly deployed. Different techniques also have strengths and weaknesses. A Van Westendorp survey may demonstrate how prices for certain products (like a seating section) are perceived, but it doesn't inform us on willingness-to-pay (covered in chapter \@ref(chapter6). A conjoint experiment might give you a better indication of willingness to pay. You could also design formal field experiments to accomplish the same thing. 

Other studies might require longer time horizons. Longitudinal studies may be useful for measuring the change in perception over time. Like other topics that we have covered, focused research looking to uncover causal links between activity and outcome tends to be the goal. Each of these stages has several substages that will need to be thought-through. The planning process is critical.

### Building and designing the questionaire

We've seen that building surveys can be extremely complex if you are trying to build a durable study. In this section we'll focus on building the questionaire. Coding survey questionaires is painful work. I try to follow the following principles:

1. Have a plan for how you are going to use and analyze the data. 
2. Don't ask a question if you are not going to use it.
3. Don't survey too much or too often.
4. Pay attention to survey burden in terms of length

Some surveys may be very focused and will be looking to uncover just one or a few pieces of insight. Other surveys may be very broad and be more more exploratory in nature. [@Blair2014] Luckily, there are many research tools that can help you design effective surveys. Products such as Qualtrics^[https://www.qualtrics.com/] or Survey Monkey^[https://www.surveymonkey.com/] will even automatically analyze your survey in terms of burden. They also contain banks of questions that you can use as a resource.

Often times you'll break a larger survey into specific sections:

- Demographics
- Brand
- Satisfaction
- Product

As a rule, try to keep surveys as short and as relevant as possible. Think carefully about sequencing. For instance, what is the most important thing you need to know? Put those questions in the front followed by any qualifying information. 

### Qualifying your sample

It is often critical to qualify your sample. Qualifying your sample will make the results more relevant and may reduce the costs ^[If you are administering a survey through an agency and are incentivizing respondents] of deploying the survey. These questions may be behavioral or demographic. This section might ask questions such as:

> 1. What is your gender?
> - Male
> - Female

This is important because you might have a quota. A sample that is 85% male may not be desirable. There are also guides about how to ask questions that are increasingly becoming controversial. Inclusivity is also something to consider. You can find any number of guides on writing inclusive surveys^[https://www.surveymonkey.com/mp/diversity-and-inclusion-survey-templates]. Be consistnet. Additionally, you might have quota limits on specific ethnicities. 

> 2. What is your ethnicity?
> - White or Caucasion
> - Black or African American
> - Eastern Indian 
> - Asian
> - Native American or Pacific Islander
> - Latinx

Did we denote these ethnicities correctly? It's important to think about and different nomenclatures go in and out of fashion. For example, _Latinx_ has begun to replace "Hispanic or Latino." I am not here to judge the merits of replacing these terms. Just be aware that everyone will have an opinion here. Build yourself a backstop of awareness. _Hispanic_ is also a difficult concept. What makes someone Hispanic? Are they also black or white? Is this important? You'll have to make judgment calls based on what you are trying achieve with your survey.

Some people may even poison your sample. Many surveys qualify with a question such as:

> 3. Do you are anyone in your family work in marketing research?

If someone works in marketing research they may understand some of the mechanisms that you are trying to deploy. This could bias the results of certain types of questions such as a conjoint analysis. 

In sports, it is also very common to ask about fan avidity:

> 4. Are you a fan of the Nashville Game Hens? 

However, it is often unwise to ask about specific avidity in the screening section. A better method might be to ask a question like this:

> 4. Please rate the following activities in terms of your interest:

|Activity | Interested | Not Interested |
|:-:|:-:|:-:|
| Knitting class       |  |  |
| Attending a MLB game |  |  |   
| Attending a concert  |  |  |  
| ... | ... | ... |

If this survey is being distributed through a third party, you won't be giving away the fact that the survey is about the Game Hens. It might also allow you to disqualify anyone who isn't interested in attending a game. It all depends on what you are trying to accomplish. 

In addition to screening questions, dummy questions are typically added to a survey to guard against indifferent respondents. For instance, you might embed a question like this into your survey:

> 26. Please select the fourth answer to this question:
> - Answer 1
> - Answer 2
> - Answer 3
> - Answer 4

You will be surprised at how many people will get this question wrong. It is probably best to disqualify all responses from someone who gets this question incorrect.  

### Typical survey questions

There are certain questions that almost always tend to be asked on surveys. I include a section on demographics here because it is usually of interest and is commonly included on questionnaires. There are preferred ways to broach this subject and I think it is important to discuss them specifically. 

If you are able to track respondents, you may already have their demographic information. If your survey doesn't require an answer to a question it is important to think about where this information is sequenced on the survey. A good practice is to ask the respondent if they would like to answer some demographic questions:

> Would you like to answer a few demographic questions?

This will prevent people from ignoring the rest of the survey if they aren't interested in answering demographic questions. You might also consider putting demographic questions at the end of the survey. This will ensure that you collect other information that you might deem as more important. Additionally, you'll want to consider if you are using this data longitudinally. Changing the format of these questions may make analysis difficult if you are comparing the data to older data sets. 

Let's walk through some typical examples of demographic questions. This seems a little pedantic, but how you ask these questions is important. 

Instead of asking for an age, I prefer to ask for birth year and then to calculate the age:

> 1. What is the year of your birth?

This will make it easier to compare this data to data collected in the past or the future. It also makes it easy to place people into demographic buckets. Additionally, you'll be able to build more accurate scatter plots of the data. When I can, I try to collect numerical data. While age can be a sensitive subject, I haven't seen a problem with simply asking for a birth year. 

Asking about educational achievement is also common. Why do we care? Education is often a proxy for wealth. Someone may not be comfortable telling you their income, but education isn't as taboo.

> 1. What is the highest level of education that you have completed?
> - High school
> - Some college
> - College 
> - Graduate degree

Marital status is also commonly asked. You'll want to include an _other_ category here. You will typically see many other arrangements such as _separated_, _divorced_, or _widowed_. I don't typically include them. If you are asking about something to do with sports what are you going to do with this? Yes, sports may be a salve for loneliness, but how are you going to find all the widowers? I just don't see a lot of practical application here in our context. When possible, keep it simple and omit it if you can't think of a possible use for it outside of exploratory analysis. Some answers might be simple proxies for asking about things such as sexuality.

> 2. What is your Marital Status? 
> - Single
> -	Married
> -	Partnership
> - Other

Asking about children is also typical. Some sports are seen as family activities more than others. Additionally, stoking interest in young people is a longer term strategic play. How much effort do merchandisers put into appealing to young people with sports? 

> 3. Are there any children under the age of 18 living in your household?
> - Yes
> - No

Almost all sports look to develop youth and understanding how many children attend games is important. Knowing the age of children is also important. There is a big difference between a 5 year old and a 16 year old. If the respondent answers 'yes' to the preceding question you would typically present them with something like the following question:

> 3.a. Please select their age(s). 
> -	0 to 2
> -	3 to 5
> -	6 to 10
> -	11 to 15
> -	16 to 17

In this case we are using a multi-select. multi-select is more difficult to work with on the back-end and will require additional data wrangling. The more complicated the question structure, the less likely you will be to actually use it. You have to strike a balance bewteen the ideal and the practical.  

Geography is especially important for a club. Season ticket holders likely live in a relatively small area that surrounds the stadium or ballpark. Idiosyncrasies in a market also make understanding the relative geography important. The lack of rail or other infrastructure may make the stadium less accessible from certain parts of the region. The most generalized way to get geography is by asking for a zipcode. 

> 4. Please enter your zipcode:

If you have ticketing or shipping info, you may not need this data point. It is obviously best to get an actual address so that you can collect the latitude and longitude, but zipcode is the next best readily available piece of information. 

Income is a little tricky. If the survey isn't anonymous, many people may choose not to answer this question or deceptively answer it. I'll go ahead and include the net present value of my company life insurance in the figure. We could all use more money. Additionally, this question would be more interesting if it was continuous in nature. We can force it to be later if we would like. One of the big decisions here is how granular to make the question. 

> 5. What is your annual household income?
> -	Under $10,000
> -	$10,000 -  $49,999
> -	$50,000 -  $99,999
> -	$100,000 - $149,999
> -	$150,000 - $199,999
> -	$200,000 - $249,999
> -	More than $250,000

This data is ordinal in nature, meaning that we want it displayed in a specific and logical order. Often questions answers are randomly reshuffled. This is done to protect against bias introduced by someone habitually answering questions in the same way. Some answers will need to be randomized, but if the question is long, it might make sense to alphabetize the answers. Let's look at an example:

> 6. Which answer best describes your occupation?
> -	Administration/Managerial
> -	Agriculture
> -	Clerical/White Collar
> -	Craftsman/Blue Collar
> -	Educator
> -	Financial
> -	Homemaker
> -	Legal
> -	Medical
> -	Professional/Technical
> -	Retired
> -	Sales/Service
> -	Self Employed
> -	Student
> -	Other

Are these occupations logically organized? Is _Agriculture_ an occupation or an industry? Do you care if someone is in the military or works as a youth pastor at a church? This is more of a _color_ question. If you don't have a specific use for it, you may consider omitting it. _Other_ is likely to attract a large number of responses. If someone is an accountant do they consider themselves Clerical or Finance? I don't typically like this question. 

There are many other demographic questions that could be conceived, but the preceding examples cover the basics that you are likely to deploy. Pay attention to how the answers are displayed and the data type. This stuff always requires some specific care. 

#### Avidity questions

Understanding avidity is also important in sports. This also tends to be misunderstood. How can you measure someone's avidity in sports? There are several explicit and implicit signals that might demonstrate avidity. Which individual in the following example is the most _avid_ fan? 

- A person purchases season tickets for \$700
- A person purchases season tickets for \$20,000
- A person purchases single game tickets for \$1,500

These explicit signals likely demonstrate some level of affinity if not avidity. There are also interactions at play. Are we actually just measuring wealth? Be cautious about avidity. If you simply organize spend into leveled buckets you probably aren't measuring avidity. 

Implicit signals are more subtle. 

- A person purchases merchandise online
- A person visits the website often
- A person enrolls their child in a free kid's club membership

The person might have purchased items for a gift. We just don't know. You might also ask a person specific questions. A common one might be:

> 7. How big of a fan are you?
> -	I love the Game Hens. I live and die for them.
> -	I really like the Game Hens. They are one of my favorite teams.
> -	I identify with the Game Hens, but am a casual fan.
> - I don't realy care about the Game Hens. I am not a fan.
> - I hate the Hens. I hope they lose every game.

I tend to think of this sort of question on a likert scale. Something like 1-5 or 1-7. This is a typically used convention and you can think of what lies underneath these questions in the same way. "I love the Game Hens. I live and die for them." represents a five. You can see how it is difficult to word these questions. Pay attention here. You can easily word a question that is ambiguous or difficult to understand. Additionally, should you include an odd or even number of answers. An even number of responses makes someone pick one side or the other. This could be useful information. 

## Brand affinity

Gauging brand avidity is difficult. We'll explore a tool to take a look at one component of brand avidity called a perceptual map. We'll use the library `anacor` [@R-anacor] to accomplish a part of this task. This package is build to assist with correspondence analysis^[https://en.wikipedia.org/wiki/Correspondence_analysis]. Do a little research on this topic.   


```r
#-----------------------------------------------------------------
# Calculating scores for perceptual data
#-----------------------------------------------------------------
library(anacor)
pd <- as.data.frame(FOSBAAS::perceptual_data)
row.names(pd) <- c('Chickens','Titans','Predators') 

anHolder <- anacor(pd,ndim=2)

anHolderGG <- 
  data.frame(dim1 = c(anHolder$col.scores[,1],
                      anHolder$row.scores[,1]), 
             dim2 = c(anHolder$col.scores[,2],
                      anHolder$row.scores[,2]),
             type = c(rep(1,length(anHolder$col.scores[,1])),
                      rep(2,length(anHolder$row.scores[,1]))))
```

This function used the aggregated perceptual data that we created in chapter two. The question read like this:

> How do you feel about the following sports properties? Please check all that apply for each of the teams listed. 

This initial data set took the form of a multi-select table: 

|Team|Friendly|Exciting|Winners|Losers|
|:-:|:-:|:-:|:-:|:-:|
|Came Hens|   |   | |  |
|Predators|  |  |  |  |
|Grizzlies  |   |   |   |  |




```r
#-----------------------------------------------------------------
# Create perceptual map
#-----------------------------------------------------------------
library(scales)
library(RColorBrewer)
library(grid)
library(gridExtra)

basePal     <- c('grey60','mediumseagreen','grey40','steelblue1')

g_xlab     <- '\n PC1 (55.7%)'
g_ylab     <- 'PC2 (44.3%) \n'
g_title    <- 'Nashville Area Sports Perceptual Map \n'
     
PM <- 
  ggplot(data = anHolderGG,aes(x=dim1,y=dim2,
                               colour=factor(type)))         +
  geom_point(size = .5, fill = 'white', colour = 'White')    +
  geom_segment(data = anHolderGG, aes(x = 0, y = 0, 
                                          xend = dim1, 
                                          yend = dim2), 
                  arrow = arrow(length=unit(0.2,"cm")), 
                  alpha = 0.75, color = "steelblue2")        +
  geom_text(aes(label       =  rownames(anHolderGG)),
                  size         = 3.2,
                  position     = "jitter")                   +
  scale_color_manual(values = basePal,
                        name   = 'Perception',
                        breaks = c(1,2),
                        guide  = FALSE)                      + 
  xlab(g_xlab)                                               + 
  ylab(g_ylab)                                               + 
  ggtitle(g_title)                                           + 
  graphics_theme_1                                           +
  geom_vline(xintercept = 0,lty=4,alpha = .4)                +
  geom_hline(yintercept = 0,lty=4,lpha = .4)                 +
  coord_cartesian(xlim = c(-.7,.9))              
#> Warning: Ignoring unknown parameters: lpha
```

This code produces the map in figure \@ref(fig:chninepercmap)

<div class="figure">
<img src="images/ch9_perceptual_map.png" alt="Perceptual map of Nashville Sports Properties" width="100%" />
<p class="caption">(\#fig:chninepercmap)Perceptual map of Nashville Sports Properties</p>
</div>

How do we read a perceptual map? In this case, the _Chickens_ tend to be seen as _Fun_ and _Expensive_ relative to the other properties. What does this mean? Perhaps we want to be seen as innovative. Being being seen as innovative in our market may make us more attractive to certain sponsors. Whatever our motivation, a perceptual map allows you to visualize feelings around your brand relative to other brands. You can use it over time to take measurements around these feelings relative to initiatives that you hope will alter perception in your favor. 


## Other topics

We didn't cover very much in this chapter out of necessity. There is simply too much material. We covered some of the high points and discussed fundamental components of research such as hypothesis testing and sampling. We also covered basic survey design and a couple of examples of survey analysis. We didn't really talk about causal models, but we have examples of this sort of research throughout the book. It is often useful to think about survey design through the lens of answering a specific question with a causal model. Main subjects that we didn't cover that you should be aware of include:

- Social listening
- Brand personality studies
- Models based on acquisition
- Product recommendation
- Developing and positioning products
- Intercept surveys
- In-depth interviews
- focus groups
- Competitive intelligence
- Incentivization

The most obvious subject that we didn't cover is _social listening_, but we will cover it a little here. Social listening has become a large industry and there are dozens of platforms that can aid you. While it is important to monitor and respond to social content, I believe sentiment analysis is of little practical value. Additionally, wordclouds and other typical consumption techniques for social are interesting but aren't typically surprising or informative. Feel free to disagree with me here. This sentiment comes from practice. 

Where I do find social listening value is through the lens of media equivalency. Your sponsorship and social team needs to understand how much content is being placed through social channels and how to value that content. There are multiple ways to do this, but you will likely need the help of a platform for this task. Like any other media content evaluation, you'll need to take volume, quality, and some arbitrary value to estimate how much you are returning to sponsors.  

We are only going to give a nod to focus groups. Where are focus groups interesting in sports? I believe they serve a role in public relations in terms of season ticket holders. This is especially true outside of the traditional focus group that might be looking at customer preferences or constraints. Fan councils have become important, but care must be taken to ensure that these groups remain on task. They can have a tendency to degrade into complaint centers.    

We aren't going to mention the other topics at all. If you want to learn about them, there are resources available everywhere. There are also hundreds of agencies that would gladly work with you. Sports teams are attractive marketing platforms and working with them is prestigious. Take advantage of that prestige. The trick is to know what quality research entails and to find a partner that understands it as well. This is a more difficult task than you think. You've been warned. 

## Key concepts and chapter summary

Research should be a foundation of strategic initiatives. Whether you are improving an operations process, pricing tickets, or building pitch decks for a sponsorship team, producing credible research is critical. We covered five main topics in this chapter:

- Planning and survey design
- Questionnaire design and pretesting
- Final design and planning
- Sample selection and data collection
- data coding, analysis and reporting

Research is an enormous topic, but by focusing on a few wildly used practices you can develop sound strategies for both leveraging and creating your own research. We covered a number of important concepts and linked these activities to chapter \@ref(chapter5) and chapter \@ref(chapter6).  

We also covered sampling, typical question styles, data types, and two specific examples covering brand affinity and conjoint experiments. Keep a few principles in mind as you deploy surveys:  

- You can't always trust it
- Different techniques can lead to more practical outcomes
- Sampling is difficult
- Analyzing results takes some special care
- Conflicting outcomes can confound application
- It isn't always worth conducting


