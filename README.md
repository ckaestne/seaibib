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
> Pro tip: A google scholar alert for
citations to this paper is a good way to notice new SE4ML publications.

Amershi, Saleema, Andrew Begel, Christian Bird, Robert DeLine, Harald Gall, Ece Kamar, Nachiappan Nagappan, Besmira Nushi, and Thomas Zimmermann. "[Software engineering for machine learning: A case study](https://andrewbegel.com/papers/Software_Engineering_for_ML.pdf)." In 2019 IEEE/ACM 41st International Conference on Software Engineering: Software Engineering in Practice (ICSE-SEIP), pp. 291-300. IEEE, 2019. https://doi.org/10.1109/icse-seip.2019.00042.

> A good description of the SE4ML challenges at Microsoft, characterizing
the challenges of different roles and grounded in interviews and a large
scale survey. Motivating well how pervasive ML is in modern systems and describing 
best practices and some challenges.


## Testing

*There is a lot of work that covers testing ML systems in some form, most
of it seems focused on fairly narrow properties of a model. Testing an ML-enabled
system should be much broader, including system testing and testing of 
the infrastructure (e.g., learning pipeline and update mechanisms) and
testing in production.*

Breck, Eric, Shanqing Cai, Eric Nielsen, Michael Salib, and D. Sculley. 2017. “The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction.” 2017 IEEE International Conference on Big Data (Big Data). https://doi.org/10.1109/bigdata.2017.8258038.

> Nice position paper that discusses the many different aspects of quality assurance in an ML project, beyond just model and data quality. Includes some examples and a checklist of QA steps to consider. Good introduction to the problem and based on practical experience at Google. (Note this is a slightly extended version from a similarly titled paper)


Tang, Diane, Ashish Agarwal, Deirdre O'Brien, and Mike Meyer. "[Overlapping experiment infrastructure: More, better, faster experimentation](https://dl.acm.org/doi/pdf/10.1145/1835804.1835810)." In Proceedings of the 16th ACM SIGKDD international conference on Knowledge discovery and data mining, pp. 17-26. 2010.

Bakshy, Eytan, Dean Eckles, and Michael S. Bernstein. "[Designing and deploying online field experiments](https://dl.acm.org/doi/pdf/10.1145/2566486.2567967)." In Proceedings of the 23rd international conference on World wide web, pp. 283-292. 2014.



> Two papers discussing infrastructure for A/B testing (which is a good foundation and frequently used for testing ML systems in production) at Google and Facebook. More focused on infrastructure around it, but useful for getting into a discussion on how to test in production.

Zhang, Jie M., Mark Harman, Lei Ma, and Yang Liu. 2019. “[Machine Learning Testing: Survey, Landscapes and Horizons](http://arxiv.org/abs/1906.10742).” arXiv [cs.LG]. arXiv. 

> Broad survey on testing in machine learning. Includes many pointers, including different test strategies and different kinds of testing. While the pointers are useful, I was frustrated with many descriptions, definitions, and classifications and find little synthesis in this paper; e.g., I was hoping for clearer definitions of "ML bug", "data bug" or a clear discussion of specifications. Grey literature is not discussed either.


### (Model Invariants)

Xie, Xiaoyuan, Joshua WK Ho, Christian Murphy, Gail Kaiser, Baowen Xu, and Tsong Yueh Chen. "[Testing and validating machine learning classifiers by metamorphic testing](https://www.sciencedirect.com/science/article/pii/S0164121210003213)." Journal of Systems and Software 84, no. 4 (2011): 544-558.

> This paper discusses the idea of metamorphic testing. The key idea is that in the absence of a specification about what the model should do (which is the whole point of using ML), we might still be able to give partial specifications in terms of invariants about how outputs should relate for input pairs. For example, robustness conditions might be expressed by indicating that similar inputs should produce the same output or that linearly scaling all features or adding irrelevant features should not affect the outcome for certain classifiers. This is an interesting direction that enables testing of a number of invariants for ML models (there are several papers by Murphy and Kaiser on this topic).


Ribeiro, Marco Tulio, Sameer Singh, and Carlos Guestrin. "[Semantically equivalent adversarial rules for debugging NLP models](https://www.aclweb.org/anthology/P18-1079.pdf)." In Proceedings of the 56th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), pp. 856-865. 2018.

