---
layout:     post
title:      2021-11-27-Design pattern-CQRS
subtitle:   CQRS - Command and Query Responsibility Segregation
date:       2021-11-27
author:     BY HY
header-img: img/post-bg-designpattern.png
catalog: true
tags:
    - Design Pattern
    - Software Architecture
---
# CQRS - 读写分离

Command and Query Responsibility Segregation separates read and update operations for a data store. Basic CRUD data system works well with same data model. In complex cases, the read side might perform many different queries, returning DTOs(data transfer objects) with different shapes. Object mapping can become complicated. On the write side, the model may implement complex validation and business logic.

On the other hand, read and write workloads are often asymmetrical, with very different performance and scale requirements.

