1\. Don't Write Logs by Yourself (AKA Don't Reinvent the Wheel)
---------------------------------------------------------------

Never, ever use printf or write your log entries to files by yourself, or handle log rotation by yourself. Please do your ops guys a favor and use a standard library or system API call for this. This way, you're sure the running application will play nicely with the other system components and will log to the right place or network services without special system configuration.

So, if you just use the system API, then this means logging with `syslog(3)`. Learn how to use it.

If you instead prefer to use a logging library, there are plenty of those especially in the Java world, like [Log4j](https://logging.apache.org/log4j/2.x/), [JCL](https://commons.apache.org/logging/guide.html), [slf4j](http://www.slf4j.org/) and [logback](http://logback.qos.ch/). My favorite is the combination of slf4j and logback because it is very powerful and relatively easy to configure (and allows JMX configuration or reloading of the configuration file).

The best thing about slf4j is that you can change the logging backend when you see fit. It is especially important if you're coding a library, because it allows anyone to use your library with their own logging backend without any modification to your library.

There are also several other logging libraries for different languages, like for ruby: Log4r, [stdlib logger](http://www.ruby-doc.org/stdlib-1.9.3/libdoc/logger/rdoc/Logger/Application.html), or the almost perfect [Jordan Sissel's Ruby-cabin](https://github.com/jordansissel/ruby-cabin)

And if your argument for not using a logging library is CPU consumption, then you have my permission to skip this blog post. Sure you should not put log statements in tight inner loops, but otherwise, you'll never see the difference.

2\. Log at the Proper Level
---------------------------

If you followed the first best practice, then you can use a different log level per log statement in your application. One of the most difficult task is to find at what level this log entry should be logged.

Here I've given some advice:

-   *TRACE level*: this is a [code smell](https://en.wikipedia.org/wiki/Code_smell) if used in production. This should be used during development to track bugs, but never committed to your VCS.
-   *DEBUG level*: log at this level about anything that happens in the program. This is mostly used during debugging, and I'd advocate trimming down the number of debug statement before entering the production stage, so that only the most meaningful entries are left, and can be activated during troubleshooting.
-   *INFO level*: log at this level all actions that are user-driven, or system specific (ie regularly scheduled operations...)
-   *NOTICE level*: this will certainly be the level at which the program will run when in production. Log at this level all the notable events that are not considered an error.
-   *WARN level*: log at this level all events that could potentially become an error. For instance if one database call took more than a predefined time, or if an in-memory cache is near capacity. This will allow proper automated alerting, and during troubleshooting will allow to better understand how the system was behaving before the failure.
-   *ERROR level*: log every error condition at this level. That can be API calls that return errors or internal error conditions.
-   *FATAL level*: too bad, it's doomsday. Use this very scarcely, this shouldn't happen a lot in a real program. Usually logging at this level signifies the end of the program. For instance, if a network daemon can't bind a network socket, log at this level and exit is the only sensible thing to do.

Note that the default running level in your program or service might widely vary. For instance, I run my server code at level *INFO* usually, but my desktop programs run at level *DEBUG*. Because it's very hard to troubleshoot an issue on a computer you don't have access too, and it's far easier when doing support or customer service to ask the user to send you the log than teaching her to change the log level and then send you the log.

Of course YMMV.

3\. Employ the Proper Log Category
----------------------------------

Most logging libraries I cited in the first tip allow you to specify a logging category. This category allows us to classify the log message, and will ultimately, based on the logging framework configuration, be logged in a distinct way or not logged at all.

Most of the time Java developers use the fully qualified class name where the log statement appears as the category. This is a scheme that works relatively fine if your program respects the [simple responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle).

Log categories in [Java logging](https://www.scalyr.com/blog/get-started-quickly-with-java-logging/) libraries are hierarchical, so for instance logging with category `com.daysofwonder.ranking.ELORankingComputation` would match the top level category `com.daysofwonder.ranking`. This would allow the ops engineer to set up a logging configuration that works for all the ranking subsystem by just specifying configuration for this category. But it could at the same time, produce logging configuration for child categories if needed.

We can extend the paradigm a little bit further to help to troubleshoot the specific situation.

Imagine that you are dealing with a server software that responds to user based request (like a [REST API](https://restfulapi.net/) for instance). If your server is logging with this category `my.service.api.<apitoken>` (where apitoken is specific to a given user), then you could either log all the API logs by allowing `my.service.api` or a single misbehaving API user by logging with a more detailed level and the category `my.service.api.<bad-user-api-token>`. Of course, this requires a system where you can change logging configuration on the fly.

4\. Write Meaningful Log Messages
---------------------------------

This might probably be the most important best practice. There's nothing worse than cryptic log entries assuming you have a deep understanding of the program internals.

When writing your log entries messages, always anticipate that there are emergency situations where the only thing you have is the log file, from which you have to understand what happened. Doing it right might be the subtle difference between getting fired and promoted.

When a developer writes a log message, it is in the context of the code in which the log directive is to be inserted. Under these conditions, we tend to write messages that infer on the current context. Unfortunately, when reading the log itself this context is absent, and those messages might not be understandable.

One way to overcome this situation (and that's particularly important when writing at the warn or error level), is to add remediation information to the log message. Or if that's not possible, what was the purpose of the operation and its outcome.

Also, don't add a log message that depends on a previous message's content. The reason is that those previous messages might not appear if they are logged in a different category or level. Or worse, they can appear in a different place (or way before) in a multi-threaded or asynchronous context.

5\. Write Log Messages in English
---------------------------------

This might seem a strange piece of advice, especially coming from a French guy. First, I still think English is much more concise than French and better suits technical language. Why would you want to log in French if the message contains more than 50% English words?

This being put aside, here are the essential reasons behind this practice:

-   English means your messages will be in logged with ASCII characters. This is particularly important because you can't really know what will happen to the log message, nor what software layer or media it will cross before being archived somewhere. If your message uses a special charset or even UTF-8, it might not render correctly at the end, but worst it could be corrupted in transit and become unreadable. Still remains the question of logging user-input which might be in diverse charset and/or encoding.
-   If your program is to be used by most and you don't have the resources for a full localization, then English is probably your best alternative. Now, if you have to localize one thing, localize the interface that is closer to the end-user (it's usually not the log entries).
-   if you localize your log entries (like for instance all the warning and error level), make sure you prefix those by a specific meaningful error-code. This way people can do a language-independent Internet search and find information. Such a great scheme has been used a while ago in the VMS operating system, and I must admit it is very effective. If you were to design such a scheme, you could adopt this one: APP-S-CODE or APP-S-SUB-CODE, with respectively:
    -   APP: your application name on 3 letters
    -   S: severity on 1 letter (ie D: debug, I: info...)
    -   SUB: the sub part of the application this code pertains to
    -   CODE: a numeric code specific to the error in question

6\. Add Context to Your Log Messages
------------------------------------

So, there's nothing worse than this kind of log message:

|

1

 |

```
 Transaction failed
```

 |

or

|

1

 |

```
User operation succeeds
```

 |

or in case of API exceptions:

|

1

 |

```
java.lang.IndexOutOfBoundsException
```

 |

Without proper context, those messages are only noise, they don't add value and consume space that could have been useful during troubleshooting.

Messages are much more valuable with added context, like:

|

1

 |

```
Transaction 2346432 failed: cc number checksum incorrect
```

 |

or

|

1

 |

```
User 54543 successfully registered e-mail user@domain.com
```

 |

or

|

1

 |

```
IndexOutOfBoundsException: index 12 is greater than collection size 10
```

 |

Since we're talking about exceptions in this last context example, if you happen to propagate up exceptions, make sure to enhance them with context appropriate to the current level, to ease troubleshooting, as in this java example:

Context propagation

|

1
2
3
4
5
6
7

 |

```
  public void storeUserRank(int userId, int rank, String game) {
    try {
      ... deal database ...
    } catch(DatabaseException de) {
      throw new RankingException("Can't store ranking for user "+userId+" in game "+ game + " because " + de.getMessage() );
    }
  }

```

 |

So the upper-layer client of the rank API will be able to log the error with enough context information. It's even better if the context becomes parameters of the exception itself instead of the message, this way the upper layer can use remediation if needed.

An easy way to keep a context is to use the [*MDC*](http://www.slf4j.org/manual.html#mdc) some of the Java logging library implements. The *MDC* is a per-thread associative array. The logger configuration can be modified to always print the *MDC* content for every log line. If your program uses a per-thread paradigm, this can help solve the issue of keeping the context. For instance, this Java example is using the *MDC *to log per user information for a given request:

MDC example

|

1
2
3
4
5
6
7
8
9
10
11
12

 |

```
  class UserRequest {
    ...
    public void execute(int userid) {
      MDC.put("user", userid);

      // ... all logged message now will display the user=<userid> for this thread context ...
      log.info("Successful execution of request");

      // user request processing is now finished, no need to log our current user anymore
      MDC.remote("user");
    }
  }

```

 |

Note that the *MDC* system doesn't play nice with asynchronous logging scheme, like [Akka](http://akka.io/)'s logging system. Because the MDC is kept in a per-thread storage area and in asynchronous systems you don't have the guarantee that the thread doing the log write is the one that has the MDC. In such a situation, you need to log the context manually with every log statement.

7\. Log in Machine Parseable Format
-----------------------------------

Log entries are really good for humans but very poor for machines. Sometimes it is not enough to manually read log files, you need to perform some automated processing (for instance for alerting or auditing). You want to centrally store your logs and be able to perform search requests.

So what happens when you embed the log context in the string like in this hypothetical logging statement?:

Difficult to parse

|

1

 |

```
log.info("User {} plays {} in game {}", userId, card, gameId);

```

 |

This will produce this kind of text:

Difficult to parse

|

1

 |

```
2013-01-12 17:49:37,656 [T1] INFO  c.d.g.UserRequest  User 1334563 plays 4 of spades in game 23425656

```

 |

Now, if you want to parse this, you'd need the following (untested) regex:

Difficult to parse

|

1

 |

```
  /User (\d+) plays (.+?) in game (\d+)$/

```

 |

Well, this is not easy and very error-prone, just to get access to string parameters your code already knows natively.

So what about this idea, I believe [Jordan Sissel](http://www.semicomplete.com/) first introduced in his ruby-cabin library: Let's add the context in a machine parseable format in your log entry. Our aforementioned example could be using JSON like this:

Easy to parse

|

1

 |

```
2013-01-12 17:49:37,656 [T1] INFO  c.d.g.UserRequest  User plays {'user':1334563, 'card':'4 of spade', 'game':23425656}

```

 |

Now your log parsers can be much easier to write, indexing becomes straightforward and you can enable all logstash[ ](http://logstash.net/)power.

8\. But Make the Logs Human-Readable as Well
--------------------------------------------

Log files should be machine-parsable, no doubt about that. But they should also be human-readable as well. Why is that?

Simply put, people will read the log entries. And those will probably be (somewhat) stressed-out developers, trying to troubleshoot a faulty application. Don't make their lives harder than they have to be by writing log entries that are hard to read.

OK, but how do we achieve human-readable logs? Well, the Scalyr blog has an [entire post covering just that](https://www.scalyr.com/blog/log-formatting-best-practices-readable/), but here are the main tidbits:

-   Use a standard date and time format (ISO8601)
-   Add timestamps either in UTC or local time plus offset
-   Employ [log levels](https://www.scalyr.com/blog/logging-levels/) correctly
-   Split logs of different levels to different targets to control their granularity
-   Include the stack trace when logging exceptions
-   Include the thread's name when logging from a multi-threaded application

9\. Don't Log Too Much or Too Little
------------------------------------

That might sound stupid, but there is a right balance for the amount of log.

Too much log and it will really become hard to get any value from it. When manually browsing such logs, there is too much clutter which when trying to troubleshoot a production issue at 3AM is not a good thing.

Too little log and you risk to not be able to troubleshoot problems: troubleshooting is like solving a difficult puzzle, you need to get enough material for this.

Unfortunately, there is no magic rule when coding to know what to log. It is thus very important to strictly respect the first two best practices so that when the application will be live it will be easier to increase or decrease the log verbosity.

One way to overcome this issue is during development to log as much as possible (do not confuse this with logging added to debug the program). Then when the application enters production, perform an analysis of the produced logs and reduce or increase the logging statement accordingly to the problems found. Especially during troubleshooting, note the part of the application you wished you could have more context or logging, and make sure to add those log statements to the next version (if possible at the same time you fix the issue to keep the problem fresh in memory). Of course, that requires an amount of communication between ops and devs.

This can be a complex task, but I would recommend refactoring logging statements as much as you refactor the code. The idea would be to have a tight feedback loop between the production logs and the modification of such logging statements. It's even more efficient if your organization has a continuous delivery process in place, as the refactoring can be constant.

Logging statements are some kind of code metadata, at the same level of code comments. It's really important to keep the logging statements in sync with the code. There's nothing worse when troubleshooting issues to get irrelevant messages that have no relation to the code processed.

10\. Think of Your Audience
---------------------------

Why add logging to an application?

The only answer is that someone will have to read it one day or later (or what is the point?). More importantly, it's interesting to think about who will read those lines. Depending on the person you think will read the log messages you're about to write, the log message content, context, category, and level can be quite different.

Those persons can be:

-   an end-user trying to troubleshoot herself a problem (imagine a client or desktop program)
-   a system-administrator or operation engineer troubleshooting a production issue
-   a developer either for debugging during development or solving a production issue

Of course, the developer knows the internals of the program, thus her log messages can be much more complex than if the log message is to be addressed to an end-user. So adapt your language to the intended target audience, you can even dedicate separate categories for this.

11\. Don't Log for Troubleshooting Purposes Only
------------------------------------------------

Just as log messages can be written for different audiences, log messages can be used for different reasons. Even though troubleshooting is certainly the most evident target of log messages, you can also use log messages very efficiently for:

-   *Auditing*: this is sometimes a business requirement. The idea is to capture significant events that matter to the management or legal people. These are statements that describe usually what users of the system are doing (like who signed-in, who edited that, etc...).
-   *Profiling*: as logs are timestamped (sometimes to the millisecond level), it can become a good tool to profile sections of a program, for instance by logging the start and end of an operation, you can either automatically (by parsing the log) or during troubleshooting infer some performance metrics without adding those metrics to the program itself.
-   *Statistics*: if you log each time a certain event happens (like a certain kind of error or event) you can compute interesting statistics about the running program (or the user behaviors). It's also possible to hook this to an alert system that can detect too many errors in a row.

12\. Avoid Vendor Lock-In
-------------------------

This tip was already partially covered by the first one, but I think it's worth mentioning it in a more explicit manner.

So, the advice here is simple: avoid being locked to any specific vendor. Organize your logging strategy in such a way that, should the need arise, it becomes simple to swap a logging library or framework with another one.

How do you do that?

One way is to make sure your application code doesn't mention the third-party tool explicitly by making use of a wrapper. Rather, create a logger interface with the appropriate methods, and a class that implements it. Then, add to this class the code that actually calls the third-party tool. That way, you protect your application from the third-party tool. If you ever need to replace it with another one, just a single place has to change in the whole application.

In order to make this approach easier, you can adopt a logging façade, such as slf4j, which the post already mentioned. This project offers a standardized abstraction over several logging frameworks, making it very easy to swap one for another.

13\. Don't Log Sensitive Information
------------------------------------

Finally, a [logging security](https://www.scalyr.com/blog/java-exceptions-log/) tip: don't log sensitive information.  First, the obvious bits. Make sure you never log:

-   Passwords
-   Credit card numbers
-   Social security numbers

Now, the not so obvious things you shouldn't log.

-   Session identifiers Information the user has opted out of
-   Authorization tokens
-   PII (Personal Identifiable Information, such as personal names)

Also, you have to make sure you're not inadvertently breaking the law. There are laws and regulations that prohibit you from recording certain pieces of information. The most famous of such regulation is probably [GDPR](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation) but it isn't the only one. Make sure you know and follow the laws and regulations from your country and region.