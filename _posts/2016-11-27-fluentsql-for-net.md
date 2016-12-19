---
layout: post
title:  "FluentSql for Dapper - A Walk through the code"
date:   2016-11-27 21:13:52 -0500
categories: Sql statements for Dapper
tags: Dapper Sql .NET Data Access
---
<div class="message" >
FluentSql is a library that Produces Sql statements for Dapper
</div>

FluentSql was designed with the goal of writing Sql like statements using C# or VB while using a fluent api. In addition, the library can produce different flavors of Sql statements: Oracle, MySql, Postgres, Sql Server. As of this version (1.7.9) the library produces Sql Server statements only. It is my intension that by describing how this library is put together there will be developers that would like to join the effort in moving this work forward.

![placeholder](https://ernestoherrera.github.io/public/images/FluentSqlDiagram_Medium.png)

At start up, FluentSql uses the class that implements IDatabaseMapper interface. By default, the SqlServerDatabaseMapper class is selected if there is no other assigned. The only method that this class has to implement is the following:

    IEnumerable<Table> MapDatabase(IDbConnection connection, IEnumerable<Database> targetDatabases);

This method returns a list of Table objects that describe each table in the target database. In turn, the Table object has a public property that returns a list of Column objects. This is task number one when creating a new supporting Sql dialect. One can look into SqlServerConstants class to see the Sql statements that were used to map a Sql server database.

After the database is mapped out, the class that implements IEntityMapper looks for entity types that match the database table names. Since the entity types are named in the singlular, and, sometimes, the database tables are named in the plural, the EntityMapper class attempts to match the entity name with the table name by turning the table name to its singular form.

Implementing the ISqlGenerator interface is step number two when creating a new Sql dialect. The SqlServerSqlGenerator class is a good example as to how to build the new class. In short, all the base classes that implement query functionality are already developed and most of the work that needs to be done is to overwrite the ToSql method.

In some instances, one may need to provide Sql dialect specific tests. One of the goals of this project is to make the current set of test cases work for the different Sql dialects. Therefore, one does not need to implement all test cases.

<iframe src="https://ghbtns.com/github-btn.html?user={{ site.github_username }}&repo=FluentSql&type=fork&count=true" frameborder="0" scrolling="0" width="170px" height="20px"></iframe>
<div><a href="https://github.com/ernestoherrera/FluentSql" style="color:#000">{% octicon mark-github %} Project site</a></div>


