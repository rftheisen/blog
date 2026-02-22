---
cover: .gitbook/assets/computerlab.gif
coverY: 0
---

# Amplify your learning by building a home lab

***



How do you stay up-to-date in an industry that is always evolving?&#x20;

How do you get into an industry like this?

&#x20;How do you stay relevant or even ahead in an industry like this?&#x20;

I'll give you an hint..... it's not about credentials (degrees, certifications, etc..) it's really all about skills & capability. Your credentials and pursuit of credentials should net you skills as you obtain the piece of paper. If you are obtaining credentials without skills, then something is wrong with the training program you are using. It should be hands-on and aligned with the skills & systems companies are using now and will be using in the future. One of the best things you can do to ensure this for yourself is by building your own Learning Infrastructure. Whether you are looking at IT Ops, Software Development or Cybersecurity you will benefit from building an infrastructure as you learn. That's what I do!&#x20;

As I become aware of a new skill, trend or system, I set it up & maintain it in my lab environment at home. Hopefully I can inspire you to do the same for yourself and maybe even your team. The information I've shared below can help you set up a lab infrastructure.\\

***

### My Home Lab/Content Creation Studio

Your home lab will evolve over the years. Your first iteration does not have to be a high performance compute datacenter made up of a cluster of H100s that can train large language models. Mine started out as a less than impressive collection of web cams, a mic, cheap plastic cabinets, an old Dell PowerEdge server and a laptop. Yes, my first content creation system and center point of my lab was a laptop. It was a Surface Book 2.&#x20;

Before I started creating content online I would often tell my wife:&#x20;

"Before I can start making videos I need more powerful hardware so I can have the best production value."&#x20;

She would just say: "Just start on your laptop!"&#x20;

We would argue about it but she was right! Just start with what you have now and kick your **needsmoretechidous** to the curb.

***

### My Home Lab Setup in 2021

Feel proud of your first iteration of your home lab. You are just getting started and that is something to celebrate. It will evolve over the years and throughout your career. Here is a video I made sharing one of my earliest home labs:&#x20;

{% embed url="https://youtu.be/lJZgZzk9xMs" %}

***

### My Latest Home Lab Setup 2024&#x20;

My current setup is purpose built for learning, content creation, penetration testing, systems administration, IT systems engineering, DevOps, and Software Development. I use Proxmox and VMware ESXI for virtualization so I can setup up various scenarios I read, hear and learn about. I see my home lab as an essential resource to maintain a relevant skillset.

{% embed url="https://youtu.be/bbgNV-FlgP4?si=7gKIcihIeLFHuRM1" %}

What's in my home lab:&#x20;

*   A powerful gaming/content creation PC

    * Intel I9 based build&#x20;
    * 32 GB of RAM&#x20;
    * 2 TB of NVME SSD Storage&#x20;
    * RTX 3080 TI GPU
    * External WiFi Antenna&#x20;


*   3 Dell PowerEdge R420s&#x20;

    * These servers have been discontinued but I use them to practice with administering hypervisors


*   6 Intel-based Mac Minis

    * These were gifted to me and I am currently running Ubuntu on them
    * I administer them using Red Hat's Ansible. They are currently running in a Kubernetes cluster configuration (MicroK8s)
    * Im practicing with containerizing applications on this cluster


*   2 broken down HP laptops

    * I need to fix these and give them away as gifts
    * I will often accept forgotten hardware and give it away to people who want to get their home lab started up


*   Triple monitor setup&#x20;

    * This makes managing live streams simple and helps with multi-tasking&#x20;
    * Each new monitor I add feels like adding an additional brain


*   Ubiquiti Dream Machine Pro

    * This acts as my switch, router and next generation firewall
    * I also use the built-in OpenVPN server to connect into my lab when I am away from home


* 4 Cisco 2960 switches&#x20;
* 2 Cisco 2911 routers
  * The Cisco gear is for practicing network concepts and making networking videos. I believe if you can learn networking from Cisco's perspective you can learn any vendor.

### Building your Home Lab

It would be awesome to have an unlimited budget for lab equipment but most of us just do not have that. I've built my home lab with this in mind and I recommend you do the same, at least at first. Here are some steps to follow as you build:

Identify the skills, job role, and type of work you are trying to achieve

Common job titles to search:&#x20;

* SOC Analyst
* IT Support Analyst
* Help Desk Analyst&#x20;
* Network Administrator
* Linux Administrator
* Network Engineer
* Active Directory Administrator
* Systems Administrator&#x20;
* IT Systems Engineer
* Software Engineer&#x20;
* Software Developer&#x20;
* Data Analyst
* DevOps Engineer
* Threat Hunter
* IT Instructor&#x20;
* Cybersecurity Analyst&#x20;
* Penetration Tester

Just to name a few....

It'd be a good idea to search for some of these titles in your area or with the company for which you want to work. Even if you are an entrepreneur this can give you some insight on what companies need help with.&#x20;

Isn't that what a job posting is in the first place?.... a signal for help.&#x20;

As you scan the postings, you'll gain insight on the systems and skills they are looking for help managing. Make a Learning Journey List of the skills you find so you can use it with search engines and AI chatbots.

Common sites to use on your search:&#x20;

* Google&#x20;
* LinkedIn
* Ziprecruiter
* Glassdoor&#x20;
* Monster&#x20;
* Indeed
* ChatGPT
* Perplexity
* Anthropic's Claude

#### Identify resources where you can obtain hardware & software for free or low cost

You would be surprised how many organizations offer at least one of their software products for free.&#x20;

