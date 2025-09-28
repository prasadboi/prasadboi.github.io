---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======

* M.S. in CS @ NYU (Courant Institute of Mathematical Sciences), Aug. 2024 - May 2026 (Expected)
* B.Engg. in Computer Science, Birla Institute of Technology and Science, Pilani - Hyderabad, Aug. 2019 - June 2023

Work experience
======

* Jun 2023 – Aug 2024: Data Analytics Engineer
  * Providence Health Care — Hyderabad, India
  * Engineered ETL pipelines in **Azure Data Factory** for an in-house migration tool (Ultrasonic), handling **10M+** rows across heterogeneous sources/targets.
  * Built a **Snowflake** analytics framework and **Power BI** dashboards with advanced stored procedures; internalized marketing KPIs and eliminated **>$2M** in outsourcing.
  * Shipped **CI/CD** for SQL deployments (Azure DevOps), cutting ~**60 hours/month** of manual work.
  * **STACK:** Azure Data Factory, Snowflake, Python, SQL, Power BI, Azure DevOps

* Jan 2023 – Jun 2023: Machine Learning Intern  
  * SuperPe.in (formerly Mewt.in) — Bengaluru, India
  * Built analytics dashboards for sales/merchant funnels; identified bottlenecks that reduced drop-offs by **~40%**.
  * Developed an **OCR** pipeline (Google Vision + OpenCV) to extract/validate IDs with **~97%** accuracy; deployed on **AWS Lambda + EFS**.
  * Prototyped a multi-agent and **RAG** enabled assistant (LangChain + Milvus) to automate customer query resolution. Included features -- conversation history, session management, token streaming, vector search
  * **STACK:** PostgreSQL, FastAPI, OpenCV, LangChain, Milvus, AWS, Google Cloud Vision, OpenAI API

Skills
======

* **ML Engineering**
  * Search & Ranking, RAG, ML Systems, Vector DBs, NLP, CV, LLMs, Distributed training/inference
  * PyTorch, Tensorflow, Hugging Face, Weights & Biases, LangChain, vLLM

* **Data Engineering**
  * SQL, PostgreSQL, Snowflake, Vector DBs, HDFS, MapReduce, Azure Data Factory, Power BI
  * ETL, Database Design, CI/CD

* **Software Engineering**
  * Java, C/C++, Python, REST Framework, FastAPI, Django, CUDA, Git, Docker, Kubernetes, Singularity;
  * AWS S3, Amazon EC2, AWS Lambda, Google Compute Engine
  * Distributed Systems, Microservice Architecture, High Performance Computing Systems

Publications
======

  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  
<!-- Talks
======
  <ul>{% for post in site.talks reversed %}
    {% include archive-single-talk-cv.html  %}
  {% endfor %}</ul> -->
  
Teaching
======

  <ul>{% for post in site.teaching reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  
<!-- Service and leadership
======

* Currently signed in to 43 different slack teams -->
