---
title: hystrix.cheatsheet

date: 2020-11-14T19:07:13+01:00
---#-#
#-# Annotations
#-#

#-# @HystrixCollapser

Property                      Default                                Description
--------                      -------                                -----------
collapserKey                  Name of annotated method               Specifies a collapser key.
batchMethod                   -                                      Method name of batch command which must have the following signature: java.util.List method(java.util.List).
scope                         Scope.REQUEST                          Defines what scope the collapsing should occur within.
collapserProperties           {}                                     Specifies collapser properties.


#-# @HystrixCommand

Property                      Default                                Description
--------                      -------                                -----------
groupKey                      Class name of annotated method         Used for grouping together commands such as for reporting, alerting, etc.
commandKey                    Name of annotated method               Hystrix command key
threadPoolKey                 -                                      The thread-pool key is used to represent a HystrixThreadPool for monitoring, metrics publishing, caching and other such uses.
fallbackMethod                -                                      The method to process fallback logic which should be defined in the same class as the HystrixCommand.
commandProperties             {}                                     Specifies command properties
threadPoolProperties          {}                                     Specifies thread pool properties.
ignoreExceptions              {}                                     Defines exceptions which should be ignored and wrapped to throw in HystrixBadRequestException.


#-# @HystrixProperty

Property                      Default                                Description
--------                      -------                                -----------
name                          -                                      Property name.
value                         -                                      Property value.


#-# @CacheResult

Property                      Default                                Description
--------                      -------                                -----------
cacheKeyMethod                -                                      A method name to be used to get a key for request caching.


#-# @CacheRemove

Property                      Default                                Description
--------                      -------                                -----------
commandKey                    Name of annotated method               The name of the Hystrix command for which the cache should be cleared.
cacheKeyMethod                -                                      A method name to be used to get a key for request caching.


#-# @CacheKey

Property                      Default                                Description
--------                      -------                                -----------
value                         -                                      Allows to specify the name of a certain argument property.



#-#
#-# Properties
#-#

#-# @HystrixCollapser.collapserProperties

Property                                              Default        Description
--------                                              -------        -----------
maxRequestsInBatch                                    Int.MAX        The max nr of requests allowed in a batch before this triggers a batch execution.
timerDelayInMilliseconds                              10             The number of milliseconds after the creation of the batch that its execution is triggered.
requestCache.enabled                                  true           Indicates whether request caching is enabled for HystrixCollapser.execute() and HystrixCollapser.queue() invocations.


#-# @HystrixCommand.commandProperties

# Execution
Property                                              Default        Description
--------                                              -------        -----------
execution.isolation.strategy                          THREAD         The isolation strategy HystrixCommand.run() executes with.
execution.isolation.thread.timeoutInMilliseconds      1000           The time in milliseconds after which the caller will observe a timeout and walk away from the command execution.
execution.timeout.enabled                             true           Indicates whether the HystrixCommand.run() execution should have a timeout.
execution.isolation.thread.interruptOnTimeout         true           Indicates whether the HystrixCommand.run() execution should be interrupted when a timeout occurs.
execution.isolation.semaphore.maxConcurrentRequests   10             Max nr of requests allowed to a HystrixCommand.run() method when using ExecutionIsolationStrategy.SEMAPHORE.


# Fallback
Property                                              Default        Description
--------                                              -------        -----------
fallback.isolation.semaphore.maxConcurrentRequests    10             The max nr of requests a HystrixCommand.getFallback() method is allowed to make from the calling thread.
fallback.enabled                                      true           Determines whether a call to HystrixCommand.getFallback() will be attempted when failure or rejection occurs.


# Circuit Breaker
Property                                              Default        Description
--------                                              -------        -----------
circuitBreaker.enabled                                true           Determines whether a circuit breaker will be used to track health and to short-circuit requests if it trips.
circuitBreaker.requestVolumeThreshold                 20             The minimum number of requests in a rolling window that will trip the circuit.
circuitBreaker.sleepWindowInMilliseconds              5000           The amount of time, after tripping the circuit, to reject requests before allowing attempts again to determine if the circuit should again be closed.
circuitBreaker.errorThresholdPercentage               50             The error percentage at or above which the circuit should trip open and start short-circuiting requests to fallback logic.
circuitBreaker.forceOpen                              false          Forces the circuit breaker into an open (tripped) state in which it will reject all requests. Takes precedence over circuitBreaker.forceClosed.
circuitBreaker.forceClosed                            false          Forces the circuit breaker into a closed state in which it will allow requests regardless of the error percentage.


# Metrics
Property                                              Default        Description
--------                                              -------        -----------
metrics.rollingStats.timeInMilliseconds               10000          The duration of the statistical rolling window, in milliseconds. This is how long Hystrix keeps metrics for the circuit breaker to use and for publishing.
metrics.rollingStats.numBuckets                       10             The number of buckets the rolling statistical window is divided into.
metrics.rollingPercentile.enabled                     true           Indicates whether execution latencies should be tracked and calculated as percentiles.
metrics.rollingPercentile.timeInMilliseconds          60000          The duration of the rolling window in which execution times are kept to allow for percentile calculations
metrics.rollingPercentile.numBuckets                  6              The number of buckets the rollingPercentile window will be divided into.
metrics.rollingPercentile.bucketSize                  100            The maximum number of execution times that are kept per bucket. If more executions occur during the time they will wrap around and start over-writing at the beginning of the bucket.
metrics.healthSnapshot.intervalInMilliseconds         500            The time to wait between allowing health snapshots to be taken that calculate success and error percentages and affect circuit breaker status.