The Open Source movement/philosophy really has given us technologists the opportunity to experiment and learn at a low cost, especially when it comes to software tools & operating systems. If you are a student and have a .edu email address you can find tons of student discounts and intitiaves that can save you several thousands of dollars on licensing for labs, so please ask your school about this.&#x20;

In the United States we have institutions called community colleges that offer great education at a low cost, often times you can get grants that cover the cost & give you some extra money. Many of these community colleges are partnered with companies in the IT industry.&#x20;

Companies like&#x20;

* Red Hat
* Microsoft
* Amazon&#x20;
* Cisco&#x20;
* Palo Alto Networks&#x20;

These partnerships allow schools to give their students (you) access to enterprise grade software & cloud platforms. If you aren't currently enrolled in a school please don't be discouraged, there are lots of great resources for you as well.

***

### The Anatomy of a Home Lab

In general I believe you should build your home lab to have the following components:&#x20;

* Desktop hardware&#x20;

This should be for practicing administering desktop systems (clients). Ideally you will want to have 1 or 2 systems running Windows because over 70% of enterprises are running on Windows operating systems. Windows administration is a pretty easy skill to develop and is beneficial knowledge in:&#x20;

* IT support&#x20;
* System/Network administration&#x20;
* Cybersecurity focused roles (SOC analyst, Penetration tester, etc...)

Ask family and friends if they have any computers laying around that you could have. This may seem weird but it will surprise you how far you can get by just asking. I've acculumated countless pieces of technology for my home lab over the years that I got by simply asking!&#x20;

* Server Hardware

Servers are technically systems that service requests. You could practice with server side technologies on laptops, desktops or even in VMs. The term server hardware is normally associated with enterprise grade hardware where the form factor is built to house more capacity. It is common to see this kind of hardware in a blade form factor meant to be rack mounted. A great place to get good server hardware cheap is Server Superstore.

{% embed url="https://serversuperstore.com" %}

Server Superstore has some really powerful refurbished hardware for cheap. I recommend using this hardware to setup a type 1 hypervisor (also known as bare-metal hypervisor) using Proxmox or VMware ESXI. Proxmox is an opensource alternative to ESXI that has many of the same features but is free of cost. VMware is still the industry standard type 1 hypervisor but theres been a reputation hit since Broadcom acquired them, so that may change. Another option would be Microsoft's Hyper-V, there are many options out there.... why not try them all?

You would be surprised how many companies and school districts have literal garages full of powerful servers they are no longer using. One time I asked an IT director of a school district if he had any extra hardware I could have. He said yes and invited me to a medium size building that was soley dedicated to storing old hardware they were no longer using. They recently got a lot of money to refresh their entire IT infrastructure (millions of dollars) and had a garage full of decent hardware they had replaced. The IT director told me:

"Take whatever you want, we will write it off.... otherwise we are having a guy from a tech recycling company to come pick it up."

Someone in your sphere of influence could have the same level of access to technology. You wont know if you dont ask.&#x20;

* Network Hardware

Try to get at least 2 old Cisco switches and 2 old Cisco routers. This way you can learn enterprise networking skills on a well known vendor that is still quite wide spread. Keep in mind that a lot of companies are trying to get away from Cisco products because of the price but they are reliable devices and a lot of fun to learn on. Having Cisco hardware can help tremendously if you are preparing for a Cisco certification exam like the CCNA.

You should also aim to get firewall hardware. Not because your home network is being bombared by malicious hackers aiming to steal all your secrets but because companies face that threat. If you want to have those skills, know firewalling is critical. There are lots of firewall vendors. I recommend you look into the following:&#x20;

* Palo Alto Networks hardware and virtual firewalls (VM-based firewalls)&#x20;
* PFsense (an opensource firewall)
  * It can be installed in a VM or on supporting hardware
  * Look into Netgate: [https://www.netgate.com](https://www.netgate.com)
* Ubiquiti Dream Machine Pro&#x20;
  * This is a pretty solid next generation firewall that can get you used to cloud-managed networking
* Cisco's ASA series

You can find network hardware on eBay for pretty cheap.

***

### What about Cloud Labs?&#x20;

I am recommending all this on-premises focused infrastructure because it is still a valuable and in-demand skill to have. I happen to believe a lot of companies will actually trend back on-prem as the costs for IaaS and SaaS get out of hand. That and LLM powered Chatbots enabling IT professionals to start developing more custom tooling. Here is one leading-edge signal that supports my prediction:&#x20;

{% embed url="https://basecamp.com/cloud-exit" %}

However, this trend back on-prem hasn't happened yet. Developing cloud skills can be a valuable skill. I recommend experiment with all three major cloud providers:&#x20;



1. Amazon's Web Services (AWS)
2. Microsoft's Azure
3. Google Cloud Platform (GCP)

Start by experimenting with setting up VMs on each just to see how it works and to get familiar with the user interface of each. Try to stay in the free tier with each to save money. You will notice that they typically require a credit card, so they can charge you for paid for instances and services. Be careful with this! Don't just click the top-end instance and start it up, you could potential set yourself back hundreds of dollars in minutes, perhaps thousands if you accidentally leave an instance running for long.&#x20;

After you have experimented with setting up VMs in each try to host a simple website or wordpress site on an instance. This will give you a start in understanding how hosting in the cloud works.

### Go Build it!

That should be enough home lab information to get you started. Your next steps should be to come up with a plan to start getting some of this equipment and practicing with it. If you need some tips or scenarios please feel free to reach out to me directly through LinkedIn or Discord. I run a learning community on Discord called LTN Labs. If you enjoyed this article then you would probably love being part of the community.&#x20;

Click this link to join us:&#x20;

{% embed url="https://discord.gg/ET93fpp" %}

Keep learning!
