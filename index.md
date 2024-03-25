---
layout: post
title:  "NTCIR-18 Automatic Evaluation of LLMs (AEOLLM) Task"
date:   2024-03-22
categories: mediator feature
tags: featured
markdown: kramdown
image: /assets/images/tokyo-night-view-i82930.jpeg
image2: /assets/images/tokyo-night-view-i82930.jpeg
---

Introduction
===
The Automatic Evaluation of LLMs (AEOLLM) task is a new core task in [NTCIR-18](https://research.nii.ac.jp/ntcir/ntcir-18/) to support in-depth research on large language models (LLMs) evaluation. As LLMs grow popular in both fields of academia and industry, how to effectively evaluate the capacity of LLMs becomes an increasingly critical but still challenging issue. Existing methods can be divided into two types: manual evaluation, which is expensive, and automatic evaluation, which faces many limitations including the task format (the majority belong to multiple-choice questions) and evaluation criteria (occupied by reference-based metrics). To advance the innovation of automatic evaluation, we proposed the Automatic Evaluation of LLMs (AEOLLM) task which focuses on generative tasks and encourages reference-free methods. Besides, we set up diverse subtasks such as summary generation, non-factoid question answering, text expansion, and dialogue generation to comprehensively test different methods. We believe that the AEOLLM task will facilitate the development of the LLMs community.

Methodology
===
First, we choose four subtasks as shown in the table:
- **Fully Observed Session Search (FOSS)**: For a *k*-length session, we provide full session contexts in the first (*k-1*) queries. Participants need to re-rank the candidate documents for the last query of a session. This setting follows TREC Session Tracks to enable ad-hoc evaluation by using metrics such as NDCG, AP, and RBP, etc.
- **Partially Observed Session Search (POSS)**: In this subtask, we truncate all sessions before the last query. For a session with *k* queries (*k* &ge; 2), we only reserve the session contexts in the first queries, where *1* &le; *n* &le; *k-1*. The value of *n* varies in different sessions. Participants will need to re-rank documents for the last *k*-*n* queries(query) according to the partially observed contextual information in previous search rounds. Session-level metrics such as RS-DCG and RS-RBP will be adopted for the evaluation of system effectiveness.

Differences between SS and previous related work
---

| | NTCIR-16 Session Search (SS) | TREC Session Tracks |
| :------ | :------ | :------ |
| Number of Sessions (in Chinese) | - Training: 147, 154, with human relevance labels for the last query of 2, 000 sessions.<br> - FOSS Testing Subtask: 1, 817.<br> - POSS Testing Subtask: 1, 203. | English: 76~1, 257 |
| Session Datasets | - Extracted from a Sogou search log and two field study datasets | Session Track 2011-2014 |
| Document Collection | - With about 1, 000, 000 documents.<br>- Contains 81.23 candidate documents in average for all queries in the testing set. | ClueWeb09/ClueWeb12 |
| Source/Generation of session data | Refined from a search log from Sogou.com or extracted from two large-scale field studies. | Generated by real search users based on manually designed topics. |
| Support from log analysis for annotation? | &radic; | &times; |
| Support session-level evaluation? | &radic; | &times; |


Expected Results
---
We plan to attract at least 15 active participants. As this is the first year, we only construct **Chinese-centric** session collections. Participants could leverage the training set for either single-task or multi-task learning. As for the testing collection, the number of session in both subtasks are expected to be more than 1,000. Having collected running results from all teams, we will recruit accessors for relevance annotation and further use both query-level and session-level metrics for evaluation. Through these efforts, we hope that there will be a technological breakthrough in optimizing session-level document ranking.


Important Dates
---
*All deadlines are at 11:59pm in the Anywhere on Earth (AOE) timezone.*  
<span class="event">**Session Search registration Due**:</span> <span class="date">👉Aug 25, 2021</span>  
<span class="event">**Dataset Release**:</span> <span class="date">Aug 15, 2021</span>  
<span class="event">**Formal Run**:</span> <span class="date">Oct 1, 2021 - Nov 30, 2021</span>  
<span class="event">**Relevance Assessment**:</span> <span class="date">Dec, 2021 - Jan, 2022</span>    
<span class="event">**Evaluation Result Release**:</span> <span class="date">Feb 1, 2022</span>  
<span class="event">**Draft Task Overview Paper Release**:</span> <span class="date">Feb 1, 2022</span>  
<span class="event">**Draft Participant Paper Submission Due**:</span> <span class="date">Mar 1, 2022</span>  
<span class="event">**All Camera-ready Paper Submission Due**:</span> <span class="date">May 1, 2022</span>  
<span class="event">**NTCIR-16 Conference in NII, Tokyo, Japan**:</span> <span class="date">Jun 2022</span><br> 


Evaluation Measures
---
For the FOSS subtask, we adopt nDCG, AP, and RBP, etc.  
For the POSS subtask, we use session-level metrics such as RS-DCG and RS-RBP.  
The official evaluation tool is coming soon!


Data and File format
---
We provide three directories:
```
NTCIR-16-SS
|
|----- ./document_collection 
|              	|----- ./doc [A collection with about 1, 000, 000 pages. Each directory contains about 10, 000 files. ]
|              	|----- qid2docs.json [A file mapping testing query IDs into their corresponding candidate document IDs.]
|
|----- ./sessions
|			|----- ./training |----- training_sessions.txt		
|			|
|			|----- ./testing
|						|----- ./FOSS |------ testing_sessions_foss.txt		
|						|
|						|----- ./POSS |------ testing_sessions_poss.txt						
|				
|----- ./training_human_labels |----- human_labels.txt
|----- README.md
```

1) Firstly, for all session files, each session is split by two line breaks (```\n\n```).  

