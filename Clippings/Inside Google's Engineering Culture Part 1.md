---
title: "Inside Google's Engineering Culture: Part 1"
source: "https://newsletter.pragmaticengineer.com/p/google"
author:
  - "[[Gergely Orosz]]"
published: 2025-09-09
created: 2025-10-02
description: "A broad and deep dive in how Google works, from the perspective of SWEs and eng managers. What makes Google special from an engineering point of view, engineering roles, compensation, and more"
tags:
  - "clippings"
---
### A broad and deep dive in how Google works, from the perspective of SWEs and eng managers. What makes Google special from an engineering point of view, engineering roles, compensation, and more

Today, the tech giant Google reaches more people with its products than any other business in the world across all industries, via the likes of Google Search, Android, Chrome, Gmail, and more. It also operates the world’s most-visited website, and the second most-visited one, too: YouTube. Founded in 1998, Google generated the single largest profit ($115B after all costs and taxes) of all companies globally, last year.

Aside from its size, Google is known for its engineering-first culture, and for having a high recruitment bar for software engineers who, in return, get a lot of autonomy and enjoy good terms and conditions. Employees are known as “Googlers,” and new joiners – “Nooglers” – get fun swag when they start. An atmosphere of playful intellectual curiosity is encouraged in the workplace, referred to internally as “Googleyness” – more on which, later. This culture is a major differentiator from other Big Tech workplaces.

But what is it really like to work at Google? What’s the culture like, how are things organized, how do teams get things done – and how different is Google from any other massive tech business, truly?

**This article is a** ***“things I wish I’d known about Google before joining as an SWE / engineering manager”.***It’s for anyone who wants to work at Google, and is also a way to learn, understand, and perhaps get inspired by approaches that work for one of the world’s leading companies.

This mini-series of articles focusing on Google contains more information about more aspects of its engineering culture than has been published in one place before, I believe. We’ve spent close to 12 months researching it, including having conversations with 25 current and former engineering leaders and software engineers at Google; the majority of whom are at Staff (L6) level or above.

Of course, it’s impossible to capture every detail of a place with more than 60,000 software engineers, and whose product areas (Google’s version of orgs) and teams work in different ways. Google gives a lot of freedom to engineers and teams to decide how they operate, and while we cannot cover all that variety, we aim to provide a practical, helpful overview.

In part 1 of this mini-series, we cover:

1. **Overview**. Google generates more revenue than Microsoft and Meta, and is the Big Tech giant that likely employs the most software engineers across 25+ engineering offices. The mission statement is to “organize the world's information and make it universally accessible and useful.”
2. **What makes Google special?** Behind the variety of approaches to work is a universal engineering culture for tools and practices. Google has a unique, custom engineering stack, and has built systems differently from competitors since day one, making it a “tech island”. Google has historically been more open than other Big Tech companies about its inner workings. With 120+ active products, it is most similar to Microsoft in the breadth of work it does, and in the opportunities there are for software engineers to work on different things.
3. **Levels and roles.** There’s a dual-track career ladder between levels L2 and L11, and a Tech Lead Manager (TLM) role as a “third career path”. Google’s leveling process during interviews is the strictest in the industry, and “tech lead” is a role, not a level. Other engineering roles include SRE, EngProd, Research Scientist, DevRel, and UXE. Other roles that interact with engineering include Product Managers, Program Managers, [TPMs](https://newsletter.pragmaticengineer.com/p/what-tpms-do), designers, and tech writers.
4. **Compensation.** Google pays at the top of regional markets, and is known for its standout compensation which includes base pay, equity, cash bonus, and sometimes a signing-on bonus. Examples of this top-of-market pay:
	- Mid-level engineer (L4) usually pays in the range of:
		- $250-350K in total compensation in the US
		- Other regions: £125-185K in the UK, €140-180K in Germany, CHF 210-260K in Switzerland, CA$210-280K in Canada, A$200-280K in Australia, zł380-450K in Poland, and ₹65-88 lakh in India
	- Staff software engineer (L6) usually pays in the range of:
		- $550-700K in total compensation in the US
		- Other regions: £270-380K in the UK, €250-330K in Germany, CHF 370-500K in Switzerland, CA$420-650K in Canada, A$350-550K in Australia, zł750-850K in Poland, and ₹1.5-2.2 crore in India
	- We cover entry-level (L3), senior (L5), senior staff (L7) packages, and also Google-specific bonuses like peer bonuses, spot bonuses, and award programmes.
	- Google is one of few companies to offer a financially rewarding career path for engineers which doesn’t push them into management
5. **Hiring.** Google has a notoriously difficult interview process which is copied by many other tech companies. Data structures and algorithms interviews, system design, “Googleyness”, and leadership interviews are also features of recruitment, and some teams use domain deepdives and takehomes. Final recruitment decisions are made by a Hiring Committee, but that’s still not the end of the process – successful candidates then go through “team matching”.

This article is around twice as long as most deepdives; there are just so many details worth sharing about Google!

For similar deepdives, see **[Inside Meta’s engineering culture](https://newsletter.pragmaticengineer.com/p/facebook)**, **[Inside Amazon’s engineering culture](https://newsletter.pragmaticengineer.com/p/amazon)**, and [other engineering culture deepdives](https://newsletter.pragmaticengineer.com/t/engineering-culture-deepdive) — including that of OpenAI, Stripe and Figma.

*Programming note: this week, an episode of The Pragmatic Engineer Podcast will be released tomorrow (Wednesday), and there will be no edition of The Pulse.*

## 1\. Overview

Let’s begin with a quick rundown of the numbers that give Google the most users and customers of any business, globally:

- #1 and #2 most-visited websites: Google.com is the [most popular website](https://www.similarweb.com/top-websites/) in the world, and YouTube is #2. Google.com gets [85 billion monthly visits](https://www.reddit.com/r/AINewsMinute/comments/1kn1n9t/google_still_dominates_the_internet_81_billion/) – more than the next 9 most-visited websites, *combined*
- Android: around [4.2 billion](https://sqmagazine.co.uk/android-statistics/) users (circa 75% of global smartphone market share)
- Chrome: circa [3.45 billion](https://www.aboutchromebooks.com/google-chrome-statistics/) users (around 65% of global browser market share)
- Gmail: approximately [1.8 billion](https://emailsorters.com/blog/gmail-statistics/) active users

In 2015 when Google renamed itself “Alphabet”, the motivation was to separate the core web search business that earned the lion’s share of revenue from loss-making, “moonshot” ventures like Waymo, Google DeepMind, Google Fiber, etc. In practice, almost all revenue generated by Alphabet comes from the Google organizational unit, and not much has changed since. This article uses the name “Google” when referencing Alphabet.

### Incredibly profitable & ads-heavy

In absolute terms, Google is currently the most profitable company in the world; it generated $115 billion in profit (net income) over the past 12 months on $371 billion in revenue. For comparison, here are other Big Tech companies’ net incomes during the period:

- Microsoft: $101 billion (from $281 billion in revenue)
- Apple: $99 billion ($408 billion revenue)
- Meta: $71 billion ($178 billion revenue)
- Amazon: $70 billion ( $670 billion revenue)

At its core, Google is still an advertising company; around 75% of revenue comes from selling ads on Google Search, YouTube, and the Google Ads network. However, the business has several services that don’t rely on ads for revenue:

- **Google Cloud:** the #3 cloud provider behind AWS and Azure generates more than $50 billion in annual revenue (around 13% of total revenue). *Google Workspace income is included in this number.*
- **Hardware plus subscriptions**: Pixel smartphones, Nest smart home gadgets, Fitbit wearables, YouTube Premium, and Google One subscriptions. Google makes more than $40 billion per year from these (circa 10% of revenue)

Google has several loss-making businesses that might one day turn a profit, such as:

- **Gemini and AI:** Google is a leader in AI with its Gemini models that are integrated in several products like web search. It is both a free and paid product, and is likely loss-making at present.
- **Waymo**: the leader in self-driving vehicles, now serving more than 1 million rides per month in San Francisco and Phoenix, in the US.
- **Google Fiber**: ultra-fast fiber-optic provider with data speeds from 1 Gbps to 8 Gbps. It operates in 25 cities across 19 US states, including Austin (Texas), Atlanta (Georgia), Chicago (Illinois), Miami (Florida), Denver (Colorado), and San Diego (California).

![](https://substackcdn.com/image/fetch/$s_!XUp3!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F37d535f4-b7e5-4e75-8936-80e3baf1305e_1436x970.png)

Google’s revenue breakdown for 2024

### Global offices

Google employs 183,000 people worldwide and hit peak headcount in 2022, with 190,000 workers. In 2023, there were mass layoffs and headcount has since stopped rising:

![](https://substackcdn.com/image/fetch/$s_!EqPQ!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fde80a8c6-2754-431b-ab28-929837e869f1_1172x872.png)

Google no longer growing as fast as until 2022

As mentioned above, Google employs around 60,000 software engineers, which we can deduce because in 2020 this number was 50,000, [as shared](https://abseil.io/resources/swe-book/html/ch16.html) in the book *“Software Engineering at Google,”* – around 35% of all staff. Headcount growth since that time suggests that 60K engineers work there today. This makes Google one of the largest employers of software engineers; Amazon employs nearly [35,000](https://newsletter.pragmaticengineer.com/p/amazon) developers, and Meta [around 32,000](https://newsletter.pragmaticengineer.com/p/facebook) software engineers. We’re confident Google has the highest “software engineering ratio” among the Big Tech giants.

**Google runs more than 25 engineering offices.** The biggest:

- **US:** Mountain View (corporate headquarters) and the surrounding Bay Area, San Francisco, New York, and Seattle (Kirkland), plus several smaller ones in places like Cambridge (MA), Los Angeles (CA), San Diego (CA), Pittsburgh (PA), Raleigh and Durham (NC).
- **Canada: Toronto, Montreal, Waterloo, and Kitchener**
- **Europe:** Zurich (Switzerland), London (UK), Dublin (Ireland), Munich (Germany), and Paris (France) are the largest. Smaller offices include Hamburg (Germany), Milan (Italy), Amsterdam (Netherlands), Madrid (Spain), Stockholm (Sweden), Copenhagen and Aarhus (Denmark), Helsinki (Finland), Warsaw and Krakow (Poland), Prague (Czechia), Vilnius (Lithuania), Bucharest (Romania), and Budapest (Hungary).
- **India:** Bangalore and Hyderabad are the largest offices.
- **South America**: Mexico City (Mexico), Sāo Paulo and Belo Horizonte (Brazil)
- **Middle East, Asia and Australia:** Tel Aviv (Israel), Tokyo (Japan), Sydney (Australia), New Taipei City (Taiwan)

Google has [more than 70 offices](https://about.google/company-info/locations/) across 50+ countries. *The total number of offices is higher than engineering offices, because many of Google’s offices have no software engineering teams in those locations, but are for non-technical teams like Sales, Marketing, Consulting (e.g. for Google Cloud), and other functions.*

Although not typical, Google can hire engineers to work from mainly non-engineering offices as “singletons”. A current Google engineer told us:

> “Singletons are not particularly common, but rather exceptions on an individual basis. Some are left-overs from a brief period of remote hiring during the pandemic, some are specialists or very senior ICs who have a bit more leverage in negotiations and choice of where they work.”

“Singletons” can also work in engineering offices: in that case, they would be the lone engineer working for their team in that location, everyone else on their team being in other locations. Singletons are not common at Google, but our research suggests there are many more of them than at other Big Tech companies and larger scaleups.

### History, mission, values

As is well known by now, Google was founded by PhD students Larry Page and Sergey Brin, who devised a more efficient search engine algorithm called [PageRank](https://en.wikipedia.org/wiki/PageRank). Using PageRank for searching the web resulted in much-improved results than the most popular rival search engines of the time, such as Yahoo!, AltaVista, Lycos, and Ask Jeeves. Some of these were portals which “featured” sites to visit (like AltaVista), and others were rudimentary search engines that gave up to 15 not-particularly-accurate results.

![](https://substackcdn.com/image/fetch/$s_!UiaY!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2ffd4e5c-708e-4fa9-a8b1-3cd6b3b4916a_1356x1422.png)

Leading search engines in the year 2000. Google resisted the popular “featured sites” design of the era

The rest, as they say, is history: two years after launching, Google became the dominant search engine and also a verb (“let me Google this.”) It gave more and better search results, and had a much cleaner interface than its rivals.

The company’s mission has changed over time:

- **“Organize the world's information and make it universally accessible and useful”.** This was the founding mission in 1998 and hasn’t changed.
- **“Don’t be evil”.** An unofficial motto which was part of Google’s code of conduct [from around](https://en.wikipedia.org/wiki/Don%27t_be_evil) 2000, to remind staff to act ethically. It remained until 2015, when Google became Alphabet.
- **“Do the right thing”.** The motto for the company [since 2015](https://www.engadget.com/2015-10-02-alphabet-do-the-right-thing.html), which replaced “don’t be evil”.

Google also has [five core values](https://about.google/company-info/commitments/):

- Protecting users
- Building and deploying AI responsibly
- Expanding opportunity
- Helping solve society’s challenges
- Building for everyone

Current Googlers report that these values are not particularly emphasized during day-to-day work, and that they feel pretty abstract and “corporate”. This light-touch approach is different from competitors like online retailer Amazon, whose [16 leadership principles](https://newsletter.pragmaticengineer.com/i/49561596/amazons-leadership-principles) might as well be chiselled in stone on the walls.

**“Googleyness” is something most workers at the company share.** It’s a trait Google focuses on during its hiring process as something all employees should possess. The term is vague, but adds up to being smart, adaptable, and a team player who’s nice to be around. We cover Googleyness more in the “Hiring” section.

![](https://substackcdn.com/image/fetch/$s_!WJFO!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2fc9ef5b-a19a-43f5-9fa5-135e644aeb2a_1280x720.png)

Playful and ambitious: Googleyness begins with the famous “Noogler” hat. Source: former Google engineer, Mohammad Fraz (a “Xoogler”) from his video ‘ Google joining kit ’

There are plenty of publicly observable instances of “Googleyness” in Google’s own products, which show just how engineering-driven its culture is. For example, try searching “recursion” on Google:

![](https://substackcdn.com/image/fetch/$s_!BFio!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7c38a067-89ab-4a72-be5a-f15584b4b529_1506x386.png)

Recursion is a tricky concept to explain to non-engineers. Instead of explaining, Google simply showcases the concept in Google Search by displaying “Did you mean: recursion?” Click on this link and it brings you back to the same page… recursion!

## 2\. What makes Google special?

From talking with 25 current and former Googlers, here’s what makes it distinct from other Big Tech companies.

### No “single” Google

Google is divided into Product Areas which operate like standalone companies. These are often called “PAs” or “orgs” internally. The main PAs:

- **Knowledge and Information**: includes Google Search, internal platforms, and core services
- **YouTube**: everything related to the video-sharing arm
- **Cloud: G** oogle Cloud Platform and Workspace
- **Ads and Monetization:** products like Google Ads, AdSense, and AdMob
- **Platforms and Devices:** software platforms like Android, Chrome, Chrome OS, and hardware like Pixel, Nest, Fitbit, Chromecast, Google TV, and Google Home devices

Orgs have their own goals, priorities, metrics, and planning cadences. And within each org, teams have a lot of independence to decide their way of working. An engineer’s experience in one team in an org can be very different from another engineer’s in a different team in another org! Here’s how one current Google engineer explained it to us:

> “Your experience is heavily dependent on your team. If you work on a mature product, you will be met with a lot of process. If you work in a more zero-to-one project, there is more code to be written.”

A tech lead confirmed that priorities differ by PA:

> “Priorities between PAs differ drastically. In all fairness, they are also different between subteams in the same PA. Google is very into peer-to-peer negotiation to get things done, as opposed to top-down priorities. Personally, I find the amount of negotiation to be a little inefficient and exhausting, and would not say no to more top-down direction!”

### One engineering culture

Even though product areas and teams work independently, the engineering culture seems pretty universal, judging by the engineers we’ve talked to.

**Practices, tooling, and tech stacks are very similar.** Whether someone works in YouTube, Ads and Commerce, or another product area, they use the same internal tools, the same processes for things like code review, testing, and documentation, and also the same monorepo and continuous integration processes – except for a few open source projects like Android and Chromium.

That most of Google’s 60,000 engineers use almost identical tooling means it is little effort to move teams, which helps make internal moves easy, as it involves a lot less change to processes and tooling, meaning a lower cognitive load that makes onboarding faster, overall.

**Politics and culture vary between PAs and teams.** It would be impossible for the culture to be identical in thousands of engineering teams, split across dozens of locations. Here are the big differences, according to engineers:

- **Politics**. How do you influence decision makers in your org to prioritize things that matter to your team? Doing so requires being good at the subtle art of influencing, knowing the most influential people, and making them your allies. This is a tricky business at any mid-sized or larger company. *We previously covered [internal politics for software engineers and managers](https://newsletter.pragmaticengineer.com/p/internal-politics-part-1).*
- **Culture and perf.** Google says there’s “one engineering culture,” but engineers told us that different orgs prioritize different things; some value quality more, others focus on innovation, and others prioritize shipping fast. Performance evaluation is known as GRAD (Google Reviews and Development) and is org-specific, meaning expectations for each level differ slightly across orgs. *We will cover this topic in part two of this mini-series.*

### Unique engineering stack

Google’s engineering org exists in a different world from that which other tech companies operate in. This comes down to one thing: scale.

Google had to build systems at the scale of serving hundreds of millions of users a decade before any other company in the world reached a similar scale. This meant it innovated unique systems and solutions to massive scaling challenges, and that publicly-available tools were shipped outside Google only a decade or so later.

Whatever tools or vendors your current company uses to deal with scale, it’s likely that Google built its own versions 10 or more years earlier:

- **Borg** (manage containers at scale): predates container orchestration platform, Kubernetes
- **Borgmon/Monarch** (observability at scale): predates observability solution, Datadog
- **Codesearch** (code searching in massive codebases): predates code search vendor, Sourcegraph
- **Piper** (source control at Google scale): predates source control leader, GitHub

Google occupies an unusual position where it makes no sense to adopt industry-standard tools like GitHub and Kubernetes because its existing stack is so well integrated. A current Google engineer explained why it rarely uses external services or tools, even if they can handle Google’s scale:

> “Google makes everything work so *well*. Since the entire tech stack is in-house, every system has built-in transparent integration with the in-house corporate authn/z system, and also with the ‘magical billing’ system.
> 
> External products always have to:
> 
> 1. Provide auth abstractions
> 2. Provide billing abstractions
> 
> These two constraints make adopting new tools *really* friggin' hard!”

### Building systems differently since day one

Engineering at Google has been different from the rest of the world since it was founded.From its beginnings in 1998, the company bet big on speed and reliability being differentiators for all its products. They expected the web search tool to deal with planet-scale load, and the same for subsequent products like Gmail that launched with 1GB of free storage in 2004. This was unheard of at a time when storage was much more expensive. The assumption was that these products needed to be able to handle billions of users.

To achieve this scale, Google simply had to build a custom tech stack from the start, as there were no commercially-available tech stacks around to handle planet-scale load. Back in the late ‘90s, the conventional wisdom was to vertically scale machines; that is, buy the biggest possible server (called a mainframe), and try to make an application run on a single server. Sun was one of the biggest mainframe vendors of the time, and most companies invested heavily in expensive, high-performance hardware.

Google took a different route by choosing to buy cheap, commodity hardware, and to build data center clusters that made use of tens of thousands of relatively cheap machines to handle loads that not even the largest mainframes in the world could soak up.

Here’s how Google’s search cluster worked in 2003, from t [he Google whitepaper](https://static.googleusercontent.com/media/research.google.com/en//archive/googlecluster-ieee.pdf) describing the Google cluster architecture:

> “To provide sufficient capacity to handle query traffic, our service consists of multiple clusters distributed worldwide.
> 
> Each cluster has around a few thousand machines, and the geographically distributed setup protects us against catastrophic data center failures (like those arising from earthquakes and large-scale power failures).
> 
> A DNS-based load-balancing system selects a cluster by accounting for the user’s geographic proximity to each physical cluster. The load-balancing system minimizes round-trip time for the user’s request, while also considering the available capacity at the various clusters”.

Back then, this kind of approach was revolutionary, and no other company published so much detail about its custom data center setup. Google kept publishing details on how it organized and operated clusters, such as this writeup in the “ *[Site Reliability Engineering at Google](https://sre.google/sre-book/table-of-contents/) ”* book:

“The topology of a Google data center:

- Tens of machines are placed in a rack.
- Racks stand in a row.
- One or more rows form a cluster.
- Usually a datacenter building houses multiple clusters.
- Multiple datacenter buildings that are located close together form a campus”.

![](https://substackcdn.com/image/fetch/$s_!uslE!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa9f76bd3-9414-480b-bc12-b8feed95d553_900x488.png)

Google datacenter campus topology. Source: Site Reliability Engineering at Google

### Unusual openness

Compared to every other Big Tech company, Google has been very open and transparent about how it works externally and internally. *Note, this openness seems to have reduced since around 2020.*

Internally, *basically* *everything* used to be available to all workers: planning docs, strategies, code, documentation, et-al. This company-wide access changed to Product Area-wide access following leaks in 2020. A former Google Cloud engineer told us:

> “The ‘default open’ policy started to change around 2019-2020. This was when GCP got involved with more potentially controversial topics, and confidential documents were leaked to the press more often.
> 
> The default share setting for internal Google Docs used to be company-wide visibility. From around 2019-2020, the default visibility is PA-level visibility, meaning you can only search documents in your PA, not from across Google.”

Externally, Google has published [more than 10,000 papers](https://research.google/pubs/) with details about how the company works and how products are built. No other business has published more about its inner workings.

Famously, in 2017 Google published a paper titled [Attention is All You Need](https://research.google/pubs/attention-is-all-you-need/), describing a novel network architecture called “transformers.” This paper was the foundation for Large Language Models (LLMs) and this idea is at the core of ChatGPT and other LLMs. By publishing this paper instead of holding on to its breakthrough, Google may have brought forward the AI boom by a few years!

### Tech island

Everything about software engineering is unique at Google. New joiners can throw out their knowledge of how to use source control, how to run CI/CD, and how to manage infrastructure. Google has different, unique systems for everything related to building, deploying, and maintaining software, and all of it has to be learnt.

The term “tech island” was coined by Urs Hölzle, Google employee #8, in an internal document nearly a decade ago. As a former Googler told us:

> “The “tech island” term was first used by Urs Hölzle years back in his doc about how Google’s unique tech stack (aka “living on its own tech island”) could be a problem in the longer term. In his doc, he argued we should seek ways to get closer to the ‘tech mainland,’ rather than continue existing on our own island.
> 
> Early in the 2000s, doing things the ‘Google way’ was an advantage. But as the industry catches up, with all the advancements in open source, this ‘tech island’ nature started to hurt productivity. For example, Google now has a sharper learning curve for new hires compared to companies that use ‘industry standard’ tech stacks.”

The debate on whether Google should continue as a tech island or get closer to the mainland is controversial, a current engineer at Google told us:

> “The idea of moving to a more standardized tech stack itself is somewhat controversial inside Google. Some longtime Googlers I’ve talked to have gotten so used to the internal tech that they strongly believe it’s supreme. Of course, there are believers at the other extreme, who attempted to go full steam to get Google on GCP, as GCP’s services are public-facing and not specific to Google and thus are the ‘mainland.’ However, efforts to move over failed miserably.
> 
> **A more dominant viewpoint these days is that Google should take a hybrid approach**: use GCP and converge with open source when it makes sense. This is opposed to a “lift and shift” approach of moving everything over to a more standard stack. The hybrid approach acknowledges that certain Google services would never work without internal tech.”

### Doing many things

Compared to the likes of Meta and Amazon, Google builds a plethora of products, platforms, and technologies:

- **Search engine**: the main product
- **Operating systems**: Android and ChromeOS
- **Browser**: Chrome
- **Hardware**: Pixel devices and ChromeOS notebooks
- **Cloud provider**: Google Cloud
- **Enterprise tools**: Google Docs and Google Meet
- **Content platform**: YouTube
- **Music streaming service: YouTube Music**
- **Developer tools**: Flutter, Firebase
- **Programming languages and open source**: Go, Kubernetes, Angular, PyTorch, and others

The Big Tech company closest to Google in sheer breadth of products is probably Microsoft. The Windows maker also has a search engine (Bing), operating system (Windows), browser (Edge), hardware (Surface), cloud provider (Azure), enterprise tools (Office 365, Microsoft Teams), social networks (LinkedIn, GitHub), developer tools (VS Code), and programming languages / open source (TypeScript,.NET and others).

Being an engineer at Google means potentially working with anything from docs, to video transcoding, to mobile apps, or infrastructure. If a new challenge is sought, workers can switch teams to a completely different area:

![](https://substackcdn.com/image/fetch/$s_!4d-s!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fba0338d5-116e-419a-a70a-456acf4186ef_1600x1157.png)

Google has more than 120 actively developed products

## 3\. Levels and roles

Google has a dual-track career ladder for software engineers and engineering managers – plus an interesting role called Tech Lead Manager (TLM). Each level typically pays very similarly in total compensation (we cover more on compensation in the next section).

This means that as an individual contributor, it’s possible to earn similarly to managers and directors without needing to manage engineers. At L5 and L6, engineers who take on tech lead responsibilities often have the opportunity to join the manager career ladder. Those who want to lead small teams but not become managers can be TLMs. Here’s how levels look on these parallel tracks:

![](https://substackcdn.com/image/fetch/$s_!RdLf!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1a36263f-aa9a-4901-a68b-2a94fc9b3005_1094x694.png)

Google’s engineering levels on the IC, manager, and TLM ladders

*We published a deepdive covering similarities and differences across the IC, manager, and TLM roles in [Engineering career paths at Big Tech and scaleups](https://newsletter.pragmaticengineer.com/p/engineering-career-paths).*

### Software engineering career track

The SWE career ladder is pretty alike other Big Tech companies and scaleups, partly because many places create their engineering career ladders by using Google’s as a model.

**Google’s leveling during interviews is the strictest in tech.** It’s common for new engineers to be [downleveled](https://newsletter.pragmaticengineer.com/p/the-seniority-rollercoaster) when they arrive: for example, a Senior Engineer at Amazon might get an L4 (SWE III) role, or a Staff Engineer at a scaleup might be offered an L5 (Senior SWE) role at Google. This is usually for two reasons:

- Google’s Hiring Committee makes hiring and leveling decisions, and downleveling is far more common. The company would rather hire someone with room to grow than hire them at a level they’ll struggle with.
- Google pays top of the market. Even when downleveling, an offer from Google often means a pay rise. If there’s an offer with higher pay for a position from which it should be easier to get promoted to the next level, then why not accept?

*We cover more on downleveling and upleveling in the issue [The seniority rollercoaster](https://newsletter.pragmaticengineer.com/p/the-seniority-rollercoaster).*

**“Tech Lead” is a role, not a level.** Tech Leads are responsible for the technical aspects of projects, like owning the architecture, driving tech decisions, prioritising work, and taking on project management. They are chosen by the engineering manager of each project and don’t do any type of people management.

The matter of levels is usually less about a manager assigning a tech lead role than it is about a project’s scope. Even an L3 engineer can be assigned to lead a simple project, especially as doing so will make a good case for promotion to L4. Engineers get a lot of autonomy, so taking the lead on an initiative and becoming the “de facto tech lead” is also common. *We cover more on this topic in [Software engineers leading projects.](https://newsletter.pragmaticengineer.com/p/engineers-leading-projects)*

**The position of Google Fellow is very hard to achieve.** There are probably no more than 20 Google Fellows currently at the company among 60,000 engineers; fewer than 0.1% of all Google engineers are at this level. In some ways, this is logical: it becomes exponentially harder to get to the next level after L6 (Staff) level, so it follows that there are far fewer L7s than L6s, and even fewer L8s than L7s, etc.

Notable Google Fellows include [Urs Hölzle](https://en.wikipedia.org/wiki/Urs_H%C3%B6lzle) (engineer #8 and Google’s first VP of Engineering), [Amit Singhal](https://en.wikipedia.org/wiki/Amit_Singhal) (headed up Google Search for 15 years), and [Blaise Agüera y Arcas](https://en.wikipedia.org/wiki/Blaise_Ag%C3%BCera_y_Arcas) (CTO of Technology & Society).

There are only two Senior Fellows at Google (at L11 level): [Sanjay Ghemawat](https://en.wikipedia.org/wiki/Sanjay_Ghemawat) and [Jeff Dean](https://en.wikipedia.org/wiki/Jeff_Dean). The pair made massive contributions to making Google’s infrastructure scalable and resilient, including writing [MapReduce](https://en.wikipedia.org/wiki/MapReduce). The New Yorker covers their story in “ [The Friendship that made Google Huge](https://www.newyorker.com/magazine/2018/12/10/the-friendship-that-made-google-huge) ”.

### Tech Lead Manager role

The Tech Lead Manager role originated at Google before other companies like Uber adopted a similar position. It’s a blend of individual contributor and manager, where an L6-or-above individual contributor takes on 4-6 direct reports, and adopts the title “Tech Lead Manager.”

From talking to engineering managers at Google, this is the logic behind the role:

- Many Staff+ engineers (at L6 and above) do *not* want to become fulltime managers, nor do they want to manage large teams
- However, many are excellent tech leads
- For projects that only need a tiny team – 5-6 people at most – why not create a “hybrid” leadership role? The L6+ de facto tech lead also acts as a manager
- Constraint: the team cannot grow above 6 people
- As a standalone role, TLM perf takes into account that they do *some* people management, and cannot do as much IC work as a peer with zero reports

**The TLM role is more common at Google than at other Big Tech companies.** As a current Staff Engineer told us:

> “I have not seen TLM's deployed as much as at Google. TLM positions are usually served by the strongest ICs managing small teams. The goal is to ship quicker with less red tape. For example, I had an L7 TLM, and I observed L8 TLMs manage teams of 4-6 ICs.
> 
> These TLM's tend to be *very* capable ICs who want to ship very fast with a very small team. The TLM role is also pretty common on research projects”.

The biggest downside of the TLM role is that it’s hard to progress further. On the IC and manager ladders, there are clear-enough expectations for how to get promoted to the next level. But as a TLM, an engineer can expect to stay at the level for as long as they’re a TLM. This is another reason why the role is more suited for L7+ ICs who do not expect – or even want – more promotions.

### Manager career track

Engineering managers are responsible for the productivity, performance, and happiness of their reports. The most common ratio for manager-to-engineers is between 1:8 and 1:12. At the extremes, it can be as low as only 3 reports, or as high as around 30. The higher the number, the less attention a manager can give each report and the more they risk burnout.

Activities expected of engineering managers include:

- Coaching engineers so they grow professionally
- Supporting the career development of reports
- Performance management: go through the GRAD (Google Reviews and Development) process
- Be involved in hiring and parts of the compensation discussions; the higher level an engineering manager is, the more involvement they have. Directors-and-above often have more say in compensation

**Engineering managers need to have been engineers.** The book *“Software Engineering at Google”* explains how the company mandates an engineering background:

> “Many companies bring in trained people managers who might know little to nothing about software engineering to run their engineering teams. Google decided early on that its software engineering managers should have an engineering background. This meant hiring experienced managers who used to be software engineers, or training software engineers to be managers.”

**Google used to trust its engineering managers much less.** A former Google Staff Engineer told us:

> “Google did not trust managers in the early days. The systems were all designed so that individual managers were of limited influence. Promotions weren't decided by managers; they went to a promo committee of engineers! Your manager assessment was just one of the inputs to the committee.
> 
> Managers couldn't block team members from moving teams and didn't get to set hiring bars for their teams.
> 
> At one point, managers were responsible for your salary but not your equity – which was granted at the Director level – so your manager did not even know your full compensation package.”

Today, managers enjoy more trust, but still don’t have all that much say in equity allocation, even though they do see the total compensation of their direct reports.

For more reading on management and leadership at Google, see the “ [How to lead a team](https://abseil.io/resources/swe-book/html/ch05.html) ” chapter in *“Software Engineering at Google”*.

### Other roles

Outside of software engineers (SWEs) and engineering managers, there are more engineering roles at Google.

**Site Reliability Engineers (SREs)** is a role invented by Google in 2003. “Site” originally referred to “Google.com”, and SREs are responsible for operating large sites and applications. As Dave O’Connor, one of the first SREs, [recalled](https://newsletter.pragmaticengineer.com/p/reliability-engineering) about the origins of this role:

> “In 2003, the SRE role was born. Ben Treynor Sloss had been tasked with building Google’s “production team” and in his own words, he built “what happens when you ask a software engineer to design an operations team.” This turned into the birth of the SRE function at Google. From the outset, SRE was staffed in varying measures by systems/operations experts and software engineers. A large part of the remit of the team was to build the tools and practices required to operate Google’s fleet.”

Each Product Organization has its own SRE team, usually of 30-200 SREs. They partner with software engineers, as described in [How Google SRE and developers work together](https://research.google/pubs/how-google-sre-and-developers-work-together/):

![](https://substackcdn.com/image/fetch/$s_!djde!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa61fd33c-0694-4f03-bb72-e2ee32b061c5_1600x888.png)

How SRE and devs partner at Google

The SRE role was popularized by [Google’s SRE book](https://docs.google.com/document/d/1hVEWRpdFm78Wu0pZlJR1WXdH-2JDvFY6vknLiRpDG2E/edit?usp=sharing) in 2016, which is a free title that can be [read here](https://docs.google.com/document/d/1hVEWRpdFm78Wu0pZlJR1WXdH-2JDvFY6vknLiRpDG2E/edit?usp=sharing). We also covered more about the SRE role in the article, [What is Reliability Engineering](https://newsletter.pragmaticengineer.com/p/reliability-engineering).

Other roles worth mentioning:

**EngProd**: A function that ensures engineers and teams have the tooling and environment necessary to work on a product: setting up things like test rigs, running applications, packaging, setting up test labs for devices, staging environments, etc.

**Research scientists (RS).** Work alongside SWEs and do research. The recruitment bar is very high, and a PhD is not sufficient in itself. In fact, at Google most folks with PhDs who do research are SWEs rather than RSs, who need to have both a standout publication record of academic papers, and be good at coding.

**DevRel:** short for Developer Relations, and sometimes also called Developer Advocate. Activities include:

- Creating articles and videos targeting engineers
- Presentations at conferences and online
- Being “customer zero”: early adopters and testers of new things
- Friction logging (also called ‘frictioning’): dogfooding, with the explicit goal to capture points of friction

DevRel is an *engineering* position, not a marketing one; a fair amount of features and tools for Google products come from DevRels.

The role is usually external-facing, involving working with developers using Google’s tools and platforms. However, there are internal-facing DevRel roles which focus on advocating for and supporting teams across different organisations and PAs.

**UX Engineers (UXE):** this is a subset of SWE, and a hybrid role in which UXEs work with the Design and Dev teams on things like:

- Prototyping
- Frontend development
- Design systems development, such as working on Material Design
- UI framework development

A downside of being an UXE instead of an SWE at Google is that internally there are far fewer career opportunities because there are 10x or more SWE positions than UXE ones.

**Sales Engineer** **(SE), Customer Engineer (CE),****Technical Solutions Engineer**: these roles are more common in the Google Cloud unit. Sales Engineers work with GCP customers, and are usually involved in the sales process. Customer Engineers work between sales, customers, and product teams, and are similar to [forward-deployed engineers](https://newsletter.pragmaticengineer.com/p/forward-deployed-engineers) (FDEs). Technical Solutions Engineers often work with large customers, including the public sector, similar to what forward-deployed engineers do. *We covered more about FDEs in the issue [What are Forward Deployed Engineers, and why are they so in demand?](https://newsletter.pragmaticengineer.com/p/forward-deployed-engineers)*

Google has many niche engineering roles, from Network Engineer, through Systems Development Engineer, and other hardware roles. For example, Google develops its own CPUs and so hires for unique roles like [Silicon Operations Engineers](https://www.google.com/about/careers/applications/jobs/results/104916867683885766-senior-silicon-operations-engineer?q=engineer&page=3) who develop custom chips, working with Google’s manufacturing suppliers.

You can browse all of Google’s open roles [on its jobs site](https://www.google.com/about/careers/applications/jobs/results?employment_type=FULL_TIME).

**Non-engineering roles inside the tech org:** in these roles people typically don’t write code – or do so very rarely. SWEs frequently work with:

- **Product Managers:** these work with SWEs to make sure the *right thing* gets built.
- **Program Managers:** similar to Product Managers but they manage projects, processes, or operations.
- **Technical Program Managers (TPMs):** similar to Program Managers but with additional technical expertise. *We previously covered [what TPMs do and what software engineers can learn from them](https://newsletter.pragmaticengineer.com/p/what-tpms-do).*
- **Designers**: there are many subsets of this role: UX designers, UI/visual designers, motion designers, user researchers, UX researchers (UXRs), design program managers (DPMs), and conversation designers (CUI)
- **Tech writers:** produce the documentation and code samples used in public for developer pages like on Android, Cloud, etc.

## 4\. Compensation

If Google is known for one thing among tech professionals, it’s the comp. Ninety-nine percent of companies can’t or won’t match the compensation Google offers, and it’s an open secret that the company is willing to pay more than a rival offers for senior hires and candidates they *really* want to recruit.

As a manager at Uber, I had this experience when we were hiring for a new office in Bangalore, India. Candidates who had an offer from us and also had one from Google, almost always failed to choose Uber. This was because when they told Google about our offer, it simply added 10% to beat ours.

### Compensation structure

The compensation package comprises several components:

- **Base salary.** Annual compensation is paid bi-weekly in the US and Canada, and monthly in Europe. This is a fixed amount that isn’t affected by any performance factors.
- **Equity / stock**. Upon joining Google, there’s a new joiner equity package, which vests over 4 years. 33% vests in year 1, 33% in year 2, 22% in year 3 and 12% in year 4. Once the stock vests, it can be sold any time, or held.
- **Sign-on bonus.** Not given to every new hire, but more senior hires (L5 and above) can negotiate a one-off cash bonus when joining Google. It’s paid during the first months of employment, but might need to be repaid if the recipient resigns within two years.

At the end of the year, bonuses are paid in a mix of cash and equity:

- **Cash bonus.** If performance expectations are met, there’s a target cash bonus. If performance is above or below expectations, it can vary accordingly.
- **Equity refreshers.** At the end of the year, there’s usually an equity refresher alongside a cash bonus, if performance expectations were met. The equity refresher vests over 4 years in 25% increments.

**Total compensation (TC)** is the sum of base salary + cash bonus + equity paid.

### Typical L3 and L4 compensation packages

Let’s look at some typical new hire packages. *The best data source for these packages is [Levels.fyi](https://www.levels.fyi/companies/google/salaries/software-engineer), where you can browse thousands of Google packages.*

**Entry-level SWE: $160-250K in the US,** and proportionally lower in other regions. The L3 position is entry-level at Google. The company hires new grads and those with a few years of experience.

![](https://substackcdn.com/image/fetch/$s_!a3wW!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F524d2a5f-f2b0-412e-a5fd-e2e584bbca68_1236x834.png)

Real offers by Google. Source of most data points: Levels.fyi, Google L3 compensation

**Google’s compensation is location-based.** It pays top-tier compensation in the [trimodal compensation model](https://newsletter.pragmaticengineer.com/p/trimodal). However, the company adjusts packages by location and ensures it pays more than *regional* rivals. However, when looking at L3 compensation packages, it’s clear total compensation is significantly higher in the US and Switzerland than other regions.

Since Google’s pay is location-based, it’s theoretically possible for someone in a lower-cost location to get a better full-remote offer than Google makes. But in my experience, this is rare because high-paying full-remote positions are typically for senior software engineers-and-above – and Google starts to pay really well at that level. Plus, for very strong candidates the company can always offer more.

**L4** is mid-level, still below the Senior SWE (L5) position. Typical ranges for this level:

- **US**: $250,000–350,000 (total annual compensation)
- **Switzerland:** CHF 210,000–260,000
- **UK:** £125,000–£185,000
- **Germany and Ireland:** €140,000–€180,000
- **Canada:** CA$210,000–$280,000
- **Australia:** A$200,000–$280,000
- **Poland:** zł380,000—zł450,000 in Poland,
- **India:** ₹65–₹88 lakh

### Senior SWE (L5) and Staff SWE (L6) compensation

Senior SWE can earn up to $500K in the US. This is the level at which equity becomes more important compared to base salary. The Senior (L5) level is where compensation jumps significantly due to equity packages. Equity can usually be negotiated when receiving an offer, but keep in mind that it can be much lower or – in lucky cases! – higher than the offers below:

![](https://substackcdn.com/image/fetch/$s_!GW6V!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Feb4b4bad-ec0c-4f5b-83b9-63adb1660d9b_1228x846.png)

Actual compensation packages at Google, including some for longtime employees. Source: Levels.fyi, L5 Google packages

**L6** is the Staff Engineer role. This is a challenging role to both get hired into, and it’s also several times harder to get promoted internally, than it is the L4 → L5 promotion. Here’s how this position typically pays in annual total compensation:

- **US:** $550,00–700,000
- **Switzerland:** CHF 370,000–500,000
- **UK:** £270,000–380,000
- **Germany and Ireland:** €250,000–330,000
- **Canada:** CA$420,000–650,000
- **Australia:** A$350,000–550,000
- **Poland:** zł750,000—850,000 in Poland,
- **India:** ₹1.5-2.2 crores

### Million dollar job: Senior Staff SWE

The L7 (Senior Staff SWE) position is the lowest at which it’s possible to make more than $1M per year in total compensation for some folks in the US – usually in the Bay Area. Compensation packages are heavily equity-weighted: the initial grant and refreshers determine how high these packages go. These jobs almost always pay above $600K in the US and the variance starts to become very high.

![](https://substackcdn.com/image/fetch/$s_!XYU7!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fcbcfdbfd-9070-4f48-8598-d982555127f9_1228x808.png)

Actual compensation packages at Google. Data source: Levels.fyi, L7 Google packages

Reaching an L6 position is hard enough at Google, and being promoted internally to L7 is exponentially harder. Getting hired externally to this position usually requires that candidates have worked in a similar role at another Big Tech company for a long time, made industry-wide impact, or achieved recognition in a specific area. At present, folks in ML and AI seem to be getting the higher compensation packages, as these roles are harder to recruit than “traditional” SWE roles.

**Getting to L6+ levels is very difficult in smaller offices.** L7 positions are predominantly in the US and in larger offices like Switzerland. In offices like Bangalore, these positions are few and far between, and smaller offices often do not have L7-and-above levels. L8 jobs are usually limited to main US offices in the Bay Area, New York, Seattle, and LA, and Switzerland.

**Great pay is one reason why experienced engineers stay 10+ years at the company.** Google offers a predictable career path for experienced engineers; with skill and luck, one can keep increasing their earnings while staying an individual contributor!

Most companies require engineers to become managers or senior managers in order to earn the kind of compensation that Google pays L6-and-above engineers. This can have the effect of being “golden handcuffs” because for an L6+ engineer at Google, it’s hard to find anywhere offering pure individual contributor work without taking a massive pay cut!

### Peer bonuses, spot bonuses, award programmes

Google’s generous compensation doesn’t stop at base salaries, equity, and annual cash bonuses: the company has bonus types that are rare at other tech companies.

**Peer bonuses** are small awards you can nominate colleagues for. The amount varies per location: around $200 per nomination in the US and Zurich, and are used to say “thank you” for good work. While the amount is pretty minor, the special thing is that it comes from peers! And it can add up: if you get one such nomination per month from a colleague you help out, that’s around $2,400 per year. As a current software engineer explained to us:

> “Peer bonuses are used frequently, and you can give up to five per quarter. It’s typical to do so, for example; ‘thanks for dropping your normal work and helping me fix this bug yesterday!”

There are sensible limitations on the bonus: every engineer can give out up to five peer bonuses per quarter, and cannot nominate the same person in consecutive quarters. Plenty of large companies have internal systems for employees to thank each other (in a way their manager sees), but micro cash bonuses are unique to Google!

**Spot bonuses** are awarded by managers and are given as a “thank you” for going above-and-beyond and delivering a large impact. Spot bonuses tend to range from $200 to $2,000. Spot bonuses have been awarded for successfully completing major launches, and for standout (sometimes heroic!) ones.

**Award programmes** are rewards for whole teams which complete a massive achievement. For example, all team members might get a $5,000 bonus or an all-expenses-paid trip to Iceland for completing a very important launch.

## 5\. Hiring

There are unique elements in Google’s hiring process: algorithmic interviews, “Googleyness”, and team matching.

### Algorithmic interviews

Google is probably the place which sent algorithmic interviews mainstream; aka those we call “LeetCode” interviews.

A Google interview loop for software engineers almost always includes coding, which is an algorithmic challenge to be solved in 30-60 minutes. *This type of interview is frequently called the data structures and algorithms interview (DSA).*

Questions could include being asked to implement an exotic data structure like a [circular queue](https://leetcode.com/problems/design-circular-queue/description/), [hashmap](https://leetcode.com/problems/design-hashmap/description/), or a [time-based key-value store](https://leetcode.com/problems/time-based-key-value-store/description/). Candidates could be asked to implement solutions to algorithmic questions like [Two Sum](https://leetcode.com/problems/two-sum/description/): *“given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target”,* or [longest common prefix](https://leetcode.com/problems/longest-common-prefix/description/): “ *write a function to find the longest common prefix string among an array of strings and hundreds of others”.*

These coding interviews can be completed in any language candidates feel comfortable with, and most choose a language they are hands-on in, and which is expressive and easy to work with. You’re not allowed to use libraries for heavy lifting: you can only use basic elements, and need to build any structures or utilities you’d want to use. If the interview is in-person and with a whiteboard, then doing a pseudocode implementation can be an acceptable first pass, but candidates are expected to write correct code on the whiteboard which would compile and run as your optimal solution.

The book *“ [Cracking the Coding Interview](https://www.crackingthecodinginterview.com/) ”* was written by former Google software engineer Gayle Laakmann McDowell to help engineers prepare for algorithmic interviews. It has had six editions, and there’s also a sequel, *[Beyond Cracking the Coding Interview](https://www.beyondctci.com/)*. Lead author Mike Mroczka has shared tips in this newsletter about [how experienced engineers get unstuck during coding interviews.](https://newsletter.pragmaticengineer.com/p/how-to-get-unstuck-during-coding-interviews)

A common criticism of these interviews is that they don’t mirror day-to-day work. However, Google and many other large companies maintain these interviews for solid reasons:

- **Good-enough heuristic.** Engineers who do well in these interviews are usually solid coders. Put the other way, it’s very hard for candidates to do well if their coding skills are weak.
- **Easy to scale for new interviewers**. Google has tens of thousands of engineers doing interviews, and they add thousands of new ones every year. For this reason, a process is needed to which it’s easy enough to onboard people, so that even new interviewers can evaluate candidates pretty well.
- **Easy to replace leaked questions.** At Google’s scale, it’s a fact of life that questions get leaked to the outside world. So, an interview process with a bank of thousands of interchangeable interview questions is necessary.
- **Can be done in an hour**. Interviews cannot take too long, and a process that took days or weeks wouldn't work because candidates are often employed fulltime elsewhere and can’t take several days off for a trial week, for instance.

Google [offers preparation materials](https://techdevguide.withgoogle.com/resources/?topics=algorithms&topics=data-structures) for coding interviews which list potential questions and explanations of concepts that might come up.

### Typical interview process

Here’s what a typical software engineer interview process looks like at the world’s most profitable company:

![](https://substackcdn.com/image/fetch/$s_!w-SE!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3d2953a8-1d37-47c8-b5a2-50b44e93c4ea_1226x1168.png)

Interviews one typically needs to pass to get a software engineer offer at Google

Each stage is tougher and more time-consuming than the last. The onsite interview is typically organized into 2-3 back-to-back interviews, a lunch break, then another 2-3 interviews. The term “onsite” derives from how Google used to fly candidates “on site” to an office. Since 2020, most onsite interviews are done via video call on Google Meet. There are signs of Google starting to bring back in-person interviews for *some* interviews, but most hiring is done via video call at the time of publication.

**“Googleyness” is Google’s version of “cultural fit.”** In his book [Work Rules](https://www.amazon.com/Work-Rules-Insights-Inside-Transform/dp/1455554790), Google’s former VP of People, Laszlo Bock defines this:

> “Googleyness encompasses traits like intellectual humility, conscientiousness, comfort with ambiguity, and a propensity for collaboration. It embodies the cultural fit that Google seeks beyond just technical skills.”

Google veteran Andy Milo has been there 15 years, and [defines](https://www.google.com/about/careers/applications/stories/google-sales-engineering-insights/) Googleyness like this:

> “Throughout my years here, I’ve realized that Googleyness has so many components. If I had to boil it down to three things that stick out the most, they would be:

1. Putting the user first
2. Thinking 10x
3. Always doing the right thing.

With those three things as a guidepost, I think we can help the world accomplish amazing things”.

Googleyness usually comes down to demonstrating traits like:

- Curiosity
- Being humble and open to feedback
- Getting things done
- Doing the right thing
- Keeping standards high
- Having novel ideas

For L5-and-above levels, leadership is also assessed. A guide which Google distributed to product managers contains advice about the Googleyness and Leadership interview:

> “Google’s Product Managers dream of the next moonshot idea, thrive in ambiguity, value feedback, effectively challenge the status quo, and do the right thing. They lead and influence effectively, manage projects, get things done, work as a team, and strive for self development.
> 
> They demonstrate curiosity to know more, and are able to come up with novel product concepts and feature improvements. Understand what it means to be Googley by reading [Google’s corporate philosophy](https://about.google/company-info/philosophy/) and the Google Values”.

This advice is for PMs, but also applies to senior-and-above engineers and engineering managers.

*We cover more on hiring processes in the deepdives [Hiring software engineers](https://newsletter.pragmaticengineer.com/p/hiring-software-engineers) and [Hiring an engineering manager](https://newsletter.pragmaticengineer.com/p/hiring-engineering-managers).*

### Preparing for Google interviews

Few job interviews come with more in-depth preparation resources than Google’s data structure and algorithm and systems design interviews, and these have become standard at most of Big Tech and scaleups. Below are a few popular resources. *I have no affiliation with these resources, and none are affiliate links. Find out more in my ethics statement.*

**Google’s in-house preparation materials:** Google provides a mix of videos, articles, and exercises to help prepare for its interviews. Unlike many resources, they are free and worth [checking out.](https://techdevguide.withgoogle.com/paths/interview/)

![](https://substackcdn.com/image/fetch/$s_!rQ_w!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F89511214-ccfe-48c5-8e9f-576c3d0d37e6_1534x748.png)

Google’s Interview Prep Guide

**Technical screening, data structures and algorithms**: There are countless books, videos, and online courses on preparing for LeetCode-style interviews:

- **Books**: [Cracking the Coding Interview](https://www.crackingthecodinginterview.com/) is very well known, and the more recent [Beyond Cracking the Coding Interview](https://www.beyondctci.com/) is a timely update. [Elements of Programming Interviews](https://elementsofprogramminginterviews.com/), [Programming Pearls](https://www.amazon.com/Programming-Pearls-2nd-Jon-Bentley/dp/0201657880), and [The Algorithm Design Manual](https://www.algorist.com/) are also helpful in preparing.
- **Sites**: [LeetCode](https://leetcode.com/) is the most popular site for practicing thousands of algorithmic coding interviews. Others include [Codewars](https://www.codewars.com/), [Project Euler](https://projecteuler.net/), and others.
- **Courses**: [NeetCode](https://neetcode.io/) is the most popular online course, currently. There are [dozens of other courses.](https://www.google.com/search?q=data+structures+and+algorithm+course&sca_esv=af69388857e2a179&source=hp&ei=zq2-aImEAZuB9u8P-aqt4Qg&iflsig=AOw8s4IAAAAAaL673vnIKgez-lZwyi0p6HKAvhjjii7W&ved=0ahUKEwiJo7O8-MiPAxWbgP0HHXlVK4wQ4dUDCBc&uact=5&oq=data+structures+and+algorithm+course&gs_lp=Egdnd3Mtd2l6IiRkYXRhIHN0cnVjdHVyZXMgYW5kIGFsZ29yaXRobSBjb3Vyc2UyBxAAGIAEGAoyBxAAGIAEGAoyBxAAGIAEGAoyBxAAGIAEGAoyBxAAGIAEGAoyBxAAGIAEGAoyBxAAGIAEGAoyBxAAGIAEGAoyBxAAGIAEGAoyBxAAGIAEGApI3CFQAFj8IHAAeACQAQCYAWKgAdQRqgECMza4AQPIAQD4AQGYAiSgApASwgIFEAAYgATCAgsQLhiABBjRAxjHAcICBRAuGIAEwgIOEC4YgAQYxwEYjgUYrwHCAggQLhiABBjUAsICBxAuGIAEGAqYAwCSBwIzNqAH-boDsgcCMza4B5ASwgcHMTQuMjEuMcgHMA&sclient=gws-wiz)
- **YouTube:** there is an overwhelming amount of content on YouTube; just search “ [data structures and algorithms](https://www.youtube.com/results?search_query=data+structures+algorithms) ” or a more specific term. Lots of software engineers who have passed these interviews share their own approaches and preparation advice.

**Systems design**: this is another area that has been thoroughly documented.

- **Books:**[System Design Interview: Volume 1](https://www.amazon.com/System-Design-Interview-insiders-Second/dp/B08CMF2CQF) and [Volume 2](https://www.amazon.com/System-Design-Interview-Insiders-Guide/dp/1736049119) by Alex Xu, and [Designing Data-Intensive Applications](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321) by Martin Kleppmann, are the most popular preparation materials. *We’ve shared [a chapter on designing a payments system from the System Design Interview book](https://newsletter.pragmaticengineer.com/p/payments-system)*
- **Courses**: [ByteByteGo](https://bytebytego.com/) by Alex Xu is popular. There are dozens of other courses available by searching for [“systems design interview course”](https://www.google.com/search?q=systems+design+interview+course)
- **YouTube videos: similarly to data structure and algorithms preparation videos, there is plenty of material**

**Domain deepdive**: prepare to succeed by becoming an expert in your domain and mastering common tools, frameworks and practices, knowing how exactly they work, what the tradeoffs are – and by building things in the domain.

**Googleyness and leadership Interview:** understand Google’s values, summarize your experiences and achievements in order to use the best examples during the interview, and look into behavioural interview tips like [the STAR method](https://www.google.com/search?q=behaviorual+interview+star+method). This interview is a pretty typical “hiring manager interview.” Most candidates struggle with the more technical interviews, not with this one.

### Hiring Committee (HC)

At most businesses, a hiring decision comes after an onsite interview and a debrief. The decision typically belongs to the hiring manager who is often the candidates’ future manager. But at Google, it’s different. After each interview, the interviewers submit written feedback and their overall rating of a candidate according to a hiring-recommendation scoring system:

- Strong Hire (SH)
- Hire (H)
- Lean Hire (LH)
- Lean No Hire (LNH)
- No Hire (NH)
- Strong No Hire (SNH)

At this point, a dedicated Hiring Committee takes the feedback and makes its own hiring decision. Gayle Laakmann Mcdowell explained the process in the 2016 edition of [Cracking The Coding Interview](https://www.crackingthecodinginterview.com/):

> “Written feedback is submitted to a hiring committee (HC) of engineers and managers to make a hire/no-hire recommendation. Feedback is typically broken down into four categories (Analytical Ability, Coding, Experience and Communication) and you are given an overall score from 1.0 to 4.0. The HC usually does not include any of your interviewers. If it does, it’s purely by chance.
> 
> To extend an offer, the HC wants to see at least one interviewer who is an ‘enthusiastic endorser’. In other words, a packet with scores of 3.6, 3.1, 3.1, and 2.6 is better than all 3.1s.
> 
> You do not necessarily need to excel in every interview, and your phone screen performance is usually not a strong factor in the final decision.
> 
> If the hiring committee recommends an offer, your packet will go to a compensation committee, and then to the executive management committee. Returning a decision can take several weeks because there are so many stages and committees”.

**Referrals do make a difference in the hiring process.** Beyond interview performance, the only factor that can sway the hiring committee is a strong reference from a current Googler. So, if you know someone at Google, ask them to refer you with a note; if they worked with you previously and have positive things to say, this could turn a “no hire” into a “hire” decision.

### Team matching and packet expiry

Once the hiring committee decides upon a “hire,” an offer does not immediately follow. A successful candidate first needs to find a team that wants them. Pre-2023, this process was pretty speedy because Google was always growing and teams were hungry for hires. However, team matching is today becoming a hurdle where some “hire” recommendations get stuck. As we reported [in The Pulse:](https://newsletter.pragmaticengineer.com/i/160142389/team-match-evolution)

> “Team matching has evolved into a de facto second interview, despite companies' efforts to present it otherwise. From our conversations with hiring managers, we've found they commonly interview ten candidates to fill a single position. These managers strongly advise candidates to thoroughly prepare for this phase and customize their presentations specifically for the team they want to join.”

**Clearing the hiring committee is followed by a year-long window during which a team needs to “claim” a successful candidate before an offer is made.** With team matching becoming more of a hurdle, it’s worth knowing that there is a deadline by which to cement your place at the company. A recent Reddit post by an external L4 candidate interviewing at Google complained that they got one “Strong Hire”, two “Hire”, and one “Lean Hire”, and an overall “Hire” recommendation from the Committee. But despite these credentials, they had received zero offers. A commenter speculated that this was due to a lack of interest among teams, [writing](https://www.reddit.com/r/leetcode/comments/1c452rx/confused_on_my_google_interview_feedback/):

> “You just didn’t get any interest from hiring managers. Since the headcount got cut at Google it’s been extremely common to “pass” the on-site but get zero team matches. You have one year to match with a team before your interview packet expires”.

**Overall, Google’s hiring committee process creates greater internal mobility than in most of Big Tech.** A former engineering manager explained the benefits of Google’s hiring committee and team matching process:

> “The fundamental difference with other companies is how Google did company-wide hiring, rather than team-based hiring. Google hired *you*, and then you ended up on a team. That means that the people who interviewed you might not be people you ever saw again, the manager for a team didn't interview the people joining the team, etc.
> 
> The theory was that this approach would result in higher standards. When a manager *really* needs to make a hire, they might be willing to lower their hiring bar so they can make a hire *now*, rather than wait months.
> 
> The downside of this approach is that when you join, you don’t yet know what team you were joining – it was common to accept a Google offer and then learn what team you were on, on your first day. People who had strong preferences about teams sometimes simply did not accept the Google offer.
> 
> The upside was more inter-team trust and internal mobility. At a place like Microsoft, you had to interview again to change teams, because each team had different hiring standards, and so teams would not trust that other teams had the same standards as their own. At Google, when you want to change teams, no interviews are needed.”

**During Google’s fast growth era, team matching was about “calling dibs”.** A former engineering manager shares a fascinating anecdote about how team matching worked:

> “When I joined in 2007 in the New York office, there was a NYC-wide system where every team with open headcount was ranked in priority order. The list of new hires for the coming Monday was sent out. In priority order, each team got to take someone off the list or pass, and forward the list on. This repeated until all new hires were allocated to a team.
> 
> This process was a point of contention with candidates and new hires because there were candidates that certain lower priority teams *really* wanted but did not get, and some candidates were *really* set to work at lower priority teams, but did not get to them. Over the years, this process went through a lot of iterations to take team and candidate preferences better into account”.

## Takeaways

Phew! This has been a lot of information – and we’re barely halfway through the material we amassed during months of research into what it’s like working at Google. In the second part of this mini-series we’ll get into Google’s performance review process for engineers, internal systems, engineering processes, how teams and engineers get things done, and share nuggets of good advice from Googlers for thriving at one of the world’s most successful companies.

*Thank you to all current and former Googlers who have contributed by sharing details and insights – many of which are published here for the first time.*

I hope you found this article useful. If you have details about Google for the benefit of other readers, please do so in the comments, or send us a message.