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
just another format of text file? In this case we need a different class to
grab that data. Now because I've defined a `MovieFinder` interface, this won't
alter my `moviesDirectedeBy` method. But I still need to get an instance of the
right finder implementation into place.

Figure 1 shows the dependencies for this situation. The `MovieLister` class is
dependent on both the MovieFinder interface and upon the implementation. We
would prefer it if it were only dependent on the interface, but then how do we
make an instance to work with?

In my book P of EAA, we described this situation as a Plugin. The
implementation class for the finder isn't lined into the program at compile
time, since I don't know what my friends are going to use. Instead we want my
lister to work with any implementation, and for that implementation to be
plugged in at some later point, out of my hands. The problem is how can I make
that link so that my lister class is ignorant of the implementation class, but
can still talk to an instance to do its work.

Expanding this into a real system, we might have dozens of such services and
components. In each acse we can abstarct our use of these components by talking
to them through an interface (and using an adapter if the component isn't
designed with an interface in mind). But if we wish to deploy this system in
different ways, we need to use plugins to handle the interaction with these
services so we can use different implementations in different deployments.

So the core problem is how do we assemble these plugins into an application?
This is one of the main problems that this new breed of lightweight containers
face, and universally they all do it using __Inversion of Control__.


Inversion of Control
--------------------
When these containers talk about how they are so useful because they implement
"Inversion of Control" I end up very puzzled. __Inversion of Control__ is a
common characteristic of frameworks, so saying that these lightweight
containers are special because they use Inversion of control is like saying my
car special because it has wheels.

The question is: "What aspect of control are they inverting?" When I first ran
into inversiono of control, it was in the main control of a user interface.
Early user interfaces were controlled by the application program. You would
have a sequence of commands like "Enter name", "enter address"; your program
would drive the prompts and pick up a respose to each one. With graphical (or
even screen based) UIs framework would contain this main loop and your program
instead event handlers for the various fields on the screen. The main control
of the program was inverted, moved away from you to the framework.

For this new breed of containers the inversion is about how they lookup a
plugin implementation by directly instantiating it. This stops the finder from
being a plugin. The approach that these containers use is to ensure that any
use of a plugin follows some convention that allows a separate assembler module
to inject the implementation into the lister.

As a result I think we need a more specific name for this pattern. Inversion of
Control is too generic a term, and thus people find it confusing. As a result
with a lot of discussion with various IoC advocates we settled on the name
_Dependency Injection_.

I'm going to start by talking about the various forms of Dependency Injection,
but I'll point out now that that's not the only way of removing the dependency
from the application class to the plugin implementation. The other pattern you
can use to do this is Service Locator, and I'll discuss that after I'm done
with explaining Dependency Injection.


Forms of Dependency Injection
-----------------------------

The basic idea of the Dependency Injection is to have a separate object, an
assembler, that populates a field in the lister class with an appropriate
implementation for the finder interface, resulting in a dependency diagram
along the lines of Figure 2.

There are three main styles of dependency injection. The names I'm using for
them are Constructor Injection, Setter Injection, and Interface Injection. If
you read about this stuff in the current discussions about Inversion of Control
you'll hear these referred to as type 1 IoC (Interface Injection), type 2 IoC
(setter injectiono), type 3 IoC (Constructor Injection). I find numeric names
rather hard to remember, which is why I've used the names I have here.


Constructor Injection with PicoContainer
----------------------------------------

I'll start with showing how this injection is done using a lightweight
container called PicoContainer. I'm starting here primarily because several of
my colleagues at ThoughtWorks are very active in the development of
PicoContainer (yes, it's a sort of corporate nepotism.)

PicoContainer uses a constructor to decide how to injet a finder implementation
into the lister class. For this to work, the movie lister class needs to declare
a constructor that includes everything it needs injected.

```
class MovieLister...
    public MovieLister(MovieFinder finder)
    {
        this.finder = finder;
    }
```

The finder itself will also be managed by the PicoContainer, and as such will
have the filename of the text file injected into it by the container.

```
class ColonMovieFinder
    public ColonMovieFinder (String filename)
    {
        this.filename = filename;
    }
```

The PicoContainer then needs to be told which implementation class to associate
with each interface, and which string to inject into the finder.

```
private MutablePicoContainer configureContainer(){
    MutablePicoContainer pico = new DefaultPicoContainer();
    Parameter[] finderParams = {new ConstantParameter("movies1.txt")};
    pico.registerComponentImplementation(MovieFinder.class,
        ColonMovieFinder.class, finderParams);
    pico.registerComponentImplementation(MovieLister.class);
    return picol;
}
```

This configuration code is typically set up in a different class. For our
example, each friend who uses my lister might write the appropriate
configuration code in some setup class of their own. Of course it's common to
hold this kind of configuration information in separate config files. you can
write a class to read a config file and set up the container appropriately.
Although PicoContainer doesn't contain this functionality itself, there is a
closely related project called NanoContainer that provides the appropriate
wrappers to allow you to have XML configuration files. Such a nano container
will parse the XML and then configure an underlying PicoContainer. The
philosophy of the project is to separate the config file format from the
underlying mechanism.

To use the container you write code something like this.

```
public void testWithPico(){
    MutablePicoContainer pico = configureContainer();
    MovieLister lister = (MovieLister)
        pico.getComponentInstance(MovieLister.class);
    Movie[] movies = lister.moviesDirectedBy("Sergio Leone");
    asssertEquals("Once upon a time in the West", movies[0].getTitle());
}
```

Although in this example I've used constructor injection PicoContainer also
supports setter injection, although its developers do prefer constructor
injection.