2) **Each training session is formatted as follows:**
```
SessionID	87
----------------------------
画杨桃	q198	1427848224.93
1	http://www.lbx777.com/yw06/x_hyt/kewen.htm	d1882	404	0	-1
2	http://pic.sogou.com/pics?query=%BB%AD%D1%EE%CC%D2&p=40230500&st=255&mode=255	d1883	<unk>	0	-1
3	http://tv.sogou.com/v?query=%BB%AD%D1%EE%CC%D2&p=40230600&tn=0&st=255	d1884	画杨桃-搜索页	0	-1
4	http://baike.sogou.com/v8080089.htm	d1885	画杨桃	0	-1
5	http://www.lspjy.com/thread-112497-1-1.html	d1886	人教版小学三年级下册语文《画杨桃》教学设计优质课教案	0	-1
6	http://weixin.qq.com/	d5	微信，是一个生活方式	0	-1
7	http://wenku.baidu.com/view/fa4903205901020207409c89.html	d1887	【图文】画杨桃_百度文库	0	-1
8	http://www.21cnjy.com/2/8135/	d1888	画杨桃课件_	0	-1
9	http://wenwen.sogou.com/s/?sp=S%E7%94%BB%E6%9D%A8%E6%A1%83	d1889	搜狗搜索	0	-1
10	http://www.aoshu.com/e/20090604/4b8bcabd28495.shtml	d1890	画杨桃_三年级语文下册课件_奥数网	0	-1
----------------------------
画杨桃ppt课件	q199	1427848230.2
1	http://wenku.baidu.com/view/bfe0c8edf8c75fbfc67db205.html	d1894	【图文】画杨桃ppt课件精品_百度文库	1	1427848232.105
2	http://www.1ppt.com/kejian/8846.html	d1895	《画杨桃》PPT课件	0	-1
3	http://www.1ppt.com/kejian/8851.html	d1896	《画杨桃》PPT课件6	0	-1
4	http://www.xiexingcun.com/xy6/HTML/53403.html	d1897	《画杨桃》公开课ppt课件（24页）-免费高速下载	0	-1
5	http://renjiaoban.21jiao.net/sanxia/huayangtao/	d1898	<unk>	0	-1
6	http://yuwen.chazidian.com/kejian108520/	d1899	画杨桃ppt课件下载	0	-1
7	http://www.docin.com/d-239045.html	d1900	<unk>	0	-1
8	http://www.glzy8.com/show/162484.html	d1901	11画杨桃PPT课件_管理资源吧	0	-1
9	http://www.xiexingcun.com/xy6/HTML/17470.html	d1902	《画杨桃》ppt课件-免费高速下载	0	-1
10	http://www.xiexingcun.com/xy6/HTML/61592.html	d1903	《画杨桃》ppt课件【13页】-免费高速下载	0	-1
----------------------------
画杨桃ppt	q200	1427848257.0
1	http://wenku.baidu.com/view/300cd979f242336c1eb95e2b.html	d1904	【图文】画杨桃PPT_百度文库	1	1427848258.188
2	http://www.1ppt.com/kejian/8846.html	d1895	《画杨桃》PPT课件	0	-1
3	http://wenku.baidu.com/view/e7e42c25b4daa58da0114ad4.html	d1905	【图文】画杨桃ppt课件_百度文库	0	-1
4	http://www.xiexingcun.com/xy6/HTML/53403.html	d1897	《画杨桃》公开课ppt课件（24页）-免费高速下载	0	-1
5	http://www.docin.com/d-239045.html	d1900	<unk>	0	-1
6	http://www.xiexingcun.com/xy6/HTML/53401.html	d1906	《画杨桃》ppt课件（19页）-免费高速下载	0	-1
7	http://www.landong.com/x_yw_117_3640.htm	d1907	<unk>	0	-1
8	http://www.xiexingcun.com/xy6/HTML/61592.html	d1903	《画杨桃》ppt课件【13页】-免费高速下载	0	-1
9	http://www.1ppt.com/kejian/8851.html	d1896	《画杨桃》PPT课件6	0	-1
10	http://www.doc88.com/p-891111956128.html	d1908	【精品】：画杨桃PPT	0	-1
```
* The first line: ```<SessionID><tab><session ID>```, such as ```SessionID	87```.
* The first line in a query: ```<query string><tab><query ID><tab><query start time>```, such as ```画杨桃	q198	1427848224.93```.
* Each rest line in a query: ```<rank><tab><url><tab><document ID><tab><document title><tab><clicked><tab><click timestamp>```, such as ```2	http://www.1ppt.com/kejian/8846.html	d1895	《画杨桃》PPT课件	0	-1```.
* If the title of a document is unknown, then the document title will be represented by ```<unk>```.
* If a document is not clicked, then the click timestamp is -1.

