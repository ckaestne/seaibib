# Software Engineering for AI/ML -- An Annotated Bibliography

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

Author: Christian Kästner, CMU

## Context

While the academic literature on solving software engineering problems with
machine learning techniques (ML4SE or AI4SE) abounds and has a long history,
there is far less academic research on how to improve the engineering
of systems with AI/ML components (SE4ML or SE4AI). 

With an interest primarily for teaching a software engineering class
for AI/ML systems ([course web page](https://ckaestne.github.io/seai/),
[paper about the course](https://arxiv.org/abs/2001.06691)), I tried
to read up on the field. I had several interesting discussions since
and have shared my collection of papers on the topic repeatedly and received
some pointers to other papers as well. In an effort to help the community
I'm sharing here a list of papers that I found interesting and useful
with some sparse notes.

All notes are my personal opinions.

If you have suggestions for other readings (with or without annotations)
consider sending a pull request :)

## Key Resources

Hulten, Geoff. [Building Intelligent Systems: A Guide to Machine Learning Engineering](https://www.buildingintelligentsystems.com/). Apress. 2018

> This is the best book that I'm aware of that covers the 
software engineering aspects of building ML systems, including
coverage of requirements, architecture, quality assurance,
and process. We used it as textbook for our course and assigned
many chapters as reading. 
Coverage is often more broad than deep and there is an overwhelming
amount of bulleted lists (not uncommon for SE textbooks), but
it is a great introduction to the topic.

Sculley, David, Gary Holt, Daniel Golovin, Eugene Davydov, Todd Phillips, Dietmar Ebner, Vinay Chaudhary, Michael Young, Jean-Francois Crespo, and Dan Dennison. "[Hidden technical debt in machine learning systems](http://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf)." In Advances in neural information processing systems, pp. 2503-2511. 2015. 

> Position paper. Probably the most cited paper in this field (and the original 
title *"Machine learning: The high interest credit card of technical debt"* is
one of my favorite paper titles), describes the challenges in building ML
systems and how poor engineering choices can  be very expensive. While the
"technical debt" metaphor is a bit forced and does not align with how I'd
teach technical debt and most of the description is rather abstract and not
well grounded in the SE literature, the paper provides a great argument that a
machine learning system is more than just the ML model and building and
operating it is a serious undertaking. 
> 
> Pro tip: A google scholar alert for citations to this paper is a good way to notice new SE4ML publications.

Amershi, Saleema, Andrew Begel, Christian Bird, Robert DeLine, Harald Gall, Ece Kamar, Nachiappan Nagappan, Besmira Nushi, and Thomas Zimmermann. "[Software engineering for machine learning: A case study](https://andrewbegel.com/papers/Software_Engineering_for_ML.pdf)." In 2019 IEEE/ACM 41st International Conference on Software Engineering: Software Engineering in Practice (ICSE-SEIP), pp. 291-300. IEEE, 2019. 

> A good description of the SE4ML challenges at Microsoft, characterizing
the challenges of different roles and grounded in interviews and a large
scale survey. Motivating well how pervasive ML is in modern systems and describing best practices and some challenges.

Ozkaya, Ipek. "[What Is Really Different in Engineering AI-Enabled Systems?](https://ieeexplore.ieee.org/abstract/document/9121629)" *IEEE Software* 37, no. 4 (2020): 3-6.

> Concise opinion paper (editorial), discussing that building software system with AI components is harder but not necessarily that different from building traditional software systems. This very much mirrors my own opinion shared in my class and talks. Touches on many great points regarding specifications, requirements, and safety. Essentially a call to action that we need more software engineering.

## Quality Assurance

*There is a lot of work that covers testing ML systems in some form, most
of it seems focused on fairly narrow properties of a model. Testing an ML-enabled
system should be much broader, including system testing and testing of 
the infrastructure (e.g., learning pipeline and update mechanisms) and
testing in production.*

Breck, Eric, Shanqing Cai, Eric Nielsen, Michael Salib, and D. Sculley. 2017. “[The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction](https://research.google/pubs/pub46555.pdf).” IEEE International Conference on Big Data (Big Data). 2017.

> Nice position paper that discusses the many different aspects of quality assurance in an ML project, beyond just model and data quality. Includes some examples and a checklist of QA steps to consider. Good introduction to the problem and based on practical experience at Google. (Note this is a slightly extended version from a similarly titled paper)

Kaestner, Christian. "[Machine Learning is Requirements Engineering — On the Role of Bugs, Verification, and Validation in Machine Learning](https://medium.com/@ckaestne/machine-learning-is-requirements-engineering-8957aee55ef4)." Medium Blog Post. 2020.

> My own discussion of the role of specifications in machine learning. Many testing papers below that focus on model quality (rather than infrastructure quality, as Breck above) are rather vague and confusing to me with regard to specifications. I argue that machine learning corresponds to the requirements engineering phase of a project rather than the implementation phase and, as such, terminology that relates to validation (i.e., do we build the right system, given stakeholder needs) is more suitable than terminology that relates to verification (i.e., do we build the system right, given a specification). That is, machine learning suggests a specification (like specification mining and invariant detection) rather than provides an implementation for a known specification (like synthesis).

Tang, Diane, Ashish Agarwal, Deirdre O'Brien, and Mike Meyer. "[Overlapping experiment infrastructure: More, better, faster experimentation](https://dl.acm.org/doi/pdf/10.1145/1835804.1835810)." In Proceedings of the 16th ACM SIGKDD international conference on Knowledge discovery and data mining, pp. 17-26. 2010.

Bakshy, Eytan, Dean Eckles, and Michael S. Bernstein. "[Designing and deploying online field experiments](https://dl.acm.org/doi/pdf/10.1145/2566486.2567967)." In Proceedings of the 23rd international conference on World wide web, pp. 283-292. 2014.

> Two papers discussing infrastructure for A/B testing (which is a good foundation and frequently used for testing ML systems in production) at Google and Facebook. More focused on infrastructure around it, but useful for getting into a discussion on how to test in production.

Ashmore, Rob, Radu Calinescu, and Colin Paterson. "[Assuring the machine learning lifecycle: Desiderata, methods, and challenges](https://arxiv.org/abs/1905.04223)." arXiv preprint arXiv:1905.04223. 2019.

> Survey on testing in machine learning, going through the stages of an ML pipeline. Many pointers and reasonable organization. Seems more from an ML perspective than an SE perspective, but broadly covers many aspects including data aquisition, data quality, robustness, safety, monitoring, and so forth. A little vague on specifications as usual and little focus on the overall system quality. No information on the used research process.

Zhang, Jie M., Mark Harman, Lei Ma, and Yang Liu. “[Machine Learning Testing: Survey, Landscapes and Horizons](http://arxiv.org/abs/1906.10742).” arXiv preprint 1906.10742. 2019 (to appear in TSE)

> Another broad survey on testing in machine learning. Includes many pointers, including different test strategies and different kinds of testing. While the pointers are useful, I was frustrated with many descriptions, definitions, and classifications and find little synthesis in this paper; e.g., I was hoping for clearer definitions of "ML bug", "data bug" or a clear discussion of specifications. Grey literature is not discussed either.

Riccio, Vincenzo, Gunel Jahangirova, Andrea Stocco, Nargiz Humbatova, Michael Weiss, and Paolo Tonella. "[Testing machine learning based systems: a systematic mapping](https://www.pre-crime.eu/techreps/TR-Precrime-2020-03.pdf)." Empirical Software Engineering (2020): 1-62.

> Yet another survey paper on ML testing. It frames the problem as testing the entire system with an ML component, but rarely goes beyond quality assurance just for the model. Somewhat biased toward self-driving cars. Again, I have quite some quibbles with many claims and definitions, e.g. model vs system or what is a specification or what is a bug. As for the other surveys, I'd suggest to use it for an overview and skim for the pointers.


### (Test Data Curation)

Barash, Guy, Eitan Farchi, Ilan Jayaraman, Orna Raz, Rachel Tzoref-Brill, and Marcel Zalmanovici. "[Bridging the gap between ML solutions and their business requirements using feature interactions](https://dl.acm.org/doi/abs/10.1145/3338906.3340442)." In Proceedings of the 2019 27th ACM Joint Meeting on European Software Engineering Conference and Symposium on the Foundations of Software Engineering, pp. 1048-1058. 2019.

> Discusses how to slice validation data into subsets to observe how the model is doing on different subpopulations. Simple yet useful idea. Nice analogy to blackbox testing (they frame it in terms of combinatorial testing, though equivalence classes may be a better fit). Approach is used to slice data rather than generate new test data, which aligns also with Hulten's recommendations and [my lecture](https://ckaestne.github.io/seai/S2020/slides/04_modelquality/modelquality.html)/[blog post](https://medium.com/@ckaestne/a-software-testing-view-on-machine-learning-model-quality-d508cb9e20a6) on testing.

Ré, Christopher, Feng Niu, Pallavi Gudipati, and Charles Srisuwananukorn. "[Overton: A Data System for Monitoring and Improving Machine-Learned Products](https://arxiv.org/abs/1909.05372)." *arXiv preprint arXiv:1909.05372* (2019).

> Overview of a system design (at Apple) that focuses on slicing and improving training data incrementally. The model building part is automated and the system focuses on the training and validation data, making it easy to add more data and labels (using semi-supervised learning ideas). Nice demonstration of the importance and effectiveness of slicing data for the evaluation (see above).

See also paper in the [requirements section](https://github.com/ckaestne/seaibib#requirements-engineering) below.

### (Model Invariants)

Segura, Sergio, Gordon Fraser, Ana B. Sanchez, and Antonio Ruiz-Cortés. "[A survey on metamorphic testing](https://core.ac.uk/download/pdf/74235918.pdf)." IEEE Transactions on software engineering 42, no. 9 (2016): 805-824.

> This paper discusses the idea of metamorphic testing and summarizes much work in this area. The key idea is that in the absence of a specification about what the model should do (which is the whole point of using ML), we might still be able to give partial specifications in terms of invariants about how outputs should relate for input pairs. For example, robustness conditions might be expressed by indicating that similar inputs should produce the same output or that linearly scaling all features or adding irrelevant features should not affect the outcome for certain classifiers. This is an interesting direction that enables testing of a number of invariants for ML models. The paper gives many pointers to other work in this area.


Ribeiro, Marco Tulio, Sameer Singh, and Carlos Guestrin. "[Semantically equivalent adversarial rules for debugging NLP models](https://www.aclweb.org/anthology/P18-1079.pdf)." In Proceedings of the 56th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), pp. 856-865. 2018.

> Example of testing for invariants in NLP models (in line with metamorphic testing, even though they do not refer to that concept). Here one expects certain linguistic invariants, for example, replacing "isn't" by "is not" should not change the outcome. These invariants are used to derive and prioritize tests and to then improve the model with more input data.

Singh, Gagandeep, Timon Gehr, Markus Püschel, and Martin Vechev. "[An abstract domain for certifying neural networks](https://dl.acm.org/doi/pdf/10.1145/3290354)." Proceedings of the ACM on Programming Languages 3, no. POPL (2019): 1-30.

> This is an example of a large group of paper that proofs specific invariants about models. For example, the specification could be that a model is robust to certain changes to its inputs (e.g., changing the brightness of pixels by +/- 20%) on the training set or certain classes of inputs. In contrast to much testing work, here results are verified over all input changes covered by a specification.

Galhotra, Sainyam, Yuriy Brun, and Alexandra Meliou. "[Fairness testing: testing software for discrimination](https://dl.acm.org/doi/pdf/10.1145/3106237.3106277)." In Proceedings of the 2017 11th Joint Meeting on Foundations of Software Engineering, pp. 498-510. 2017.

> Another application of testing invariants: here, for fairness certain outputs should be independent of changes to sensitive attributes. To simple for practical use in my book; limited to "fairness through blindness" (or "unawareness" or "anti-classification") and group fairness (but seemingly without addressing correlations in the data, since samples are generated uniformly).


Ding, J., D. Zhang, and X. Hu. 2016. “[A Framework for Ensuring the Quality of a Big Data Service](https://ieeexplore.ieee.org/iel7/7557343/7557418/07557439.pdf).” In 2016 IEEE International Conference on Services Computing (SCC), 82–89.

> Another example of using metamorphic testing, using domain knowledge about the problem to come up with invariants. Nice concrete example, though not the easiest read.

Ribeiro, Marco Tulio, Sameer Singh, and Carlos Guestrin. "[Anchors: High-precision model-agnostic explanations](https://sameersingh.org/files/papers/anchors-aaai18.pdf)." In Thirty-Second AAAI Conference on Artificial Intelligence. 2018.

> Approach for explaining black-box models that is essentially invariant mining, not that far from Daikon. The paper identifies rules that, with high probability, are sufficient to explain a specific prediction for a subset of all inputs. These invariants can then explain part of the model and could potentially be used as partial specifications or test cases.


### (Testing ML Frameworks)

Srisakaokul, Siwakorn, Zhengkai Wu, Angello Astorga, Oreoluwa Alebiosu, and Tao Xie. "[Multiple-implementation testing of supervised learning software](https://www.aaai.org/ocs/index.php/WS/AAAIW18/paper/viewPDFInterstitial/17301/15599)." In Workshops at the Thirty-Second AAAI Conference on Artificial Intelligence. 2018.

> Good example of a paper that tests the implementation of the ML algorithm (not the model or resulting system). Here differential testing is used to compare multiple student implementations. Nice demonstration of the idea, though it is not clear how far this would be practical beyond fairly simple learning algorithms implemented in student projects.

Xie, Xiaoyuan, Joshua WK Ho, Christian Murphy, Gail Kaiser, Baowen Xu, and Tsong Yueh Chen. "[Testing and validating machine learning classifiers by metamorphic testing](https://www.sciencedirect.com/science/article/pii/S0164121210003213)." Journal of Systems and Software 84, no. 4 (2011): 544-558.

> This paper applies metamorphic relations to the learning framework itself. That is, it defines invariants/assertions about how inputs (training data) and outputs (learned models) should relate.


### (Other Quality Assurance Work)


Pei, Kexin, Yinzhi Cao, Junfeng Yang, and Suman Jana. "[DeepXplore: Automated whitebox testing of deep learning systems](https://doi.org/10.1145/3132747.3132785.)." In proceedings of the 26th Symposium on Operating Systems Principles, pp. 1-18. 2017. 

> Differential testing between multiple models (e.g., learned from the same data with different parameters) and input generation that aims to identify inputs that have different outputs across the models. Unclear to me how useful this would be in practice.


Zhang, Yuhao, Yifan Chen, Shing-Chi Cheung, Yingfei Xiong, and Lu Zhang. "[An empirical study on TensorFlow program bugs](https://doi.org/10.1145/3213846.3213866)." In Proceedings of the 27th ACM SIGSOFT International Symposium on Software Testing and Analysis, pp. 129-140. 2018.

Zhang, Tianyi, Cuiyun Gao, Lei Ma, Michael R. Lyu, and Miryung Kim. "[An empirical study of common challenges in developing deep learning applications](http://web.cs.ucla.edu/~miryung/Publications/isese2019-deeplearningchallenge.pdf)." In The 30th IEEE International Symposium on Software Reliability Engineering (ISSRE). 2019.

> These two papers are examples of papers that analyzes public bug reports from issue trackers or question-answer sites (stackoverflow) for machine-learning frameworks. They characterize the kinds of problems developers and users tend to have, some some solutions. Many issues seem to be common framework issues, such as documentation issues and breaking APIs. Some challenges, such as probabilistic correctness and missing debuggers, seem more ML specific.

Seshia, Sanjit A., Dorsa Sadigh, and S. Shankar Sastry. "[Towards verified artificial intelligence](https://arxiv.org/abs/1606.08514)." arXiv preprint arXiv:1606.08514 (2016).

> Good framing why formal verification (or really any form of testing) is so difficult in machine learning systems in the first two sections: We neither have a specification, nor a good grasp of the environment, and in addition the system is often evolving itself. After explaining why it is so difficult, the paper points to several potentially interesting research areas, but none of them seem to overcome the fundamental problems, especially that of missing specifications.


## Debugging

Molnar, Christoph. "[Interpretable machine learning. A Guide for Making Black Box Models Explainable](https://christophm.github.io/interpretable-ml-book/)", 2019. 

> Though primarily about interpretability, this book provides a great overview of techniques to understand and debug models. 
The book covers both inherently interpretable models and many techniques for ex-post explanations inferred from blackbox models. Explanations can be shown to the user (though the book is fairly shallow on the challenges of doing this and larger system design questions), but they also seem very useful in understanding model (mis-)behavior, understanding individual wrong predictions and outliers. The book covers both techniques for understanding the model and understanding characteristics of the training data. Written in a fairly accessible and pragmatic style, covering the important math but also providing good intutions.

Ma, Shiqing, Yingqi Liu, Wen-Chuan Lee, Xiangyu Zhang, and Ananth Grama. "[MODE: automated neural network model debugging via state differential analysis and input selection](https://dl.acm.org/doi/pdf/10.1145/3236024.3236082)." In Proceedings of the 2018 26th ACM Joint Meeting on European Software Engineering Conference and Symposium on the Foundations of Software Engineering, pp. 175-186. 2018.

> Uses a SE mindset (delta debugging, slicing) to approach the problem of debugging deep neural networks, especially to identify features that are critical for misbehavior with the goal of providing better learning data (framed as "root cause identification" of "training bugs"). Fairly pragmatic.

Ma, Shiqing, Yousra Aafer, Zhaogui Xu, Wen-Chuan Lee, Juan Zhai, Yingqi Liu, and Xiangyu Zhang. "[LAMP: data provenance for graph based machine learning algorithms through derivative computation](https://dl.acm.org/doi/pdf/10.1145/3106237.3106291)." In Proceedings of the 2017 11th Joint Meeting on Foundations of Software Engineering, pp. 786-797. 2017.

> Interesting idea to identify which inputs to a machine-learning algorithm have large effects on the produced model (i.e., some form of sensitivity analysis). Focused on specific classes of graph-based algorithms like Pagerank.




## Data Quality and Data Management

Schelter, Sebastian, Dustin Lange, Philipp Schmidt, Meltem Celikel, Felix Biessmann, and Andreas Grafberger. 2018. “[Automating Large-Scale Data Quality Verification](http://www.vldb.org/pvldb/vol11/p1781-schelter.pdf).” Proceedings of the VLDB Endowment International Conference on Very Large Data Bases 11 (12): 1781–94.

> Good paper discussing data validation, including schema validation and
checking distributions. The key innovation in the paper is doing this at
scale (at Amazon), whereas the specification mechanisms seem rather straightforward, 
but generally well written and teachable.


Polyzotis, Neoklis, Sudip Roy, Steven Euijong Whang, and Martin Zinkevich. 2017. “[Data Management Challenges in Production Machine Learning](https://dl.acm.org/doi/pdf/10.1145/3035918.3054782).” In Proceedings of the 2017 ACM International Conference on Management of Data, 1723–26. ACM.

> Short tutorial notes, not very deep, but providing a decent overview of past work in the database community


Hynes, Nick, D. Sculley, and Michael Terry. "[The data linter: Lightweight, automated sanity checking for ml data sets](http://learningsys.org/nips17/assets/papers/paper_19.pdf)." In NIPS MLSys Workshop. 2017.

> Neat idea to develop a linter that looks for common "code smells" in dataset and internal data structures (e.g., when integers are stored as strings). This is an early but great example of how some classic SE ideas (static analysis tools, dynamic invariant detection, code smells) can be translated to solve new problems in an ML context. It is not quite obvious how far one can take this idea, but it is a great starting point for discussions and a nice illustration of potential SE4ML work.

Ratner, Alexander, Stephen H. Bach, Henry Ehrenberg, Jason Fries, Sen Wu, and Christopher Ré. "[Snorkel: Rapid training data creation with weak supervision](https://arxiv.org/abs/1711.10160)." Proceedings of the VLDB Endowment, 11(3), 269-282, 2017.

> Description of Snorkel, an approach to semi-automatically label training data, where humans provide partial training functions (e.g., labeling some instances based simply on some keywords). The system will learn automatically which of these partial labels to trust and will produce training labels at scale. This is an interesting strategy to gather training data that may work in a number of domains and has been used by a number of companies -- worth exploring. Many further discussions can be based on this, e.g., how to combine manual labels with different confidence, how to combine manual and automatic labels, which labels to trust, how much to involve crowdworkers in labeling and on which data points, etc.


## Requirements Engineering

*I have the impression that many practical problems in building AI-enabled systems are 
really requirements engineering problems. For example: There are many different notions
of fairness, but which one is the right one for the project? How does the model interact
with the environment and what safeguards should be installed to detect feedback loops or
assure safety in those interactions? Unfortunately, the literature on requirements engineering for AI-enabled systems seems rather sparse.*

Vogelsang, Andreas, and Markus Borg. "[Requirements Engineering for Machine Learning: Perspectives from Data Scientists](https://arxiv.org/pdf/1908.04674.pdf)." In Proc. of the 6th International Workshop on Artificial Intelligence for Requirements Engineering (AIRE), 2019. 

> Strong argument for the importance of requirements engineering when building ML-enabled systems. Covering many qualities and what kind of requirements should be solicited, including requirements about data quality and quanitity, provenance, monitoring, and protected classes and attributes. Also makes a good case for the role of a requirements engineer to identify a suitable measure of accuracy to mediate between users and data scientists. Based on 4 interviews only and sometimes reads more like a well argued opinion paper.

Rahimi, Mona, Jin LC Guo, Sahar Kokaly, and Marsha Chechik. "[Toward Requirements Specification for Machine-Learned Components](https://ieeexplore.ieee.org/document/8933771)." In 2019 IEEE 27th International Requirements Engineering Conference Workshops (REW), pp. 241-244. IEEE, 2019.

> Idea paper that outlines a path of how requirements engineering can be useful in better understanding domain and context of a problem and how this helps in better curating a high-quality dataset for training and also how to drive validation of the model. Uses a running vision example of pedestriant detection.

Corbett-Davies, Sam, and Sharad Goel. "[The measure and mismeasure of fairness: A critical review of fair machine learning](https://arxiv.org/abs/1808.00023)." arXiv preprint arXiv:1808.00023 (2018).

> A comprehensive an critical discussion of different fairness measures often discussed in the ML community. It's kind of depressing how many different notions and problems there are and how few solutions. Even though they don't discuss requirements engineering in the paper, I put it here because it shows the complicated mess that fairness makes when trying to identify the right fairness requirements for an ML-enabled system. A requirements engineer must work with stakeholders to identify suitable requirements and make a lot of decisions, which won't be easy but will be necessary. This paper will probably give the requirements engineer the right vocabulary to talk to ML experts who need to assure the requirement and will provide enough pointers to identify what issues to probe for when talking to stakeholders.

Holstein, Kenneth, Jennifer Wortman Vaughan, Hal Daumé III, Miro Dudik, and Hanna Wallach. "[Improving fairness in machine learning systems: What do industry practitioners need?](http://users.umiacs.umd.edu/~hal/docs/daume19fairness.pdf)" In Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems, pp. 1-16. 2019.

> An interview study with engineers that consider fairness in their ML-enabled products. This one looks at the system/software-engineering level, beyond narrow fairness properties at the model level and discusses problems and strategies broadly, including fairness considerations across all lifecycle stages, possible checklists, best practices, holistic auditing, possibly even resulting in changes in system design. It does not mention requirements, but many issues are deeply rooted in requirements engineering and system design work.

Madaio, Michael A., Luke Stark, Jennifer Wortman Vaughan, and Hanna Wallach. "[Co-Designing Checklists to Understand Organizational Challenges and Opportunities around Fairness in AI](http://www.jennwv.com/papers/checklists.pdf)." In Proceedings of the 2020 CHI Conference on Human Factors in Computing Systems, pp. 1-14. 2020.

> Another great paper that looks at requirements engineering for fairness in production ML systems in practice. It looks at challenges and suggest a checklist. It argues that it's really all about the process integration and about taking a system level view (rather than focusing on model properties). Includes the actual checklist.

Kulynych, Bogdan, Rebekah Overdorf, Carmela Troncoso, and Seda Gürses. "[POTs: protective optimization technologies](https://arxiv.org/abs/1806.02711)." In Proceedings of the 2020 Conference on Fairness, Accountability, and Transparency, pp. 177-188. 2020.

> This is the only ML paper I have seen that explicitly discusses requirements engineering with Jackson's world vs machine framing. It nicely frames the fairness problem as a system problem and explicitly discusses the interface between the environment and the implementation's specification and how assuring fairness only at the model level is insufficient. The rest of the paper, then essentially suggests adversarial hacking through changes in the environment to drive the model to make fairer or globally better decisions -- that is, distributing the problem, affected people can increase the cost of certain outcomes thus making an ML system recommend other outcomes that are more benefitial to them. Interesting position paper, even if just for the framing in Sec 2.

## Software Architecture and Design

Washizaki, Hironori, Hiromu Uchida, Foutse Khomh, and Yann-Gaël Guéhéneuc. "[Machine Learning Architecture and Design Patterns](http://www.washi.cs.waseda.ac.jp/wp-content/uploads/2019/12/IEEE_Software_19__ML_Patterns.pdf)." Paper draft under review, 2019

> A useful collection of design patterns, architectural patterns, and anti-patterns derived from a literature survey of 19 papers and 19 grey literature articles. Not a detailed discussion and no detailed pattern description, but pointers to the sources, a list of patterns names, and an overview of their relations, that are likely useful for further exploration and discussions, see their [web site](http://www.washi.cs.waseda.ac.jp/ml-patterns/). Many of the patterns seem to relate more to big-data processing than ML, but are likely useful when building ML-enabled systems. 

Daniel Smith. "[Exploring Development Patterns in Data Science](https://www.theorylane.com/2017/10/20/some-development-patterns-in-data-science/)." TheoryLane Blog Post. 2017.

> Short blog post arguing to decompose ML pipeline from a single notebook into multiple services using cloud infrastructure. Bit polemic but well argued, short opinion piece.


## Process

Studer, Stefan, Thanh Binh Bui, Christian Drescher, Alexander Hanuschkin, Ludwig Winkler, Steven Peters, and Klaus-Robert Mueller. "[Towards CRISP-ML (Q): A Machine Learning Process Model with Quality Assurance Methodology](https://arxiv.org/abs/2003.05155)." arXiv preprint arXiv:2003.05155 (2020).

> Fairly detailed overview of an ML-development process, starting early with business needs and covering all steps to deployment. Not necessarily new or grounded in new data, but a very nice and well-written overview. Good early reading to understand the full scope of SE4ML, beyond just building models.

Serban, Alex, Koen van der Blom, Holger Hoos, and Joost Visser. "[Adoption and Effects of Software Engineering Best Practices in Machine Learning](https://arxiv.org/pdf/2007.14130)." In Proc. ACM/IEEE International Symposium on Empirical Software Engineering and Measurement (2020).

> Collection of best practices, mostly focused on the model pipeline not the larger system. In a larger survey, practitioners indicate which practices they follow, resulting in interesting ranks in Table 2. Results show that MLOps topics like versioning, monitoring and experiment management are fairly broadly adopted, whereas quality assurance practices and hyperparameter tuning are less adopted.

## Safety & Robustness

*There is a significant amount of machine learning research on safety and security, especially on narrow properties of robustness, but also some system-level discussions on safeguard mechanisms. A software engineering professional should probably understand the tools and techniques.*

Borg, Markus, Cristofer Englund, Krzysztof Wnuk, Boris Duran, Christoffer Levandowski, Shenjian Gao, Yanwen Tan, Henrik Kaijser, Henrik Lönn, and Jonas Törnqvist. "[Safely entering the deep: A review of verification and validation for machine learning and a challenge elicitation in the automotive industry](https://www.atlantis-press.com/journals/jase/125905766)." Journal of Automotive Software Engineering. Volume 1, Issue 1, Pages 1 - 19. 2019

> Summary of the current thinking about safety of ML components in self-driving cars, based on literature review, a survey, and several industry workshops. Provides a decent overview from an engineering perspective, providing pointers to a long history of ML-related safety work in aerospace and automotive research that is likely a good starting point for further exploration. Mostly fairly high-level; among others, emphasizes the system nature of the problem and ideas with regard to design strategies for safety, such as safety cages and fail-safe systems.

Salay, Rick, Rodrigo Queiroz, and Krzysztof Czarnecki. "[An analysis of ISO 26262: Using machine learning safely in automotive software](https://arxiv.org/pdf/1709.02435)." *arXiv preprint arXiv:1709.02435* (2017).

Salay, Rick, and Krzysztof Czarnecki. "[Using machine learning safely in automotive software: An assessment and adaption of software process requirements in ISO 26262](https://arxiv.org/pdf/1808.01614)." *arXiv preprint arXiv:1808.01614* (2018).

> The first provides a decent overview of safety thinking at the system level in the automotive industry and how that thinking aligns with current safety standards. While it does not go into specific safety techniques, it shows the overall mindset and the relevant concerns. The second, longer report goes more in into details and provides several concrete architectural patterns (esp. Sec 7).

Singh, Gagandeep, Timon Gehr, Markus Püschel, and Martin Vechev. "[An abstract domain for certifying neural networks](https://dl.acm.org/doi/pdf/10.1145/3290354)." Proceedings of the ACM on Programming Languages 3, no. POPL (2019): 1-30.

> (Discussed also above under model invariants) This is an example of a large group of paper that determines whether all pertubations of an input within a certain bound all produce the same prediction. The search space by these pertubations and their combinations is typically very large and formal methods are used to produce conservative results (i.e., when it reports robustness against these pertubations it actually guaranteed to always return the same prediction, but there can be false positives). This is one of the more readable papers in this area that I have seen, but I'm not aware of any paper that really discusses how to use these robustness guarantees in production (typical scenarios seem to be to test robustness for a training set, for a set of important test cases, or to test it at runtime to make sure that a specific result is not just caused by a pertubation) and whether the considered pertubations are relevant or interesing for practical cases.


Cohen, Jeremy M., Elan Rosenfeld, and J. Zico Kolter. "[Certified adversarial robustness via randomized smoothing](https://arxiv.org/abs/1902.02918)." In Proc. International Conference on Machine Learning, p. 1310--1320, 2019.

> Discusses *randomized smoothing*, an interesting approach to evaluating robustness: Sample predictions not only about a specific input but also about perturbed versions of that input around that input and report the most common prediction as the result. As a consequence, the prediction will be less sensitive to minor changes in the input. Black box technique that works for any kind of model. If sampled frequently enough, as discussed in the paper, also probabilistic bounds can be provided, although at significant computational costs (they use 100K model inferences per input).

## Security & Privacy

Huang, Ling, Anthony D. Joseph, Blaine Nelson, Benjamin IP Rubinstein, and J. Doug Tygar. "[Adversarial machine learning](http://people.cs.vt.edu/~gangwang/class/cs6604/papers/Adversarial_AISEC.pdf)." In *Proceedings of the 4th ACM Workshop on Security and Artificial Intelligence*, pp. 43-58. 2011.

> Broad overview of security and privacy concerns (with examples of SVNs, predates DNN). Illustrates concerns quite well with two running examples of spam detection and network traffic analysis. Focuses on the model only.

Liu, Qiang, Pan Li, Wentao Zhao, Wei Cai, Shui Yu, and Victor CM Leung. "[A survey on security threats and defensive techniques of machine learning: A data driven view](https://www.researchgate.net/profile/Qiang_Liu14/publication/323154427_A_Survey_on_Security_Threats_and_Defensive_Techniques_of_Machine_Learning_A_Data_Driven_View/links/5a92b6e345851535bcd84848/A-Survey-on-Security-Threats-and-Defensive-Techniques-of-Machine-Learning-A-Data-Driven-View.pdf)." *IEEE access* 6 (2018): 12103-12117.

> Fairly accessible survey on security threats and defense techniques, providing a decent overview. Focus on the model itself.

## Reproducibility, Provenance

Halevy, Alon, Flip Korn, Natalya F. Noy, Christopher Olston, Neoklis Polyzotis, Sudip Roy, and Steven Euijong Whang. "[Goods: Organizing Google's datasets](https://dl.acm.org/doi/pdf/10.1145/2882903.2903730)." In Proceedings of the 2016 International Conference on Management of Data, pp. 795-806. 2016.

> This is a neat paper describing how data dependencies can be extracted
automatically from log files at Google. While the solution probably does
not generalize to many smaller organizations, the problem description
is well done and the solution is interesting. 


## Computational Notebooks

*There is quite a bit of work on computational notebooks recently, mostly 
focused on the exploratory work that data scientists perform. Some of this
is focused on poor software engineering practices, e.g., with regard to
testing, modularity, reuse, versioning, dependency management, and determinism.*

Pimentel, Joao Felipe, Leonardo Murta, Vanessa Braganholo, and Juliana Freire. "[A large-scale study about quality and reproducibility of Jupyter notebooks](http://www2.ic.uff.br/~leomurta/papers/pimentel2019a.pdf)." In 2019 IEEE/ACM 16th International Conference on Mining Software Repositories (MSR), pp. 507-517. IEEE, 2019.

> Interesting mining repository exploration of Jupyter notebooks on GitHub, finding among others that many cannot be reproduced


Psallidas, Fotis, Yiwen Zhu, Bojan Karlas, Matteo Interlandi, Avrilia Floratou, Konstantinos Karanasos, Wentao Wu et al. "[Data Science through the looking glass and what we found there](https://arxiv.org/pdf/1912.09536.pdf)." arXiv preprint arXiv:1912.09536 (2019).

> Similar study of notebooks, but at much larger scales, including 6 million notebooks from GitHub and 2 million from Microsoft. Lots of statistics on usage and trends, sometimes a bit shallow but at a massive scale: for example, that most notebooks use only few libraries, that there are huge numbers of notebook authors, and that static analysis seems feasible.


Kery, Mary Beth, Marissa Radensky, Mahima Arya, Bonnie E. John, and Brad A. Myers. "[The story in the notebook: Exploratory data science using a literate programming tool](https://dl.acm.org/doi/pdf/10.1145/3173574.3173748)." In Proceedings of the 2018 CHI Conference on Human Factors in Computing Systems, pp. 1-11. 2018.

> Interview study with Jupyter users to understand their practices and challenges, highlighting especially the exploratory nature and the challenges with regard to cleaning up work and versioning. Subsequent work by the same authors suggested versioning tooling.

Chattopadhyay, Souti, Ishita Prasad, Austin Z. Henley, Anita Sarma, and Titus Barik. "[What’s Wrong with Computational Notebooks? Pain Points, Needs, and Design Opportunities](https://web.eecs.utk.edu/~azh/pubs/Chattopadhyay2020CHI_NotebookPainpoints.pdf)." In Proceedings of the CHI Conference on Human Factors in Computing Systems, 2020.

> An interesting and very useful study about pain points in using Notebooks, mostly through interviews and short-term field observations, followed up with a mid-sized survey. Lots of interesting insights about day-to-day problems, including large challenges due to poor tool support, scalability challenges, lack of refactoring, difficulty sharing and deploying work.


Kandel, Sean, Andreas Paepcke, Joseph M. Hellerstein, and Jeffrey Heer. "[Enterprise data analysis and visualization: An interview study](http://vis.stanford.edu/files/2012-EnterpriseAnalysisInterviews-VAST.pdf)." IEEE Transactions on Visualization and Computer Graphics 18, no. 12 (2012): 2917-2926.

> Earlier work on problems that data scientists have (here data scientists seem to work more on reporting, less on software teams). Not only covering notebooks, but similar results to the more recent studies: Tracking rationale in exploratory programming is a key challenge, no abstraction, little reuse, negative results get lost; data scientists have different profiles from developers but often work with them; data scientists rarely collaborate with other data scientists.

Head, Andrew, Fred Hohman, Titus Barik, Steven M. Drucker, and Robert DeLine. "[Managing messes in computational notebooks](https://dl.acm.org/doi/pdf/10.1145/3290605.3300500)." In Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems, pp. 1-12. 2019.

> Nice project to provide tool support for Jupyter notebooks, creating dependency graphs and using static slicing to clean notebooks.

Liu, Jiali, Nadia Boukhelifa, and James R. Eagan. 2019. “[Understanding the Role of Alternatives in Data Analysis Practices](https://doi.org/10.1109/TVCG.2019.2934593).” IEEE Transactions on Visualization and Computer Graphics, August.

> Interview study to understand how data scientists explore variations when developing models. Useful context to understand how data scientists operate.

Matthew Seal, Kyle Kelley, and Michelle Ufford. "[Part 2: Scheduling Notebooks at Netflix](https://netflixtechblog.com/scheduling-notebooks-348e6c14cfd6?gi=4c5ad1d3f7f)." Netflix Technology Blog. 2018

> At least I find it rather surprising to use Notebooks for automation in production. Might be an interesting architectural and infrastructure decision worth discussing.

## Human-AI Interaction

*This area is interesting and has seen significant attention recently, but goes beyond my typical software engineering considerations. See the [Human-AI Interaction](http://www.humanaiclass.org/) class at CMU for more pointers.*

Kocielnik, Rafal, Saleema Amershi, and Paul N. Bennett. "Will you accept an imperfect AI? Exploring designs for adjusting end-user expectations of AI systems." In *Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems*, pp. 1-14. 2019.

> Cool mturk-style study to explore different means of setting expectations for users that the ML predictions of the system might be occasionally wrong. This is useful to think at the system level about mitigations for incorrect predictions, here focusing on how to present them to users. Discusses three concrete UI designs for a realistic setting (scheduling assistant).

## Interdisciplinary teams

Kim, Miryung, Thomas Zimmermann, Robert DeLine, and Andrew Begel. "[Data scientists in software teams: State of the art and challenges](https://doi.org/10.1109/tse.2017.2754374)." IEEE Transactions on Software Engineering 44, no. 11 (2017): 1024-1038.

> Discusses the role of data scientists and their challenges through interviews and surveys. See also the subsequent Amershi paper for a more ML-specific view.

Ryan Orban. "[Bridging the Gap Between Data Science & Engineer: Building High-Performance Teams](https://www.slideshare.net/ryanorban/bridging-the-gap-between-data-science-engineer-building-highperformance-teams)." Presentation 2016

> Short presentation about the different roles of data scientists and software engineers and how to build interdisciplinary teams. Matches very closely my view of software engineering for AI-enabled systems, in that we still need data scientists and software engineers (and operators, and ...) as separate disciplines, but that we need a Devops-like integration around a common understanding and a joint mission.



## Misc

*Various recommended and useful resources that do not fit well into the other categories.*

Zinkevich, Martin. 2017 “[Rules of Machine Learning: Best Practices for ML Engineering](http://martin.zinkevich.org/rules_of_ml/rules_of_ml.pdf).”

> Blog post. List of advice about engineering ML-enabled systems based on experience at Google. Many good pointers.

Sculley, D., Matthew Eric Otey, Michael Pohl, Bridget Spitznagel, John Hainsworth, and Yunkai Zhou. 2011. “[Detecting Adversarial Advertisements in the Wild](https://doi.org/10.1145/2020408.2020455).” Proceedings of the 17th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining - KDD ’11.

> Nice case study paper from a team at Google that explicitly discusses the various challenges of building an ML-based system that go beyond just the modeling part, including issues like automatic calibration, composing many models, and teamwork in interdisciplinary teams. Include an architecture diagram. Despite some vagueness, we use it in class as a case study to show the importance of software engineering in ML projects.

Sendak, Mark P., William Ratliff, Dina Sarro, Elizabeth Alderton, Joseph Futoma, Michael Gao, Marshall Nichols et al. "[Real-World Integration of a Sepsis Deep Learning Technology Into Routine Clinical Care: Implementation Study](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7391165/)." *JMIR medical informatics* 8, no. 7 (2020): e15182.

> Another case study I like and which use in class to discuss the system nature of machine-learning project. The paper mostly focuses on organizational and requirements aspects of building and deploying an ML-enabled system, with relatively little details on the actual model training.

Géron, Aurélien. "[Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow: Concepts, Tools, and Techniques to Build Intelligent Systems](https://learning.oreilly.com/library/view/hands-on-machine-learning/9781492032632/)". 2nd Edition, O'Reilly Media, 2019.

> One of many books explaining how various machine-learning techniques (including a quite extensive treatment of deep learning), and also shows pragmatically how to use the corresponding techniques with various libraries. Spends about half a page talking very superficially about deployment and evaluation in production (Section "Launch, Monitor, and Maintain Your System"), but is otherwise squarely in the data science camp. Overall accessible and quite detailed introduction that invites to immediate play with some datasets and build some models.

Polyzotis, Neoklis, Sudip Roy, Steven Euijong Whang, and Martin Zinkevich. "[Data lifecycle challenges in production machine learning: a survey](https://dl.acm.org/doi/pdf/10.1145/3299887.3299891)." ACM SIGMOD Record 47, no. 2 (2018): 17-28.

> Essay/position paper with many pointers from the Tensorflow team. Key message is that ML can learn from data management community. Interesting, but not very deep and the survey part seems ad-hoc.


Arpteg, Anders, Björn Brinne, Luka Crnkovic-Friis, and Jan Bosch. "[Software engineering challenges of deep learning](https://ieeexplore.ieee.org/iel7/8496898/8498147/08498185.pdf)." In 2018 44th Euromicro Conference on Software Engineering and Advanced Applications (SEAA), pp. 50-59. IEEE, 2018.

> Discussion of SE challenges in deep learning projects. Useful list of challenges, apparently grounded in interviews with engineers in 7 projects. The discussion remains rather abstract with little explicit grounding in the interview data.

Hermann, Jeremy, Mike Del Balso, Rene Schmidt, and Jakob Holdgaard Thomsen. 2017. “[Meet Michelangelo: Uber’s Machine Learning Platform](https://eng.uber.com/michelangelo-machine-learning-platform/).” Uber Engineering Blog. September 5, 2017. .

> Interesting blog post about the ML infrastructure at Uber and the challenges of building production systems.


Patel, Kayur, James Fogarty, James A. Landay, and Beverly Harrison. "[Investigating statistical machine learning as a tool for software development](http://www.kayur.org/papers/chi2008.pdf)." In Proceedings of the SIGCHI Conference on Human Factors in Computing Systems, pp. 667-676. 2008.

> Early paper on how data science practices are different from software engineering practices (pre notebook days), finding how iterative and exploratory programming are pervasive. Emphasizes the difficulty of understanding features, evaluating quality, and a lack of tooling for iterative/exploratory programming. Fig 3 is pretty cool, showing how participants in their experiments incrementally improved accuracy of their models.


O'Leary, Katie, and Makoto Uchida. "[Common problems with Creating Machine Learning Pipelines from Existing Code](https://research.google/pubs/pub48984.pdf)." Proc. Third Conference on Machine Learning and Systems (MLSys) (2020).

> Short paper describing experience from Google's customer workshops with where developers struggle building ML systems. Key results: Need a mindset that focuses on pipelines not models and need to develop best practices and reusable patterns/fragments/abstractions that can be composed in pipelines.

Rudin, Cynthia. "[Stop explaining black box machine learning models for high stakes decisions and use interpretable models instead](https://arxiv.org/pdf/1811.10154)." Nature Machine Intelligence 1, no. 5 (2019): 206-215.

> Interesting (potentially controversial) position paper emphasizing the difference between interpretability and explainability in machine learning. Argues that in many cases simple and interpretable models may perform similarly well to opaque models.

Kleppmann, Martin. “[Designing data-intensive applications: The big ideas behind reliable, scalable, and maintainable systems](https://dataintensive.net/).” O'Reilly Media, Inc., 2017.

> Excellent book about distributed and big data systems. Not directly related to machine learning, but covers fundamentals of data storage and data processing (batch, stream, ...) at scale. Excellent discussion of principles and tradeoffs.

Strubell, Emma, Ananya Ganesh, and Andrew McCallum. "[Energy and Policy Considerations for Deep Learning in NLP](https://arxiv.org/pdf/1906.02243.pdf)." In *Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics*, pp. 3645-3650. 2019.

> Short paper illustrating very clearly the computation cost and environmental impact of training deep neural networks (esp. with hyperparameter optimization). Makes a strong argument that these costs should be considered when designing models or systems.

## Others with notes

*Not necessarily papers and books I recommend, but they may be of interest for specific concerns.*

Smith, Jeff. Machine Learning Systems: Designs that Scale. Manning Publications Co., 2018.

> Book on building scalable machine learning systems. Focuses on elastic/reactive system design and suggests specific design decisions, such as working with immutable data. Many concrete implementation examples given in Scala. The book is very readable but opinionated and somewhat narrow and low level. It describes specific implementation patterns for design solutions it suggests, but it definitively reflects on tradeoffs and software engineering concerns.

Stoica, Ion, Dawn Song, Raluca Ada Popa, David Patterson, Michael W. Mahoney, Randy Katz, Anthony D. Joseph et al. "[A Berkeley view of systems challenges for AI](https://arxiv.org/pdf/1712.05855)." arXiv:1712.05855 (2017).

> High-level position paper, often focused on robotics.

Kanewala, Upulee, and James M. Bieman. 2014. “[Testing Scientific Software: A Systematic Literature Review](https://arxiv.org/pdf/1804.01954).” Information and Software Technology 56 (10): 1219–32.

> Survey on testing techniques, covering also approaches for testing systems without oracles, some of which apply to ML. 

Zhang, Mengshi, Yuqun Zhang, Lingming Zhang, Cong Liu, and Sarfraz Khurshid. "[DeepRoad: GAN-based metamorphic testing and input validation framework for autonomous driving systems](https://www.researchgate.net/profile/Yuqun_Zhang2/publication/327122887_DeepRoad_GAN-based_metamorphic_testing_and_input_validation_framework_for_autonomous_driving_systems/links/5dea272e299bf10bc343e530/DeepRoad-GAN-based-metamorphic-testing-and-input-validation-framework-for-autonomous-driving-systems.pdf)." In Proceedings of the 33rd ACM/IEEE International Conference on Automated Software Engineering, pp. 132-142. 2018.

> Practical application of metamorphic testing for generating test cases

Zhou, Hucheng, Jian-Guang Lou, Hongyu Zhang, Haibo Lin, Haoxiang Lin, and Tingting Qin.  "[An Empirical Study on Quality Issues of Production Big Data Platform](https://doi.org/10.1109/icse.2015.130)." IEEE/ACM 37th IEEE International Conference on Software Engineering. 2015

> Study of operational issues of large map reduce cluster. Mostly hardware failures not captured by redundancy mechanisms. No direct ML aspect, but useful for discussing large distributed ML jobs at scale and some discussion of debugging from logging data.

Chen, Zhenpeng, Yanbin Cao, Yuanqiang Liu, Haoyu Wang, Tao Xie, and Xuanzhe Liu. "[Understanding Challenges in Deploying Deep Learning Based Software: An Empirical Study](https://arxiv.org/pdf/2005.00760)." Proc. FSE (2020).

> Another StackOverflow study, this time focused on questions that developers ask regarding deploying deep learning models. Mostly API/documentation style questions close to the model rather than broader system deployment or MLOps questions and fairly shallow insights, but still potentially useful to see what developers struggle with current infrastructure at the API level. 

Lwakatare, Lucy Ellen, Aiswarya Raj, Jan Bosch, Helena Holmström Olsson, and Ivica Crnkovic. "[A taxonomy of software engineering challenges for machine learning systems: An empirical investigation](https://research.chalmers.se/publication/512250/file/512250_Fulltext.pdf)." In *International Conference on Agile Software Development*, pp. 227-243. Springer, 2019.

> Brief discussion of 7 case studies, mostly finding MLOps-style problems. The paper concludes with a potentially interesting maturity model (Sec 5), that, while not visibly grounded in data, may be a good starting point for discussions for framing different kinds of ML projects.

Wan, Zhiyuan, Xin Xia, David Lo, and Gail C. Murphy. "[How does machine learning change software development practices?](https://core.ac.uk/download/pdf/275589732.pdf)" *IEEE Transactions on Software Engineering* (2019).

> Discussion of challenges in developing ML systems based on interviews and a survey. Unfortunately, the paper does not distinguish consistently between the ML model, the framework used to learn the model, and the the system with an ML component, nor does it clearly distinguish between roles of software engineers or data scientists, leading to rather murky and questionable claims.

## Other Lists

Miryung Kim has been teaching seminars at UCLA on debugging and data science/ML that is a great source for recommended readings as well, see http://web.cs.ucla.edu/~miryung/teaching/CS239-Winter2017/main.xhtml and http://web.cs.ucla.edu/~miryung/teaching/CS239-Winter2019/main.xhtml

Pooyan Jamschidi is teaching "Machine Learning Systems" a UofSC and recommended several readings to me when preparing for my course: https://pooyanjamshidi.github.io/mls/

Larysa Visengeriyeva has assembled an amazing list of resources on MLOps and related topics (books, talks, blog posts): https://github.com/visenger/mlops-references
