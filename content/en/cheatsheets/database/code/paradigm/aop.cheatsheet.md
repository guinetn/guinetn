---
title: aop.cheatsheet

date: 2020-11-14T19:07:13+01:00
---#-#
#-# Pointcut
#-#

# A pointcut is a program element that picks out join points and exposes data from the execution context of those join points.
# Pointcuts are used primarily by advice. They can be composed with boolean operators to build up other pointcuts.

               any type and number of args ─┐
                                 method ─┐  │
                                class ─┐ │  │
                                       │ │  │
@Pointcut("execution(public * com.demo.*.*(..))")
              │        │    │
              │        │    └─ any return type
              │        └─ access modifier
              └─ designator

#-# Pointcut designators

Type      Designator    Description
----      ----------    -----------
method    call          The pointcut will find all methods that calls a method in the demo package.
method    execution     The pointcut will find all methods in the demo package.
method    withincode    All the statements inside the methods in the demo package.
type      within        All statements inside the a class that ends with Test.
field     get           All reads to jdbcTemplate fields of type JdbcTemplate in the integration.db package. Includes all methods on this field if it’s an object.
field     set           When you set the jdbcTemplate field of type JdbcTemplate in the integration.db package to a new value.

@Pointcut("[method designator](* aspects.trace.demo.*.*(..))")
public void traceMethodsInDemoPackage() {}

@Pointcut("[type designator](*..*Test)")
public void inTestClass() {}

@Pointcut("[field designator](private org.springframework.jdbc.core.JdbcTemplate integration.db.*.jdbcTemplate)")
public void jdbcTemplateGetField() {}