> Example of testing for invariants in NLP models (in line with metamorphic testing, even though they do not refer to that concept). Here one expects certain linguistic invariants, for example, replacing "isn't" by "is not" should not change the outcome. These invariants are used to derive and prioritize tests and to then improve the model with more input data.

Singh, Gagandeep, Timon Gehr, Markus Püschel, and Martin Vechev. "[An abstract domain for certifying neural networks](https://dl.acm.org/doi/pdf/10.1145/3290354)." Proceedings of the ACM on Programming Languages 3, no. POPL (2019): 1-30.

> This is an example of a large group of paper that proofs specific invariants about models. For example, the specification could be that a model is robust to certain changes to its inputs (e.g., changing the brightness of pixels by +/- 20%) on the training set or certain classes of inputs. In contrast to much testing work, here results are verified over all input changes covered by a specification.

Galhotra, Sainyam, Yuriy Brun, and Alexandra Meliou. "[Fairness testing: testing software for discrimination](https://dl.acm.org/doi/pdf/10.1145/3106237.3106277)." In Proceedings of the 2017 11th Joint Meeting on Foundations of Software Engineering, pp. 498-510. 2017.

> Another application of testing invariants (here, for fairness certain outputs should be independent of changes to sensitive attributes). Fairly straightforward and limited to group fairness if I recall correctly.


