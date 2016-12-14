---
layout: post
title:  "FluentSql for Dapper - A Walk through the code"
date:   2016-11-27 21:13:52 -0500
categories: Sql statements for Dapper
tags: Dapper Sql .NET Data Access
---
<div class="message">
# A .NET library that Produces Sql statements for Dapper
</div>
FluentSql was designed with the goal of writing Sql like statements using C# or VB. While using one Fluent interface, the library can produce different flavors of Sql statements: Oracle, MySql, Postgres, Sql Server. As of this version (1.7.9) the library produces Sql Server statements. It is my intension that by describing the architecture of this library there will be developers that would like to help in developing FluentSql further.

