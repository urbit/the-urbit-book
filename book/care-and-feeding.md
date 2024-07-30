##  What is Urbit?

Urbit is a new vision for how an Internet can work:  secure, decentralized, and owned by the individuals and communities that build it.  There's a lot of jargon involved, but the basic idea is that every part of the network has an encrypted censorship-proof communications channel to every other part.  You don't need permission to spend or receive money, to publish or share software, or to say anything you like.

Before we start using Urbit, we need to get a couple of concepts straight.  Urbit consists of two separate pieces, and you need both of them.

- **Urbit ID**.  Your Urbit ID is your identity on the network.  An Urbit ID is cryptographically secure:  it's yours, permanently.  Like a website, once you've acquired it and set it up, you don't need to think much about anything except the name.
- **Urbit OS**.  Your Urbit OS is the software that you actually run in order to use Urbit practically.  Like a web browser (and often using a web browser), this is the software that you will use in practice.

In most cases, the context should be clear enough that we don't need to distinguish them once we're operational.


##  Lesson 1:  Getting Up and Running

> ### Objectives
> 
> 1. Set up and operate an Urbit ship.
> 2. Leave a ship running in a persistent session.

So you're a proud new owner of an Urbit ship.  It's time to boot it up for the first time.

> ### What is an "Urbit ship"?
>
> An Urbit ship is the actual identity you will have on Urbit's network.  It is most commonly a "planet", or regular permanent identity, but it may be a "comet", or temporary identity, if you're on the network without having bought or acquired a plent first.
> 
> Developers often prefer to use “fake ships”, ships which do not have a public Urbit ID.  *The Urbit Book* lessons are written such that you won't break your ship by completing them, so it's safe to complete this using your regular ship.

There are two paths here, depending on whether you are using a hosting service (like Tlon or Red Horizon) or running the ship yourself.  Based on which of those you are doing, you should follow the appropriate path below.

> ### How do I know if I'm hosted or not?
>
> You are hosted if one of these is true:
> 1. You acquired the ship from a "claim code" or "lure link".
> 2. You only access the ship through the web browser.
>
> You are self-hosted if one of these is ture:
> 1. You have a "master ticket" for your ship.
> 2. You are going to run the ship on your own hardware (like a laptop, Raspberry Pi, or Native Planet unit).
> 3. You are going to run the ship on a cloud provider (like Digital Ocean, AWS, or Google Cloud).
>
> If you're still not sure, hit up `@UrbitFoundation` on Twitter and we'll be happy to help.

### Hosted Ships

If a ship is running with a hosting provider, that means that your Urbit ship is running as a persistent server on the host's hardware.  You access it exclusively through a web browser, and you may not need to carry out certain maintenance or setup tasks.

#### Accessing Your Ship

Your hosting provider has shared a URL with you.  When you go to that link, you should see the "Landscape" page (perhaps after logging in).  This is a grid of app icons.  On a fresh Urbit, there will not be very many of them, but at a minimum you should see a Tlon app and a Terminal app.  We'll use both of them soon.

#### Navigating the Apps

Like a smartphone, clicking on any of the icons opens a new browser tab.  You can explore a little if you like—you shouldn't be able to break anything as long as you don't uninstall an app at this point.

Jump down to the heading "What is a ship?".

### Self-Hosted Ships

If you are running your ship yourself, then you get to have a bit more fun at the cost of a bit more labor.  If you are hosted, you can read this section for information but you shouldn't follow these steps now.

If you have already started your ship before, you can skip ahead to the heading "Accessing Your Ship".

#### Acquiring the Keyfile