# Request Context
Property                                              Default        Description
--------                                              -------        -----------
requestCache.enabled                                  true           Indicates whether HystrixCommand.getCacheKey() should be used with HystrixRequestCache to provide de-duplication functionality via request-scoped caching.
requestLog.enabled                                    true           Indicates whether HystrixCommand execution and events should be logged to HystrixRequestLog


#-# @HystrixCommand.threadPoolProperties

Property                                              Default        Description
--------                                              -------        -----------
coreSize                                              10             The maximum number of HystrixCommands that can execute concurrently.
maxQueueSize                                          -1             The maximum queue size of the BlockingQueue implementation. If you set this to -1 then SynchronousQueue will be used, otherwise a positive value will be used with LinkedBlockingQueue.
queueSizeRejectionThreshold                           5              The queue size rejection threshold — an artificial maximum queue size at which rejections will occur even if maxQueueSize has not been reached.
keepAliveTimeMinutes                                  1              The keep-alive time.
metrics.rollingStats.timeInMilliseconds               10000          The duration of the statistical rolling window. This is how long metrics are kept for the thread pool.
metrics.rollingStats.numBuckets                       10             The number of buckets the rolling statistical window is divided into.



#-#
#-# Examples
#-#

#-# Commands

# Synchronous Execution
@HystrixCommand(groupKey="UserGroup", commandKey = "GetUserByIdCommand")
public User getUserById(String id) {
  return userResource.getUserById(id);
}

# Asynchronous Execution
@HystrixCommand
public Future<User> getUserByIdAsync(final String id) {
  return new AsyncResult<User>() {
    @Override
    public User invoke() {
      return userResource.getUserById(id);
    }
  };
}

# Reactive Execution
@HystrixCommand
public Observable<User> getUserById(final String id) {
  return new ObservableResult<User>() {
    @Override
    public User invoke() {
      return userResource.getUserById(id);
    }
  };
}

# Fallback
@HystrixCommand(fallbackMethod = "defaultUser")
public User getUserById(String id) {
  return userResource.getUserById(id);
}
@HystrixCommand(fallbackMethod = "defaultUserSecond")
private User defaultUser(String id) {
  return new User();
}
@HystrixCommand
private User defaultUserSecond(String id) {
  return new User("def", "def");
}

# Error Propagation
@HystrixCommand(ignoreExceptions = {BadRequestException.class})
public User getUserById(String id) {
  return userResource.getUserById(id);
}


#-# Configuration

# Command Properties
@HystrixCommand(
  commandProperties = {
    @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "500")
  },
  threadPoolProperties = {
    @HystrixProperty(name = "coreSize", value = "30"),
    @HystrixProperty(name = "maxQueueSize", value = "101"),
    @HystrixProperty(name = "keepAliveTimeMinutes", value = "2"),
    @HystrixProperty(name = "queueSizeRejectionThreshold", value = "15"),
    @HystrixProperty(name = "metrics.rollingStats.numBuckets", value = "12"),
    @HystrixProperty(name = "metrics.rollingStats.timeInMilliseconds", value = "1440")
  }
)
public User getUserById(String id) {
  return userResource.getUserById(id);
}

# Hystrix collapser
@HystrixCollapser(batchMethod = "getUserByIds")
public Future<User> getUserById(String id) {
  return null;
}
@HystrixCommand
public List<User> getUserByIds(List<String> ids) {
  List<User> users = new ArrayList<User>();
  for (String id : ids) {
    users.add(new User(id, "name: " + id));
  }
  return users;
}
Future<User> f1 = userService.getUserById("1");
Future<User> f2 = userService.getUserById("2");
Future<User> f3 = userService.getUserById("3");
Future<User> f4 = userService.getUserById("4");
Future<User> f5 = userService.getUserById("5");


#-# Caching

# Cache key generator
@CacheResult(cacheKeyMethod = "getUserByNameCacheKey")
@HystrixCommand
public User getUserByName(String name) {
  return storage.getByName(name);
}
private Long getUserByNameCacheKey(String name) {
  return name;
}

# Get-Set-Get pattern
@CacheResult
@HystrixCommand
public User getUserById(@CacheKey String id) { // GET
  return storage.get(id);
}
@CacheRemove(commandKey = "getUserById")
@HystrixCommand
public void update(@CacheKey("id") User user) { // SET
  storage.put(user.getId(), user);
}



#-#
#-# References
#-#

[01] https://github.com/Netflix/Hystrix/wiki
[02] https://github.com/Netflix/Hystrix/tree/master/hystrix-contrib/hystrix-javanica



