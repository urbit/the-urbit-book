#   The Care and Feeding of Ships

##  Learning Objectives:

By completing this lesson, learners will be able to:

- Confidently operate their Urbit ship.
  - Start and run an Urbit ship.
  - Carry out preventive maintenance and understand why each part matters.
  - Recover from minor crashes without help.
  - Recover from major crashes with guidance.

Each lesson should take 15–20 minutes to complete.  You should complete exercises as you read through the lesson.

---

##  What is Urbit?

Urbit is a new vision for how an Internet can work:  secure, decentralized, and owned by the individuals and communities that build it.  There's a lot of jargon involved, but the basic idea is that every part of the network has an encrypted censorship-proof communications channel to every other part.  You don't need permission to spend or receive money, to publish or share software, or to say anything you like.

Before we start using Urbit, we need to get a couple of concepts straight.  Urbit consists of two separate pieces, and you need both of them.

- **Urbit ID**.  Your Urbit ID is your identity on the network.  An Urbit ID is cryptographically secure:  it's yours, permanently.  Like a website, once you've acquired it and set it up, you don't need to think much about anything except the name.
- **Urbit OS**.  Your Urbit OS is the software that you actually run in order to use Urbit practically.  Like a web browser (and often using a web browser), this is the software that you will use in practice.

In most cases, the context should be clear enough that we don't need to distinguish them once we're operational.


##  Lesson 1:  Getting Up and Running

So you're a proud new owner of an Urbit ship.  It's time to boot it up for the first time.

> ### What is an "Urbit ship"?
>
> An Urbit ship is the actual identity you will have on Urbit's network.  It is most commonly a "planet", or regular permanent identity, but it may be a "comet", or temporary identity, if you're on the network without having bought or acquired a plent first.

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

If you are hosted, you should access your terminal from the Landscape page at the Terminal app.  If you are self-hosted, you can use the terminal directly 

basic commands

> ##  Why Can't I Type `Urbit`?
>
> The Dojo prompt has an unusual property:  it will not let you type what it thinks to be invalid commands or code.  That means that sometimes you try to type something and nothing appears at the cursor.  Or sometimes you copy and paste something and it gets garbled.  In both cases, the Dojo parser disagrees that what you're trying to enter is an acceptable command syntax.
>
> To really dig into this, we would have to look at Urbit's programming language, Hoon.  But for *The Urbit Book*, we promised we wouldn't, so we won't!

ship details
azimuth etc.

`|mount`

##  Lesson 3:  The Web Interface

faster
search for an app

##  Lesson 4:  Maintaining the Ship


##  Lesson 5:  What's Going Wrong?


##  Lesson 6:  Starting More Ships

While we are not going to break your ship in *The Urbit Book* lessons, you may want to keep things tidy on your main ship.  In that case, completing the lessons using a secure disposable identity is a great way to experiment.

If you are self-hosting a planet, you have available to you 2³² "moons".  These are wholly-owned inferior identities that you can use.

> ##  Hosted Moons?
>
> Hosted planets also have moons, but hosting providers do not currently support running them on the hosting platform. Thus the process for running moons crosses over into self-hosted territory.  If you are hosted, you can use the same procedure here, but you'll need to run the moon on your own hardware.

A moon depends on its planet to contact other points.  You'll need to run the planet the whole time that you are using the moon.

