# Software Engineering for AI/ML -- An Annotated Bibliography

Author: [Christian Kästner](https://www.cs.cmu.edu/~ckaestne/), Carnegie Mellon University

## Context

While software engineering academics used to focus on solving software engineering problems with
machine learning techniques (ML4SE or AI4SE),
more recently there has been increasing interest in how to improve the engineering
of systems with ML components (SE4ML or SE4AI). Work on this topic is scattered across many communities, including software engineering, machine learning, human-computer interaction, security, humanities, and many others.

With an interest originally for teaching a class
about engineering ML-enabled systems that brings software engineers and data scientists together ([course web page](https://ckaestne.github.io/seai/),
[paper about the course](https://arxiv.org/abs/2001.06691), [upcoming textbook](https://ckaestne.medium.com/machine-learning-in-production-book-overview-63be62393581)), I tried
to read up on the field. In an effort to help the community
I'm sharing here a list of papers that I found interesting and useful
with some sparse notes. 

All notes are my personal opinions.

If you have suggestions for other papers (with or without notes)
*open an issue* please.

## Table of Contents

* [Key resources](#1-key-resources)
* [Quality assurance](#2-quality-assurance)
  * [Surveys](#21-quality-assurance-surveys)
  * [Slicing test data](#22-slicing-test-data)
  * [Unit testing / testing capabilities](#23-unit-testing--testing-capabilities)
  * [Model invariants](#24-model-invariants)
  * [Testing ML frameworks](#25-testing-ml-frameworks)
  * [QA in production](#26-quality-assurance-in-production)
  * [Other](#27-other-quality-assurance-work)
* [Debugging and interpretability](#3-debugging-and-interpretability)
* [Data quality and data management](#4-data-quality-and-data-management)
* [Requirements engineering](#5-requirements-engineering)
  * [Fairness](#51-fairness)
* [Software architecture and design](#6-software-architecture-and-design)
  * [Model API documentation](#61-model-api-documentation)
* [Process](#7-process)
* [Safety & robustness](#8-safety--robustness)
* [Security & privacy](#9-security--privacy)
* [Reproducibility & provenance](#10-reproducibility-provenance)
* [Interdisciplinary teams](#11-interdisciplinary-teams)
* [Human-AI interaction](#12-human-ai-interaction)
* [Computational notebooks](#13-computational-notebooks)
* [ML libraries and APIs](#14-machine-learning-libraries-and-apis)
* [Misc](#15-misc)


## 1. Key Resources

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
> title *"Machine learning: The high interest credit card of technical debt"* is
> one of my favorite paper titles), describes the challenges in building ML
> pipelines and how poor engineering choices can  be very expensive. 
> This paper was instrumental in considering code within ML pipelines and is 
> often discussed in an MLOps context; it is still very much model-centric and does
> not discuss parts of the system that use the deployed model. While the
> "technical debt" metaphor is a bit forced and does not align with how I'd
> teach technical debt and most of the description is rather abstract and not
> well grounded in the SE literature, the paper provides a great argument that a
> machine learning system is more than just the ML model and building and
> operating it is a serious undertaking. 
>
> Pro tip: A google scholar alert for citations to this paper is a good way to notice new SE4ML publications.

Amershi, Saleema, Andrew Begel, Christian Bird, Robert DeLine, Harald Gall, Ece Kamar, Nachiappan Nagappan, Besmira Nushi, and Thomas Zimmermann. "[Software engineering for machine learning: A case study](https://andrewbegel.com/papers/Software_Engineering_for_ML.pdf)." In 2019 IEEE/ACM 41st International Conference on Software Engineering: Software Engineering in Practice (ICSE-SEIP), pp. 291-300. IEEE, 2019. 

> A good description of the SE4ML challenges at Microsoft, characterizing
the challenges of different roles and grounded in interviews and a large
scale survey. Motivating well how pervasive ML is in modern systems and describing best practices and some challenges.

Ozkaya, Ipek. "[What Is Really Different in Engineering AI-Enabled Systems?](https://ieeexplore.ieee.org/abstract/document/9121629)" *IEEE Software* 37, no. 4 (2020): 3-6.

> Concise opinion paper (editorial), discussing that building software system with AI components is harder but not necessarily that different from building traditional software systems. This very much mirrors my own opinion shared in my class and talks. Touches on many great points regarding specifications, requirements, and safety. Essentially a call to action that we need more software engineering.

Passi, Samir, and Phoebe Sengers. "[Making data science systems work](https://journals.sagepub.com/doi/full/10.1177/2053951720939605)." *Big Data & Society* 7, no. 2 (2020).

> In-depth case study in one project of how requirements are negotiated and influence design decisions and the other way around. Strong illustration of how goals of system and model may diverge, of how different team members understand their goals and make decisions, and of how they negotiate requirements and design decisions as the system evolves. "Making it work" is a nice way of framing "building a system that is actually useful for a business". Very detailed and approachable description of the case, a legal chatbot.

Giray, Görkem. "[A software engineering perspective on engineering machine learning systems: State of the art and challenges](https://arxiv.org/abs/2012.07919)." *Journal of Systems and Software* 180 (2021): 111031.

> Comprehensive survey of SE4ML research in the academic software engineering literature. I appreciate going beyond a model-centric focus and discussing the entire system. The survey does a good job of synthesizing and organizing insights from many papers. It is entirely limited to papers in software engineering venues, which restricts the scope to a manageable set, but unfortunately excludes the interesting work from many other communities.

## 2. Quality Assurance

*There is a lot of work that covers testing ML systems in some form, most
of it seems focused on fairly narrow properties of a model. Testing an ML-enabled
system should be much broader, including testing the entire system that includes a model and testing of 
the infrastructure (e.g., learning pipeline and update mechanisms) and
testing in production.*

Breck, Eric, Shanqing Cai, Eric Nielsen, Michael Salib, and D. Sculley. 2017. “[The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction](https://research.google/pubs/pub46555.pdf).” IEEE International Conference on Big Data (Big Data). 2017.

> Nice position paper that discusses the many different aspects of quality assurance in an ML project, beyond just model and data quality. Good introduction to the problem and based on practical experience at Google. Despite it's broader scope it is still model-centric and  focuses only on the ML pipeline, not how it interacts with the rest of the system. Includes some examples and a checklist of QA steps to consider. (Note this is a slightly extended version from a similarly titled paper)

Kaestner, Christian. "[Machine Learning is Requirements Engineering — On the Role of Bugs, Verification, and Validation in Machine Learning](https://medium.com/@ckaestne/machine-learning-is-requirements-engineering-8957aee55ef4)." Medium Blog Post. 2020.

> My own discussion of the role of specifications in machine learning. Many testing papers below that focus on model quality (rather than infrastructure quality, as Breck above) are rather vague and confusing to me with regard to specifications. I argue that machine learning corresponds to the requirements engineering phase of a project rather than the implementation phase and, as such, terminology that relates to validation (i.e., do we build the right system, given stakeholder needs) is more suitable than terminology that relates to verification (i.e., do we build the system right, given a specification). That is, machine learning suggests a specification (like specification mining and invariant detection) rather than provides an implementation for a known specification (like synthesis).

Siebert, Julien, Lisa Joeckel, Jens Heidrich, Koji Nakamichi, Kyoko Ohashi, Isao Namba, Rieko Yamamoto, and Mikio Aoyama. "[Towards Guidelines for Assessing Qualities of Machine Learning Systems](https://arxiv.org/pdf/2008.11007)." In International Conference on the Quality of Information and Communications Technology, pp. 17-31. Springer, Cham, 2020.

> The paper discusses quality attributes of a production ML system beyond just the ML components. It is explicit about considering multiple views of different components, of the entire system, and of the environment the system is embedded it. These views are useful for guiding a discussion of which qualities to consider. Importantly, the paper provides a concrete example of a system by Fujitsu and lists a large number of qualities considered in Table 1 -- very useful for teaching.

Nushi, Besmira, Ece Kamar, Eric Horvitz, and Donald Kossmann. "[On human intellect and machine failures: troubleshooting integrative machine learning systems](http://erichorvitz.com/human_repair_AI_pipeline.pdf)." In *Proceedings of the Thirty-First AAAI Conference on Artificial Intelligence*, pp. 1017-1025. 2017.

> The paper is really about interfaces and blame assignment between multiple ML models that are composed in a system. It discusses the problem with a concrete example (nice!) with three ML models for creating text labels for images, illustrating non-local and non-monotonic effects. The concrete solution requires that individual models can be evaluated and improved with crowd workers, but may be less relevant than the overall framework and example.

### 2.1. Quality Assurance Surveys
*Several surveys have been written on testing of ML models, mostly all around the same time with similar coverage. They tend to be all model-centric, focusing on mostly on the model (e.g., input generation, robustness), rarely on the pipeline, and almost never on the rest of the system.*

Ashmore, Rob, Radu Calinescu, and Colin Paterson. "[Assuring the machine learning lifecycle: Desiderata, methods, and challenges](https://arxiv.org/abs/1905.04223)." arXiv preprint arXiv:1905.04223. 2019.

> Survey on testing in machine learning, going through the stages of an ML pipeline. Many pointers and reasonable organization. Seems more from an ML perspective than an SE perspective, but broadly covers many aspects including data aquisition, data quality, robustness, safety, monitoring, and so forth. A little vague on specifications as usual and little focus on the overall system quality. No information on the used research process.

Zhang, Jie M., Mark Harman, Lei Ma, and Yang Liu. "[Machine learning testing: Survey, landscapes and horizons](http://arxiv.org/abs/1906.10742))." *IEEE Transactions on Software Engineering* (2020).

> Another broad survey on testing in machine learning. Includes many pointers, including different test strategies and different kinds of testing. While the pointers are useful, I was frustrated with many descriptions, definitions, and classifications and find little synthesis in this paper; e.g., I was hoping for clearer definitions of "ML bug", "data bug" or a clear discussion of specifications. Grey literature is not discussed either.

Riccio, Vincenzo, Gunel Jahangirova, Andrea Stocco, Nargiz Humbatova, Michael Weiss, and Paolo Tonella. "[Testing machine learning based systems: a systematic mapping](https://www.pre-crime.eu/techreps/TR-Precrime-2020-03.pdf)." Empirical Software Engineering (2020): 1-62.

> Yet another survey paper on ML testing. It frames the problem as testing the entire system with an ML component, but rarely goes beyond quality assurance just for the model. Somewhat biased toward self-driving cars. Again, I have quite some quibbles with many claims and definitions, e.g. model vs system or what is a specification or what is a bug. As for the other surveys, I'd suggest to use it for an overview and skim for the pointers.

Braiek, Houssem Ben, and Foutse Khomh. "[On testing machine learning programs](https://arxiv.org/abs/1812.02257)." *Journal of Systems and Software* 164 (2020): 110542.

> Yet another survey on ML model testing, possibly the earliest of these (submitted in 2018)

Huang, Xiaowei, Daniel Kroening, Wenjie Ruan, James Sharp, Youcheng Sun, Emese Thamo, Min Wu, and Xinping Yi. "[A survey of safety and trustworthiness of deep neural networks: Verification, testing, adversarial attack and defence, and interpretability](https://arxiv.org/abs/1812.08342)." *Computer Science Review* 37 (2020): 100270.

> Yet another survey, this one extremely broad and ambitious in scope, covering robustness verification, test case generation, test coverage, adversarial attack and defense strategies, and even explanation techniques. This one focuses exclusively on the model and on invariants (mostly robustness) at the model level; it does not relate the techniques or invariants to actual safety concerns at the system level. Nice overview, even though I again have many issues with specific definitions and claims.

### 2.2. Slicing Test Data

*Several papers focus on the idea of looking at subsets of test data evaluate the model on different subpopulations, rather than just looking at a single average accuracy result.*

Barash, Guy, Eitan Farchi, Ilan Jayaraman, Orna Raz, Rachel Tzoref-Brill, and Marcel Zalmanovici. "[Bridging the gap between ML solutions and their business requirements using feature interactions](https://dl.acm.org/doi/abs/10.1145/3338906.3340442)." In Proceedings of the 2019 27th ACM Joint Meeting on European Software Engineering Conference and Symposium on the Foundations of Software Engineering, pp. 1048-1058. 2019.

> Discusses how to slice validation data into subsets to observe how the model is doing on different subpopulations. Simple yet useful idea. Nice analogy to blackbox testing (they frame it in terms of combinatorial testing, though equivalence classes may be a better fit). Approach is used to slice data rather than generate new test data, which aligns also with Hulten's recommendations and [my lecture](https://ckaestne.github.io/seai/S2020/slides/04_modelquality/modelquality.html)/[blog post](https://medium.com/@ckaestne/a-software-testing-view-on-machine-learning-model-quality-d508cb9e20a6) on testing.

Cabrera, Ángel Alexander, Erica Fu, Donald Bertucci, Kenneth Holstein, Ameet Talwalkar, Jason I. Hong, and Adam Perer. "[Zeno: An interactive framework for behavioral evaluation of machine learning](https://dl.acm.org/doi/abs/10.1145/3544548.3581268)." In *Proceedings of the 2023 CHI Conference on Human Factors in Computing Systems*, pp. 1-14. 2023.

> Practical slicing tool with a nice user interface, providing flexibility in with custom slicing functions. Grounded in an interview study.

Ré, Christopher, Feng Niu, Pallavi Gudipati, and Charles Srisuwananukorn. "[Overton: A Data System for Monitoring and Improving Machine-Learned Products](https://arxiv.org/abs/1909.05372)." *arXiv preprint arXiv:1909.05372* (2019).

> Overview of a system design (at Apple) that focuses on slicing and improving training data incrementally. The model building part is automated and the system focuses on the training and validation data, making it easy to add more data and labels (using semi-supervised learning ideas). Nice demonstration of the importance and effectiveness of slicing data for the evaluation (see above).

Oakden-Rayner, Luke, Jared Dunnmon, Gustavo Carneiro, and Christopher Ré. "[Hidden stratification causes clinically meaningful failures in machine learning for medical imaging](https://dl.acm.org/doi/abs/10.1145/3368555.3384468)." In *Proceedings of the Conference on Health, Inference, and Learning*, pp. 151-159. 2020.

> Short and simple example of how rare systematic problems get lost in noise in standard evaluations but how domain knowledge, error analysis, and clustering can each help to identify relevant slices during model evaluation.

See also papers in the [requirements section](#5-requirements-engineering) below and the Slice Finder paper in the [debugging section](#3-debugging-and-interpretability) or my [blog post](https://ckaestne.medium.com/a-software-testing-view-on-machine-learning-model-quality-d508cb9e20a6) on the topic.

### 2.3. Unit Testing / Testing Capabilities

*A number of different papers discuss (more or less explicitly) how to test specific capabilities or partial specifications of a model – which relates closely to traditional unit testing. Capabilities are usually concepts that a model shall learn that mirror domain knowledge or human strategies toward the problem, but that only capture a specific part of the solution. The approaches usually curate or generate test datasets specifically for these capabilities – i.e., unit tests consisting of multiple data points. Assuring capabilities is associated (more or less explicitly) with selecting more robust models that better generalize beyond the training distribution. Several capabilities also relate to invariants described below.*

Kaestner, Christian. "[Rediscovering Unit Testing: Testing Capabilities of ML Models](https://towardsdatascience.com/rediscovering-unit-testing-testing-capabilities-of-ml-models-b008c778ca81)." Medium Blog Post. 2021.

> Shameless plug of my blogpost discussing this area and several papers in it more systematically, including how to identify capabilities and how to curate tests.

Ribeiro, Marco Tulio, Tongshuang Wu, Carlos Guestrin, and Sameer Singh. "[Beyond Accuracy: Behavioral Testing of NLP Models with CheckList](https://homes.cs.washington.edu/~wtshuang/static/papers/2020-acl-checklist.pdf)." In Proceedings ACL, p. 4902–4912. (2020).

> Paper suggests ways of generating test cases for capabilities of NLP models: First step is to list specific capabilities of a model (e.g., to handle negation or typos in sentences); for each capability then test cases are curated. Test cases are created by writing simple template-based generators (think: QuickCheck) of sentences with holes, where tool support is given for identifying values for those holes (synonyms etc). The model is then tested on those generated sentences, either by giving an expected value (e.g., all sentences generated from a template are positive) or by using invariants (metamorphic relations), see below. The paper shows many examples of tests and invariants; the evaluation shows that this approach of testing is useful for production teams to test whether the models actually learn basic capabilities.

Naik, Aakanksha, Abhilasha Ravichander, Norman Sadeh, Carolyn Rose, and Graham Neubig. "[Stress test evaluation for natural language inference](https://www.aclweb.org/anthology/C18-1198.pdf)." Proceedings of the 27th International Conference on Computational Linguistics, p. 2340--2353 (2018).

> Similar to the CheckList paper, this paper identifies 6 capabilities for NLP models, after performing an error analysis of common wrong predictions (think: root cause analysis). Capability tests are separated as competency tests, distraction tests, and noise tests, each encoding tests for specific capabilities, such as understanding antonyms or ignoring spelling errors. Test data is generated following handwritten patterns. The term “stress test” is explicitly introduced, but I consider it very misleading from a software testing perspective.

McCoy, R. Thomas, Ellie Pavlick, and Tal Linzen. "[Right for the wrong reasons: Diagnosing syntactic heuristics in natural language inference](https://arxiv.org/pdf/1902.01007)." Proc. ACL (2019).

> Inverse strategy from testing capabilities: Testing for known common shortcuts (maybe anti-capabilities). They identify three shortcut heuristics often used by NLP models (no discussion how identified and how this would generalize) and then create test data using patterns, not unlike the stress testing and CheckList papers above. That is, instead of testing capabilities, the absence of shortcut heuristics is tested.

Kaushik, Divyansh, Eduard Hovy, and Zachary C. Lipton. "[Learning the difference that makes a difference with counterfactually-augmented data](https://openreview.net/pdf/6267805abf4a2ab7b3f971c759b8c669e6060774.pdf)." Proc. International Conference on Learning Representations (ICLR), (2020).

> Another paper that (implicitly) discusses capabilities of NLP systems. In the context of a sentiment analysis, they instruct crowd-workers to minimally modify existing sentences to change the sentiment of the text. They similarly instruct crowd-workers to minimally modify sentences to change the outcome of inference tasks. By manually analyzing the kind of changes their participants make, they find 15 common patterns, which could be interpreted as capabilities they want the model to understand, such as sarcasm, distinguishing facts from hopes, and negation. While aimed at collecting additional training data rather than generating test data, the same strategy can be used to identify capabilities and to curate test data for those capabilities.

Talmor, Alon, Yanai Elazar, Yoav Goldberg, and Jonathan Berant. "[oLMpics-on what language model pre-training captures](https://arxiv.org/abs/1912.13283)." *Transactions of the Association for Computational Linguistics* 8 (2020): 743-758.

> Another paper that proposes generators for creating test data for 9 specific capabilities for NLP reasoning tasks, including numeric reasoning, distinguishing always from often, handling conjunctions of facts and multi-hop reasoning. Origin of the capabilities not discussed.

Barnes, Jeremy, Lilja Øvrelid, and Erik Velldal. "[Sentiment Analysis Is Not Solved! Assessing and Probing Sentiment Classification](https://arxiv.org/abs/1906.05887)." In *Proceedings of the 2019 ACL Workshop BlackboxNLP: Analyzing and Interpreting Neural Networks for NLP*, pp. 12-23. 2019.

> Systematic analysis of mistakes of mistakes of sentiment analysis models to identify capabilities (or patterns) with which the models struggle. Good example of identifying capabilities from the data (similar to Naik et al above). No testing proposed.

D'Amour, Alexander, Katherine Heller, Dan Moldovan, Ben Adlam, Babak Alipanahi, Alex Beutel, Christina Chen et al. "[Underspecification presents challenges for credibility in modern machine learning](https://arxiv.org/abs/2011.03395)." *arXiv preprint arXiv:2011.03395* (2020).

> The paper argues strongly for evaluating models with tests of core abstractions of the task (similar to the checklist paper above, which they call stress tests) beyond just evaluating accuracy on data samples taken from the same population. While the paper focuses on showing that models with similar accuracy can differ in how they generalize to other distributions (is this really surprising?), it contains several pointers to papers where the community seems to pick up on the importance of additional tests.

Geirhos, Robert, Jörn-Henrik Jacobsen, Claudio Michaelis, Richard Zemel, Wieland Brendel, Matthias Bethge, and Felix A. Wichmann. "[Shortcut learning in deep neural networks](https://arxiv.org/abs/2004.07780)." *Nature Machine Intelligence* 2, no. 11 (2020): 665-673.

> Excellent and easy to read survey of the problem of shortcut learning (i.e. not using intended capabilities) and some directions to address it. Good introduction and examples; very good (visual) description of i.i.d. vs out-of-distribution concerns.

Gardner, Matt, Yoav Artzi, Victoria Basmov, Jonathan Berant, Ben Bogin, Sihao Chen, Pradeep Dasigi et al. "[Evaluating Models’ Local Decision Boundaries via Contrast Sets](https://arxiv.org/abs/2004.02709)." In *Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing: Findings*, pp. 1307-1323. 2020.

> Well argued position paper that ML competitions should include challenging datasets at the decision boundary to test specific capabilities. Good visual illustration of i.i.d. challenges. No discussion of how to identify relevant capabilities though, left to the author of the dataset.

Weber, Noah, Leena Shekhar, and Niranjan Balasubramanian. "[The Fine Line between Linguistic Generalization and Failure in Seq2Seq-Attention Models](https://aclanthology.org/W18-1004.pdf)." In *Proceedings of the Workshop on Generalization in the Age of Deep Learning*, pp. 24-27. 2018.

> Very short paper showing with an illustrative experiment the importance of learning the right structure for a task, rather than surface learning. Very explicit about how the right linguistic structure (and nothing else) is needed to generalize beyond the training distribution (“linguistic generalization”).

Von Rueden, Laura, Sebastian Mayer, Jochen Garcke, Christian Bauckhage, and Jannis Schuecker. "[Informed machine learning–towards a taxonomy of explicit integration of knowledge into machine learning](https://arxiv.org/abs/1903.12394v1)." *Learning* 18 (2019): 19-20.

> Very high level survey of different approaches to use domain knowledge *in addition* to data during training in machine learning. Provides a good overview and classification of different approaches. Domain knowledge can have many forms such as rules and constraints, some might correspond to invariants and capabilities. This has potential implications for robustness, fairness, capabilities, and safety. (Not quite sure where to categorize this – it is not about quality assurance, but kind of the inverse of capability testing, by encoding the domain knowledge directly during training rather than testing it after the fact)

### 2.4. Model Invariants

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

Kang, Daniel, Deepti Raghavan, Peter Bailis, and Matei Zaharia. "[Model Assertions for Monitoring and Improving ML Model](https://arxiv.org/abs/2003.01668)." In Proceedings of MLSys 2020.

> Discusses use cases of “soft” assertions or invariants that show inconsistencies, especially across time series data and across multiple classifiers, without having to have access to labels. Table 5 in the appendix has a very good overview of different invariants and the paper discusses several plausible examples. Note that these invariants are probabilistic in nature rather than hard tests. This can be used for testing and runtime monitoring (e.g., runtime adaptation and safety mechanisms) without the need for labels! Unfortunately, the paper is very vague about concrete interfaces and technical details and focuses primarily on ML details for additional active learning and weak supervision use cases.

Salay, Rick, and Krzysztof Czarnecki. "Improving ML safety with partial specifications." In *International Conference on Computer Safety, Reliability, and Security*, pp. 288-300. Springer, Cham, 2019.

> Good discussion of why providing specifications for ML models is infeasible, followed by a somewhat abstract but well argued discussion of how partial specifications may be used in many different ways regardless. The discussion, while fairly abstract, covers several different facts, including suggesting that some specifications may be feasible on learned intermediate representations, that probabilistic constraints may be provided for data, that partial specifications may be provided for how to safely process model outputs, or that partial  specifications may be encoded during training.


### 2.5. Testing ML Frameworks

Srisakaokul, Siwakorn, Zhengkai Wu, Angello Astorga, Oreoluwa Alebiosu, and Tao Xie. "[Multiple-implementation testing of supervised learning software](https://www.aaai.org/ocs/index.php/WS/AAAIW18/paper/viewPDFInterstitial/17301/15599)." In Workshops at the Thirty-Second AAAI Conference on Artificial Intelligence. 2018.

> Good example of a paper that tests the implementation of the ML algorithm (not the model or resulting system). Here differential testing is used to compare multiple student implementations. Nice demonstration of the idea, though it is not clear how far this would be practical beyond fairly simple learning algorithms implemented in student projects.

Xie, Xiaoyuan, Joshua WK Ho, Christian Murphy, Gail Kaiser, Baowen Xu, and Tsong Yueh Chen. "[Testing and validating machine learning classifiers by metamorphic testing](https://www.sciencedirect.com/science/article/pii/S0164121210003213)." Journal of Systems and Software 84, no. 4 (2011): 544-558.

> This paper applies metamorphic relations to the learning framework itself. That is, it defines invariants/assertions about how inputs (training data) and outputs (learned models) should relate.

Cheng, Dawei, Chun Cao, Chang Xu, and Xiaoxing Ma. "[Manifesting bugs in machine learning code: An explorative study with mutation testing](https://ieeexplore.ieee.org/iel7/8424855/8424858/08424982.pdf)." In *2018 IEEE International Conference on Software Quality, Reliability and Security (QRS)*, pp. 313-324. IEEE, 2018.

> Using mutation testing to mutate the machine learning code (e.g. SVM) to see how robust the ML implementations are to subtle faults. Shows that many mutations to the learning code lead to small degradation of accuracy of the produced models without a crash and that metamorphic testing (as in the paper above) was also not useful to find these kinds of faults.

### 2.6. Quality Assurance in Production

*Model accuracy is often not a very useful metric in itself. In practice it is important to assess the system with real-world inputs. In this context, designing  telemetry, monitoring systems, and running A/B experiments is very common.*

Bernardi, Lucas, Themistoklis Mavridis, and Pablo Estevez. "150 successful machine learning models: 6 lessons learned at Booking.com." In Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining, pp. 1743-1751. 2019.

> Experience report of building various models in a production system, examples of ML-driven products (seems to start with "what could we predict" rather than with "what does this product need"). Good illustration with concrete examples how model accuracy may not align with business success measures of the product (sales) and some speculation why. Strong focus on A/B testing with business metrics rather than model accuracy.

Tang, Diane, Ashish Agarwal, Deirdre O'Brien, and Mike Meyer. "[Overlapping experiment infrastructure: More, better, faster experimentation](https://dl.acm.org/doi/pdf/10.1145/1835804.1835810)." In Proceedings of the 16th ACM SIGKDD international conference on Knowledge discovery and data mining, pp. 17-26. 2010.

Bakshy, Eytan, Dean Eckles, and Michael S. Bernstein. "[Designing and deploying online field experiments](https://dl.acm.org/doi/pdf/10.1145/2566486.2567967)." In Proceedings of the 23rd international conference on World wide web, pp. 283-292. 2014.

> Two papers discussing infrastructure for A/B testing (which is a good foundation and frequently used for testing ML systems in production) at Google and Facebook. More focused on infrastructure around it, but useful for getting into a discussion on how to test in production.

Kohavi, Ron, Diane Tang, and Ya Xu. *Trustworthy Online Controlled Experiments: A Practical Guide to A/B Testing*. Cambridge University Press, 2020.

> Book providing a deep dive into A/B testing, including detailed discussions of statistics.

Myllyaho, Lalli, Mikko Raatikainen, Tomi Männistö, Jukka K. Nurminen, and Tommi Mikkonen. "[On misbehaviour and fault tolerance in machine learning systems](https://arxiv.org/abs/2109.07989)." *Journal of Systems and Software* 183 (2022): 111096.

> Small-scale interview study with a useful list of typical system-level mitigation strategies to handle wrong predictions of models, especially Table 2.

### 2.7. Other Quality Assurance Work

Renggli, Cedric, Bojan Karlaš, Bolin Ding, Feng Liu, Kevin Schawinski, Wentao Wu, and Ce Zhang. "[Continuous integration of machine learning models with ease.ml/ci: Towards a rigorous yet practical treatment](https://arxiv.org/abs/1903.00278)." *arXiv preprint arXiv:1903.00278* (2019).

> This paper emphasizes an interesting aspect with regard to learning-validation-testing data splits and overfitting that I didn’t previously appreciate but that’s obvious in hindsight: When using a dataset to make decisions about a model (here with a CI framing) results from that evaluation will eventually leak into the model and lead to overfitting, hence new test data is needed. The core of the paper is about deciding how much test data is needed and when it needs to be replaced. The CI framing seems rather incidental or even misleading though, as the key problem does not relate to regression testing but toward deciding whether a model outperforms another.

Pei, Kexin, Yinzhi Cao, Junfeng Yang, and Suman Jana. "[DeepXplore: Automated whitebox testing of deep learning systems](https://doi.org/10.1145/3132747.3132785.)." In proceedings of the 26th Symposium on Operating Systems Principles, pp. 1-18. 2017. 

> Differential testing between multiple models (e.g., learned from the same data with different parameters) and input generation that aims to identify inputs that have different outputs across the models. Unclear to me how useful this would be in practice.

Seshia, Sanjit A., Dorsa Sadigh, and S. Shankar Sastry. "[Towards verified artificial intelligence](https://arxiv.org/abs/1606.08514)." arXiv preprint arXiv:1606.08514 (2016).

> Good framing why formal verification (or really any form of testing) is so difficult in machine learning systems in the first two sections: We neither have a specification, nor a good grasp of the environment, and in addition the system is often evolving itself. After explaining why it is so difficult, the paper points to several potentially interesting research areas, but none of them seem to overcome the fundamental problems, especially that of missing specifications.

Tramer, Florian, Vaggelis Atlidakis, Roxana Geambasu, Daniel Hsu, Jean-Pierre Hubaux, Mathias Humbert, Ari Juels, and Huang Lin. "[FairTest: Discovering unwarranted associations in data-driven applications](https://core.ac.uk/download/pdf/249325231.pdf)." In 2017 IEEE European Symposium on Security and Privacy (EuroS&P), pp. 401-416. IEEE, 2017.

> Approach to explore correlations between protected attributes and prediction outcomes in *subpopulations* of the dataset. The key idea is that there may not be such a correlation (generalizes to various fairness measures on the confusion matrix) for the entire population, but it may well exists for certain subpopulations, e.g., only among low-income residence do we observe gender-based discrimination. The key contribution is an efficient search among subpopulations inspired by decision tree learning algorithms. Explicitly adopts testing and debugging terminology and goes beyond the simple invariants (anti-classification) in many other fairness testing papers, i.e., it can account for unfairness through correlated attributes.

## 3. Debugging and Interpretability

*How do we understand what a model does and why it is wrong? Debugging seems closely related with the quest for interpretability, even if just through approximations. This can focus on the model as well as on the data or the learning algorithm. (Some interpretability/explanability papers are listed in the Human-AI Interaction section below, because they focus on how end user rather than developers understand explanations.)*

Molnar, Christoph. "[Interpretable machine learning. A Guide for Making Black Box Models Explainable](https://christophm.github.io/interpretable-ml-book/)", 2019. 

> Though primarily about interpretability, this book provides a great overview of techniques to understand and debug models. 
The book covers both inherently interpretable models and many techniques for ex-post explanations inferred from blackbox models. Explanations can be shown to the user (though the book is fairly shallow on the challenges of doing this and larger system design questions), but they also seem very useful in understanding model (mis-)behavior, understanding individual wrong predictions and outliers. The book covers both techniques for understanding the model and understanding characteristics of the training data. Written in a fairly accessible and pragmatic style, covering the important math but also providing good intutions.

Lipton, Zachary C. "[The Mythos of Model Interpretability: In machine learning, the concept of interpretability is both important and slippery](https://dl.acm.org/doi/pdf/10.1145/3236386.3241340)." *Queue* 16, no. 3 (2018): 31-57.

> Good and compact overview of different goals and notions of explainablity, interpretability, trust, and transparency and a quick overview of different techniques in this area.

Bhatt, Umang, Alice Xiang, Shubham Sharma, Adrian Weller, Ankur Taly, Yunhan Jia, Joydeep Ghosh, Ruchir Puri, José MF Moura, and Peter Eckersley. "[Explainable machine learning in deployment](https://dl.acm.org/doi/abs/10.1145/3351095.3375624)." In Proceedings of the 2020 Conference on Fairness, Accountability, and Transparency, pp. 648-657. 2020.

> An interview study asking practioners about how they use explainability techniques. Finding that they are mostly used internally, mostly for debugging, and mostly using SHAP values. Also somewhat useful includes abstract examples/scenarios of how explainability techniques are used in 6 companies.

Kaur, Harmanpreet, Harsha Nori, Samuel Jenkins, Rich Caruana, Hanna Wallach, and Jennifer Wortman Vaughan. "[Interpreting interpretability: understanding data scientists' use of interpretability tools for machine learning](https://harmanpk.github.io/Papers/CHI2020_Interpretability.pdf)." In *Proceedings of the 2020 CHI conference on human factors in computing systems*, pp. 1-14. 2020.

> Similarly to the paper above, studying how practitioners (might) use two explainability libraries (SHAP and GAM), however focused exclusively on data scientists using explainability tools for insights during model building. Interesting study design with three steps, but really narrow and tool-focused questions. Finding that many data scientists in the study do not well understand what these libraries do and hence commonly overtrust and undertrust them.

Ma, Shiqing, Yingqi Liu, Wen-Chuan Lee, Xiangyu Zhang, and Ananth Grama. "[MODE: automated neural network model debugging via state differential analysis and input selection](https://dl.acm.org/doi/pdf/10.1145/3236024.3236082)." In Proceedings of the 2018 26th ACM Joint Meeting on European Software Engineering Conference and Symposium on the Foundations of Software Engineering, pp. 175-186. 2018.

> Uses a SE mindset (delta debugging, slicing) to approach the problem of debugging deep neural networks, especially to identify features that are critical for misbehavior with the goal of providing better learning data (framed as "root cause identification" of "training bugs"). Fairly pragmatic.

Ma, Shiqing, Yousra Aafer, Zhaogui Xu, Wen-Chuan Lee, Juan Zhai, Yingqi Liu, and Xiangyu Zhang. "[LAMP: data provenance for graph based machine learning algorithms through derivative computation](https://dl.acm.org/doi/pdf/10.1145/3106237.3106291)." In Proceedings of the 2017 11th Joint Meeting on Foundations of Software Engineering, pp. 786-797. 2017.

> Interesting idea to identify which inputs to a machine-learning algorithm have large effects on the produced model (i.e., some form of sensitivity analysis). Focused on specific classes of graph-based algorithms like Pagerank.

Chung, Yeounoh, Neoklis Polyzotis, Kihyun Tae, and Steven Euijong Whang. "[Automated data slicing for model validation: A big data-AI integration approach](https://arxiv.org/abs/1807.06068)." IEEE Transactions on Knowledge and Data Engineering (2019).

> Approach to automatically identify subsets of the data for which the model accuracy is lower than average/other subsets. This automatically slices the validation data based on different features (like decision tree learning). Not that different from approaches in the [Slicing Test Data](#22-slicing-test-data) section, but not guided by humans, hence this seems more useful for debugging than for (regression) testing. Also briefly mentions applications to different quality functions, including fairness and accuracy difference after model update. Paper is heavily focused on underlying technical approach.


Amershi, Saleema, Max Chickering, Steven M. Drucker, Bongshin Lee, Patrice Simard, and Jina Suh. "[Modeltracker: Redesigning performance analysis tools for machine learning](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.697.1689&rep=rep1&type=pdf)." In Proceedings of the 33rd Annual ACM Conference on Human Factors in Computing Systems, pp. 337-346. 2015.

> Description and evaluation of a visual debugging tool to explore wrong predictions and possible causes. Supports use cases for detecting mislabled data, missing features, and outliers. Integrated into the larger ML pipeline for labeling and data management. Also nice overview of other visualization techniques in related work.

Zhang, Xuezhou, Xiaojin Zhu, and Stephen Wright. "[Training Set Debugging Using Trusted Items](https://arxiv.org/pdf/1801.08019.pdf)." In *Thirty-Second AAAI Conference on Artificial Intelligence*. 2018.

> Neat idea on debugging training data: Use a trusted subset of the data to see whether other untrusted training data is responsible for wrong predictions in this subset, or what’s the smallest change to the training data to make the model work on the trusted data. 

## 4. Data Quality and Data Management

Sambasivan, Nithya, Shivani Kapania, Hannah Highfill, Diana Akrong,
Praveen Paritosh, and Lora M. Aroyo. "[“Everyone wants to do the model
work, not the data work”: Data Cascades in High-Stakes
AI](https://dl.acm.org/doi/abs/10.1145/3411764.3445518)". In
Proceedings of the Conference on Human Factors in Computing
Systems, pp. 1-15. 2021.

> Strong argument about how data quality matters and lack of focus in data quality will impact the system later (similar to the argument in software engineering that bugs remaining in the system from requirements to deployment are much harder to fix than those found early). This paper has a strong system focus, showing how a narrow focus on modeling undervalues data collection, data quality work, and the entire outcome of the system. Discusses many different notions of data quality, beyond just schema. Discusses involving humans, incentives, power structures, and documentation in data collection. Excellent introduction to the literature around data quality (with many pointers). Interview study with 53 participants from India, USA and East and West
> African countries. Likely generalizes easily beyond “high-stakes” framing.

Møller, Naja Holten, Claus Bossen, Kathleen H. Pine, Trine Rask Nielsen, and Gina Neff. "[Who does the work of data?](https://ora.ox.ac.uk/objects/uuid:d666c069-1c8e-458a-8e8e-88fdb5884510)" *Interactions* 27, no. 3 (2020): 52-55.

> Short essay arguing about the value (and underappreciation) of the work that goes into data collection work and the socio-technical infrastructure involved. Data work adds a human component, requires oversight and domain knowledge but is often not valued.

Sambasivan, Nithya, and Rajesh Veeraraghavan. "[The Deskilling of Domain Expertise in AI Development](https://www.rajeshveera.org/s/The_Deskilling_of_Domain_Expertise_in_AI_Development.pdf)." In *Proceedings of the Conference on Human Factors in Computing Systems*, pp. 1-14. 2022.

> Follow up to the data cascades paper, studying through interviews how people performing data collection and data entry are often perceived as lazy, corrupt, and low status but not as partners. Also surveying interventions often involving surveillance and incentives. Highlighting an often broken collaboration, resulting in data quality issues.

Schelter, Sebastian, Dustin Lange, Philipp Schmidt, Meltem Celikel, Felix Biessmann, and Andreas Grafberger. 2018. “[Automating Large-Scale Data Quality Verification](http://www.vldb.org/pvldb/vol11/p1781-schelter.pdf).” Proceedings of the VLDB Endowment International Conference on Very Large Data Bases 11 (12): 1781–94.

> Good paper discussing data validation, including schema validation and
checking distributions. The key innovation in the paper is doing this at
scale (at Amazon), whereas the specification mechanisms seem rather straightforward, 
but generally well written and teachable.

Polyzotis, Neoklis, Martin Zinkevich, Sudip Roy, Eric Breck, and Steven Whang. "[Data validation for machine learning](https://mlsys.org/Conferences/2019/doc/2019/167.pdf)." *Proceedings of Machine Learning and Systems* 1 (2019): 334-347.

> Similar in spirit to the Amazon paper above, describes data validation efforts at Google, mostly at a fairly high level. Mostly relates to schema enforcement and detecting drift between feature value distributions between batches of data. Also describes some efforts at suggesting schema inference (effectively specification/invariant mining) to help with adoption and evolution. Also suggests some simple fuzzing to detect crashing bugs in ML components for generated inputs that fit the schema. Can be read as support for schemas as interfaces between teams and components in ML-based systems. 


Polyzotis, Neoklis, Sudip Roy, Steven Euijong Whang, and Martin Zinkevich. 2017. “[Data Management Challenges in Production Machine Learning](https://dl.acm.org/doi/pdf/10.1145/3035918.3054782).” In Proceedings of the 2017 ACM International Conference on Management of Data, 1723–26. ACM.

> Short tutorial notes, not very deep, but providing a decent overview of past work in the database community


Hynes, Nick, D. Sculley, and Michael Terry. "[The data linter: Lightweight, automated sanity checking for ml data sets](http://learningsys.org/nips17/assets/papers/paper_19.pdf)." In NIPS MLSys Workshop. 2017.

> Neat idea to develop a linter that looks for common "code smells" in dataset and internal data structures (e.g., when integers are stored as strings). This is an early but great example of how some classic SE ideas (static analysis tools, dynamic invariant detection, code smells) can be translated to solve new problems in an ML context. It is not quite obvious how far one can take this idea, but it is a great starting point for discussions and a nice illustration of potential SE4ML work.

Ratner, Alexander, Stephen H. Bach, Henry Ehrenberg, Jason Fries, Sen Wu, and Christopher Ré. "[Snorkel: Rapid training data creation with weak supervision](https://arxiv.org/abs/1711.10160)." Proceedings of the VLDB Endowment, 11(3), 269-282, 2017.

> Description of Snorkel, an approach to semi-automatically label training data, where humans provide partial training functions (e.g., labeling some instances based simply on some keywords). The system will learn automatically which of these partial labels to trust and will produce training labels at scale. This is an interesting strategy to gather training data that may work in a number of domains and has been used by a number of companies -- worth exploring. Many further discussions can be based on this, e.g., how to combine manual labels with different confidence, how to combine manual and automatic labels, which labels to trust, how much to involve crowdworkers in labeling and on which data points, etc.

Barrak, A., Eghan, E.E. and Adams, B. 2021. "[On the Co-evolution of ML Pipelines and Source Code-Empirical Study of DVC Projects](https://ieeexplore.ieee.org/abstract/document/9425888)". In 2021 IEEE International Conference on Software Analysis, Evolution and Reengineering (SANER) (pp. 422-433). IEEE.

> DVC (https://dvc.org/) is an open source tool for versioning data
> and ML workflows. Paper conducts empirical analysis of 391 open
> source projects which use DVC. The 25 most active projects are
> further analysed to understand prevalence of ML versioning tools and
> the challenges associated with them. The results indicate that ML
> versioning is a relatively young practise with data versioning being
> the most utilised feature. A high coupling between source code and
> DVC files is noted while coupling between test files and DVC files
> is negligible.

Boyd, Karen L. "[Datasheets for Datasets help ML Engineers Notice and Understand Ethical Issues in Training Data](http://karenboyd.org/blog/wp-content/uploads/2021/09/Datasheets_Help_CSCW-5.pdf)." Proceedings of the ACM on Human-Computer Interaction 5, no. CSCW2 (2021): 1-27.

> Controlled experiment whether participants with datasheets as data documentation realize ethical issues earlier and whether they discuss them differently (they do). Datasheets are characterized as “context documents” and essentially framed as a form of nudging. The paper uses a useful theoretical framing around ethical sensitivity.

Foidl, Harald, Michael Felderer, and Rudolf Ramler. "[Data Smells: Categories, Causes and Consequences, and Detection of Suspicious Data in AI-based Systems](https://arxiv.org/abs/2203.10384)." *arXiv preprint arXiv:2203.10384* (2022).

> A catalog of different “data smells” and corresponding detection mechanisms, based on an analysis of grey literature and academic papers. Using both heuristic rules and ML-based detectors.

## 5. Requirements Engineering

*I have the impression that many practical problems in building AI-enabled systems are 
really requirements engineering problems. For example: There are many different notions
of fairness, but which one is the right one for the project? How does the model interact
with the environment and what safeguards should be installed to detect feedback loops or
assure safety in those interactions? Unfortunately, the literature explicitly on requirements engineering for AI-enabled systems seems rather sparse – but there are many papers that are implicitly mostly about requirements engineering.*

Vogelsang, Andreas, and Markus Borg. "[Requirements Engineering for Machine Learning: Perspectives from Data Scientists](https://arxiv.org/pdf/1908.04674.pdf)." In Proc. of the 6th International Workshop on Artificial Intelligence for Requirements Engineering (AIRE), 2019. 

> Strong argument for the importance of requirements engineering when building ML-enabled systems. Covering many qualities and what kind of requirements should be solicited, including requirements about data quality and quanitity, provenance, monitoring, and protected classes and attributes. Also makes a good case for the role of a requirements engineer to identify a suitable measure of accuracy to mediate between users and data scientists. Based on 4 interviews only and sometimes reads more like a well argued opinion paper.

Rahimi, Mona, Jin LC Guo, Sahar Kokaly, and Marsha Chechik. "[Toward Requirements Specification for Machine-Learned Components](https://ieeexplore.ieee.org/document/8933771)." In 2019 IEEE 27th International Requirements Engineering Conference Workshops (REW), pp. 241-244. IEEE, 2019.

> Idea paper that outlines a path of how requirements engineering can be useful in better understanding domain and context of a problem and how this helps in better curating a high-quality dataset for training and also how to drive validation of the model. Uses a running vision example of pedestriant detection.

Passi, Samir, and Solon Barocas. "[Problem formulation and fairness](https://dl.acm.org/doi/abs/10.1145/3287560.3287567)." In *Proceedings of the Conference on Fairness, Accountability, and Transparency*, pp. 39-48. 2019.

> In-depth study of a failed project illustrating the challenges in problem formulation in machine-learning projects. Shows how finding the right proxy measure to measure success is essential for a project. While not the primary concern, it also discusses how the right problem formulation is powerful in shaping ethical considerations. 

Nalchigar, Soroosh, Eric Yu, and Karim Keshavjee. "[Modeling machine learning requirements from three perspectives: a case report from the healthcare domain](http://www.cs.utoronto.ca/~soroosh/papers/Modeling%20machine%20learning%20requirements%20from%20three%20perspectives%20a%20case%20report%20from%20the%20healthcare%20domain.pdf)." *Requirements Engineering* 26, no. 2 (2021): 237-254.

> Approach for requirements modeling in ML projects, identifying stakeholders and their goals, decision needs, and questions where ML might help. Single but very illustrative case study, showing lots of concrete results.

Kulynych, Bogdan, Rebekah Overdorf, Carmela Troncoso, and Seda Gürses. "[POTs: protective optimization technologies](https://arxiv.org/abs/1806.02711)." In Proceedings of the 2020 Conference on Fairness, Accountability, and Transparency, pp. 177-188. 2020.

> This is the only ML paper I have seen that explicitly discusses requirements engineering with Jackson's world vs machine framing. It nicely frames the fairness problem as a system problem and explicitly discusses the interface between the environment and the implementation's specification and how assuring fairness only at the model level is insufficient. The rest of the paper, then essentially suggests adversarial hacking through changes in the environment to drive the model to make fairer or globally better decisions -- that is, distributing the problem, affected people can increase the cost of certain outcomes thus making an ML system recommend other outcomes that are more benefitial to them. Interesting position paper, even if just for the framing in Sec 2.

Subbaswamy, Adarsh, Peter Schulam, and Suchi Saria. "[Preventing failures due to dataset shift: Learning predictive models that transport](http://proceedings.mlr.press/v89/subbaswamy19a/subbaswamy19a.pdf)." In *The 22nd International Conference on Artificial Intelligence and Statistics*, pp. 3118-3127. PMLR, 2019.

> Interesting idea that: If we know how data is generated or what dependencies underly the system and the input features, and more importantly know which of those processes/relationships/features are likely to change (coming from domain knowledge elicited with requirements engineering I assume), we can integrate this information in the modeling process and make the model more robust with regard to these kind of changes. That is we do not learn on certain relationships and thus  don’t need to update the model for data/concept drift as often. Unclear to me how practical and the evaluation seems fairly artificial, but I like the direction.

Wiens, Jenna, Suchi Saria, Mark Sendak, Marzyeh Ghassemi, Vincent X. Liu, Finale Doshi-Velez, Kenneth Jung et al. "[Do no harm: a roadmap for responsible machine learning for health care](http://www.regenhealthsolutions.info/wp-content/uploads/2019/08/Do-no-harm-a-roadmap-for-responsible-machine.pdf)." *Nature medicine* 25, no. 9 (2019): 1337-1340.

> Position paper with a fairly high-level overview of what it takes to build and deploy machine learning products in health care settings. Lot’s of emphasis on what are essentially all requirements engineering challenges of understanding the domain, involving stakeholders, integrating the product into practice, etc etc.

Banks, Alec, and Rob Ashmore. "[Requirements Assurance in Machine Learning](http://ceur-ws.org/Vol-2301/paper_8.pdf)." In *SafeAI@ AAAI*. 2019.

> Short position paper essentially arguing that training data implicitly provides the requirements or specifications for an ML model and hence the quality of the training data should be the key focus in quality assurance for models. Maps concerns in validating requirements with concerns in validating data quality.

Pine, Kathleen H., and Max Liboiron. "[The politics of measurement and action](http://www.kpine.net/wp-content/uploads/2012/10/politics-of-measurement_CHI-format_CAMERA-READY-V2-4.pdf)." In *Proceedings of the 33rd Annual ACM Conference on Human Factors in Computing Systems*, pp. 3147-3156. 2015.

> 2 short case studies of how activists purposefully create measures to indicate harms and achieve change. While not directly related to machine learning, it provides a good overview of the politics of measurement and how shaping the decision what gets to be measured is highly influential in system design.

### 5.1. Fairness

*Much of the interesting fairness discussions are really about requirements engineering in my book. Once a fairness measure and protected attributes are defined, measurement is typically not very challenging. The challenge is in identifying what notion of fairness is appropriate, a typical requirements engineering problem (and process challenge) negotiating the demands of various stakeholders. Here are a couple of papers that I liked.*

Corbett-Davies, Sam, and Sharad Goel. "[The measure and mismeasure of fairness: A critical review of fair machine learning](https://arxiv.org/abs/1808.00023)." arXiv preprint arXiv:1808.00023 (2018).

> A comprehensive an critical discussion of different fairness measures often discussed in the ML community. It's kind of depressing how many different notions and problems there are and how few solutions. Even though they don't discuss requirements engineering in the paper, I put it here because it shows the complicated mess that fairness makes when trying to identify the right fairness requirements for an ML-enabled system. A requirements engineer must work with stakeholders to identify suitable requirements and make a lot of decisions, which won't be easy but will be necessary. This paper will probably give the requirements engineer the right vocabulary to talk to ML experts who need to assure the requirement and will provide enough pointers to identify what issues to probe for when talking to stakeholders.

Holstein, Kenneth, Jennifer Wortman Vaughan, Hal Daumé III, Miro Dudik, and Hanna Wallach. "[Improving fairness in machine learning systems: What do industry practitioners need?](http://users.umiacs.umd.edu/~hal/docs/daume19fairness.pdf)" In Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems, pp. 1-16. 2019.

> An interview study with engineers that consider fairness in their ML-enabled products. This one looks at the system/software-engineering level, beyond narrow fairness properties at the model level and discusses problems and strategies broadly, including fairness considerations across all lifecycle stages, possible checklists, best practices, holistic auditing, possibly even resulting in changes in system design. It does not mention requirements, but many issues are deeply rooted in requirements engineering and system design work.

Madaio, Michael A., Luke Stark, Jennifer Wortman Vaughan, and Hanna Wallach. "[Co-Designing Checklists to Understand Organizational Challenges and Opportunities around Fairness in AI](http://www.jennwv.com/papers/checklists.pdf)." In Proceedings of the 2020 CHI Conference on Human Factors in Computing Systems, pp. 1-14. 2020.

> Another great paper that looks at requirements engineering for fairness in production ML systems in practice. It looks at challenges and suggest a checklist. It argues that it's really all about the process integration and about taking a system level view (rather than focusing on model properties). Includes the actual checklist.

Bietti, Elettra. "[From ethics washing to ethics bashing: a view on tech ethics from within moral philosophy](https://dl.acm.org/doi/pdf/10.1145/3351095.3372860)." In *Proceedings of the 2020 Conference on Fairness, Accountability, and Transparency*, pp. 210-219. 2020.

> Arguing that most ethics discussions around AI and tech are too narrow as a tool for a purpose without allowing broader investigation involving all stakeholders, thus leading to a frustration with corporate ethics initiatives (ethics washing, ethics bashing). The paper then outlines the real role that moral philosophy can plan, which to me reads a lot like requirements engineering at the societal level: Stepping back, viewing all perspectives, trying to balance all views. May not be immediately useful, but I found the discussion interesting.

Binns, Reuben. "[Fairness in machine learning: Lessons from political philosophy](http://proceedings.mlr.press/v81/binns18a/binns18a.pdf)." In *Conference on Fairness, Accountability and Transparency*, pp. 149-159. PMLR, 2018.

> Interesting overview of the philosophical arguments around discrimination and fairness. Useful introduction to the topic.

Yeom, Samuel, and Michael Carl Tschantz. "[Avoiding Disparity Amplification under Different Worldviews](https://dl.acm.org/doi/abs/10.1145/3442188.3445892)." In *Proceedings of the 2021 ACM Conference on Fairness, Accountability, and Transparency*, pp. 273-283. 2021.

> Another paper that points out how different views and goals of fairness lead to very different approaches. The key point is that bias can be difficult to assess if your observations may be biased, but different assumptions about whether observations are biased lead to very different fairness approaches.

Rakova, Bogdana, Jingying Yang, Henriette Cramer, and Rumman Chowdhury. "[Where responsible AI meets reality: Practitioner perspectives on enablers for shifting organizational practices](https://arxiv.org/abs/2006.12358)." *Proceedings of the ACM on Human-Computer Interaction* 5, no. CSCW1 (2021): 1-23.

> Another excellent interview study on fairness practice, showing current practices but also wants and aspirations. Strong focus on embedding practices into processes and establishing clear responsibilities; also discusses the role of activists in an organization. Based on 26 interviews in 19 organizations.

Greene, Daniel, Anna Lauren Hoffmann, and Luke Stark. "[Better, nicer, clearer, fairer: A critical assessment of the movement for ethical artificial intelligence and machine learning](https://core.ac.uk/download/pdf/211327327.pdf)." In *Proceedings of the 52nd Hawaii International Conference on System Sciences* (2019).

> Analysis of 2018 ML ethics guidelines and their themes. Arguing that they are technology driven and focused on better designs only rather than considering societal issues more broadly, accepting human responsibility, but also having various blind spots.

Metcalf, Jacob, and Emanuel Moss. "[Owning ethics: Corporate logics, silicon valley, and the institutionalization of ethics](https://datasociety.net/wp-content/uploads/2019/09/Owning-Ethics-PDF-version-2.pdf)." *Social Research: An International Quarterly* 86, no. 2 (2019): 449-476.

> Essay, grounded in interviews with people in corporate ML ethics roles, exploring the tensions between various goals, while embedded in corporate business logics. For example highlighting a typical focus on technology and meritocracy and how it influences what kind of solutions are considered and how it can lead to ethics washing.

Wieringa, Maranke. "[What to account for when accounting for algorithms: a systematic literature review on algorithmic accountability](https://dl.acm.org/doi/abs/10.1145/3351095.3372833)." In *Proceedings of the Conference on Fairness, Accountability, and Transparency*, pp. 1-18. 2020.

> Detailed discussion and definition of the concept of accountability, and the various dimensions and concerns it entails. Somewhat dry and not really specific to ML at all, but useful framing and illustration of what accountability means in different contexts.

Shen, Hong, Wesley H. Deng, Aditi Chattopadhyay, Zhiwei Steven Wu, Xu Wang, and Haiyi Zhu. "[Value cards: An educational toolkit for teaching social impacts of machine learning through deliberation](https://dl.acm.org/doi/abs/10.1145/3442188.3445971)." In *Proceedings of the Conference on Fairness, Accountability, and Transparency*, pp. 850-861. 2021.

> Teaching approach to illustrate the conflicting requirements in fairness discussions, using personas and checklists on recidivism data.

Srivastava, Megha, Hoda Heidari, and Andreas Krause. "[Mathematical notions vs. human perception of fairness: A descriptive approach to fairness for machine learning](https://dl.acm.org/doi/abs/10.1145/3292500.3330664)." In *Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining*, pp. 2459-2468. 2019.

> Adaptive survey design to elicit fairness preferences between competing fairness notions with a few questions. Interesting strategy to elicit scenario-specific fairness requirements from non-technical stakeholders.

Raji, Inioluwa Deborah, I. Elizabeth Kumar, Aaron Horowitz, and Andrew Selbst. "[The fallacy of AI functionality](https://dl.acm.org/doi/abs/10.1145/3531146.3533158)." In *2022 ACM Conference on Fairness, Accountability, and Transparency*, pp. 959-972. 2022.

> Essay paper with an interesting premise: Many ML-enabled systems simply do not work for their intended purpose and we should worry about this much more before we worry about fairness details. This largely seems to refer to models being to inaccurate for practical use, though the paper never defines its key concept of “AI functionality”. Mostly an interesting collection of problem stories, sorted in various problems like impossible tasks, post-deloyment issues, and communication failures.

Grgic-Hlaca, Nina, Elissa M. Redmiles, Krishna P. Gummadi, and Adrian Weller. "[Human perceptions of fairness in algorithmic decision making: A case study of criminal risk prediction](https://dl.acm.org/doi/abs/10.1145/3178876.3186138)." In Proceedings of the 2018 World Wide Web Conference, pp. 903-912. 2018.

> Analysis of a large scale survey on what participants consider as fair in criminal risk prediction and how that relates to larger preferences about privacy and other underlying principles. The study illustrates clearly how fairness considerations are entangled in politics and how navigating and negotiating different preferences is an essential task is system design. It additionally shows how disambiguating underlying principles can help to explain different preferences.

## 6. Software Architecture and Design

*Design of machine-learning pipelines, and more importantly design of systems that use machine learning components. How does one integrate such a component in the rest of the system? For example, how to design the system anticipating that the model will make wrong predictions eventually?*

Lakshmanan, Valliappa, Sara Robinson, and Michael Munn. *Machine learning design patterns*. O'Reilly Media, 2020.

> Interesting book collecting a number of design patterns for building and deploying ML models. Patterns are described in lots of details with examples and concrete code snippets. It is very model focused and example driven, but covers the whole machine learning pipeline including feature engineering, training, and serving. Especially the coverage of MLOps (stateless serving function, transform, feature store, ...) seem useful and cover many modern tools and practices.

Washizaki, Hironori, Hiromu Uchida, Foutse Khomh, and Yann-Gaël Guéhéneuc. "[Machine Learning Architecture and Design Patterns](http://www.washi.cs.waseda.ac.jp/wp-content/uploads/2019/12/IEEE_Software_19__ML_Patterns.pdf)." Paper draft, 2019

> A useful collection of design patterns, architectural patterns, and anti-patterns derived from a literature survey of 19 papers and 19 grey literature articles. Not a detailed discussion and no detailed pattern description, but pointers to the sources, a list of patterns names, and an overview of their relations, that are likely useful for further exploration and discussions, see their [web site](http://www.washi.cs.waseda.ac.jp/ml-patterns/). Many of the patterns seem to relate more to big-data processing than ML, but are likely useful when building ML-enabled systems. 

Daniel Smith. "[Exploring Development Patterns in Data Science](https://www.theorylane.com/2017/10/20/some-development-patterns-in-data-science/)." TheoryLane Blog Post. 2017.

> Short blog post arguing to decompose ML pipeline from a single notebook into multiple services using cloud infrastructure. Bit polemic but well argued, short opinion piece.

Yokoyama, Haruki. "Machine learning system architectural pattern for improving operational stability." In *2019 IEEE International Conference on Software Architecture Companion (ICSA-C)*, pp. 267-274. IEEE, 2019.

> One of the few papers actually discussing architectural design and tradeoffs of an ML-enabled system explicitly, discussing the integration of ML and non-ML parts. While I feel the design is maybe fairly standard, the paper has actually a nice concrete example and corresponding architectural models that seems very useful for teaching.

Hazelwood, Kim, Sarah Bird, David Brooks, Soumith Chintala, Utku Diril, Dmytro Dzhulgakov, Mohamed Fawzy et al. "[Applied machine learning at facebook: A datacenter infrastructure perspective](https://research.fb.com/wp-content/uploads/2017/12/hpca-2018-facebook.pdf)." In *2018 IEEE International Symposium on High Performance Computer Architecture (HPCA)*, pp. 620-629. IEEE, 2018.

> Paper discussing the infrastructure for learning and serving ML models at Facebook (including discussions of hardware design). Discusses many quality attributes and constraints that are relevant in operation, including cost, latency, model-updated frequency needs, large amounts of data, and ability to recover from outages. For example, it includes an explicit discussion of the cost of outdated models. Much of this is useful input for discussing design constraints and architectural tradeoffs.

Peng, Zi, Jinqiu Yang, Tse-Hsun Chen, and Lei Ma. "A first look at the integration of machine learning models in complex autonomous driving systems: a case study on Apollo." In *Proceedings of the 28th ACM Joint Meeting on European Software Engineering Conference and Symposium on the Foundations of Software Engineering*, pp. 1240-1250. 2020.

> Interesting paper analyzing the source code and architecture of the Baidu’s Apollo self-driving car software. Finding 28 models that are often chained and combined with nontrivial glue code and non-ML components. This makes a strong case to go beyond testing individual models but to test also the interactions with non-ML code and the interactions among multiple models.

Serban, Alex, and Joost Visser. "[An Empirical Study of Software Architecture for Machine Learning](https://arxiv.org/abs/2105.12422)." *arXiv preprint arXiv:2105.12422* (2021).

> Interview study with 10 software architects working on ML-based projects, combined with literature analysis and small-scale survey. Lists several challenges and possible solutions, though scope seems to drift beyond software architecture, describing many well known challenges around model development and deployment. 

Lewis, Grace A., Ipek Ozkaya, and Xiwei Xu. "Software Architecture Challenges for ML Systems." In *2021 IEEE International Conference on Software Maintenance and Evolution (ICSME)*, pp. 634-638. IEEE, 2021.

> Position paper framing the positive contributions software architecture can bring to building ML systems. Argues for architecture as a coordination point between disciplines and for observability as a key quality driver.

Shankar, Shreya, Rolando Garcia, Joseph M. Hellerstein, and Aditya G. Parameswaran. "[Operationalizing machine learning: An interview study](https://arxiv.org/abs/2209.09125)." *arXiv preprint arXiv:2209.09125* (2022).

> Interview study with 18 participants on MLOps, eliciting pain points and practices. Decent overview and introduction to MLOps practices. Entirely model-centric focused on deploying a model and pipeline, not the rest of the system using the model. Emphasizing the need for engineering and organizational interventions and a few engineering tradeoffs.

### 6.1. Model API Documentation

Mitchell, Margaret, Simone Wu, Andrew Zaldivar, Parker Barnes, Lucy Vasserman, Ben Hutchinson, Elena Spitzer, Inioluwa Deborah Raji, and Timnit Gebru. "[Model cards for model reporting](https://arxiv.org/abs/1810.03993)." In *Proceedings of the conference on fairness, accountability, and transparency*, pp. 220-229. 2019.

> Position paper suggesting model cards as a short (1 page) documentation of the purpose and limits of the model, evaluation results, and considerations regarding fairness. Illustrated with two good examples. Strongly motivated by fairness discussions, but also a decent starting point for thinking more broadly about how to document a model.

Arnold, Matthew, Rachel KE Bellamy, Michael Hind, Stephanie Houde, Sameep Mehta, Aleksandra Mojsilović, Ravi Nair, Karthikeyan Natesan Ramamurthy, Darrell Reimer, Alexandra Olteanu, David Piorkowski, Jason Tsay, and Kush R. Varshney. "[FactSheets: Increasing trust in AI services through supplier's declarations of conformity](https://arxiv.org/pdf/1808.07261.pdf)." *IBM Journal of Research and Development* 63, no. 4/5 (2019): 6-1.

> Position paper suggesting fact sheets as documentation of a model and the assurances provided. Similar to model cards, but much broader in scope, including for example safety, explainability, and lineage concerns. Limited explanation on most points though; linked arxiv.org version has some examples in the appendix.

## 7. Process

*Several papers on the process of model development and how processes for data scientists and software engineers may differ. See also section Requirements Engineering/Fairness above for challenges of integrating fairness considerations into the process and section Interdisciplinary Teams below for process challenges at the interface between teams.*

Studer, Stefan, Thanh Binh Bui, Christian Drescher, Alexander Hanuschkin, Ludwig Winkler, Steven Peters, and Klaus-Robert Mueller. "[Towards CRISP-ML (Q): A Machine Learning Process Model with Quality Assurance Methodology](https://arxiv.org/abs/2003.05155)." arXiv preprint arXiv:2003.05155 (2020).

> Fairly detailed overview of an ML-development process, starting early with business needs and covering all steps to deployment. Not necessarily new or grounded in new data, but a very nice and well-written overview. Good early reading to understand the full scope of SE4ML, beyond just building models.

Serban, Alex, Koen van der Blom, Holger Hoos, and Joost Visser. "[Adoption and Effects of Software Engineering Best Practices in Machine Learning](https://arxiv.org/pdf/2007.14130)." In Proc. ACM/IEEE International Symposium on Empirical Software Engineering and Measurement (2020).

> Collection of best practices, mostly focused on the model pipeline not the larger system. In a larger survey, practitioners indicate which practices they follow, resulting in interesting ranks in Table 2. Results show that MLOps topics like versioning, monitoring and experiment management are fairly broadly adopted, whereas quality assurance practices and hyperparameter tuning are less adopted. Comes with a nice list of the practices on their [web page](https://se-ml.github.io/practices/).

Haakman, Mark, Luís Cruz, Hennie Huijgens, and Arie van Deursen. "[AI Lifecycle Models Need To Be Revised. An Exploratory Study in Fintech](https://arxiv.org/pdf/2010.02716)." *arXiv preprint arXiv:2010.02716* (2020).

> Nice interview study with 17 participants at ING bank about their process in building and deploying ML models. Shows many concerns about provenance, regulation, and security driving decisions and identifying extra steps in common data science process models. Mostly focused on the model and its deployment (data science view), not a larger system it may be integrated in.

Martínez-Plumed, Fernando, Lidia Contreras-Ochando, Cesar Ferri, José Hernández Orallo, Meelis Kull, Nicolas Lachiche, Maréa José Ramírez Quintana, and Peter A. Flach. "[CRISP-DM Twenty Years Later: From Data Mining Processes to Data Science Trajectories](https://research-information.bris.ac.uk/files/220614618/TKDE_Data_Science_Trajectories_PF.pdf)." IEEE Transactions on Knowledge and Data Engineering (2019).

> Discussion how today's data science differs from past data mining (less prescriptive, more exploratory) and how hence CRISP-DM is too rigid a model to cover the diverse processes. The paper essentially proposes a megamodel with different process steps, which projects might pass through in different orders (called trajectories). Gives examples of different trajectories that may be appropriate in different projects. Limited evaluation, but interesting discussion. Focused on data science side, not building entire system though.

Kaestner, Christian. “[On the process for building software with ML components](https://ckaestne.medium.com/on-the-process-for-building-software-with-ml-components-c54bdb86db24).” Medium Blog Post, 2020.

> My own (early) thoughts on how process differs for data science and software engineering, but also how both of them might be integrated into a larger picture.

Mailach, Alina and Norbert Siegmund. “[Socio-Technical Anti-Patterns in Building ML-Enabled Software: Insights from Leaders on the Forefront](https://sws.informatik.uni-leipzig.de/wp-content/uploads/2023/01/socio-technical-anti-patterns-icse2023.pdf).” *2023 IEEE/ACM 45th International Conference on Software Engineering (ICSE)* (2023): 690-702.

> Analysis of talks in the MLOps community finding various anti-patterns that often relate to process and organizational issues, such as poor hiring, hype-driven development, and redundant development.


## 8. Safety & Robustness

*There is a significant amount of machine learning research on safety and security, especially on narrow properties of robustness, but also some system-level discussions on safeguard mechanisms outside of the model. A software engineering professional should probably understand the tools and techniques. Many testing papers in the section Quality Assurance above cover robustness properties.*

Borg, Markus, Cristofer Englund, Krzysztof Wnuk, Boris Duran, Christoffer Levandowski, Shenjian Gao, Yanwen Tan, Henrik Kaijser, Henrik Lönn, and Jonas Törnqvist. "[Safely entering the deep: A review of verification and validation for machine learning and a challenge elicitation in the automotive industry](https://www.atlantis-press.com/journals/jase/125905766)." Journal of Automotive Software Engineering. Volume 1, Issue 1, Pages 1 - 19. 2019

> Summary of the current thinking about safety of ML components in self-driving cars, based on literature review, a survey, and several industry workshops. Provides a decent overview from an engineering perspective, providing pointers to a long history of ML-related safety work in aerospace and automotive research that is likely a good starting point for further exploration. Mostly fairly high-level; among others, emphasizes the system nature of the problem and ideas with regard to design strategies for safety, such as safety cages and fail-safe systems.

Salay, Rick, Rodrigo Queiroz, and Krzysztof Czarnecki. "[An analysis of ISO 26262: Using machine learning safely in automotive software](https://arxiv.org/pdf/1709.02435)." *arXiv preprint arXiv:1709.02435* (2017).

Salay, Rick, and Krzysztof Czarnecki. "[Using machine learning safely in automotive software: An assessment and adaption of software process requirements in ISO 26262](https://arxiv.org/pdf/1808.01614)." *arXiv preprint arXiv:1808.01614* (2018).

> The first provides a decent overview of safety thinking at the system level in the automotive industry and how that thinking aligns with current safety standards. While it does not go into specific safety techniques, it shows the overall mindset and the relevant concerns. The second, longer report goes more in into details and provides several concrete architectural patterns (esp. Sec 7).

Zendel, Oliver, Markus Murschitz, Martin Humenberger, and Wolfgang Herzner. "[CV-HAZOP: Introducing test data validation for computer vision](https://openaccess.thecvf.com/content_iccv_2015/html/Zendel_CV-HAZOP_Introducing_Test_ICCV_2015_paper.html)." In *Proceedings of the IEEE International Conference on Computer Vision*, pp. 2066-2074. 2015.

> An application and extension of classical HAZOP techniques for hazard analysis to vision components, suggesting among others new guidewords.

Singh, Gagandeep, Timon Gehr, Markus Püschel, and Martin Vechev. "[An abstract domain for certifying neural networks](https://dl.acm.org/doi/pdf/10.1145/3290354)." Proceedings of the ACM on Programming Languages 3, no. POPL (2019): 1-30.

> (Discussed also above under model invariants) This is an example of a large group of paper that determines whether all pertubations of an input within a certain bound all produce the same prediction. The search space by these pertubations and their combinations is typically very large and formal methods are used to produce conservative results (i.e., when it reports robustness against these pertubations it actually guaranteed to always return the same prediction, but there can be false positives). This is one of the more readable papers in this area that I have seen, but I'm not aware of any paper that really discusses how to use these robustness guarantees in production (typical scenarios seem to be to test robustness for a training set, for a set of important test cases, or to test it at runtime to make sure that a specific result is not just caused by a pertubation) and whether the considered pertubations are relevant or interesing for practical cases.


Cohen, Jeremy M., Elan Rosenfeld, and J. Zico Kolter. "[Certified adversarial robustness via randomized smoothing](https://arxiv.org/abs/1902.02918)." In Proc. International Conference on Machine Learning, p. 1310--1320, 2019.

> Discusses *randomized smoothing*, an interesting approach to evaluating robustness: Sample predictions not only about a specific input but also about perturbed versions of that input around that input and report the most common prediction as the result. As a consequence, the prediction will be less sensitive to minor changes in the input. Black box technique that works for any kind of model. If sampled frequently enough, as discussed in the paper, also probabilistic bounds can be provided, although at significant computational costs (they use 100K model inferences per input).

Shneiderman, Ben. "Bridging the gap between ethics and practice: Guidelines for reliable, safe, and trustworthy Human-Centered AI systems." *ACM Transactions on Interactive Intelligent Systems (TiiS)* 10, no. 4 (2020): 1-31.

> Essay-style paper on the many layers of considerations necessary for building safe software systems, with a nice framing of software engineering practices framed by culture and regulation (see Fig 1!). The specific discussions seem somewhat shallow and ad-hoc, but there are several interesting pointers throughout.

Ishikawa, Fuyuki, and Yutaka Matsuno. "[Continuous argument engineering: Tackling uncertainty in machine learning based systems](https://www.researchgate.net/profile/Yutaka_Matsuno2/publication/327113121_Continuous_Argument_Engineering_Tackling_Uncertainty_in_Machine_Learning_Based_Systems_SAFECOMP_2018_Workshops_ASSURE_DECSoS_SASSUR_STRIVE_and_WAISE_Vasteras_Sweden_September_18_2018_Proceedings/links/5dd2b18392851c382f4999d9/Continuous-Argument-Engineering-Tackling-Uncertainty-in-Machine-Learning-Based-Systems-SAFECOMP-2018-Workshops-ASSURE-DECSoS-SASSUR-STRIVE-and-WAISE-Vaesteras-Sweden-September-18-2018-Procee.pdf)." In *International Conference on Computer Safety, Reliability, and Security*, pp. 14-21. Springer, Cham, 2018.

> Well argued short position paper on how to integrate uncertainty and monitoring in safety cases and goal modeling notations. Essentially acknowledges that not all problems can be foreseen, but instead provides means to express uncertainty and a mandate to monitor the system in production and add more codncerns and evidence when new problem categories are surfaced.

Kaestner, Christian. “[Why Robustness is not Enough for Safety and Security in Machine Learning](https://towardsdatascience.com/why-robustness-is-not-enough-for-safety-and-security-in-machine-learning-1a35f6706601).” Medium Blog Post 2021.

> My attempt to understand the robustness discussion and how it would be useful for practical safety and security concerns in software systems that use ML components. Explains the problem and then argues that robustness is a very narrow technical property with limited practical value, argues that safety must really be considered at the system level.

Slovic, Paul. “Perception of risk.” *Science* 236 4799 (1987): 280-5 .

> A high-level overview of how lay people approach risk not objectively, but how additional factors like dread and a lack of control play a big role in perceiving risk. In contrast, well understood, present, concrete and voluntary risks are perceived as less important. Useful for framing how automation with ML might be perceived as particularly risky in some applications and explanations might shift risk perceptions, as well as explaining for where people prefer regulation.

## 9. Security & Privacy

*A few papers on security and privacy in machine learning. Much focus is on adversarial machine learning, which largely relates to robustness properties discussed in section Safety above.*

Huang, Ling, Anthony D. Joseph, Blaine Nelson, Benjamin IP Rubinstein, and J. Doug Tygar. "[Adversarial machine learning](http://people.cs.vt.edu/~gangwang/class/cs6604/papers/Adversarial_AISEC.pdf)." In *Proceedings of the 4th ACM Workshop on Security and Artificial Intelligence*, pp. 43-58. 2011.

> Broad overview of security and privacy concerns (with examples of SVNs, predates DNN). Illustrates concerns quite well with two running examples of spam detection and network traffic analysis. Focuses on the model only.

Liu, Qiang, Pan Li, Wentao Zhao, Wei Cai, Shui Yu, and Victor CM Leung. "[A survey on security threats and defensive techniques of machine learning: A data driven view](https://www.researchgate.net/profile/Qiang_Liu14/publication/323154427_A_Survey_on_Security_Threats_and_Defensive_Techniques_of_Machine_Learning_A_Data_Driven_View/links/5a92b6e345851535bcd84848/A-Survey-on-Security-Threats-and-Defensive-Techniques-of-Machine-Learning-A-Data-Driven-View.pdf)." *IEEE access* 6 (2018): 12103-12117.

> Fairly accessible survey on security threats and defense techniques, providing a decent overview. Focus on the model itself.

McGraw, Gary, Harold Figueroa, Victor Shepardson, and Richie Bonett. "[An architectural risk analysis of machine learning systems: Toward more secure machine learning](https://berryvilleiml.com/docs/ara.pdf)." Technical report, Berryville Institute of Machine Learning, v 1.0 (2020).

> Fairly systematic and comprehensive list of possible security problems and corresponding controls and high-level strategies (not explicitly grounded or evaluated). Contains a useful architectural breakdown of the ML parts of a system, especially with regards to data. Could very well be used as a checklist during threat modeling. 

Wilhjelm, Carl, and Awad A. Younis. "[A threat analysis methodology for security requirements elicitation in machine learning based systems](https://qrs20.techconf.org/QRSC2020_FULL/pdfs/QRS-C2020-4QOuHkY3M10ZUl1MoEzYvg/891500a419/891500a419.pdf)." In *2020 IEEE 20th International Conference on Software Quality, Reliability and Security Companion (QRS-C)*, pp. 426-433. IEEE, 2020.

> Discussion of how ML-specific attacks can be mapped to STRIDE threat modeling with an example in the “evaluation” section. Not grounded but plausible.

Feffer, Michael, Anusha Sinha, Zachary C. Lipton, and Hoda Heidari. "[Red-Teaming for Generative AI: Silver Bullet or Security Theater?](https://arxiv.org/abs/2401.15897)" arXiv preprint arXiv:2401.15897 (2024).

> A critical discussion of the current discourse on "red teaming" analyzing six red-teaming reports and literature on the topic showing that it is poorly defined and used entirely inconsistently. Most work in this area is not systematic and does not have a clear articulation of safety properties or a threat model or any other specifications. While the paper does not explicitly makes the point, it becomes obvious that red teaming is a distraction and a good example of regulatory capture.

See also this [annotated bibliography](https://berryvilleiml.com/references/).


## 10. Reproducibility, Provenance

Halevy, Alon, Flip Korn, Natalya F. Noy, Christopher Olston, Neoklis Polyzotis, Sudip Roy, and Steven Euijong Whang. "[Goods: Organizing Google's datasets](https://dl.acm.org/doi/pdf/10.1145/2882903.2903730)." In Proceedings of the 2016 International Conference on Management of Data, pp. 795-806. 2016.

> This is a neat paper describing how data dependencies can be extracted
automatically from log files at Google. While the solution probably does
not generalize to many smaller organizations, the problem description
is well done and the solution is interesting. 

Cummaudo, Alex, Scott Barnett, Rajesh Vasa, John Grundy, and Mohamed Abdelrazek. "[Beware the evolving 'intelligent' web service! An integration architecture tactic to guard AI-first components](https://arxiv.org/abs/2005.13186)." *arXiv preprint arXiv:2005.13186* (2020).

> Paper discussing the problem of (silent) API evolution of webservices that provide ML  predictions, such as image classification, which trigger problems in client applications: Models of those services are updated, both internally and with regard to the domain of possible outputs without any public versioning or communication. The paper focuses on a mechanism to detect this when one has no control over the service, but I think the larger picture may be even more important for thinking about interface design: How to version (public or internal) prediction services and how to communicate such changes.

## 11. Interdisciplinary Teams

*Building software systems with machine learning components requires expertise in several domains, almost always by bringing together people with different backgrounds in interdisciplinary teams. Several papers explore how to foster such collaboration in a ML context, often with a focus on understanding particularly the interactions between data scientists and software engineers.*

Kim, Miryung, Thomas Zimmermann, Robert DeLine, and Andrew Begel. "[Data scientists in software teams: State of the art and challenges](https://doi.org/10.1109/tse.2017.2754374)." IEEE Transactions on Software Engineering 44, no. 11 (2017): 1024-1038.

> Discusses the role of data scientists and their challenges through interviews and surveys. See also the subsequent Amershi paper for a more ML-specific view.

Nahar, Nadia, Shurui Zhou, Grace Lewis, and Christian Kästner. “[Collaboration Challenges in Building ML-Enabled Systems: Communication, Documentation, Engineering, and Process](https://arxiv.org/abs/2110.10234).” In Proceedings of the 44th International Conference on Software Engineering (ICSE), May 2022.

> Our own interview study on collaboration challenges between data scientists and software engineers when building production ML systems. Lots of problems arise at the interface between the ML component and the rest of the system. Engineering is often undervalued, ML is difficult to fit into the larger process, documentation at the interfaces is often a big problem, and even communication across discipline boundaries can be difficult. The paper highlights that team structures differ substantially, but that certain problems associated with certain decisions such as whether to develop the model first and then build a system around it or whether to start with the system.

Busquim, Gabriel, Hugo Villamizar, Maria Julia Lima, and Marcos Kalinowski. "[On the Interaction Between Software Engineers and Data Scientists When Building Machine Learning-Enabled Systems](https://arxiv.org/abs/2402.05334)." In *International Conference on Software Quality*, pp. 55-75. Springer, 2024.

> Case study exploring in one project the collaboration challenges between software engineers and data scientists building a product, based on 4 interviews. Even though findings (e.g., regarding siloing and documentation) might not be novel and hard to generalize, it has several illustrative and concrete stories illustrating common challenges beyond the model. Most problems here evolve around the input and output data of the model API.

Almahmoud, Jumana, Robert DeLine, and Steven M. Drucker. "[How teams communicate about the quality of ML models: A case study at an international technology company](https://dl.acm.org/doi/abs/10.1145/3463934)." Proceedings of the ACM on Human-Computer Interaction 5, no. GROUP (2021): 1-24.

> Analysis of communication about model qualities between data scientists and other team members, based on 15 interviews and a large scale survey within Microsoft. Focuses mostly on mechanics of who communicates about what, in which form, and with which goals. Highlights conflicts between model and product goals, the importance of AI literacy, not having a common language, and model-first or model-only development challenges. Identifies that the most common communication goals regard risk management and explaining errors.

Passi, Samir, and Steven J. Jackson. "[Trust in data science: Collaboration, translation, and accountability in corporate data science projects](https://dl.acm.org/doi/abs/10.1145/3274405)." *Proceedings of the ACM on Human-Computer Interaction* 2, no. CSCW (2018): 1-28.

> Observations from two case studies about real negotiations between data scientists and business folks about what model is good enough and how trust in the model overall is incrementally established. Lots of evidence for the many human decisions when building a model that are all underdocumented and formed through intutition.

Ryan Orban. "[Bridging the Gap Between Data Science & Engineer: Building High-Performance Teams](https://www.slideshare.net/ryanorban/bridging-the-gap-between-data-science-engineer-building-highperformance-teams)." Presentation 2016

> Short presentation about the different roles of data scientists and software engineers and how to build interdisciplinary teams. Matches very closely my view of software engineering for AI-enabled systems, in that we still need data scientists and software engineers (and operators, and ...) as separate disciplines, but that we need a Devops-like integration around a common understanding and a joint mission.

Yang, Qian, Jina Suh, Nan-Chen Chen, and Gonzalo Ramos. "[Grounding interactive machine learning tool design in how non-experts actually build models](http://www.audentia-gestion.fr/MICROSOFT/Machine_Teaching_DIS_18.pdf)." In *Proceedings of the 2018 Designing Interactive Systems Conference*, pp. 573-584. 2018.

> Interesting view on how people without data science training (mostly software engineers) build machine learning models. In short, they often don’t check for generalization, don’t analyze their data or features much, and strongly prefer to write code. Points out communication and education gaps. Nice contrast between data scientists and software engineers, here focused on the data science tasks.

Wang, Dakuo, Justin D. Weisz, Michael Muller, Parikshit Ram, Werner Geyer, Casey Dugan, Yla Tausczik, Horst Samulowitz, and Alexander Gray. "[Human-AI Collaboration in Data Science: Exploring Data Scientists' Perceptions of Automated AI](https://www.researchgate.net/profile/Michael_Muller/publication/335703274_Human-AI_Collaboration_in_Data_Science_Exploring_Data_Scientists'_Perceptions_of_Automated_AI/links/5d76a0294585151ee4ab0338/Human-AI-Collaboration-in-Data-Science-Exploring-Data-Scientists-Perceptions-of-Automated-AI.pdf)." Proceedings of the ACM on Human-Computer Interaction 3, no. CSCW (2019): 1-24.

> IBM-internal interview study of how data scientists and software engineers think of AutoML and similar tools. Anticipating that AutoML is here to stay and that it will lead to augmentation rather than replacement of data scientists and will provide teaching opportunities.

Lvov, Ilia. "[Project Management in Social Data Science: integrating lessons from research practice and software engineering](http://hdl.handle.net/10023/18936)." PhD diss., University of St Andrews, 2019.

> In-depth case studies of interdisciplinary data science projects (from a social science angle), discussing many observed challenges related to collaboration,  process, and various tradeoffs. Lots of interesting observations. Afterward, an SE-inspired process model is suggested (and evaluated!) with checklists for all stages to foster planning and measuring progress. It seems that these checklists are useful to bring different stakeholders together and give them a joint planning document (boundary object).

Muller, Michael, Ingrid Lange, Dakuo Wang, David Piorkowski, Jason Tsay, Q. Vera Liao, Casey Dugan, and Thomas Erickson. "[How data science workers work with data: Discovery, capture, curation, design, creation](http://tomeri.org/DataScienceWorkers_CHI2019.pdf)." In *Proceedings of the 2019 CHI conference on human factors in computing systems*, pp. 1-15. 2019.

> Paper exploring how data scientists engage with data through 21 interviews at IBM. Emphasizes how data wrangling (cleaning, feature engineering) requires high effort and creativity. Pushes “conversation with data” as a description of this kind of work.

Aho, Timo, Outi Sievi-Korte, Terhi Kilamo, Sezin Yaman, and Tommi Mikkonen. "[Demystifying data science projects: A look on the people and process of data science today](https://helda.helsinki.fi/bitstream/handle/10138/322911/XP2020_Data_Science_12_.pdf?sequence=1)." In *International Conference on Product-Focused Software Process Improvement*, pp. 153-167. Springer, 2020.

> Study based on 6 interviews about process, roles, and teamwork in data science projects, largely model-centric. Identifying various teamwork challenges around managing exceptions, AI literacy, changing requirements, differences between data science and software development work, and so forth.

Subramonyam, Hariharan, Jane Im, Colleen Seifert, and Eytan Adar. "[Solving Separation-of-Concerns Problems in Collaborative Design of Human-AI Systems through Leaky Abstractions](https://arxiv.org/abs/2207.01749)." In *CHI Conference on Human Factors in Computing Systems*, pp. 1-21. 2022.

> Small-scale interview study about collaboration problems between some data scientists, some project managers, and 6 *user experience designers*, showing that collaboration is needed to work on the problem definition for the model and system in a somewhat agile fashion and that AI literacy is important. Often rather vague and the actual “leaky abstraction” argument seems to misunderstand classic modularity and software engineering work in my book though.

## 12. Human-AI Interaction

*This area is interesting and has seen significant attention recently, but goes beyond my typical software engineering considerations. See the [Human-AI Interaction](http://www.humanaiclass.org/) class at CMU for more pointers.*

Yang, Qian. "[The role of design in creating machine-learning-enhanced user experience](https://www.aaai.org/ocs/index.php/SSS/SSS17/paper/viewPaper/15363)." In *2017 AAAI Spring Symposium Series*. 2017.

> Excellent position paper arguing that currently most AI-enabled systems are driven by data availability rather than a vision for a product, leading to poor user experiences. Argues for the importance of designing the user interaction before or with developing the model, which needs AI literacy from UI designers and interdisciplinary collaboration. Has several good pointers to literature for going deeper.

Kocielnik, Rafal, Saleema Amershi, and Paul N. Bennett. "[Will you accept an imperfect AI? Exploring designs for adjusting end-user expectations of AI systems](http://library.usc.edu.ph/ACM/CHI2019/1proc/paper411.pdf)." In *Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems*, pp. 1-14. 2019.

> Cool mturk-style study to explore different means of setting expectations for users that the ML predictions of the system might be occasionally wrong. This is useful to think at the system level about mitigations for incorrect predictions, here focusing on how to present them to users. Discusses three concrete UI designs for a realistic setting (scheduling assistant).

Stumpf, Simone, Adrian Bussone, and Dympna O’sullivan. "[Explanations considered harmful? user interactions with machine learning systems](http://www.doc.gold.ac.uk/~mas02mg/HCML2016/HCML2016_paper_2.pdf)." In *Proceedings of the ACM SIGCHI Conference on Human Factors in Computing Systems (CHI)*. 2016.

> Interesting short paper with a small experiment, illustrating that explanations of a model’s predictions can foster trust for the prediction up to the point that the users (here physicians for a medical diagnosis) trust the system over their own judgment and accept more wrong predictions. The sentiment is that “the model seems to know more than me” even if the prediction and explanation are wrong.

Amershi, Saleema, Dan Weld, Mihaela Vorvoreanu, Adam Fourney, Besmira Nushi, Penny Collisson, Jina Suh et al. "[Guidelines for Human-AI Interaction](https://www.microsoft.com/en-us/research/uploads/prod/2019/01/Guidelines-for-Human-AI-Interaction-camera-ready.pdf)." In *Proceedings of the 2019 CHI conference on human factors in computing systems*, pp. 1-13. 2019.

> Curated collection of a number of high-level design guidelines extracted from (grey) literature survey and heavily workshoped and evaluated. Table 1 contains the main guidelines.

Kulesza, Todd, Margaret Burnett, Weng-Keen Wong, and Simone Stumpf. "[Principles of explanatory debugging to personalize interactive machine learning](ftp://az.engr.oregonstate.edu/pub/burnett/iui15-elucidebug.pdf)." In *Proceedings of the 20th international conference on intelligent user interfaces*, pp. 126-137. 2015.

> Nice example of a user interface with explanations (here Bayes model similar to spam filter) that helps users to build a mental model and adjust weights if needed to fix wrong predictions. Very explicit about design goals and decisions; lots of pointers to related work on mental models and debugging for end users.

Cai, Carrie J., Samantha Winter, David Steiner, Lauren Wilcox, and Michael Terry. "[’Hello AI’: Uncovering the Onboarding Needs of Medical Practitioners for Human-AI Collaborative Decision-Making](https://dl.acm.org/doi/abs/10.1145/3359206)." *Proceedings of the ACM on Human-Computer Interaction* 3, no. CSCW (2019): 1-24.

> Interesting overall discussion about what information users (in this case medical practitioners) need to trust and adopt an ML model’s predictions, based on an study with pathologists. For example, need to convey a mental model of how the AI works, need to explain what data was used to train the model and what features it uses (visible and not visible in UI) to gain trust. Lots of design and data decisions here.

Jacovi, Alon, Ana Marasović, Tim Miller, and Yoav Goldberg. "[Formalizing trust in artificial intelligence: Prerequisites, causes and goals of human trust in AI](https://arxiv.org/pdf/2010.07487)." Proc. FAccT (2021).

> Interesting conceptual discussion trying to define trust and trustworthiness, including an important recognition that risk is necessary for trust. They distinguish intrinsic trust which requires that a user’s prior believe align with how the model reasons (here explanations and capability tests are useful) and extrinsic trust from a positive track record in production or a rigorous evaluation as the two key directions to increase trust. They specifically talk about how adhering to partial contracts may be sufficient to establish trust, but remain somewhat vague on the concept beyond some vague references to subpopulations and capabilities.

Springer, Aaron, Victoria Hollis, and Steve Whittaker. "[Dice in the black box: User experiences with an inscrutable algorithm](https://arxiv.org/abs/1812.03219)." AAAI Spring Symp. (2017).

> Interesting small experiment: designing a ML-based system to rate text that is actually just random. Users will go to great length to interpret meaning into the system’s actions and seek confirmation bias for their own mental model, even if the system does not have any intelligence.

Ehsan, Upol, Samir Passi, Q. Vera Liao, Larry Chan, I. Lee, Michael Muller, and Mark O. Riedl. "[The who in explainable AI: how AI background shapes perceptions of AI explanations](https://arxiv.org/abs/2107.13509)." *arXiv preprint arXiv:2107.13509* (2021).

> Another paper critically exploring how end-user explanations of models can manipulate users, but here with a focus on how people with different backgrounds (with and without ML background) interpret explanations. The experiment shows how both ML experts and non-experts overtrust explanations based on numbers, even when inscrutable. Many lessons for designing explanations and possibilities for manipulation. Good related work sections. 

Alkhatib, Ali, and Michael Bernstein. "[Street-level algorithms: A theory at the gaps between policy and decisions](https://dl.acm.org/doi/abs/10.1145/3290605.3300760)." In *Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems*, pp. 1-13. 2019.

> Essay paper with three examples suggesting to use the idea of street-level bureaucracy (bureaucrats who make local decisions with some flexibility when administering the law) to explain some friction in rolling out automated decision making, especially when it comes to outliers and novel situations that bureaucrats and react can detect while ML automation does not. Even though the paper talks little about solutions or scale challenges, this may provide some nuanced insight into human-in-the-loop design of any software automation, not just machine learning.

Colaner, Nathan. “Is explainable artificial intelligence intrinsically valuable?” *AI & SOCIETY* 37 (2021): 231-238.

> Essay paper arguing that explainability is intrinsically valuable, not just to enable debugging, improve human-AI collaboration, or support human supervision and appeals. The paper argues that explainability is valuable and needed for human dignity, to understand what is happening to oneself, for participation and inclusion in society, and procedural justice. This encourages to have a broader view of explainability in machine learning.

## 13. Computational Notebooks

*There is quite a bit of work on computational notebooks recently, mostly 
focused on the exploratory work that data scientists perform. Some of this
is focused on poor software engineering practices, e.g., with regard to
testing, modularity, reuse, versioning, dependency management, and determinism. 
Many papers in this area study pain points and suggest new tooling extensions.*

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

> Personally, I find it rather surprising to use Notebooks for automation in production. Might be an interesting architectural and infrastructure decision worth discussing.

Yang, Chenyang, Shurui Zhou, Jin L.C. Guo, and Christian Kästner. “[Subtle Bugs Everywhere: Generating Documentation for Data Wrangling Code](https://www.cs.cmu.edu/~ckaestne/pdf/ase21.pdf).” In Proceedings of the 36th IEEE/ACM International Conference on Automated Software Engineering (ASE), 2021. 

> Adapting program synthesis and test suite minimization techniques to automatically generate summaries of the transformations performed on data frames within a notebook cell. This is shown the be useful to understand what happens and identify incorrect data transformations – which seem to be very common in public notebooks.

## 14. Machine Learning Libraries and APIs

*Software engineers like to study library adoption and challenges in using libraries and APIs. There are several papers that look specifically at APIs related to machine learning. Potentially useful when trying to understand the technical environment provided for data scientists.*

Zhang, Yuhao, Yifan Chen, Shing-Chi Cheung, Yingfei Xiong, and Lu Zhang. "[An empirical study on TensorFlow program bugs](https://doi.org/10.1145/3213846.3213866)." In Proceedings of the 27th ACM SIGSOFT International Symposium on Software Testing and Analysis, pp. 129-140. 2018.

Zhang, Tianyi, Cuiyun Gao, Lei Ma, Michael R. Lyu, and Miryung Kim. "[An empirical study of common challenges in developing deep learning applications](http://web.cs.ucla.edu/~miryung/Publications/isese2019-deeplearningchallenge.pdf)." In The 30th IEEE International Symposium on Software Reliability Engineering (ISSRE). 2019.

> These two papers are examples of papers that analyzes public bug reports from issue trackers or question-answer sites (stackoverflow) for machine-learning frameworks. They characterize the kinds of problems developers and users tend to have, some some solutions. Many issues seem to be common framework issues, such as documentation issues and breaking APIs. Some challenges, such as probabilistic correctness and missing debuggers, seem more ML specific.

Dilhara, Malinda, Ameya Ketkar, and Danny Dig. "[Understanding Software-2.0: a study of machine learning library usage and evolution](https://dl.acm.org/doi/abs/10.1145/3453478)." *ACM Transactions on Software Engineering and Methodology (TOSEM)* 30, no. 4 (2021): 1-42.

> Analysis of how machine learning libraries are used in popular Python code on GitHub, complementary to past studies of library use in notebooks (see Computational Notebooks section above). Focuses on how libraries are updated, finding many of the same challenges as with other library evolution and breaking changes in non-ML libraries. Interesting brief survey with answers from 28 project maintainers that introduced machine learning late in the project, indicating applications that use ML for a new feature or to replace some prior code.

Islam, Md Johirul, Hoan Anh Nguyen, Rangeet Pan, and Hridesh Rajan. "[What do developers ask about ML libraries? A large-scale study using stack overflow](https://arxiv.org/pdf/1906.11940)." *arXiv preprint arXiv:1906.11940* (2019).

> Large scale of stackoverflow questions related to 10 machine learning frameworks. Largely quantitative reporting, for example, which stages are most covered in those questions.

Chen, Zhenpeng, Yanbin Cao, Yuanqiang Liu, Haoyu Wang, Tao Xie, and Xuanzhe Liu. "[Understanding Challenges in Deploying Deep Learning Based Software: An Empirical Study](https://arxiv.org/pdf/2005.00760)." Proc. FSE (2020).

> Another StackOverflow study, this time focused on questions that developers ask regarding deploying deep learning models. Mostly API/documentation style questions close to the model rather than broader system deployment or MLOps questions and fairly shallow insights, but still potentially useful to see what developers struggle with current infrastructure at the API level. 

## 15. Misc

*Various recommended and useful resources that do not fit well into the other categories.*

Hopkins, Aspen, and Serena Booth. "[Machine Learning Practices Outside Big Tech: How Resource Constraints Challenge Responsible Development](http://www.slbooth.com/papers/AIES-2021_Hopkins_and_Booth.pdf)." In Proceedings of the 2021 AAAI/ACM Conference on AI, Ethics, and Society (AIES ’21) (2021).

> Very interesting interview studies with 17 participants from organizations building ML products outside of Big Tech companies, showing a wide range of challenges. The initial focus is on model fairness, but it shows how resource constraints influence many design decisions and tradeoffs and create many pain points in teams. Focused mostly on model development, not the larger system.

Martínez-Fernández, Silverio, Justus Bogner, Xavier Franch, Marc Oriol, Julien Siebert, Adam Trendowicz, Anna Maria Vollmer, and Stefan Wagner. "[Software Engineering for AI-Based Systems: A Survey](https://arxiv.org/abs/2105.01984)." *arXiv preprint arXiv:2105.01984* (2021).

> Incredibly ambitious and broad survey, covering all of software engineering for systems with AI components (not just model building and deployment). The scope is so wide that it won’t cover all papers in this area, often just selecting a few papers for a field with lots of research and tools (and they exclude grey literature), but it provides a very good overview and puts a lot of effort in organizing the literature.

Ameisen, Emmanuel. "Building Machine Learning Powered Applications: Going From Idea to Product." O'Reilly Media, 2020.

> Nice book that takes a wider view of building ML applications than most, starting with discussing product goals (not just ML model goals) and going up to deployment and monitoring. It mostly stays fairly close to the model with more detailed content on the ML pipeline (including guidance for quality assurance and debugging), whereas the coverage of requirements engineering and deployment is more high-level and shallow. Overall a nice book with a healthy engineering attitude and a view that exceeds beyond the ML model.

Zinkevich, Martin. 2017 “[Rules of Machine Learning: Best Practices for ML Engineering](http://martin.zinkevich.org/rules_of_ml/rules_of_ml.pdf).”

> Blog post. List of advice about engineering ML-enabled systems based on experience at Google. Many good pointers.

Akkiraju, Rama, Vibha Sinha, Anbang Xu, Jalal Mahmud, Pritam Gundecha, Zhe Liu, Xiaotong Liu, and John Schumacher. "[Characterizing Machine Learning Processes: A Maturity Framework](https://arxiv.org/pdf/1811.04871)." In *International Conference on Business Process Management*, pp. 17-31. Springer, Cham, 2020.

> Misleading title: Paper contains a list of advice for building AI-enabled systems based on experience at IBM. Not visibly grounded or validated, but some interesting parts, especially about pain points and collaboration points. Not actually discussing a maturity model (only a short draft excerpt shown at the very end).

Horneman, Angela, Andrew Mellinger, and Ipek Ozkaya. *[AI Engineering: 11 Foundational Practices](https://apps.dtic.mil/sti/pdfs/AD1099280.pdf)*. Carnegie Mellon University Pittsburgh United States, 2020.

> Very short technical report from the SEI, with a list of all-plausible recommendations (somewhat similar to the Zinkevich post above).

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

Rahman, Md Saidur, Emilio Rivera, Foutse Khomh, Yann-Gaël Guéhéneuc, and Bernd Lehnert. "[Machine learning software engineering in practice: An industrial case study](https://arxiv.org/abs/1906.07154)." *arXiv preprint arXiv:1906.07154* (2019).

> Discussion of challenges observed in a concrete industrial machine learning project with SAP. Observations are high-level lessons learned expressed as many rules and recommendations. Unfortunately, there is little discussion of research methods or how the rules trace to observations in the project.

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

Baylor, Denis, Eric Breck, Heng-Tze Cheng, Noah Fiedel, Chuan Yu Foo, Zakaria Haque, Salem Haykal et al. "[Tfx: A tensorflow-based production-scale machine learning platform](https://stevenwhang.com/tfx_paper.pdf)." In Proceedings of the 23rd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, pp. 1387-1395. 2017.

> High-level description of the machine learning infrastructure for building pipelines and model deployment by Google. Discusses engineering concerns and integrated tools across the entire pipeline, including among others automation and tracking in data transformation, training, and deployment. 

Wagstaff, Kiri. "[Machine learning that matters](https://arxiv.org/abs/1206.4656)." In Proceedings of the 29 th International Conference on Machine Learning, (2012).

> Nice essay about how much of ML research focuses on improving ML algorithms and evaluating on benchmarks with simple metrics, rather than focusing on impact and deployments. The latter requires a much broader scope of thinking in terms of the end-users' goals and the larger system. Good motivation for studying SE4AI/production ML.

Humbatova, Nargiz, Gunel Jahangirova, Gabriele Bavota, Vincenzo Riccio, Andrea Stocco, and Paolo Tonella. "[Taxonomy of real faults in deep learning systems](https://arxiv.org/abs/1910.11015)." In *Proceedings of the ACM/IEEE 42nd International Conference on Software Engineering*, pp. 1110-1121. 2020.

> Extensive study of problems data scientists face when using deep learning frameworks, using interviews, issue analysis (of projects using these frameworks!), and stackoverflow questions. Problems mostly related to network architecture, hyperparameters, and data quality.

Jiang, Ray, Silvia Chiappa, Tor Lattimore, András György, and Pushmeet Kohli. "[Degenerate feedback loops in recommender systems](https://dl.acm.org/doi/10.1145/3306618.3314288)." In *Proceedings of the 2019 AAAI/ACM Conference on AI, Ethics, and Society*, pp. 383-390. 2019.

> Very formal paper using simulation to study the effects of feedback loops of recommender systems on filter bubbles and echo chambers. Helps understanding the problem and thinking of solutions as part of the system’s design.

## 16. Others with Notes

*Not necessarily papers and books I recommend, but they may be of interest for specific concerns.*

Kuwajima, Hiroshi, Hirotoshi Yasuoka, and Toshihiro Nakae. "[Engineering problems in machine learning systems](https://link.springer.com/article/10.1007/s10994-020-05872-w?code=2c0c0228-4ff9-45e6-9285-d6dace01edc0)." *Machine Learning* 109, no. 5 (2020): 1103-1126.

> Position paper discussing various engineering challenges when building systems with machine learning components. Makes a clear distinctions between problems related to the model and problems related to the entire system that includes the model. Discusses a range of different challenges, though it is not clear how they were selected. Concludes with a discussion of a general quality model.

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

Lwakatare, Lucy Ellen, Aiswarya Raj, Jan Bosch, Helena Holmström Olsson, and Ivica Crnkovic. "[A taxonomy of software engineering challenges for machine learning systems: An empirical investigation](https://research.chalmers.se/publication/512250/file/512250_Fulltext.pdf)." In *International Conference on Agile Software Development*, pp. 227-243. Springer, 2019.

> Brief discussion of 7 case studies, mostly finding MLOps-style problems. The paper concludes with a potentially interesting maturity model (Sec 5), that, while not visibly grounded in data, may be a good starting point for discussions for framing different kinds of ML projects.

Wan, Zhiyuan, Xin Xia, David Lo, and Gail C. Murphy. "[How does machine learning change software development practices?](https://core.ac.uk/download/pdf/275589732.pdf)" *IEEE Transactions on Software Engineering* (2019).

> Discussion of challenges in developing ML systems based on interviews and a survey. Unfortunately, the paper does not distinguish consistently between the ML model, the framework used to learn the model, and the the system with an ML component, nor does it clearly distinguish between roles of software engineers or data scientists, leading to rather murky claims.

Ishikawa, Fuyuki, and Nobukazu Yoshioka. "How do engineers perceive difficulties in engineering of machine-learning systems? Questionnaire survey." In 2019 IEEE/ACM Joint 7th International Workshop on Conducting Empirical Studies in Industry (CESI) and 6th International Workshop on Software Engineering Research and Industrial Practice (SER&IP), pp. 2-9. IEEE, 2019.

> Fairly large-scale survey about pain points in developing ML-based systems. Mostly results as expected, but nice plots summarizing the most common difficulties.

Cambo, Scott Allen, and Darren Gergle. "User-centred evaluation for machine learning." In Human and Machine Learning, pp. 315-339. Springer, Cham, 2018.

> Book chapter on how to think about the design and evaluation of an ML component in a fitness tracker. Good argument why model accuracy alone may not be a good metric and how one should probably start much earlier in requirements and design to consider how model accuracy interacts with other parts of the system and user experience.

Ishikawa, Fuyuki, and Yutaka Matsuno. "Evidence-driven Requirements Engineering for Uncertainty of Machine Learning-based Systems." In 2020 IEEE 28th International Requirements Engineering Conference (RE), pp. 346-351. IEEE, 2020.

> Proposes a goal model extension for requirements engineering that explicitly considers alternative designs dependenting on how well a ML model performs (yet to be determined, deferring the decision during design). The paper has an interesting discussion about the challenge of prototyping in ML, where it may be very difficult to establish feasbility until very late in the project.

Lwakatare, Lucy Ellen, Aiswarya Raj, Ivica Crnkovic, Jan Bosch, and Helena Holmström Olsson. "Large-scale machine learning systems in real-world industrial settings: A review of challenges and solutions." Information and Software Technology 127 (2020): 106368.

> Literature survey of mostly published industrial experience reports about building ML-based systems, analyzing reported challenges and recommendations from those papers. Very useful for pointers to a number of experience reports and some summary of common concerns, see Table 4. Identify the common concers around availability, scalability, privacy, and safety, whereas security and usability are rarely mentioned in their papers. The solution part seems maybe somewhat shallow or obvious (Table 6). Grey literature not included and intermixing experience reports with academic studies and position papers; some papers and corresponding problems are also seem a bit dated now with recent advances.

Bosch, Nathan, and Jan Bosch. "[Software Logging for Machine Learning](https://arxiv.org/pdf/2001.10794)." *arXiv preprint arXiv:2001.10794* (2020).

> Good overview of problems with analyzing log files produced by software systems (including ML-enabled systems) and some collection of pointers to related work on log file parsing etc. The specific solution essentially requires some schema management and writing log files in a compact-machine readable format and more centralized planning.

de Souza Nascimento, Elizamary, Iftekhar Ahmed, Edson Oliveira, Márcio Piedade Palheta, Igor Steinmacher, and Tayana Conte. "[Understanding Development Process of Machine Learning Systems: Challenges and Solutions](https://www.ics.uci.edu/~iftekha/pdf/W.6.pdf)." In *2019 ACM/IEEE International Symposium on Empirical Software Engineering and Measurement (ESEM)*, pp. 1-6. IEEE, 2019.

> Small-scale interview study in 3 small Brazilian companies eliciting the ML process and three problems: identifying business goals, data definition, and undefined process. Suggest a checklist for each.

Haq, Fitash Ul, Donghwan Shin, Shiva Nejati, and Lionel Briand. "[Can Offline Testing of Deep Neural Networks Replace Their Online Testing?](https://arxiv.org/abs/2101.11118)" *Empirical Software Engineering* (2021).

> Paper compares model accuracy with a safety property assessed in a simulator in the context of determining the steering angle in a self-driving car, showing that accuracy is not a meaningful predictor for assuring the safety property. Not considering much of the system beyond a single model, and not really a fair comparison, and results shouldn’t be surprising, but another good reminder that prediction accuracy evaluation evaluations alone are usually not meaningful to establish system quality.

Bosch, Jan, Helena Holmström Olsson, and Ivica Crnkovic. "[Engineering AI systems: A research agenda](https://arxiv.org/pdf/2001.07522.pdf)." In *Artificial Intelligence Paradigms for Smart Cyber-Physical Systems*, pp. 1-19. IGI Global, 2021.

> Position paper listing a number of open research challenges for AI engineering in several application domains. These observations are based on consulting and interviews with companies (small start-ups to large corporations) in various domains, though no clear traceability is provided. Main focus is on ML components rather than the whole system.

Muiruri, Dennis, Lucy Ellen Lwakatare, Jukka K Nurminen, and Tommi Mikkonen. "[Practices and Infrastructures for ML Systems–An Interview Study](https://www.techrxiv.org/articles/preprint/Practices_and_Infrastructures_for_ML_Systems_An_Interview_Study/16939192)." Preprint, 2021.

> Another interview study with data scientists, here with 23 data scientists in Finland, asking about processes and tools around ML pipelines (model centric, not system focused). List of actually used tools is interesting, seems fairly advanced, providing a strong contrast with the technical debt paper.

Burkov, Andriy. *[Machine learning engineering](https://bookshop.org/books/machine-learning-engineering/9781999579579)*. True Positive Incorporated, 2020.

> Machine learning book with a decent engineering focused, albeit still almost entirely model centric. Covers entire ML pipeline from data collection, to feature engineering, to modeling, to model deployment and monitoring, often in a compact way. Especially the coverage of data quality exceeds typical books in this area.

McMahon, Andrew P. [Machine Learning Engineering with Python: Manage the production life cycle of machine learning models using MLOps with practical examples](https://bookshop.org/books/machine-learning-engineering-with-python-manage-the-production-life-cycle-of-machine-learning-models-using-mlops-with-practical-examples/9781801079259). Packt Publishing. 2021

> One of the better of the many recent MLOps books. This does not only explain specific tools (e.g., pytest, AWS, Postman, Sparks), but also provides more general technical explanation and engineering rationals for many decisions.


## 17. Other Lists

Miryung Kim has been teaching seminars at UCLA on debugging and data science/ML that is a great source for recommended readings as well, see http://web.cs.ucla.edu/~miryung/teaching/CS239-Winter2017/main.xhtml and http://web.cs.ucla.edu/~miryung/teaching/CS239-Winter2019/main.xhtml

Pooyan Jamschidi is teaching "Machine Learning Systems" a UofSC and recommended several readings to me when preparing for my course: https://pooyanjamshidi.github.io/mls/

Larysa Visengeriyeva has assembled an amazing list of resources on MLOps and related topics (books, talks, blog posts): https://github.com/visenger/mlops-references

Awesome Software Engineering for Machine Learning: https://github.com/SE-ML/awesome-seml

Annotated bibliography on ML security papers: https://berryvilleiml.com/references/