To certify to the network that your Urbit ID is in fact valid, you need to acquire the cryptographic keyfile from [Bridge](https://bridge.urbit.org).  This is like a password that proves that you actually have permission to identify yourself as ~sampel-palnet or whomever.

1. At Bridge, you need to log in, perhaps using MetaMask or your master ticket.  You may need to sign a "Bridge Authentication Token".

2. You'll see a list of available Urbit IDs.  Select the one you wish to use.

3. You may get a message `No Network Keys Found`.  This means that the ship is "unspawned", i.e. that it has never been used by anyone in any way.  Go ahead and `Set Network Keys`.

4. Click into `Urbit OS`.  There is an option to download the keyfile.  That's what you want, so go ahead and get it.

5. Now that you have the keyfile, it's time to boot your Urbit ship.

#### Initial Boot

The initial boot process involves Urbit using your private keyfile to verify with Azimuth that you are who you claim you are, followed by downloading and implementing the “boot pill”, or set of instructions that yield a fully functional Urbit ship starting from nothing but the rules of Nock.

You'll see some interesting bits in there, like:

- `retrieving galaxy table` so you know who the major network nodes (galaxies) are
- `retrieving keys for sponsor` so you can communicate with your on-network sponsor
- `installed ### jets` so you have jet-accelerated Nock (faster computations)

This leads to `replaying events` which is the basic process for actually making a ship:  setting up the operating system, the event handler, the communications protocols, etc.

Finally, the vanes and user applications boot and you are left at the `dojo>` prompt.

Type `|hi ~zod` and you should see a response pretty quickly.  That's a network ping to the most central node in a broadly decentralized system—it's the current source of software updates over the network.

> ## Cleanup
>
> Once your Urbit ship has successfully booted, the keyfile is no longer useful.  Go ahead and delete it.  You can use a file browser or the (Unix) command line to do this, e.g. `rm sampel-palnet-1.key`.

#### Leaving It Running

Your Urbit ship is a server.  That is, it runs services that various other parts of your computer can utilize.  Right now, the main ways to interact with an Urbit ship are through your browser, through the Tlon mobile app, and through the command line.  The Dojo is the primary command-line interface (CLI) for Urbit.

First, type `help` to get a clue about what to do.  Follow its instruction and input `+start` for details.

Run some of the suggested commands, then shut down your ship with `|exit`.

Now the Urbit ship isn't running any more:  you can't access it from other ships or from the browser.  Most of the time, you'd clearly like it to just stay running.  The simplest way to to do this is to run it in a “detachable session”, or a terminal session you can come back to whenever you need to manage the ship directly.

1. The most common of these is `screen`.  To run an Urbit ship in `screen`, type `screen -S Urbit` to start a new session.
2. This time, when you start your Urbit ship, you aren't booting it for the first time.  To that end, you do not need to boot it again (and should not try to).  Simply type `./sampel-palnet/.run` to run the ship with its attached executable.
3. The Dojo prompt is visible once the restart process completes.  Instead of typing `|exit`, press `Ctrl`+`a` then `Ctrl`+`d` to detach from the `screen` session.  You'll be back out at the regular Unix prompt.
4. You can close the terminal window and walk away, and as long as the machine you're running on stays up, your ship should keep running.
5. You can reattach to the ship with `screen -X Urbit`, which will reconnect you to the Dojo terminal session.

### What Is A Ship?

To the computer, your Urbit ship is actually a folder containing the state of the program.  If you open the ship in a file browser, you can access the hidden folder `/.urb` which has a number of different folders inside of it.  In general, we don't ever need to touch these, but this is where the actual contents of your ship lives in the host OS.

Since you're just a bit curious, here's what the major pieces are:

- `/bhk` is a backup folder containing event log history.  (This may not always be present.)
- `/chk` is the main event log history.
- `/get` and `/put` are used to move data to and from the ship in certain circumstances.
- `/log` contains the main event log state, i.e. what your ship knows and does right now.

You typically won't touch these at all, but now you know that they're there.

**This lesson is complete.**


##  Lesson 2:  The Command Line Interface

> ### Objectives
>
> 1. Carry out basic computations at the command line.
> 2. Synchronize the ship's filesystem with the host OS's filesystem.
> 3. Export data as a file from a ship.

If you are hosted, you should access your terminal from the Landscape page at the Terminal app.  If you are self-hosted, you can use the terminal directly; you may need to type `screen -X Urbit` at the Bash prompt `$` to access it.

The Dojo prompt `dojo>` lets you type Hoon code or run specific short programs, much like the [Bash prompt `$`](https://en.wikipedia.org/wiki/Bash_%28Unix_shell%29) or the old DOS prompt [`C:\>`](https://en.wikipedia.org/wiki/COMMAND.COM).  Command lines require you to write commands directly or store more complicated commands as files to run on demand.

In the previous lesson, you ran the command `+start`.  This begins with a `+` “lus”, which indicates that it is a _generator_ or standalone computation, like a batch file or shell script.  Some common generators:

- `+trouble` displays debugging information.
- `+vats` displays the current installation.
- `+agents %base` displays some of the currently running apps on your ship.
- `+help` displays a generic help summary of what's on your system, or searches for matching generator files.
- `+cat` shows you the contents of a file.

Let's unpack `+cat` first of all, since it encounters a few conventions we will use.  If you want to display (“conCATenate”) the contents of a file, you need to supply the location of the file, which we'll call its “path”.  A path in Urbit uses `/` “fas” forward slashes like macOS and Linux, and it does not use a `.` “dot” to separate the file extension (that's simply the last part of the path).  We often refer to a file's location with respect to our current location, which by default is on the `%base` desk of the current ship at the present moment.  To do that, we start our path with `%` “cen” as a shortcut for “me, here, now”.

```hoon
> +cat %/gen/start/hoon
/~zod/base/~2024.7.29..19.59.55..9c0d/gen/start/hoon
::  Initial help message
::
::::  /hoon/start/gen
  ::
:-  %say
|=  *
:-  %tang
:~
:+  %rose
["" "" ""]
%+  turn
  :~  "Welcome to Urbit.  This command-line interface is the Dojo.  You can use it to"
…
```

If you mistype part of the path, then `+cat` simply reports no content at that location.

```hoon
> +cat %/gen/start/hoo
~ /~zod/base/~2024.7.29..20.02.03..a879/gen/start/hoo
```

> ### Why Can't I Type `Urbit`?
>
> The Dojo prompt has an unusual property:  it will not let you type what it thinks to be invalid commands or code.  That means that sometimes you try to type something and nothing appears at the cursor.  Or sometimes you copy and paste something and it gets garbled.  In both cases, the Dojo parser disagrees that what you're trying to enter is an acceptable command syntax.
>
> Not every part of an invalid command will be blocked:  you can type the path of a file that doesn't exist, for instance.  It's parsing based on grammar not contents.
>
> To really dig into this, we would have to look at Urbit's programming language, Hoon.  But for *The Urbit Book*, we promised we wouldn't, so we won't!

Besides simple `+` “lus” generators, we have a couple of other kinds of commands in the Dojo:

- `|` “bar” generators may make changes to your ship.  We call these “Hood” generators because `%hood` is the system app that administers them.  For instance, if you were to spawn a new moon, you would use `|moon`.  If you were to install a new app, you would use `|install`, and so forth.
- `-` “hep” threads are transient communicating computations.  They normally do something involved like check an Internet resource or communicate with another ship.

You run these the same way:  they may have some arguments, or even some optional arguments.  Compare the output of the following three commands:

```hoon
> +vats %base

> +vats %base, =verb &

> +vats, =verb &
```

The optional argument `verb` lets you specify a more verbose (detailed) output.

> ### True and False
>
> We'll see a lot of ways to write equivalent values in Urbit.  While there are subtleties to this, in general you can use them interchangeably, much as how in regular text you can write “three”, “3”, and “iii” and mean sort of the same thing.
> 
> In what you just saw, `&` is `.y` or `%.y`, the value for `TRUE` in Urbit.  This is opposed by `|`, `.n`, `%.n` for `FALSE`.
>
> Try the command with `=verb |`.

With that basis, let's look at some details of your ship's identity and operations.

- Find out who your sponsor is with `+sponsor`.
- Check connectivity to another ship with `|hi ~sampel-palnet`.

Most of these today are really built for development or troubleshooting, so we'll skip the rest for now.

### Modifying File Data

what is a desk TODO

One of the first things that you'll want to do with any desk
`|mount`

### Saving Results to File

Sometimes the result of a calculation is too big to fit on your terminal screen, or you just want to have the data in a file so you can use the values elsewhere.  In that case, you can redirect the output of a computation to a file using `*` in the Dojo.

For instance, let's use a generator to calculate the name of every planet under a given star.  We need to download and install the generator first.

The contents we want are located in a GitHub repo at [`the-urbit-book/planet-names`](https://github.com/the-urbit-book/planet-names).  Let's use the `-new-app` thread to retrieve and install the code.

```hoon
> -new-app planet-names /the-urbit-book/planet-names
```

Once that completes successfully, you can run the generator on that desk:

```hoon
> +planet-names!planet-names ~sampel
```

This will take a few seconds to complete because of the output buffering.  It's more useful (and faster) to write the results straight to disk:

```hoon
> *%/tub/sampel/txt +planet-names!planet-names ~sampel
```

Now the results are located in a file on your host OS, at `sampel-palnet/base/tub/sampel.txt`.

> ### What's that `&txt`?
> 
> The final part of any file path in Urbit is a _mark_, basically the file type.  However, the file type is smarter than a regular file type, because it includes rules on how to convert it from one kind of data to another.  In this case, we're converting from whatever the output of the generator is (a `%tang`, or formatted text list) to a list of text, which is basically a text file.  That's what the `&txt` is telling Dojo to do there.

**This lesson is complete.**

##  Lesson 3:  The Web Interface

> ### Objectives
> 
> 1. Log into a web session.
> 2. Access social groups using Tlon.
> 3. Locate and install new apps at the web interface and the CLI.

An Urbit ship is a server, meaning that it runs in the background while you access it through one or more means.  Most casual users will access Urbit through their web browser.  Hosted users use a URL designated by their hosting provider.  If you have set up a custom URL, then you should navigate there.  If you are running things locally, then try `http://localhost:8080` (Linux) or `http://localhost:80` (macOS).

You are first prompted to log in to the ship.  What is your password?  The easiest way to obtain it is to go back to your command line and run `+code`.  For instance, on a fake ship ~zod, you'll see this:

```hoon
> +code
lidlut-tabwed-pillex-ridrup
```

The login code looks like a ship name.  It is random generated and tied to your ship.  You can use `|code` to set a new one, but typically you will only need to do that if you accidentally leak the first one.

The main landing page is at `http://your.url/apps/landscape`.  This app has had a few different designations over its lifetime, notably “Grid” and “Landscape”; we'll use “Landscape” for the time being.  Landscape is like your phone's main page:  it brokers access to all of the apps you have installed, as well as provides the easiest way to obtain new ones.

faster
search for an app

### Tlon

“Tlon”, sometimes called “Groups”, is the main chat app that most folks use on Urbit today.  It's sort of like Signal, Slack, or Discord:  it makes it straightforward to set up groups containing chat channels, link collections, or long-form notebooks.  The first obstacle to using your Urbit ship socially is making contact with the communities you want to be part of.  Here are some good public groups to consider joining:

- `~halbex-palheb/uf-public` Urbit Foundation
- `~nibset-napwyn/tlon` Tlon Local
- `~hiddev-dannut/new-hooniverse` Hooniverse Developer Education
- `~dister-dozzod-lapdeg/battery-payload` `[battery payload]` Advanced Developers

Most groups cater to niche interests:

- `~natnex-ronret/door-link` door.link Music Sharing
- `~tocwex/syndicate-public` Business Services
- `~nattyv/nativeplanet` Native Planet
- `~librex-dozryc/mrb-public` _Mars Review of Books_
- `~sovref-hasfyr/scholia-pugillatoria` Combat Sports

Many people post their favorite groups in their Tlon profile, so click into the details of new friends you meet along your way.

And, of course, you can always click `+ New Group` and be the change you want to see in the world.

> ### Hosting a Group
> 
> It's often more convenient to host a group from a ship other than your primary identity.  Some folks use stars, while others prefer moons.  The main thing to keep in mind is that the hosting ship needs to be always online and available.

Some of the exercises that we will complete in future lessons, like adding chatbots, will be built into or on top of Tlon.

### Install a New App

To install an app, you need to know the publisher, or you can see if something in the suggestions list strikes your fancy.  Click `Get Urbit Apps` at the very top of the page and type `~paldev` in the search box.  You should see a list of several apps produced by developer ~palfun-foslup and hosted on his star ~paldev.  Click on `pals` and install it.  After a few seconds, you should see a new tile added to your Landscape page.  `pals` is a simple contact manager for Urbit, and several other apps use it as a basic friend list.


Landscape searches for apps by provider (rather than by app name).  One of the very best apps to install early on, therefore, is a discovery app:  `%hits`.  `%hits` is a leaderboard for app installs, that is, it shows which apps your `%pals` have installed.



You can accomplish the same thing at the command line using `|install ~sampel-palnet %app`—in this case, `|install ~bitdeg %hits`.

In a future lesson, we will also see how to publish your own software.  We say that software distribution on Urbit is “permissionless”.  That means that no one gatekeeps software publishing.  In practice, that also means that you should be cautious about installing apps from developers you do not know or trust.  The Urbit community does a good job of policing bad behavior—if you are in doubt, ask about an app or developer in one of the big Tlon groups like `~halbex-palheb/uf-public` or `~nibset-napwyn/tlon`.

**This lesson is complete.**

##  Lesson 4:  Keeping Your Ship Shipshape

> ### Objective
> 
> 1. Manage a ship's memory and working environment.

The main thing you have to worry about with a ship is memory.

memory usage on drive and in RAM

roll
chop
pack
meld

loom

> ### What is the Loom?
> 
> Urbit describes the memory arena in which a ship's Nock computations take place as the “loom”.  [The technical details](https://docs.urbit.org/system/runtime/reference/nouns#u3-the-road-model) are pretty interesting and innovative, but for now just think of it as Nock-specific RAM.
>
> By running the ship with [`--loom`](https://docs.urbit.org/manual/running/vere#--loom-size), you can specify how much memory is available for Nock computations.  These are given in terms of powers of 2, e.g. `32` is $2^{32}$, or 4 GB.



**This lesson is complete.**


##  Lesson 5:  What's Going Wrong?

> ### Objective
> 
> 1. Troubleshoot common problems for long-running ships.

Since Urbit is not yet at absolute zero, and in any case we run on real hardware rather than some platonic substrate, you will on occasion encounter difficulties.  Most problems result from external computer issues:

1. Running out of disk space.
2. Insufficient RAM (see the section “Maintaining the Ship”).
3. Solid-state drive failure.

You can also see issues from a misbehaving app, especially when a systemwide kelvin upgrade takes place.  This lesson walks through how to resolve the most common issues—it's fine to skim it or skip it, but remember that it's here someday when you need it.

### Insufficient Disk Space

If a hard drive actually runs out of space, the Urbit ship can no longer process events and write them to disk.  The fix is easy to say:  clear up some disk space by deleting things you don't need.  In practice, because of trash features and the need for a copying buffer, it can be difficult to make this work easily.

The easiest approach is to fix things on a local machine with lots of space:

1. Shut down your ship as gracefully as possible (`|exit` if it works).
2. Copy the ship over the network to a local laptop or desktop drive where you have some breathing room.  (The technique varies, but `scp -r user@remote:~/sampel-palnet .` may suffice.)
3. Carry out basic maintenance locally (`pack`, `meld`, `roll`, `chop`).
4. Confirm that the ship runs with `./sampel-palnet/.run -l` (which blocks networking, just in case).
5. ONLY NOW DELETE THE REMOTE COPY.  This is the step at which you are most likely to make a mistake, so please triple-check.  On the remote computer, `rm -r sampel-palnet`.  Clear up any other space you need to as well.
6. Zip the pier up locally (`tar cvzf sampel-palnet.tar.gz sampel-palnet`) and move it back to the remote computer (`scp -r ./sampel-palnet.tar.gz user@remote:~`).
7. Unzip the ship on the remote (`tar xvzf sampel-palent.tar.gz`).
8. Using `screen` or whichever session manager you like, start the ship normally.
9. After verifying that the ship works, triple-check and run the command `rm sampel-palnet.tar.gz` to remove the compressed version.

### Insufficient RAM

If the Urbit ship is unable to access enough memory to carry out certain tasks (compiling a new OTA update, for example, or `|meld`ing memory), you can improve its overall performance by making more RAM available either temporarily or permanently.  While you are limited by the logical memory of the device on which you are running the ship, you can at least meet a temporary surge in demand using ample [swap space](https://linuxize.com/post/create-a-linux-swap-file/).

The absolute first thing to try is just running the ship with more memory (“loom”):

```
./sampel-palnet/.run --loom 33
```

The next thing to do is fix things on a local machine with lots of RAM:

1. Shut down your ship as gracefully as possible (`|exit` if it works).
2. Zip up your ship's pier (`tar cvzf sampel-palnet.tar.gz sampel-palnet`).
3. Copy the ship over the network to a local laptop or desktop drive where you have some breathing room.  (The technique varies, but `scp -r user@remote:~/sampel-palnet.tar.gz .` may suffice.  If you were unable to zip up the ship because of space issues, just copy the directory, i.e. leave out the `.tar.gz`.)
4. Unpack the ship (`tar xvzf sampel-palnet.tar.gz`).
5. Carry out basic maintenance (`pack`, `meld`, `roll`, `chop`).
6. Confirm that the ship runs with `./sampel-palnet/.run -l` (which blocks networking, just in case).
7. ONLY NOW DELETE THE REMOTE COPY.  This is the step at which you are most likely to make a mistake, so please triple-check.  On the remote computer, `rm sampel-palnet.tar.gz`
8. Zip the pier up locally (`tar cvzf sampel-palnet.tar.gz sampel-palnet`) and move it back to the remote computer (`scp -r ./sampel-palnet.tar.gz user@remote:~`).
9. Unzip the ship on the remote (`tar xvzf sampel-palent.tar.gz`).
10. Using `screen` or whichever session manager you like, start the ship normally.
11. After verifying that the ship works, triple-check and run the command `rm sampel-palnet.tar.gz` to remove the compressed version.

Mediations:
- Increase the swap space.
- Run with more RAM.

### Solid-State Drive Failure


##  Lesson 6:  Starting More Ships

> ### Objectives
> 
> 1. Spawn subsidiary moons.
> 2. Operate multiple ships.
> 3. Connect a master ship to a slave ship for app control.

While we are not going to break your ship in *The Urbit Book* lessons, you may want to keep things tidy on your main ship.  In that case, completing the lessons using a secure disposable identity is a great way to experiment.

If you are self-hosting a planet, you have available to you 2³² "moons".  These are wholly-owned inferior identities that you can use.

> ##  Hosted Moons?
>
> Hosted planets also have moons, but hosting providers do not currently support running them on the hosting platform. Thus the process for running moons crosses over into self-hosted territory.  If you are hosted, you can use the same procedure here, but you'll need to run the moon on your own hardware.

A moon depends on its planet to contact other points.  You'll need to run the planet the whole time that you are using the moon.
