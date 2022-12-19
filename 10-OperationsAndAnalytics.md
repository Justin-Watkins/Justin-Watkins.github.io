
# Operations and Analytics  {#chapter10}



If a sports team has two fundamental core competencies they should be events management and selling tickets. These two efforts are where most of the work takes place. Additionally, a smooth operation is critical to brand perception. It is a pillar of our product and should be treated as such.  

The overarching umbrella of operations in the club context is to get fans into, around, and out of our facility safely, quickly, and conveniently. There are design, system, and technology components that must be considered. There are also optimization considerations such as the cost and number of point-of-sale units for concessions and retail, labor optimization for security, food production, the number of seats in particular sections, the number of bathrooms, etc. The list is extensive. We'll apply some techniques from the overlapping academic fields of Operations Research, Industrial Engineering, and Operations Management to analyze and solve a couple of ubiquitous _operations_ problems. 

Operations is really about studying systems and this chapter will only cover a small fraction of the field. Once again, this is about being aware of ways to approach these problems. The ocean always gets deeper. We will identify some key concepts that are easy to apply to a wide variety of problems. Additionally, venues are now being designed with more advanced capabilities in mind. These capabilities might include:

- Ordering food and beverages from your phone 
- Digital tickets
- More advanced security scanning technologies
- Security cameras that feature facial recognition
- Integrated commerce systems and loyalty mechanisms
- Integrated public transit

While these systems help to solve existing problems, they can exacerbate other issues. For instance, attempting food delivery without considering kitchen locations could lead to quality control issues. Never consider technology solutions without carefully examining the underlying execution capability. Businesses are littered with the withered husks of technology solutions that failed to deliver, were an ill fit, were a pet project of some inept executive, or simply faded away from an internal or external inability to manage the solution. 

Despite advances in technology, venues will always be faced with optimization problems around moving large numbers of people through their systems in a short amount of time. There are also additive factors such as parking or public transit, nearby entertainment districts, game day promotional items, food an beverage service, and security screenings that all must be considered. At a high level, this chapter hopes to accomplish three things:

- Introduce you to some basic Operations Management problems and solutions
- Cover even more project management at a high level
- Introduce you to the complexity of venue operations

We'll take you through a couple of examples of these problems and demonstrate some techniques for solving them. These techniques are generalized and are the basic tools that you could use to solve many interrelated operations problems. You'll come away with a better appreciation for the design and maintenance of these systems in the context of running a club. 

## Understanding basic issues with ingress