3) **Each testing session is formatted as follows:**
```
SessionID	8
----------------------------
Tensorflow	q64324	1596009033.208
1	https://tensorflow.google.cn/	d527264	TensorFlow	0	-1	2
2	http://c.biancheng.net/tensorflow/	d527265	TensorFlow教程:TensorFlow快速入门教程(非常详细)	0	-1	0
3	https://baike.baidu.com/item/Tensorflow/18828108	d527266	TensorFlow_百度百科	0	-1	0
4	https://www.oschina.net/p/tensorflow?hmsr=aladdin1e1	d527267	TensorFlow - 机器学习系统	0	-1	0
5	https://www.oschina.net/p/tensorflow?hmsr=aladdin1e1	d527267	TensorFlow - 机器学习系统	0	-1	0
6	http://playground.tensorflow.org/	d527268	tensorflow neural network playground - A Neural Network...	0	-1	2
7	https://github.com/tensorflow/tensorflow	d527269	GitHub - tensorflow/tensorflow: An Open Source Machine...	0	-1	0
8	https://www.jianshu.com/p/4665d6803bcf	d527270	TensorFlow入门极简教程(一) - 简书	0	-1	0
9	https://www.zhihu.com/question/49909565	d527271	TensorFlow 如何入门,如何快速学习? - 知乎	0	-1	0
10	https://blog.csdn.net/l7h9ja4/article/details/92857163	d527272	终于来了!TensorFlow 2.0入门指南(上篇)_机器学习算法..._CSDN博客	0	-1	0
----------------------------
Pytorch	q64325	1596009037.5
```
* The first line: ```<SessionID><tab><session ID>```, such as ```SessionID	8```.
* The first line in an observed/unobserved query: ```<query string><tab><query ID><tab><query start time>```, such as ```Tensorflow	q64324	1596009033.208```.
* Each rest line in an observed query: ```<rank><tab><url><tab><document ID><tab><document title><tab><clicked><tab><click timestamp><tab><usefulness>```, such as ```1	https://tensorflow.google.cn/	d527264	TensorFlow	0	-1	2```.
* If the title of a document is unknown, then the document title will be represented by ```<unk>```.
* If a document is not clicked, then the click timestamp is -1.
* The usefulness ratings are 4-scale (0-3), annotated by the first-tier search users. We provide this information to explore to what extent search systems will be improved if true and instant user feedback is available.

