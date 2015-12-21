Inversion of Control Containers and the Dependency Injection pattern
--------------------------------------------------------------------

_
In the Java community there's been a rush of lightweight containers that help
to assemble components from different projects into a cohesive application.
Underlying these containers is a common pattern to how they perform the wiring,
a concept they refer under the very generic name of "Inversion of Control". In
this article I dig into how this pattern works, under the more specific name of
"Dependency Injection", and contrast it with the Service Locater alternative.
The choice between them is less important than the principle of separating
configuration from use.
_

----------------------------------------

Contents
--------
- Components and Services
- A Naive Example
- Inversion of Control
- Forms of Dependency Injection
  - Constructor Injection with PicoContainer
  - Setter Injection with Spring
  - Interface Injection
- Using a Service Locater
  - Using a Segregated Interface for the Locater
  - A Dynamic Service Locater
  - Using both a Locater and injection with Avalon
- Deciding which option to use.
  - Service Locater vs. Dependency Injection
  - Constructor vs. Setter Injection
  - Code or configuration from Use
  - Separating Configuration from Use
- Some further issues
- Concluding Thoughts


----------------------------------------

One of the entertaining things about the enterprise Java world is the huge
amount of activity in building alternatives to the mainstream J2EE
technologies, much of it happening in open source. A lot of this is a reaction
to the heavyweight complexity in the mainstream J2EE word, but much of it is
also exploring alternatives an coming up with creative ideas. A common issue to
deal with is how to wire together different elements: how do you fit together
this web controller architecture with that database interface backing when they
were built by different teams with little knowledge about each other. A
number of frameworks have taken a stab at this problem, and several are
branching out to provide a general capability to assemble components from
different layers. These are often referred to as lightweight containers,
examples include PicoContainer, and Spring.

Underlying these containers are a number of interesting design principles,
things that go beyond both these specific containers and indeed the Java
platform. Here I want to start exploring some of these principles. The
examples I use are in Java, but like most of my writing the principles are
equally applicable to other OO environments, particularly .NET.


Components and Services
-------------------------

The topic of wiring elements together drags me almost immediately into the
knotty terminology problems that surround the terms service and component. You
find long and contradictory articles on the definition of these things with
ease. For my purposes here are my current uses of these overloaded terms.

I use component to mean a glob software that's intended to be used, without
change, by an application that is out of the control of the writers of the
components, although they may alter the component's behavior by extending it in
ways allowed by the component writers.

A service is similar to a component in that it's used by foreign application.
The main difference is that I expect a component to be used locally (think jar
file, assembly, dll, or a source import). A service will be used remotely
through some remote interface, either synchronous or asynchronous (e.g. web
service, messaging system, RCP, or socket).

I mostly use service in this article, but much of the same logic can be applied
to local component too. Indeed often you need some kind of local component
framework to easily access a remote service. But writing "component or service"
is tiring to read and write, and services are much more fashionable at the
moment.


A naive example
---------------

To help make all of this more concrete I'll use a running example to talk about
all of this. Like all of my examples it's one of those super-simple examples;
small enough to be unreal, but hopefully enough for you to visualize what's
going on without falling into the bog of a real example.

In this example I'm writing a component that provides a list of movies directed
by a particular director. This stunningly useful function is implemented by a
single method.

```java
class MovieLister{
  public Movie[] moviesDirectedBy(String arg)
  {
    List allMovies = finder.findAll();
    for (Iterator it = allMovies.iterator(); it.hasNext();){
      Movie movie= (Movie) it.next();
      if(!movie.getDirector().equals(arg)) it.remove();
    }
    return (Movie[]) allMovies.toArray(new Movie[allMovies.size()]);
  }
}
```

The implementation of this function is naive in the extreme, it asks a finder
object (which we'll get to in  a moment) to return every film it knows about.
Then it just hunts through this list to return those directed by a particular
director. This particular piece of naively I'm not going to fix, since it's
just the scaffolding for the real point of this article.

The real point of this article is this finder object, or particular how we
connect the lister object with a particular finder object. The reason why this
is interesting is that I want my wonderful `moviesDirectedBy` method to be
completely independent of how all the movies are being stored. So all the
method does is refer to a finder, and all that finder does is know how to
respond to the `findAll` method. I can bring this out be defining an interface
for the finder.

```java
public interface MovieFinder {
  List findAll();
}
```

Now all of this is very well decoupled, but at some point I have to come up
with a concrete class to actually come up with the movies. In this case I put
the code for this in the constructor of my lister class.

```java
class MovieLister {
  private MovieFinder(){
    finder = new ColondelimitedMovieFinder("movies1.txt");
  }
}
```

The name of the implementation class comes from the fact that I'm getting my
list from a colon delimited text file. I'll spare you the details, after all
the point is just that there's some implementation.

Now if I'm using this class for just myself, this is all fine and dandy. But
what happens when my friends are overwhelmed by a desire for this wonderful
functionality and would like a copy of my program? If they also store their
movie listings in a colon delimited then everything is wonderful. If they have
a different name for they movie file, then it's easy to put the name of the
file in a properties file. But what if they have a completely different form of
storing their movie listing: a SQL database, an XML file, a web service, or
just another format of text file? In this case we need a different class to grab
that data.
