---
title: groovy.cheatsheet

date: 2020-11-14T19:07:13+01:00
---#-#
#-# Variables
#-#

def x = 1
println x

x = new java.util.Date()
println x

x = -3.1499392
println x

x = false
println x

x = "Groovy!"
println x



#-#
#-# Collections
#-#

# Creating an empty list
def technologies = []

# Adding elements to the list
technologies.add("Grails")
technologies << "Groovy" // Left shift adds, and returns the list
technologies.addAll(["Gradle","Griffon"])

# Removing elements from the list
technologies.remove("Griffon")
technologies = technologies - 'Grails'

# Iterate over elements of a list
technologies.each { println "Technology: $it"}
technologies.eachWithIndex { it, i -> println "$i: $it"}

# Checking list contents
contained = technologies.contains( 'Groovy' )
contained = 'Groovy' in technologies
technologies.containsAll(['Groovy','Grails'])

# Sorting lists
technologies.sort() // also mutates original list
sortedTechnologies = technologies.sort(false) // without mutating the original

# Manipulating lists
Collections.replaceAll(technologies, 'Gradle', 'gradle')
Collections.shuffle(technologies, new Random())
technologies.clear()



#-#
#-# Maps
#-#

# Creating an empty map
def devMap = [:]

# Add values
devMap = ['name':'Roberto', 'framework':'Grails', 'language':'Groovy']
devMap.put('lastName','Perez')

# Iterate over elements of a map
devMap.each { println "$it.key: $it.value" }
devMap.eachWithIndex { it, i -> println "$i: $it"}

# Evaluate if a map contains a key
assert devMap.containsKey('name')

# Evaluate if a map contains a value
assert devMap.containsValue('Roberto')

# Get the keys of a map
println devMap.keySet()

# Get the values of a map
println devMap.values()



#-#
#-# Logical Branching and Looping
#-#

# Groovy supports the usual if - else syntax
def x = 3
if (x < 1) {
  println "X lower than One"
} else if (x == 1) {
  println "One"
} else if (x == 2) {
  println "Two"
} else {
  println "X greater than Two"
}

# Groovy also supports the ternary operator
def y = 10
def x = (y > 1) ? "worked" : "failed"
assert x == "worked"

# Iterate over a range
def x = 0
for (i in 0..30) {
  x += i
}

# Iterate over a list
def x = 0
for (i in [5,3,2,1]) {
  x += i
}

# Iterate over an array
def array = (0..20).toArray()
def x = 0
for (i in array) {
  x += i
}

# Iterate over a map
def map = ['name':'Roberto', 'framework':'Grails', 'language':'Groovy']
def x = 0
for (e in map) {
  x += e.value
}



#-#
#-# Operators
#-#

Operator Overloading for a list of the common operators that Groovy supports:
http://www.groovy-lang.org/operators.html#Operator-Overloading

# Spread operator: invoke an action on all items of an aggregate object
def technologies = ['Groovy','Grails','Gradle']
technologies*.toUpperCase() // = to technologies.collect { it?.toUpperCase() }

# Safe navigation operator: used to avoid a NullPointerException
def user = User.get(1)
def username = user?.username



#-#
#-# Closures
#-#

A Groovy Closure is like a "code block" or a method pointer. It is a piece of
code that is defined and then executed at a later point.
More info at: http://www.groovy-lang.org/closures.html

# Example
def clos = { println "Hello World!" }
println "Executing the Closure:"
clos()

# Passing parameters to a closure
def sum = { a, b -> println a+b }
sum(2,4)

# Closures may refer to variables not listed in their parameter list
def x = 5
def multiplyBy = { num -> num * x }
println multiplyBy(10)

# Closure that take a single argument can omit the parameter definition
def clos = { print it }
clos( "hi" )

# Groovy can memorize closure results [1][2][3]
def cl = {a, b ->
  sleep(3000) // simulate some time consuming processing
  a + b
}

mem = cl.memoize()

def callClosure(a, b) {
  def start = System.currentTimeMillis()
  mem(a, b)
  println "Inputs(a = $a, b = $b) - took ${System.currentTimeMillis() - start} msecs."
}

callClosure(1, 2)
callClosure(1, 2)
callClosure(2, 3)
callClosure(2, 3)
callClosure(3, 4)
callClosure(3, 4)
callClosure(1, 2)
callClosure(2, 3)
callClosure(3, 4)



#-#
#-# Expando
#-#

The Expando class is a dynamic bean so we can add properties and we can add
closures as methods to an instance of this class
http://mrhaki.blogspot.mx/2009/10/groovy-goodness-expando-as-dynamic-bean.html

def user = new Expando(name:"Roberto")
assert 'Roberto' == user.name

user.lastName = 'Pérez'
assert 'Pérez' == user.lastName

user.showInfo = { out ->
  out << "Name: $name"
  out << ", Last name: $lastName"
}

def sw = new StringWriter()
println user.showInfo(sw)



#-#
#-# Metaprogramming (MOP)
#-#

# Using ExpandoMetaClass to add behaviour
String.metaClass.testAdd = {
  println "we added this"
}

String x = "test"
x?.testAdd()

# Intercepting method calls
class Test implements GroovyInterceptable {
  def sum(Integer x, Integer y) { x + y }

  def invokeMethod(String name, args) {
    System.out.println "Invoke method $name with args: $args"
  }
}

def test = new Test()
test?.sum(2,3)
test?.multiply(2,3)

# Groovy supports propertyMissing for dealing with property resolution attempts.
class Foo {
  def propertyMissing(String name) { name }
}
def f = new Foo()

assertEquals "boo", f.boo



#-#
#-# TypeChecked and CompileStatic
#-#

Groovy, by nature, is and will always be a dynamic language but it supports
typechecked and compilestatic
More info: http://www.infoq.com/articles/new-groovy-20

# TypeChecked
import groovy.transform.TypeChecked

void testMethod() {}

@TypeChecked
void test() {
    testMeethod()
    def name = "Roberto"
    println naameee
}

# Another example:
import groovy.transform.TypeChecked

@TypeChecked
Integer test() {
  Integer num = "1"
  Integer[] numbers = [1,2,3,4]
  Date date = numbers[1]
  return "Test"
}

# CompileStatic example:
import groovy.transform.CompileStatic

@CompileStatic
int sum(int x, int y) {
  x + y
}

assert sum(2,5) == 7