4) **Each line in the ```human_labels.txt``` is formatted as:**```<ID><tab><training session ID><tab><query ID><tab><document ID><tab><relevance><tab><valid>```.


Submission format
---
1) Each team can submit up to **six** NEW or REP runs for each subtask.  
2) The submission file should be named as ```[TEAMNAME]-{FOSS, POSS}-{NEW, REP}-[1-5].txt```, such as ```THUIR1-FOSS-NEW-1.txt```. Note that for the organizers' convenience, there should not be any hyphen-minus (```-```) in the TEAMNAME. A NEW run means you use a novel approach, while a REP run means you reproduce some model.  
3) As for the content, the first line should be a short English description of this particular run, such as ```BM25F with Pseudo-Relevance Feedback```. The rest lines should be formatted as ```[SessionID]<tab>[QueryID]<tab>[QueryPosInSession]<tab>[DocumentID]<tab>[Rank]<tab>[Score]<tab>[RunName]```. Such as  
```
1<tab>q3<tab>2<tab>d587602<tab>1<tab>27.73<tab>THUIR-FOSS-NEW-1
1<tab>q3<tab>2<tab>d587603<tab>2<tab>25.15<tab>THUIR-FOSS-NEW-1

```
Please do not include more than **20** candidate documents per case!

Submitting runs
--- 
TBA


Organisers
---
<em>Yiqun Liu</em> [yiqunliu@tsinghua.edu.cn] (Tsinghua University)  
<em>Jia Chen</em> [chenjia0831@gmail.com] (Tsinghua University)  
<em>Fan Zhang</em> [franky94@gmail.com] (Wuhan University)   
<em>Jiaxin Mao</em> [maojiaxin@gmail.com] (Renmin University of China)  
<em>Weizhi Ma</em> [mawz12@hotmail.com] (Tsinghua University)  
<em>Xiaohui Xie</em> [xiexh_thu@163.com] (Tsinghua University)  

<br>Contact Email: ***session-search-org@googlegroups.com***  
Please feel free to contact us! 😉


References
---
[1] Carterette, B., Kanoulas, E., Hall, M., & Clough, P. (2014). Overview of the TREC 2014 session track. [pdf](https://apps.dtic.mil/sti/pdfs/ADA618627.pdf)  
[2] Yang, G. H., & Soboroff, I. (2016). TREC 2016 Dynamic Domain Track Overview. In TREC. [pdf](http://infosense.cs.georgetown.edu/publication/80.pdf)  
[3] Zhang, F., Mao, J., Liu, Y., Ma, W., Zhang, M., & Ma, S. (2020, July). Cascade or Recency: Constructing Better Evaluation Metrics for Session Search. In Proceedings of the 43rd International ACM SIGIR Conference on Research and Development in Information Retrieval (pp. 389-398). [pdf](http://www.thuir.cn/group/~mzhang/publications/SIGIR2020-ZhangFan1.pdf)  
[4] Chen, J., Mao, J., Liu, Y., Zhang, M., & Ma, S. (2019, November). TianGong-ST: A New Dataset with Large-scale Refined Real-world Web Search Sessions. In Proceedings of the 28th ACM International Conference on Information and Knowledge Management (pp. 2485-2488). [pdf](http://www.thuir.cn/tiangong-st/CIKM19Chen.pdf)  
[5] Liu, M., Liu, Y., Mao, J., Luo, C., & Ma, S. (2018, June). Towards designing better session search evaluation metrics. In The 41st International ACM SIGIR Conference on Research & Development in Information Retrieval (pp. 1121-1124). [pdf](http://www.thuir.org/group/~YQLiu/publications/SIGIR18-Liu.pdf)  

***


Supported by
---
![](/assets/images/organizer.png)