Capacity constraints are obvious and unavoidable with ingress. If you have 30,000 to 400,000 people trying to get to the same place at the same time, lines are unavoidable. The Romans certainly understood these issues well. The Colosseum of Rome was designed with 76 vomitoria that would accommodate over 50,000 people^[https://en.wikipedia.org/wiki/Colosseum]. Ironically, the Colosseum was likely more efficient at ingress and egress than a modern stadium. Many venues require a security check involving a magnetometer. Bags must be checked, tickets may need to be scanned, building and fire codes create constraints, and internal space is taken up by concessions and mechanical infrastructure. The Romans didn't have to worry about running electricity or HVAC throughout their venues. These issues also extend outside of the building and apply to road traffic, ADA considerations, public transit, and ride-sharing partnerships. 

Getting thousands of people into a venue quickly, safely, and in an orderly fashion is difficult. There are multiple constraints to consider:

- Capacity 
- Technology 
- Procedural

Additionally, sporting events deal with surge demand on ingress and egress. Most of the time the majority of people will choose to enter the building at around the same time. Technology can alleviate some capacity constraints. However they are inextricably linked to procedural and capacity constraints. How do you alleviate some of the problems associated with Ingress? 

Eliyahu Goldratt published a book in 1984 called _The Goal_ [@Goldratt2004] which introduces us to the _Theory of Constraints_. This book gives us a simple framework for approaching a problem such as Ingress. Goldratt introduced the five-step _Process Of On-Going Improvement_:  

1. Identify the system’s bottlenecks
2. Decide how to exploit those bottlenecks
3. Subordinate every other decision to 'step two decisions'
4. Elevate the systems bottlenecks
5. if, in a previous step, a bottleneck has been broken, go back to the beginning.

A system can only have one bottleneck ^[It is more accurate to say that this system can only have one bottleneck at a time] at a time. That is what makes this process iterative. If you replace the weakest link in a chain with a stronger one, some other link may become the weakest. Let's outline an ingress process and look at some data. An Ingress process is probably going to look fairly similar at virtually every venue in the world. A typical flowchart for and ingress procedure can be seen in figure \@ref(fig:chtengate).


<div class="figure">
<img src="images/ch10_gate_process.png" alt="Typical gate entry process" width="100%" />
<p class="caption">(\#fig:chtengate)Typical gate entry process</p>
</div>


Figure \@ref(fig:chtengate) demonstrates a typical gate procedure. Although recent advances in technology have made such a process faster, this basic process is followed at most event venues. What sort of data could we extract from this process? You would typically have scan data from the ticketing process and perhaps magnetometer passes and failures. You'll know how many people come through each gate at each point of entry and when they passed through security. let's take a look at some aggregated data. 


```r
#-----------------------------------------------------------------
# Access scan data
#-----------------------------------------------------------------
scan_data <- FOSBAAS::scan_data
```



Table: (\#tab:chteningressdatatab)Aggregated scan data

|observations|scans|action_time|date    |
|:-----------|:----|:----------|:-------|
|1           |0    |61200 secs |4/1/2024|
|2           |2    |61260 secs |4/1/2024|
|3           |4    |61320 secs |4/1/2024|
|4           |7    |61380 secs |4/1/2024|
|5           |10   |61440 secs |4/1/2024|
|6           |11   |61500 secs |4/1/2024|

This data is aggregated by the number of scans by minute and is summed and bucketed. The distribution of scans can be seeing in figure \@ref(fig:chtenscansgraphicb).



```r
#-----------------------------------------------------------------
# Scans
#-----------------------------------------------------------------
x_label <- 'observation'                                             
y_label <- 'scans'                                          
title   <- 'Ticket scans by minute at gates'
scan_point <- 
  ggplot(data = scan_data,aes(x     = observations,
                              y     = scans,
                              color = date))                +
  geom_point()                                              +
  scale_x_continuous(label = scales::comma)                 +
  scale_y_continuous(label = scales::comma)                 +
  scale_color_manual(values = palette)                      +
  xlab(x_label)                                             + 
  ylab(y_label)                                             + 
  ggtitle(title)                                            +
  stat_smooth(method = "lm", formula = y ~ x + poly(x,2)-1) +
  geom_vline(xintercept = 151, lty = 4)                     +
  graphics_theme_1                                          +
  guides(color = 
         guide_legend(override.aes = list(fill = "grey99")))
```


<div class="figure" style="text-align: center">
<img src="images/ch10_scans_dist.png" alt="Distribution of ticket scans at the gates" width="100%" />
<p class="caption">(\#fig:chtenscansgraphicb)Distribution of ticket scans at the gates</p>
</div>
In general, ticket scans will follow a specific cadence. Let's use the data to make some inferences and discuss the entire problem. We'll go a little deeper into this sort of analysis in a subsequent section.  

Our ballpark has four points of entry for fans and each point of entry has four scanners. We can tell that our entry process is slightly probabilistic. Not all scans will take the same amount of time because a failure requires adjustments an another scan and people move at different paces. What is the maximum capacity of this system?

This question is actually difficult to answer because we know that some gates are likely to be busier than others at different times. We are looking for the gate with the maximum throughput under duress. You will need multiple days of observation to get a good average figure.


```r
#-----------------------------------------------------------------
# Scans
#-----------------------------------------------------------------
max_scans <- scan_data                                %>% 
             group_by(date)                           %>%
             summarise(maxScans = max(scans),
                       maxScansMean = (max(scans)/16),
                       meanScans = mean(scans),
                       medianScans = median(scans))
 
```



Table: (\#tab:chteningressthroughputmax)Maximum observed throughput

|date    |maxScans|maxScansMean|meanScans|medianScans|
|:-------|:-------|:-----------|:--------|:----------|
|4/1/2024|181     |11.3125     |103.6067 |116        |
|4/2/2024|199     |12.4375     |115.7267 |129        |
|4/3/2024|212     |13.2500     |125.0167 |139        |

The highest observed average number of scans per scanner is about 13 scans per minute across each ingress point. This means that a person went through the system every four and a half seconds for one minute at some point. However, this average may mean that some scans took ten seconds and many more took one second. We can't tell from this data. In a subsequent section we will discuss queuing theory and how to analyze wait-time by looking at service times, inter-arrival times, line-length, and queuing discipline. We are illustrating a broader point with this example. 

We can see that we are missing some key data. We can also begin to see that this problem sprawls and becomes very complex. What data are we missing? I would prefer to see:

1. The process components split and timed
2. Information on line-length 
3. Specific information at each gate and magnetometer
4. Information on inter-arrival times
5. Information on staffing numbers and procedure
6. Scaner positives and false positive numbers

What can we say about what we have? Can we identify a bottleneck? Judging by our diagram it seems that if a magnetometer is triggered that an individual is asked to walk back through it. Perhaps we could change the process so that we add staff to wand guests that triggered the gate. We could also eliminate bags or alter the magnetometer settings and then measure the differences. Not all solutions require much diligence.  

We'll expand on this example and look at an analogous project in a little more depth. Reducing wait times at concession stands.

## Reducing wait times at concessions

Everyone has spent time standing in line for food and beverage at sporting event. If you asked someone what is wrong with the system they might give you a couple of predictable responses such as "There are too many people" or "These people just don't know what they are doing." In reality, this is a complex problem that has many components:

- System constraints (number of grills, points-of-sale, etc)
- Labor (experience, training, motivation)
- Back-of-house systems (buffering demand, menu design)
- Front-of-house systems (Queuing discipline, ordering, and payment systems)

The interesting thing here is that you don't really have to acknowledge that there is a problem. Perhaps there isn't. You can look at this system simply state that we don't have enough points of sale. That is why lines are long. If we had more points of sale that would spread out the lines and the lines would be shorter. Of course, that is an incredibly reductive point of view. Let's be a little more realistic and begin by constructing a narrative:

> _Executives for the Nashville Game Hens have noticed long lines at concession stands during games. Lines tend to get noticably worse on the weekends when more fans are in the building. Additionally, customer satisfaction surveys indicate that time spent waiting in line at concession stands is a major source of dissatisfaction. The concessions manager says that "the problem is that we don't have enough points-of-sale to deal with capacity once we reach about 30,000 fans." She poses a solution that will require a large capital investment to add more points of sale by adding another restaurant concept. You are approached by an executive and asked if that is good idea..._  

Where do you go from here? You might begin by making some observations yourself. You might also look for any data that you have available. We'll assume you don't have anything. You talk to the concessions manager and she tells you that her standard is for orders to be filled in less than ninety seconds. This is an industry standard and that she achieves it _on average_.   

Without any data, this project will to have to proceed in stages. You can also take some cues from the nature of the problem itself to help devise a plan for approaching a solution. At least three of the identified project components involve some degree of process improvement. Perhaps there is an off-the-shelf process improvement framework you could adapt and leverage to help you structure the problem. Since we are looking at process improvement, let's see if we can simply apply DMAIC to this problem. DMAIC stands for _Define, Measure, Analyze, Implement, and Control._ It comes to us from Six Sigma^[https://en.wikipedia.org/wiki/Six_Sigma], a process improvement protocol that has been adapted to a number of business problems. While Six Sigma has it's roots in manufacturing, we can appropriate some of its tools here.

If you are going to use a framework you might as well go all the way and produce a project charter that lays out a full project plan. A project plan needs to include a few basic components. The two that we will concern ourselves with include:

- Project objectives
- Specific goals

Other components that a charter should cover include:

- Timelines
- Budgets
- Stakeholders
- Potential problems

We'll ignore most of the features of a project management plan and focus on Objectives and Goals. However, we make this point for a couple of reasons. The first reason is that a project plan forces you to think about how to solve a problem. This is often the most difficult part. It also forces you to create some documentation around the project. If you do not create some basic documentation around your projects it will eventually be used against you and not to your benefit. Make a habit of building project charters for any projects involving multiple stakeholders or external groups. It will make scoping projects much easier and help keep everyone on task and on budget which is indeed the point.

Let's take a close look at how we might structure some objectives for this project.

### Establishing objectives

Since we don't really know anything about this problem from a data perspective, how do we set objectives? Objectives can be a little vague, but they derive from the _business case_ and _problem statement_. Let's take a stab at establishing some objectives. We'll use some concepts from Six Sigma [@Campe2007] for this example. 

The business case is simply a statement that indicates the importance of the project. It should demonstrate why the project needs to be addressed: 

> Customer satisfaction has been linked to repeat purchases and has a demonstrable impact on year-over-year revenue. Additionally, customer satisfaction scores predicibly degrade once attendance exceeds 28,000. Surveys have concluded that improving these scores can be best achieved by decreasing the wait time at concessions throughout our venue. With over 100 games left in the season, we have an opportuinty to demonstably impact season ticket renewals. Additionally, our capital budgets must be completed in the next sixty days. 

This is a nice vague statement that establishes a few things:

1. This project is important
2. It needs to be completed
3. We have a limited amount of time to get started

Given the nature of this project, we are going to collect some data before we frame the project any further. Our data will give us a much more objective method for defining the problem and establishing goals.

### Understanding our problem

We have a goal with collecting exploratory data. We are looking for something to help build our problem statement. In this case, perhaps we can simply go out and look at line-length at a particular concept. How would this work? Let's take a closer look at a standard concession concept. 

A typical concept has eight to fifteen items on the menu. Items are purchased at differential rates and have varying prep times. Most items can be stored for about twenty minutes before quality begins to degrade. The number of points of sale vary, but most concepts have between four and twelve points of sale. Customers enter the queue and wait until a point of sale become available. They place their order, pay, and then wait at the point-of-sale for the order to be fulfilled before exiting the system.

Let's discuss the queuing discipline in a little more detail. A detialed analysis of queuing systems will be covered later in this chapter within section \@ref(queuing). However, if you are unfamiliar with how queuing systems are analyzed, I recommend spending a little time covering _Queuing Theory_ ^[https://en.wikipedia.org/wiki/Queueing_theory]. Queuing theory can be extremely complex and has many applications across a variety of disciplines. To simplify it, just think of your goal as to design systems so that the outcomes are more deterministic. Let's describe our queuing discipline in more detail since it is a critical component of this system. 

The Game Hens' concession concepts typically follow a _multi-channel, single phase (MCSP)_ queuing discipline. In a MCSP system we have a one-step (single phase) serving process where the register handles the complete transaction and there are multiple points-of-sale (channels) serving the queue. Additionally, the process follows a FIFO (first-in, first out) queue discipline where the customer waiting the longest amount of time is serviced first.

Let's extract the key elements of this system:

- Process follows a FIFO queue discipline and does not function asynchronously
- Ordering, payment, and fulfillment happen at the point-of-sale
- Fulfillment is difficult to buffer due to differential storage times and demand levels

Now that we have a little bit of detail, we can construct a plan for capturing some measurements for analysis. 

### Defining our problem and establishing goals

Appropriately scoping a project can be difficult. Most strategically oriented projects tend to sprawl when you begin to think about them. This one is no different. There are lots of considerations. Let's create a problem statement that unambiguously explains this project.

> Problem statement: Wait times for concessions services across the ballpark consistently recieve low relative satisfaction scores (less than 10% of fans give the highest rating) from our season ticket holders. Low satisfaction scores are correlelated with a higher likelihood for a specific fan to not renew their season membership. While industry standards for service times have been quoted by our vendor at ninety seconds per transaction, observed wait times often exceed this figure by over 100%. 

Goals are more precise than objectives. Since we don't have any hard data on our process, we will have to wait to establish firm goals. The initial goal will be to collect the necessary data with the hopes that we can reduce wait times. At this stage, we have no idea how much it may be possible to reduce wait times. Although there is an industry standard, we don't know if this figure has any merit. 

## Measurment and analysis 

We are going to spend the rest of this chapter walking through a tacit example of data collection and analysis. You almost never have all the data that you need. In this case, we'll need to take note of what we do have and create a plan on gathering what we don't have. Sine we will have to take live measurements, we'll need a ruberic and a budget. Additionally, our timeline will be impacted by the fact that we will need to take measurements during the game.  

### Data audit and capture

You'll want to be careful about how you capture data. You'll also want to be consistent and as thorough as possible. Spend some time thinking about this phase of the project. In this case, we know that we are going to have to capture observational data. Additionally, this data might make someone look bad. Since you have been quoted ninety seconds as the number that is being met, what happens if your measurements differ? Keep these sorts of political impediments in mind as you build your rubric. 

There are all kinds of ways to collect data in this context, but the fundamental components of that plan will be almost identical. Just google _data collection plan_. The frameworks are all very similar. You start with a specific question that you are trying to answer and then lay out the specifics of:

- Data types
- What is being measured
- How the data is to be measured
- How the data is to be captured
- How you ensure consistency

The initial goal of our analysis is to identify a bottleneck. We should be able to gather some data from our information systems. We know that scan data is being captured at the gates so we know how many people are in the park at any given time. That information may be useful.

Other data is going to have to be gathered. Leveraging the points-of-sale to estimate wait times will be lacking. Perhaps if we had cameras installed at each concept, we could use A.I. to track and clock customers. We don't. We'll have to do this the old-fashioned way. This means using people with stopwatches. This seems barbaric, but if we set firm rules around what constitutes a measurement, and you collect enough data, you should be able to get reliable estimates. 

Additionally, your concept of what information is actually needed from a business perspective will mature over time. While you would probably love to be able to track every customer through your venue at all times, is it necessary? Would you spend money here if you understood every other competing expense throughout your business? How would you use this data? CEOs and other executives have to make these decisions. Think about these problems from their broader perspective when you are confronted with them. 

The following sections will discuss our data in more detail and begin the process of analyzing it.

### Line length and total scans

Figure \@ref(fig:linelengthb) requires two separate data sets. Scans data and line length data. We have already seen our scan data.


```r
#-----------------------------------------------------------------
# Create scan data
#-----------------------------------------------------------------
library(FOSBAAS)
scans_a <- f_get_scan_data(x_value = 230,
                           y_value = 90,
                           seed    = 714,
                           sd_mod  = 10)
```



Table: (\#tab:scansashow)scan data example

| observations| scans|action_time |date     |
|------------:|-----:|:-----------|:--------|
|            1|     0|17:00       |4/1/2024 |
|            2|     2|17:01       |4/1/2024 |
|            3|     4|17:02       |4/1/2024 |
|            4|     6|17:03       |4/1/2024 |
|            5|     8|17:04       |4/1/2024 |
|            6|     9|17:05       |4/1/2024 |

Line-length data looks a little different. This data would have been collected manually by counting the number of people in line every minute. This data is also confounded by the fact that while four people may be in line, only one may order. Likewise, one person may be ordering for more than one person. When data has quirks, try to write them down. You'll have to explain them to someone at some point.  


```r
#-----------------------------------------------------------------
# Create line length data
#-----------------------------------------------------------------
line_length_a <- f_get_line_length(seed = 755,
                                   n    = 300,
                                   u1   = 22,
                                   sd1  = 8,
                                   u2   = 8 ,
                                   sd2  = 5)

line_length_a$action_time <- f_get_time_observations(17,21)
line_length_a$date <- "4/1/2024"
```


Table: (\#tab:line_length_a)line length data

 observation   lineLength  action_time   date     
------------  -----------  ------------  ---------
           1           14  17:00         4/1/2024 
           2            6  17:01         4/1/2024 
           3           18  17:02         4/1/2024 
           4            5  17:03         4/1/2024 
           5           21  17:04         4/1/2024 
           6            4  17:05         4/1/2024 


Let's take a look to see if line-length has any relationship to scans. We are looking to see if the number of people coming into the building influences line-length. The following code produces the graph in figure \@ref(fig:linelengthb).



```r
#-----------------------------------------------------------------
# Line length and scans
#-----------------------------------------------------------------
scans_a$cumScans <- cumsum(scans_a$scans)
data  <- dplyr::left_join(scans_a,line_length_a, 
                          by = "action_time")
data$color <- as.numeric(as.character(gsub(":",
                                           "",
                                           data$action_time)))

x_label  <- ('\n Cumulative Scans')
y_label  <- ('Line Length \n')
title    <- ('Line Length and cumulative scans')
legend   <- ('Time')
line_length <- 
  ggplot(data, aes(y     = lineLength, 
                   x     = cumScans, 
                   color = color))                           +    
  geom_point()                                               +
  scale_color_gradient(breaks = c(2100,2000,1900,1800,1700),
                       labels = c("9:00","8:00", "7:00", 
                                  "6:00","5:00"),
                       high = 'dodgerblue',
                       low  = 'coral',
                       name = legend)                        +
  scale_x_continuous(label = scales::comma)                  +
  xlab(x_label)                                              + 
  ylab(y_label)                                              + 
  ggtitle(title)                                             +
  stat_smooth(method = "loess", formula = y ~ x)             +
  geom_vline(xintercept = 13068, lty = 4)                    +
  graphics_theme_1  
```


<div class="figure" style="text-align: center">
<img src="images/ch10_line_length_scans.png" alt="Relationship between line length at a concession stand and scans" width="100%" />
<p class="caption">(\#fig:linelengthb)Relationship between line length at a concession stand and scans</p>
</div>
While we can see a pattern in the data where line-length tends to peak at specific times, the relationship to cumulative scans isn't very tight. It appears that fans that enter early tend to rush concession stands and fans that come in near first pitch take a seat and go to concession stands later. There is a lot of variability in this data. 

### Analyzing the results

We can analyze this data in much the same fashion as we have analyzed data in previous chapters. However, we'll introduce a new tool here called a _generalized additive model_. Be careful with this technique. While you might find that it is a silver bullet that can easily model many distributions, it is a little more difficult to work with than a math equation provided by regression. We'll use the _mgcv_ [@R-mgcv] library to access the _gam_ function. As is often the case, we'll need to do a little data preparation before applying our operation.   



```r
#-----------------------------------------------------------------
# Generalized additive model
#-----------------------------------------------------------------
library(mgcv)
scans_a$cumScans <- cumsum(scans_a$scans)
data             <- dplyr::left_join(scans_a,line_length_a, 
                              by = "action_time")

data$color <- as.numeric(as.character(gsub(":",
                                           "",
                                           data$action_time)))
gam1 <- mgcv::gam(lineLength ~ s(cumScans, bs='ps', sp=.2), 
                  data = data)

newPredict <- cbind(data, predict(gam1, interval = 'confidence'))

gr <- 
  ggplot(newPredict, aes(y     = lineLength, 
                         x     = cumScans,
                         color = color))                      +    
  geom_point(alpha=.7)                                        +
  scale_color_gradient(breaks = c(2100,2000,1900,1800,1700),
                       labels = c("9:00","8:00", "7:00", 
                                  "6:00","5:00"),
                       high = 'dodgerblue',
                       low  = 'coral',
                       name = 'Time')                         +
  geom_line(aes(y = `predict(gam1, interval = "confidence")`,
                x = cumScans),
                color = 'dodgerblue',size = 1.2)              +
  scale_x_continuous(label = scales::comma)                   +
  xlab('Cumulative Scans')                                    + 
  ylab('Line-Length')                                         + 
  ggtitle('Results of GAM on Line-Length Data')               +
  graphics_theme_1   
```

We can access a summary of our gam model to look at some of the standard statistics: 





Table: (\#tab:chtenbroommod)gam model output

----------  -------------
term        (Intercept)  
estimate    12.04333     
std.error   0.37435      
statistic   32.17132     
p.value     8.501177e-98 
conf.low    11.30962     
conf.high   12.77705     
----------  -------------

However, we can see that the data will defy an accurate fit by looking at figure \@ref(fig:gamdiagram). 


<div class="figure" style="text-align: center">
<img src="images/ch10_gam_model.png" alt="GAM output on line length data" width="100%" />
<p class="caption">(\#fig:gamdiagram)GAM output on line length data</p>
</div>

While we can see that the average fit to this data is fair, the predictive power won't be very good as a point-estimate. Ultimately, there isn't a good relationship between line-length and scans into the ballpark. However, we do see that the data appears multi-modal. Lines decrease near first pitch. This makes sense as early arrivers place their orders and take their seats. 

### Understanding wait times

Now that we have some data on line-length we can take a closer look at what is driving wait-time. We can simulate some results from measuring the broader process. We built a function _f_get_wait_times()_ to provide us with some data. This function breaks wait-times into three parts:

- Order time: The amount of time it takes to place an order
- Payment time: How long it took to fulfill payment after the order was placed
- fulfillment time: How long it took to fulfill the order after payment

This is all information that we would have had to capture through direct measurements. There wouldn't be a simple way to get this data without direct measurements. We include the function that creates the data here so that you can see that we used simple exponentially distributed data on the components of the process. This may or may not be true in practice, but we have seen similar patterns in actual data.


```r
#-----------------------------------------------------------------
# Simulate wait times function
#-----------------------------------------------------------------
f_get_wait_times <- function(seed,n = 300,time,rate1,rate2,rate3){
set.seed(seed)

order_times       <- rexp(n, rate = rate1)
payment_times     <- rexp(n, rate = rate2)
fulfillment_times <- rexp(n, rate = rate3)
total_time        <- order_times       + 
                     payment_times     + 
                     fulfillment_times

wait_times <- data.frame(transaction  = seq(1,n, by = 1),
                         orderTimes   = order_times,
                         paymentTimes = payment_times,
                         fulfillTimes = fulfillment_times,
                         totalTime    = total_time)
wait_times[] <- apply(wait_times,2,function(x) round(x,0))
return(wait_times)
}
```

This function will produce as many results as you want with order, payment, and fulfillment times being represented by exponentially distributed times in seconds.


```r
#-----------------------------------------------------------------
# Create wait times data set
#-----------------------------------------------------------------
wait_times_a <- f_get_wait_times(seed  = 755,
                                 n     = 300,
                                 rate1 = .03,
                                 rate2 = .06,
                                 rate3 = .15)
```




Table: (\#tab:simulatewaittimesb)Wait time data

| transaction| orderTimes| paymentTimes| fulfillTimes| totalTime|
|-----------:|----------:|------------:|------------:|---------:|
|           1|         39|           28|            0|        67|
|           2|          0|           56|            7|        63|
|           3|        123|            4|            4|       131|
|           4|         47|            6|           22|        75|
|           5|          4|           38|           10|        52|
|           6|          4|           37|            6|        47|
  
We can use this data to build a simulation that allows us to deconstruct total time and change some of the inputs. This will allow us to demonstrate the impact of an initiative such as mobile ordering. Mobile ordering would allow you to effectively decouple orders and possibly payment from fulfillment. Additionally, it might help demonstrate the merits of a more effecitve buffering system or a simplified menu. We'll take a closer look at how this works in the following section.  

#### analyzing the distributions of wait time components

Variance between these processes could be a problem depending on your queuing discipline. Let's take a look at the distribution of these wait times.  


```r
#-----------------------------------------------------------------
# Simulate wait times function
#-----------------------------------------------------------------
wait_dist <- 
  wait_times_a                                            %>% 
    select(orderTimes,paymentTimes,fulfillTimes)          %>%
    tidyr::pivot_longer(cols = c('orderTimes',
                                 'paymentTimes',
                                 'fulfillTimes'),
                        names_to = "measurment",
                        values_to = "seconds")            %>%
                   mutate(scale_seconds = scale(seconds))

w_dist <-  
    ggplot(wait_dist, aes(x = seconds, fill= measurment)) +    
    geom_density(alpha=.75)                               +
    geom_rug(color='coral',sides = "b")                   +
    scale_fill_manual(values=palette)                     + 
    xlab('Seconds')                                       +
    ylab('Density')                                       + 
    ggtitle('Distribution of wait-time components')       +
    graphics_theme_1 
```


<div class="figure" style="text-align: center">
<img src="images/ch10_wait_dist.png" alt="Distribution of wait time components" width="100%" />
<p class="caption">(\#fig:waittimesdista)Distribution of wait time components</p>
</div>


We can see from this graph that order times appear to have the widest variance. There is a long tail extending toward the 200 second mark. Variance kills interdependent processes. This is the enemy that we were looking to find. If we could reduce this variance, we could make the entire process more deterministic and improve wait times. 

### Simulating a component of our process

Like many of the topics we have discussed, simulation is a large and complicated topic. It is also incredibly useful for the problem that we are facing. We have already seen multiple ways to simulate data. We have used _rexp_ and _rnorm_ multiple times to create simulated data sets. This is what we are seeing in figure \@ref(fig:waittimesdista). We are creating random numbers based on parameters for exponential or normal distributions. What do we do if we simply have a data set and we want to simulate it under different conditions? How do we know what distribution to fit that will approximate the data? 

There are lots of software packages that will build simulations for you, but it is useful to understand how they might function at a base level. We'll build a couple of basic transaction simulations and then evaluate how well specific changes to our process might impact the overall system. This will give you an appreciation for how a software package might approach a problem. When possible, I have always found it useful to understand problems at their most basic level. It makes you a better decision maker.  

Simulation is a daunting subject. Non-linear least squares fits can be frustrating and there are specialized programs that make it a lot easier. Like we saw in our chapter {#chapter6}, it is easy to get into some more complex math. 


```r
#-----------------------------------------------------------------
# Simulate wait times function
#-----------------------------------------------------------------
wait_times <- FOSBAAS::wait_times_data[1:300,]
```


Table: (\#tab:mcab)Simulated wait times data

| transaction| orderTimes| paymentTimes| fulfillTimes| totalTime|
|-----------:|----------:|------------:|------------:|---------:|
|           1|         39|           28|            0|        67|
|           2|          0|           56|            7|        63|
|           3|        123|            4|            4|       131|
|           4|         47|            6|           22|        75|
|           5|          4|           38|           10|        52|
|           6|          4|           37|            6|        47|


Let's take a closer look at the wait-time data and think about how me might simulate it. We'll begin by looking at correlations between each process component. We are looking to see if any particular component is more closely correlated with the total time. There are a few packages that will build correlation tables for you, but we will go ahead and build this manually.


```r
#-----------------------------------------------------------------
# Build correlation table
#-----------------------------------------------------------------
wt_cor <- wait_times[,-1]
names(wt_cor) <- c('Order Time','Payment Time',
                   'Fulfillment Time','Total Time')

wt_cor_result      <- cor(wt_cor)
wt_cor_result      <- round(as.data.frame(wt_cor_result), 2)
wt_cor_result$type <- row.names(wt_cor_result)

cor_long <- 
  tidyr::pivot_longer(wt_cor_result,
                      cols = c('Order Time','Payment Time', 
                               'Fulfillment Time','Total Time'))
```

We'll reorder the factors so that our graph will give us the aesthetic we are looking for.


```r
#-----------------------------------------------------------------
# Build correlation table
#-----------------------------------------------------------------
cor_long$order <- factor(cor_long$type, 
                         levels=c('Fulfillment Time',
                                  'Payment Time',
                                  'Order Time',
                                  'Total Time'))
```

We'll use the _forcats_ [@R-forcats] library to access the _fct_reorder_ function. This will help order our plot. 


```r
#-----------------------------------------------------------------
# Correlation table 
#-----------------------------------------------------------------
library(forcats)
correlation_table <- 
cor_long                                                 %>%
mutate(name = fct_reorder(name, value, .fun='sum'))      %>%
ggplot(aes(x = order, y = name,fill = value))            +
  geom_tile()                                            +
  geom_text(aes(label=value))                            +
  scale_fill_gradient2(low  = "mediumseagreen", 
                     mid  = "white", 
                     high = "dodgerblue")                +
  xlab('')                                               + 
  ylab('')                                               + 
  ggtitle('Correlation table')                           +
  graphics_theme_1                                       +
  theme(axis.text.x = element_text(size = 8),
        axis.text.y = element_text(size = 8))
```

<div class="figure">
<img src="images/ch10_wait_tile.png" alt="Correlation table" width="100%" />
<p class="caption">(\#fig:mcf)Correlation table</p>
</div>

Order time is the component most highly correlated with _Total Time_. The other factors don't appear to be correlated with each other at all. You could infer all sorts of things from this data. Perhaps order time is most highly correlated with total time because no other work can take place during the order. Fulfillment time may be the least correlated with total time because we have done a good job buffering inventory. We are simply looking to see if there is a basic relationship between these variables. The fact that order time is the most highly correlated variable is important and we'll likely base our solution around mitigating long order times because it would likely have the most impact.

Always think about these problems critically. Looking at data is not enough. You need to do some field work to make sure that you understand the problem as holistically as possible.

#### Analyzing the Variance between wait time components

As we have stated, variance is our enemy. These system components are linked and depend on each other, but are not correlated. There is also a wide amount of variance.


```r
#-----------------------------------------------------------------
# Box plot of wait times
#-----------------------------------------------------------------
wait_long <- 
  tidyr::pivot_longer(wait_times,cols = c('orderTimes',
                                          'paymentTimes', 
                                          'fulfillTimes',
                                          'totalTime'))
wait_box <- 
wait_long                                             %>%
  mutate(name = fct_reorder(name, value, .fun='sum')) %>%
  ggplot(aes(x = name, y = value)) +
  geom_boxplot(fill = 'dodgerblue') +
  xlab('\n Transaction component')                              + 
  ylab('Wait time in seconds')                                  + 
  ggtitle('Variance of transaction times')                      +
  graphics_theme_1
```

<div class="figure">
<img src="images/ch10_wait_box.png" alt="Variance between components" width="100%" />
<p class="caption">(\#fig:mch)Variance between components</p>
</div>

A closer look at specified quantiles paints a clearer picture.


```r
#-----------------------------------------------------------------
# Quantiles
#-----------------------------------------------------------------
quantiles <-
apply(wait_times[,-1],
      2,
      function(x) quantile(x, probs = c(.1,0.25, 0.5, 0.75,.9)))
```


Table: (\#tab:quantiles2)quantiles for wait times

|    | orderTimes| paymentTimes| fulfillTimes| totalTime|
|:---|----------:|------------:|------------:|---------:|
|10% |          3|          1.0|          1.0|        19|
|25% |          9|          5.0|          2.0|        30|
|50% |         22|         12.0|          4.5|        45|
|75% |         42|         23.0|          8.0|        70|
|90% |         81|         39.1|         14.0|       107|

Twenty-five percent of orders take forty two seconds or more. This appears to be the biggest _problem_. It would be more accurate to say that this is the process component that likely causes the most variance in the system. Let's begin constructing our simulation by looking at a probability table of the observations. We can build a function to create a table with a little extra information. It would also be beneficial to have a little extra data. One day of transactions could certainly create some sample-size issues. Let's simulate a few thousand results. We'll pretend that we have been collecting information for a couple of weeks. Keep in mind that this could also cause other problems. If you were using regression here you might want to consider a _mixed effects_ ^[https://en.wikipedia.org/wiki/Mixed_model] model. 

Since total time is composed of the three process components, we can be sure that a regression should work pretty well in terms of explaining variance. If we regressed on this data the model should look amazing. Let's try it.


```r
#-----------------------------------------------------------------
# Simple linear model for total times
#-----------------------------------------------------------------
time_mod <- lm(totalTime ~ fulfillTimes + paymentTimes + 
                           orderTimes,data = wait_times)

stats_time_mod <- 
tibble::tibble(
  st_error     = unlist(summary(time_mod)[6]),
  r_square     = unlist(summary(time_mod)[8]),
  adj_r_square = unlist(summary(time_mod)[9]),
  f_stat       = unlist(summary(time_mod)$fstatistic[1])
)
```


Table: (\#tab:chtentotalregression)Summary stats for time model

|st_error |r_square |adj_r_square| f_stat |
|:-------:|:-------:|:----------:|:------:|
|0.5570309|0.9997996| 0.9997975  |492180.3|


As expected, the model appears to be almost perfect. We could use the equation to estimate total wait times almost perfectly. If you see results like this, there is probably something wrong. 

#### Building a simulation of our data

Finally, let's build a simulation. This section will demonstrate some of the basics to get you started. However, the method that we follow is flexible and can be used in many different ways. We'll begin by accessing the _wait_times_distribution_ data. 


```r
#-----------------------------------------------------------------
# Access the distribution data
#-----------------------------------------------------------------
library(FOSBAAS)
wait_times_distribution <- FOSBAAS::wait_times_distribution_data
```

let's take a sample of these wait times that we can use as a basis for our simulated data.


```r
#-----------------------------------------------------------------
# Get a sample of the data
#-----------------------------------------------------------------
set.seed(755)
wait_sample <- wait_times_distribution %>%
               sample_frac(size = .7)
```

Now we can begin to think about the distribution a little more carefully. We can use the _ecdf_ function to compute an _empirical cumulative distribution function_. You can think about this output as the inverse of the _quantile_ function.


```r
#-----------------------------------------------------------------
# Cumulative distribution function
#-----------------------------------------------------------------
orders <- wait_sample$orderTimes 
cdf    <- ecdf(orders)  
```



```r
#-----------------------------------------------------------------
# Cumulative distribution function
#-----------------------------------------------------------------
cdf_out <- cdf(50)
qua_out <- quantile(wait_sample$orderTimes,probs = cdf_out)

ecdf_quant <- tibble::tibble(ecdf_50 = cdf_out,
                             quantile_ecdf_50 = qua_out)
```


Table: (\#tab:chtendisplayedcf)Demonstrating the relationship between quantiles and ecdf

| ecdf_50 |quantile_ecdf_50|
|:-------:|:--------------:|
|0.7785714|    50.22143    |


About 78 percent of the observations are less than 50 seconds. It is simple to plot this function to visualize what we just did. 


```r
#-----------------------------------------------------------------
# Cumulative distribution function plot
#-----------------------------------------------------------------
cdf_plot <- 
ggplot(wait_sample, aes(orders))            + 
  stat_ecdf(geom = "step",
            color = 'dodgerblue',
            size = 1.1)                     +
  xlab('\n Orders')                         + 
  ylab('Percentage observations')           + 
  ggtitle('ECDF Order Time')                +
  geom_vline(xintercept = 50.22143,lty = 2) +
  geom_hline(yintercept = .7785714,lty = 2) +
  graphics_theme_1

```


<div class="figure">
<img src="images/ch10_ecdf_orders.png" alt="Order time ecdf" width="100%" />
<p class="caption">(\#fig:chtencumdistplota)Order time ecdf</p>
</div>

We can use this function to simulate data that fits this distribution. Let's take a random sample of data from the range of order times.



```r
#-----------------------------------------------------------------
# Simulate orders 
#-----------------------------------------------------------------
set.seed(715)
n <- 400 # observations
sim_orders <- rexp(n, rate=1/mean(wait_sample$orderTimes))

```

We can use a histogram of this data and compare it to our actual order data.


```r
#-----------------------------------------------------------------
# Compare histograms
#-----------------------------------------------------------------
hist_tab <- 
 tibble::tibble(sim_data = sim_orders,
                actual_data = sample(wait_sample$orderTimes,400))

hist_tab_long <- hist_tab %>% 
                 tidyr::pivot_longer(cols = c('sim_data',
                                              'actual_data'),
                                     names_to = "measurment",
                                     values_to = "seconds") 

hist_comp <- 
ggplot(hist_tab_long , aes(seconds))     + 
  facet_grid(.~measurment)               +
  geom_histogram(fill = 'dodgerblue')    +
  xlab('\n seconds')                     + 
  ylab('count')                          + 
  ggtitle('Simulated vs. actual values') +
  graphics_theme_1
```


<div class="figure">
<img src="images/ch10_hist_comp.png" alt="Simulated vs. actual results" width="100%" />
<p class="caption">(\#fig:chtenhistcomp)Simulated vs. actual results</p>
</div>

Our simulated data approximates the actual data very well. It should, we know that we used an exponential distribution to fit the data. We'll look at a few different methods for fitting distributions later on. For now, let's finish this exercise. 

You can't trust the results of one simulation. You'll want to create many simulations and then average the results. Let's go ahead and put together a code base that will allow us to produce a reproducible experiment. First, let's ask ourselves a question that we want to answer

> If we decreased order times by fifty percent, how would it change the average wait time? 


```r
#-----------------------------------------------------------------
# Simulate, Iterate, and aggregate
#-----------------------------------------------------------------
n <- 500 # observations

sim_orders  <- list()
sim_pay     <- list()
sim_fulfill <- list()
# Iterate
for(i in 1:500){
set.seed(i + 715)
# Simulate
sim_orders[[i]]  <-  
  rexp(n, rate=1/mean(wait_sample$orderTimes))
sim_pay[[i]]     <-  
  rexp(n, rate=1/mean(wait_sample$paymentTimes))
sim_fulfill[[i]] <-  
  rexp(n, rate=1/mean(wait_sample$fulfillTimes))
}
# Aggregate
mean_order   <- mean(sapply(sim_orders, mean))
mean_pay     <- mean(sapply(sim_pay, mean))
mean_fulfill <- mean(sapply(sim_fulfill, mean))
mean_total   <- mean_order + mean_pay + mean_fulfill
```

We now have five-hundred simulations for each phase of the total wait. We can do all kinds of things with this data. Let's take a look at the averages.



```r
#-----------------------------------------------------------------
# Aggregated results
#-----------------------------------------------------------------
mean_chart <- tibble::tibble(order   = mean_order,
                             payment = mean_pay,
                             fulfill = mean_fulfill,
                             total   = mean_total)
```


Table: (\#tab:chtenmeanchart)Reducing The impact of order times

| order  |payment |fulfill | total  |
|:------:|:------:|:------:|:------:|
|33.31705|16.80299|6.403494|56.52353|



The total average time is almost identical to what we observed. If we can reduce order time by fifteen seconds it will get the total time down to about 41 seconds. However, as we have seen this only tells part of the story. The real problem is the variance. However, with our distributions and the fact that payment, fulfillment, and orders are not correlated, the variance is unlikely to hurt us very often.   

Let's use our simulation to calculate some stats on how many orders could be fulfilled over specific time frames per point-of-sale under duress. This means that the queue is always full. Let's ask a question and answer it in different ways.

> During one hour, how much additional throughput would a register be able to process if order taking was reduced by 50%?

if our average wait time is fifty six seconds it means that we can fulfill about sixty four orders per register per hour (60 seconds/56 seconds) * 60 minutes. What does this number look like if we use samples from our simulation?


```r
#-----------------------------------------------------------------
# Results with variance
#-----------------------------------------------------------------
total_time_samp <- sim_orders[[1]]  +
                   mean_pay[[1]]    + 
                   mean_fulfill[[1]]
count_list <- list()
set.seed(715)
for(j in 1:30){
  time            <- 0
  count           <- 1
  seconds_in_hour <- 60*60
    while(time <= seconds_in_hour){
      i           <- sample(total_time_samp,1)
      time        <- time + i
      count       <- count + 1
    }
  count_list[j]   <- count - 1
}
```

Let's graph the results of our count list to see how many orders we were able to fulfill for thirty simulated hours. 


```r
#-----------------------------------------------------------------
# Observe variance in fans serviced per hour
#-----------------------------------------------------------------
counts <- tibble::tibble(fans_serviced = unlist(count_list),
                             simulation    = seq(1:30))

service_per_hour <- 
ggplot(counts , aes(x = simulation,
                    y = fans_serviced))  + 
  geom_line(color = 'dodgerblue')        +
  xlab('\n simulation')                  + 
  ylab('Fans serviced')                  + 
  ggtitle('Simulated services per hour') +
  geom_hline(yintercept = 64,lty = 4)    +
  graphics_theme_1

```


<div class="figure">
<img src="images/ch10_line_service.png" alt="Simulated vs. actual results" width="100%" />
<p class="caption">(\#fig:chtenverifyb)Simulated vs. actual results</p>
</div>

Of the thirty simulations, eight fell below the level of our average service time. When you compound this analysis with multiple registers, inter-arrival times, and different line-lengths, we can see how reducing variance is the key to consistently maximizing throughput. We also didn't talk about slack time between orders, fatigued employees, or other factors that add variance to the process.

We just covered the basics of simulation. Now, let's take a closer look at distributions. There are other tools that you can use for specific problems and you should get a brief introduction to them.

## Fitting distributions

Let's take a look at some other ways to fit distributions to data. We'll begin by building a helper function to give us a frequency table of values. 


```r
#-----------------------------------------------------------------
# Function to build a frequency table
#-----------------------------------------------------------------
f_build_freq_table <- function(variable){
  
  pr          <- as.data.frame(table(variable))
  pr$prob     <- pr$Freq/sum(pr$Freq)
  pr$variable <- as.numeric(as.character(pr$variable))  
  
  return(pr)

}
order_freq <- f_build_freq_table(wait_sample$orderTimes)
#sum(order_freq$prob)
```

We've already created this data set. Access it through the package.


```r
#-----------------------------------------------------------------
# Access frequency table data
#-----------------------------------------------------------------
freq_table  <- FOSBAAS::freq_table_data
```



```r
knitr::kable(head(freq_table),caption = 'Frequency table order time')
```



Table: (\#tab:mck)Frequency table order time

| variable| Freq|      prob|
|--------:|----:|---------:|
|        0|   45| 0.0214286|
|        1|   56| 0.0266667|
|        2|   55| 0.0261905|
|        3|   59| 0.0280952|
|        4|   51| 0.0242857|
|        5|   49| 0.0233333|
  

This frequency table represents a histogram. Let's take a look at the graph.


```r
freq_table$cumprob <- cumsum(freq_table$prob)
freq_table_graph <- 
  ggplot(freq_table,aes(x = variable,y=cumprob)) +
  geom_line(size = 1.2,color = 'dodgerblue')     +
  xlab('\n Seconds')                             + 
  ylab('Percent of Values')                      + 
  ggtitle('Table of values')                     +
  graphics_theme_1

```


```r
knitr::include_graphics('images/ch10_freq_table_graph.png')
```

<div class="figure">
<img src="images/ch10_freq_table_graph.png" alt="The ecdf" width="1750" />
<p class="caption">(\#fig:chtenfreqtablegraphz)The ecdf</p>
</div>



We have the cumulative distribution graph that we looked at earlier. This example should give you a good idea oh how the built-in function works. 

The following sections will cover fitting different models to data. There are libraries that will do much of this work for you if you are so inclined. However, it is important to understand a little bit about what is going on. Let's look at a few different potential fits for our data and begin with three common options:

- An exponential fit
- A polynomial fit
- A generalized additive model

We'll also attempt to fit a logit curve to demonstrate an important point.


```r
#-----------------------------------------------------------------
# Apply fits
#-----------------------------------------------------------------
library(mgcv)
freq_table$cumprob <- cumsum(freq_table$prob)
#-----------------------------------------------------------------
# Exponential fit
fit_ex <- 
  nls(variable ~ a*cumprob^m, data = freq_table, 
      start = list(a = 300,m=.15)) 
freq_table$pred_exp <- predict(fit_ex)
#-----------------------------------------------------------------
# Polynomial fit
fit_py <- 
  lm(freq_table$variable~poly(freq_table$cumprob,5,raw=TRUE))
freq_table$pred_poly <- predict(fit_py)
#-----------------------------------------------------------------
# GAM fit
fit_gm <- 
  mgcv::gam(variable ~ s(cumprob),data = freq_table)
freq_table$pred_gam <- predict(fit_gm)
```

Keep in mind that if you fit a polynomial with more than three degrees you are asking for trouble. I am doing it here to demonstrate how good it might look, but it is a bad idea. You are asking for an unpredictable model. Don't do it. 

To fit a logit curve we'll have to do something a little differently. We'll use the _SSlogis_ function from the _stats_ package to estimate starting points for our curve. This is a useful function, so keep it in mind.


```r
#-----------------------------------------------------------------
# Apply logit fit
#-----------------------------------------------------------------
fit_lt <- nls(variable ~ SSlogis(cumprob, Asym, xmid, scal), 
              freq_table)
cof    <- coef(summary(fit_lt))

fit <- nls(variable ~ A/(1 + exp(((-I+cumprob)/S))), 
           data = freq_table,  
           start = list(A = cof[1],I= cof[2],S = -cof[3]), 
           control = list(maxiter  =  10000), trace=TRUE)

```

We get an error. Why? Basically, a logit curve is a poor fit for this data set. This is a common problem. What do you do if you can't fit a common distribution very well? You have a few options. We included a fifth degree polynomial fit (a terrible practice), a generalized additive model, and we'll introduce one more. Let's fit a spline.  


```r
#-----------------------------------------------------------------
# Spline fit
#-----------------------------------------------------------------
fit_sp <- with(freq_table, smooth.spline(cumprob, variable))
freq_table$pred_sp <- predict(fit_sp)$y
```

Now that we have fit a few models, how can we judge which one is the best? You can start by looking at how well they fit the data. 


```r
#-----------------------------------------------------------------
# Observe fit data
#-----------------------------------------------------------------

dist_fits <- 
ggplot(freq_table,aes(y = cumprob,x = variable))            +
       geom_point(alpha = .5,size = 1)                      +
  geom_line(aes(x = pred_exp), size = 1.1 , lty = 2, 
            color = 'dodgerblue')      +
  geom_line(aes(x = pred_poly), size = 1.1, lty = 3, 
            color = 'mediumseagreen') + 
  geom_line(aes(x = pred_gam), size = 1.1, lty = 4, 
            color = 'coral')  +
  geom_line(aes(x = pred_sp), size = 1.1, lty =5, 
            color = 'orchid')  +
  ylab('\n Cumulative Probability')                          + 
  xlab('Order time in seconds')                              + 
  ggtitle('Distribution of order times')                     + 
  graphics_theme_1
```

<div class="figure">
<img src="images/ch10_dist_fits.png" alt="Variance between components" width="100%" />
<p class="caption">(\#fig:chtenfitsgraph)Variance between components</p>
</div>

Every model seems to fit the cumulative data pretty well with the exception of the exponential fit and polynomial fit. There are several ways to evaluate models against one another. For linear models, ANOVA is typically your first stop. for non linear models, AIC ^[https://en.wikipedia.org/wiki/Akaike_information_criterion] and BIC are typically used. 


```r
#-----------------------------------------------------------------
# Compare fits
#-----------------------------------------------------------------
models <- list(expon  = fit_ex,
               poly   = fit_py,
               gam    = fit_gm)

get_diagnostics <- function(mods){
  mods <- models
  aics   <- lapply(mods, function(x) AIC(x))
  bics   <- lapply(mods, function(x) BIC(x))  
  frame <- as.data.frame(matrix(nrow = length(mods), ncol = 3))
  frame[,1] <- names(mods)
  frame[,2] <- unlist(aics)
  frame[,3] <- unlist(bics)
  names(frame) <- c('model','AIC','BIC')
  return(frame)
 
}

models_table <- get_diagnostics(models)
```
  
Running _get_diagnostics_ creates the following table.


Table: (\#tab:anovaa)Model Comparisons

|model |      AIC|      BIC|
|:-----|--------:|--------:|
|expon | 1476.914| 1486.158|
|poly  | 1401.360| 1422.930|
|gam   | 1378.366| 1411.593|


The exponential line isn't the best fit. Plus, if you select random numbers for frequency and plug them into our equation the simulated distribution won't approximate our data very well. Let's simulate some results using our polynomial fit.

We can write a function that will spit-out a new value based on our polynomial model. Remember, don't use a fifth degree polynomial. This is just for demonstration. 


```r
#-----------------------------------------------------------------
# get fit
#-----------------------------------------------------------------
f_get_fifth_degree_fit <- function(new_var,dist_fit){
  var <-  coef(dist_fit)[1]              + 
         (coef(dist_fit)[2] * new_var    + 
         (coef(dist_fit)[3] * new_var^2) + 
         (coef(dist_fit)[4] * new_var^3) +
         (coef(dist_fit)[5] * new_var^4) + 
         (coef(dist_fit)[6] * new_var^5))
  return(var)
}
```

If we plug in our result from earlier we get:


```r
#-----------------------------------------------------------------
# Equation output
#-----------------------------------------------------------------
f_get_fifth_degree_fit(.7785714,fit_py)
#> (Intercept) 
#>    45.59297
```


This is pretty close to the 50 we got from the ecdf function. Let's simulate some values and graph them.


```r
#-----------------------------------------------------------------
# get fit
#-----------------------------------------------------------------
poly_fit <- 
sapply(seq(0,1,by=.005),
       function(x) f_get_fifth_degree_fit(x,fit_py))

poly_values <- tibble::tibble(y = seq(0,1,by=.005),
                              x = poly_fit)
poly_graph <- 
ggplot(poly_values,aes(x=x,y=y))             +
  geom_line(size = 1.5, lty = 3, 
  color = 'mediumseagreen')                  +
  ylab('\n Cumulative Probability')          + 
  xlab('Order time in seconds')              + 
  ggtitle('Simulated order times')           + 
  graphics_theme_1
```

Wow. Figure \@ref(fig:chtenfitsgraphb) demonstrates a horrible fit! This is one reason why you don't use high order polynomials for modeling. 

<div class="figure">
<img src="images/ch10_poly_graph.png" alt="Polynomial fit" width="100%" />
<p class="caption">(\#fig:chtenfitsgraphb)Polynomial fit</p>
</div>


We just covered the basics of fitting distributions. You now have the basic tools necessary to explain y in terms of x in a variety of ways. The main takeaway here is that you have to be careful about what you fit. Some methods will work better than others and if you aren't careful you can do some stupid things. 

## Understanding queuing systems {#queuing}

Queuing is a huge and complicated field of study and it's principles can be applied to any number of problems from Computer Engineering to queuing systems at amusement parks and airports. You will face them in sports. Queuing systems typically have three parts as described in "Operations Management" by Heizer and Rendee: [@Heizer2014]

- Arrivals or inputs into the system
- Queue discipline, or the waiting line itself
- The service facility

Each of these components have specific characteristics. For instance, arrivals will consider:

- The size of the arrival population
- The behavior of arrivals
- The pattern of arrivals

Analyzing queuing models tends to make heavy use of simulation and requires some specific forms of data collection. However, if you have your underlying assumptions correct, analyzing this data becomes an exercise in plugging good data into some equations. We'll adapt some examples from "Fundamentals of Queuing Systems" [@Thomopoulos2012]. 

Let's imagine a concessions concept with six points of sale and queuing space that can accommodate 50 people. In queuing parlance, this represents an (M/M/k/N) queue which represents a multi-server, finite capacity system. 1/lambda represents the _average time between arriving customers_ and 1/mu represents _the average service times_. We are assuming exponentially distributed inter-arrival times and service times. In reality, you'll have to make some observations to determine the distribution of service time and inter-arrival times. Let's begin by defining some terms and then we'll work through a problem using R. 


\noindent Average time between arrivals:
\begin{equation}
\tau_{a} = {1}/{\lambda}
\end{equation}

\noindent Average time to service a units:
\begin{equation}
\tau_{s} = {1}/{\mu}
\end{equation}

\noindent Average number of arrivals per unit of time:
\begin{equation}
\lambda 
\end{equation}

\noindent Average number of units processed in a unit of time for a continuously busy service facility:
\begin{equation}
\mu 
\end{equation}

\noindent Number of service facilities:
\begin{equation}
k 
\end{equation}

\noindent Utilization ratio:
\begin{equation}
\rho = \tau_{a}/\tau_{s} = \lambda/\mu \text{ : } \rho/k \text{< 1 is needed to ensure the system is in equilibrium}
\end{equation}

\noindent Number of units in the system:
\begin{equation}
n \text{ : n} \geq \text{0}
\end{equation}

We can easily translate these equations and figures into R. When you encounter Greek letters, my recommendation is to write them out. This sort of analysis can quickly get confusing. Let's carefully define our initial inputs.


```r
#-----------------------------------------------------------------
# Define terms for queuing equation
#-----------------------------------------------------------------
lambda                # Average arrivals per unit of time
mu                    # Average number of units processed 
k      <- 6           # Number of points of sale
N      <- 50          # Number that the queue can accommodate
tau_a  <- 1/lambda    # Average time between arrivals: 110 seconds
tau_s  <- 1/mu        # Average service time: 90 seconds
rho    <- tau_a/tau_s # Utilization ratio
n                     # Units in the system
```

Let's imagine a concession concept with six points of sale and space for 50 people in line. It takes about 60 seconds to service a customer and a customer arrives in line every 110 seconds. Let's define these inputs in R.


```r
#-----------------------------------------------------------------
# M/M/k/N Queue Inputs
#-----------------------------------------------------------------
k        = 2          # Number of points of sale at concept
N        = 5          # Number of people the queue can accommodate
tau_a    = 10         # time between arrivals: 40 seconds/60
tau_s    = 8          # Service time: 90 seconds/60 = 1.5
lambda   = 1/tau_a    # Customer Arrivals per minute
mu       = 1/tau_s    # Serviced customers per minute
#-----------------------------------------------------------------
# Translate to per hour figures
#-----------------------------------------------------------------
lambda_h = 60/tau_a   # Per hour
mu_h     = 60/tau_s   # Per hour
rho      = lambda/mu  # Utilization ratio
```

R has several tricks that you can use to make calculations easier. Since variables are vectorized, adding sequences is really easy. You will not need a loop. The first thing we will need to do is to calculate the probability that n (defined above) equals 0. This is given by the slightly alarming-looking equation:

\noindent Probability that n = 0:
\begin{equation}
P_{0} = 1/\{\sum_{n=0}^{k-1} \rho^n/n! + \rho^k/k![(k^{N-k+1} - \rho^{N-k+1})/(k - \rho)k^{N-k}]\}
\end{equation}

Pay attention to order of operations. The only difficult part of translating this equation is getting the parenthesis in the correct places. 


```r
#-----------------------------------------------------------------
# M/M/k/N Calculating the Probability that n = 0
#-----------------------------------------------------------------
# Create the sequence for the P0 equation
n   = seq(0, N-1, by = 1 )
# Translate the equation into R:
P0 <- 
 1/ sum(((rho^n)/factorial(n)) + ((rho^k)/
(factorial(k)*((k^(N-k+1)) - (rho^(N-k+1))/((k-rho)*(k^(N-k)))))))
```

After running this code, we can see that P0 = 0.4305395. We complete this exercise by calculating the probability of n units in the system with two equations for different levels of n. 

\noindent For n = (0,k)
\begin{equation}
P_{n} = \rho_{n}/n!P_0
\end{equation}

\noindent For n = (k + 1,N)
\begin{equation}
P_{n} = \rho_{n}/[k!k^{n-k}]P_{0}
\end{equation}


```r
#-----------------------------------------------------------------
# M/M/k/N  Probability of n units in the system
#-----------------------------------------------------------------
# For n = (0,k)
nk0 = seq(0, k, by = 1 )
Pnk0 <- rho^nk0/factorial(nk0)*P0

sum(Pnk0)

# For n = (k + 1,N)
nk1 = seq(k + 1, N, by = 1 )
Pnk1 <- rho^nk1/(factorial(k)*k^(nk1-k))*P0

sum(Pnk1)

round(sum(Pnk0,Pnk1),2)
```

We can write a helper function to help us reconcile these two options.


```r
#-----------------------------------------------------------------
# Calculate figures
#-----------------------------------------------------------------
lambda_e <- lambda*(1 - Pnk1) # Lambda Effective
rho_e    <- lambda_e/mu       # rho Effective
# Expected in queue
Lq = sum((n-k)*Pnk0)
Lq = sum((n-k)*Pnk1)
Ls = rho_e
# expected units in the system
L = Ls + Lq
# Expected service time
Ws = Ls/lambda_e # minutes in service
Wq = Lq/lambda_e # minutes in queue
W = L/lambda_e   # minutes in system
```

The following function accepts our inputs and spits out our desired output.


```r

#-----------------------------------------------------------------
# Calculate figures
#-----------------------------------------------------------------
f_get_MMKN <- function(k,N,ta,ts){
  
  lambda = 1/ta #: per minute
  mu     = 1/ts #: per minute
  rho    = lambda/mu #: utilization ratio
  
#-----------------------------------------------------------------
  # Probability of n units in the system
  # for
  n = seq(0, N-1, by = 1 )
  P0 <- 1/ sum(((rho^n)/factorial(n)) + 
               ((rho^k)/(factorial(k)*((k^(N-k+1)) - 
                   (rho^(N-k+1))/((k-rho)*(k^(N-k)))))))
  
  # Probability of n units in the system
  # for
  n = seq(0, k, by = 1 )
  Pn0 <- rho^n/factorial(n)*P0
  
  # for
  n = seq(k + 1, N, by = 1 )
  Pn1 <- rho^n/(factorial(k)*k^(n-k))*P0
  
  Pn      <- c(Pn0,Pn1)
  
#-------------------------------------------------------------------
  # calculations
  len     <- max(length(Pn))

  lambda_e  <- lambda*(1 - Pn[len])
  rho_e    <- lambda_e/mu
  
  # Expected in queue
  Ls = rho_e #   Ls = 1*Pn[2] + 2*sum(Pn[-c(1,2)])
  
  # for
  n = seq(k+2, N + 1, by = 1 )
  Lq = sum((n-(k+1))*Pn[n]) # Lq = 1*Pn[4] + 2*Pn[5] + 3*Pn[6]

  # expected units in the system
  L = Ls + Lq
  
  # Expected service time
  Ws = Ls/lambda_e # minutes in service
  Wq = Lq/lambda_e # minutes in queue
  W  = Wq + Ws   # minutes in system
  
#-------------------------------------------------------------------
  # Build output
  frame <- data.frame(matrix(nrow = 7,ncol =2))
  names(frame) <- c('Metric','Value')
  
  metric <- c('Servers:','System Capacity:','Time between arrivals:',
              'Average service time:','Minutes in service:',
              'Minutes in queue:','Minutes in system:')
  values <- c(k,N,ta,ts,Ws,Wq,W)
  
  frame[,1] <- metric
  frame[,2] <- values

  return(frame)
  
}

```

Executing this function returns a dataframe representing a list of values.


```r
#-----------------------------------------------------------------
# Run our function
#-----------------------------------------------------------------
FOSBAAS::f_get_MMKN(2,5,10,8)

```


Table: (\#tab:runwaittimesuncfeval)f_get_MMKN output

Metric                        Value
-----------------------  ----------
Servers:                   2.000000
System Capacity:           5.000000
Time between arrivals:    10.000000
Average service time:      8.000000
Minutes in service:        8.000000
Minutes in queue:          1.267664
Minutes in system:         9.267664

We now have a basic understanding of how to analyze queues. This stuff can get complex and there are a multitude of software packages that can take care of this for you. However, if you are simply plugging information into equations, the difficult part is just getting good data and choosing the correct models that accommodate it. There is lots of variation, for instance inter-arrival times may be normally distributed instead of exponentially distributed. You'll have to adapt your model to accommodate this variation. 

## Key concepts and chapter summary

Analytic techniques can be applied to a wide variety operations problems. Additionally, _Operations_ is a broad field of study that covers many different arenas. This chapter covered two major subjects: Simulation and Queuing. Both examples covered increasing throughput for concessions. While we only scratched the surface, we were introduced to a number of topics:

- Simulation: Monte Carlo simulations are relatively simple to create and are incredibly useful for evaluating a very wide variety of topics. 
- Distribution fitting: Leveraging distributions is critical to simulation. Learn to think in distributions, not point estimates. Distributions are everywhere. 
- Queuing analysis: Queues exist everywhere from electrical circuits to concession stands. Analyzing a queuing system can give you insight into how to improve it.
- Some basic project management tips: Project and change management skills are critical to operations work.

We also learned how to think about these problems. It is easy to be intellectually lazy and not take the time to truly evaluate these sorts of problems. Operations is about critical thinking in terms of a system with many interrelated components. It is also a widely studied field, so if you can conceptualize a problem correctly, you should be able to find a way to analyze and improve it.   

