Ding, J., D. Zhang, and X. Hu. 2016. “[A Framework for Ensuring the Quality of a Big Data Service](https://ieeexplore.ieee.org/iel7/7557343/7557418/07557439.pdf).” In 2016 IEEE International Conference on Services Computing (SCC), 82–89.

> Another example of using metamorphic testing, using domain knowledge about the problem to come up with invariants. Nice concrete example, though not the easiest read.


### (Testing ML Frameworks)

Srisakaokul, Siwakorn, Zhengkai Wu, Angello Astorga, Oreoluwa Alebiosu, and Tao Xie. "[Multiple-implementation testing of supervised learning software](https://www.aaai.org/ocs/index.php/WS/AAAIW18/paper/viewPDFInterstitial/17301/15599)." In Workshops at the Thirty-Second AAAI Conference on Artificial Intelligence. 2018.

> Good example of a paper that tests the implementation of the ML algorithm (not the model or resulting system). Here differential testing is used to compare multiple student implementations. Nice demonstration of the idea, though it is not clear how far this would be practical beyond fairly simple learning algorithms implemented in student projects.


### (Other Testing Work)


Pei, Kexin, Yinzhi Cao, Junfeng Yang, and Suman Jana. "[DeepXplore: Automated whitebox testing of deep learning systems](https://doi.org/10.1145/3132747.3132785.)." In proceedings of the 26th Symposium on Operating Systems Principles, pp. 1-18. 2017. 

> Differential testing between multiple models (e.g., learned from the same data with different parameters) and input generation that aims to identify inputs that have different outputs across the models. Unclear to me how useful this would be in practice.


Zhang, Yuhao, Yifan Chen, Shing-Chi Cheung, Yingfei Xiong, and Lu Zhang. "[An empirical study on TensorFlow program bugs](https://doi.org/10.1145/3213846.3213866)." In Proceedings of the 27th ACM SIGSOFT International Symposium on Software Testing and Analysis, pp. 129-140. 2018.

Zhang, Tianyi, Cuiyun Gao, Lei Ma, Michael R. Lyu, and Miryung Kim. "[An empirical study of common challenges in developing deep learning applications](http://web.cs.ucla.edu/~miryung/Publications/isese2019-deeplearningchallenge.pdf)." In The 30th IEEE International Symposium on Software Reliability Engineering (ISSRE). 2019.

> These two papers are examples of papers that analyzes public bug reports from issue trackers or question-answer sites (stackoverflow) for machine-learning frameworks. They characterize the kinds of problems developers and users tend to have, some some solutions. Many issues seem to be common framework issues, such as documentation issues and breaking APIs. Some challenges, such as probabilistic correctness and missing debuggers, seem more ML specific.


## Debugging

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

Head, Andrew, Fred Hohman, Titus Barik, Steven M. Drucker, and Robert DeLine. "[Managing messes in computational notebooks](https://dl.acm.org/doi/pdf/10.1145/3290605.3300500)." In Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems, pp. 1-12. 2019.

> Nice project to provide tool support for Jupyter notebooks, creating dependency graphs and using static slicing to clean notebooks.

Liu, Jiali, Nadia Boukhelifa, and James R. Eagan. 2019. “[Understanding the Role of Alternatives in Data Analysis Practices](https://doi.org/10.1109/TVCG.2019.2934593).” IEEE Transactions on Visualization and Computer Graphics, August.

> Interview study to understand how data scientists explore variations when developing models. Useful context to understand how data scientists operate.


## Interdisciplinary teams

Kim, Miryung, Thomas Zimmermann, Robert DeLine, and Andrew Begel. "[Data scientists in software teams: State of the art and challenges](https://doi.org/10.1109/tse.2017.2754374)." IEEE Transactions on Software Engineering 44, no. 11 (2017): 1024-1038.



> Discusses the role of data scientists and their challenges through interviews and surveys. See also the subsequent Amershi paper for a more ML-specific view.



## Misc

Zinkevich, Martin. 2017 “[Rules of Machine Learning: Best Practices for ML Engineering](http://martin.zinkevich.org/rules_of_ml/rules_of_ml.pdf).”

> Blog post. List of advice about engineering ML-enabled systems based on experience at Google. Many good pointers.

Sculley, D., Matthew Eric Otey, Michael Pohl, Bridget Spitznagel, John Hainsworth, and Yunkai Zhou. 2011. “[Detecting Adversarial Advertisements in the Wild](https://doi.org/10.1145/2020408.2020455).” Proceedings of the 17th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining - KDD ’11.

> Nice case study paper from a team at Google that explicitly discusses the various challenges of building an ML-based system that go beyond just the modeling part, including issues like automatic calibration, composing many models, and teamwork in interdisciplinary teams. Include an architecture diagram. Despite some vagueness, we use it in class as a case study to show the importance of software engineering in ML projects.

Polyzotis, Neoklis, Sudip Roy, Steven Euijong Whang, and Martin Zinkevich. "[Data lifecycle challenges in production machine learning: a survey](https://dl.acm.org/doi/pdf/10.1145/3299887.3299891)." ACM SIGMOD Record 47, no. 2 (2018): 17-28.

> Essay/position paper with many pointers from the Tensorflow team. Key message is that ML can learn from data management community. Interesting, but not very deep and the survey part is adhoc.


Arpteg, Anders, Björn Brinne, Luka Crnkovic-Friis, and Jan Bosch. "[Software engineering challenges of deep learning](https://ieeexplore.ieee.org/iel7/8496898/8498147/08498185.pdf)." In 2018 44th Euromicro Conference on Software Engineering and Advanced Applications (SEAA), pp. 50-59. IEEE, 2018.

> Discussion of SE challenges in deep learning projects. Useful list of challenges, apparently grounded in interviews with engineers in 7 projects. The discussion remains rather abstract with little explicit grounding in the interview data.

Stoica, Ion, Dawn Song, Raluca Ada Popa, David Patterson, Michael W. Mahoney, Randy Katz, Anthony D. Joseph et al. "[A Berkeley view of systems challenges for AI](https://arxiv.org/pdf/1712.05855)." arXiv:1712.05855 (2017).

> High-level position paper, often focused on robotics.

Hermann, Jeremy, Mike Del Balso, Rene Schmidt, and Jakob Holdgaard Thomsen. 2017. “Meet Michelangelo: Uber’s Machine Learning Platform.” Uber Engineering Blog. September 5, 2017. https://eng.uber.com/michelangelo/.

> Interesting blog post about the ML infrastructure at Uber and the challenges of building production systems.




## Others with notes

Smith, Jeff. Machine Learning Systems: Designs that Scale. Manning Publications Co., 2018.

> Book on building scalable machine learning systems. Focuses on elastic/reactive system design and suggests specific design decisions, such as working with immutable data. Many concrete implementation examples given in Scala. The book is very readable but opinionated and somewhat narrow and low level. It describes specific implementation patterns for design solutions it suggests, but it definitively reflects on tradeoffs and software engineering concerns.

Kanewala, Upulee, and James M. Bieman. 2014. “Testing Scientific Software: A Systematic Literature Review.” Information and Software Technology 56 (10): 1219–32.

> Survey on testing techniques, covering also approaches for testing systems without oracles, some of which apply to ML. 

Zhang, Mengshi, Yuqun Zhang, Lingming Zhang, Cong Liu, and Sarfraz Khurshid. "DeepRoad: GAN-based metamorphic testing and input validation framework for autonomous driving systems." In Proceedings of the 33rd ACM/IEEE International Conference on Automated Software Engineering, pp. 132-142. 2018.

> Practical application of metamorphic testing for generating test cases

Zhou, Hucheng, Jian-Guang Lou, Hongyu Zhang, Haibo Lin, Haoxiang Lin, and Tingting Qin. 2015. “An Empirical Study on Quality Issues of Production Big Data Platform.” 2015 IEEE/ACM 37th IEEE International Conference on Software Engineering. https://doi.org/10.1109/icse.2015.130.

> Study of operational issues of large map reduce cluster. Mostly hardware failures not captured by redundancy mechanisms. No direct ML aspect, but useful for discussing large distributed ML jobs at scale and some discussion of debugging from logging data.

Rudin, Cynthia. "Stop explaining black box machine learning models for high stakes decisions and use interpretable models instead." Nature Machine Intelligence 1, no. 5 (2019): 206-215.

> Interesting (potentially controversial) position paper emphasizing the difference between interpretability and explainability in machine learning. Argues that in many cases simple and interpretable models may perform similarly well to opaque models.

Kleppmann, Martin. Designing data-intensive applications: The big ideas behind reliable, scalable, and maintainable systems."" O'Reilly Media, Inc.", 2017.

> Excellent book about distributed and big data systems. Not directly related to machine learning, but covers fundamentals of data storage and data processing (batch, stream, ...) at scale. Excellent discussion of principles and tradeoffs.


## Papers I still need to read

Abdul, Ashraf, Jo Vermeulen, Danding Wang, Brian Y. Lim, and Mohan Kankanhalli. n.d. “Trends and Trajectories for Explainable, Accountable and Intelligible Systems: An HCI Research Agenda.” https://doi.org/10.1145/3173574.3174156.

Amershi, Saleema, Max Chickering, Steven M. Drucker, Bongshin Lee, Patrice Simard, and Jina Suh. n.d. “ModelTracker: Redesigning Performance Analysis Tools for Machine Learning.” https://doi.org/10.1145/2702123.2702509.

Andrist, Sean, Dan Bohus, Ece Kamar, and Eric Horvitz. 2017. “What Went Wrong and Why? Diagnosing Situated Interaction Failures in the Wild.” Social Robotics. https://doi.org/10.1007/978-3-319-70022-9_29.

Batini, Carlo. 2009. “Methodologies for Data Quality Assessment and Improvement.” ACM 0360: 0300.

Gorton, Ian, Ayse Basar Bener, and Audris Mockus. 2016. “Software Engineering for Big Data Systems.” IEEE Software. https://doi.org/10.1109/ms.2016.47.

Kulesza, Todd, Margaret Burnett, Weng-Keen Wong, and Simone Stumpf. 2015. “Principles of Explanatory Debugging to Personalize Interactive Machine Learning.” In Proceedings of the 20th International Conference on Intelligent User Interfaces, 126–37. ACM.

Salay, Rick, Rodrigo Queiroz, and Krzysztof Czarnecki. 2017. “An Analysis of ISO 26262: Using Machine Learning Safely in Automotive Software.” arXiv [cs.AI]. arXiv. http://arxiv.org/abs/1709.02435.

Menzies, T. 2020. “The Five Laws of SE for AI.” IEEE Software 37 (1): 81–85.

Psallidas, Fotis, Yiwen Zhu, Bojan Karlas, Matteo Interlandi, Avrilia Floratou, Konstantinos Karanasos, Wentao Wu, et al. 2019. “Data Science through the Looking Glass and What We Found There.” arXiv [cs.LG]. arXiv. http://arxiv.org/abs/1912.09536.

Islam, Md Johirul, Hoan Anh Nguyen, Rangeet Pan, and Hridesh Rajan. 2019. “What Do Developers Ask About ML Libraries? A Large-Scale Study Using Stack Overflow.” arXiv [cs.SE]. arXiv. http://arxiv.org/abs/1906.11940.

Lwakatare, Lucy Ellen, Aiswarya Raj, Jan Bosch, Helena Holmström Olsson, and Ivica Crnkovic. 2019. “A Taxonomy of Software Engineering Challenges for Machine Learning Systems: An Empirical Investigation.” In Agile Processes in Software Engineering and Extreme Programming, 227–43. Springer International Publishing.

Pons, Lena, and Ipek Ozkaya. 2019. “Priority Quality Attributes for Engineering AI-Enabled Systems.” arXiv [cs.OH]. arXiv. http://arxiv.org/abs/1911.02912.

Santhanam, P., Eitan Farchi, and Victor Pankratius. n.d. “Engineering Reliable Deep Learning Systems.”

Souza Nascimento, Elizamary de, Iftekhar Ahmed, and Edson Oliveira. n.d. “Understanding Development Process of Machine Learning Systems: Challenges and Solutions.” https://doi.org/10.1145/3239235.3268927.

Sun, Youcheng, Min Wu, Wenjie Ruan, Xiaowei Huang, Marta Kwiatkowska, and Daniel Kroening. 2018. “Concolic Testing for Deep Neural Networks.” arXiv [cs.LG]. arXiv. http://arxiv.org/abs/1805.00089.

Tao, Guanhong, Shiqing Ma, Yingqi Liu, and Xiangyu Zhang. n.d. “Attacks Meet Interpretability: Attribute-Steered Detection of Adversarial Samples.”

Washizaki, Hironori. n.d. “Machine Learning Architecture and Design Patterns.”

Washizaki, Hironori, Hiromu Uchida, Foutse Khomh, and Yann-Gael Gueheneuc. 2019. “Studying Software Engineering Patterns for Designing Machine Learning Systems.” arXiv [cs.SE]. arXiv. http://arxiv.org/abs/1910.04736.

Zhang, Xufan, Yilin Yang, Yang Feng, and Zhenyu Chen. 2019. “Software Engineering Practice in the Development of Deep Learning Applications.” arXiv [cs.SE]. arXiv. http://arxiv.org/abs/1910.03156.

## Other Lists

Miryung Kim has been teaching seminars at UCLA on debugging and data science/ML that is a great source for recommended readings as well, see http://web.cs.ucla.edu/~miryung/teaching/CS239-Winter2017/main.xhtml and http://web.cs.ucla.edu/~miryung/teaching/CS239-Winter2019/main.xhtml

Pooyan Jamschidi is teaching "Machine Learning Systems" a UofSC and recommended several readings to me when preparing for my course: https://pooyanjamshidi.github.io/mls/
