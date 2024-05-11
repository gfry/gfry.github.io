---
layout: post
title: "A Simple Data Stack That Works Is Better Than a Modern Data Stack That Nobody Uses"
date: 2024-05-11 07:10:33 +0800
categories: data
---

I liked [this article](https://medium.com/@jeremysrgt/production-ready-data-stack-in-a-week-5e679d321ea5). Not necessarily because I agree with every decision that is made in it, or because it's deeply insightful, but because it's one of the few articles I have seen that try to answer an important question:

> How do you build a useful data pipeline inside an organization that doesn't have a lot of resources to throw at data engineering?

I think this is a common case that doesn't get enough attention, in part, because it's not a particularly cool problem to solve.

There are many companies that are growing, and realize that they need to start doing something with the data they have in a separate environment. Maybe they need to create some reports as batch jobs, and don't want to burden their transactional database with it. Maybe they have some business questions that can only be answered through complex queries. Or maybe they just need to put together some dashboards to understand something about how people are using their product, or to help with customer service, but these dashboards have to be assembled from data that is currently spread throughout several places.

But, these same companies are often not growing so fast, and are not big enough yet, to be able to put together a complete data engineering team right now. Maybe they can transition one or two people to data engineering. Maybe they can hire a consultant. But they can't assemble a full, experienced, dedicated, data engineering squad. They probably also want to keep the costs of the data infrastructure contained.

I have seen this go wrong in two ways:

- They just outsource it to one of the big data platforms, to DataDog, Snowflake, Databricks, etc. Now, this can be a perfectly valid choice actually, and may even be the best choice for a lot of companies.But, especially if you are not careful and knowledgeable, can lead to vendor l;ock in and some huge bills down the line.
- Somebody in the team decides to be a hero (been there myself many times...) or the consultant is very persuasive, and a project is started to assemble a modern data stack with all the bells and whistles, something that will be able to grow basically infinitely and match whatever needs the company has in the future. One year in, nobody uses the data stack, because there are still data gaps, even in the golden zone, and they don't trust the correctness of any of the dashboards or reports. All the investment has been wasted so far, and the upper management is wondering if having a data stack at all was such a good idea.

I would like to highlight two choices that are made in the article that I think are particularly important to simplify the initial deployment and operation:

1. Using a database as your initial data lake/warehouse. You can get pretty far with a normal database. If you are feeling frisky, change PostgreSQL to DuckDB. Or maybe Clickhouse. But at first stay away from parquet files stored on S3, HDFS, or proper data warehouses like RedShift. A simpler database is going to be much easier to operate on, and will lead to fewer problems of duplicate or missing data at the beginning. Perhaps equally important, it will have a reasonable and well controlled price.
2. Using a simple task execution system instead of Airflow or similar.A cron job might be enough , really, but I really like the idea of using Fargate tasks started by CRON like events from EventBridge.

There is nothing wrong with starting with a simple data stack, that is going to meet all your needs for a couple of years (if not forever) and that will show to the rest of the company how valuable having a separate data stack is. If the company does grow exponentially, and you need a more advanced stack, you will have a much easier time justifying the kind of investment that is needed to assemble a more complex one that will actually work.