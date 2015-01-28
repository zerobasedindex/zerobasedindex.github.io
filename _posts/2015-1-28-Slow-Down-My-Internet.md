---
layout: post
title: Slow Down My Internet (for Testing)
---

## Narrative Fodder

As a engineer, you're development environment is typically tuned for performance. You've got plenty of memory, disk space, and fast/low-latency networking. However, the real-world doesn't typically conform to our development environment level of performance, particularly the networking. This is especially important for today's applications (web and mobile) as they make heavy use of web services.

The side effect of running at full-tilt during development becomes evident when you start using the app under more real-world conditions, for example, using a cellular network or crappy WiFi. Things start to break due to previously unknown race conditions, your UI starts acting unresponsive, or things just straight up crash. So QA does its job and files a bug, and you try to reproduce it, wondering how this thing could break after working flawlessly in development. 

If you could only reproduce the real-world networking conditions in your tricked-out-bug-killing development environment. Well, if you own your server, and it's running Linux, then you're in luck. If you don't own the server but you can setup a proxy (Web/Socks/SSH forward) then you can probably use the same approach but in a modified way, which you'll have to figure out.

Built into a modern Linux kernel is [netem](http://www.linuxfoundation.org/collaborate/workgroups/networking/netem) which enables NETwork EMulation of Wide Area Networks (WANs), including delay, loss, reordering, and duplication of packets. You can use netem to take your pristine network and gum it all, nice and dirty like.

## What You'll Need

1. The Linux server hosting your web services or a bridge/router in the network path
1. Root access to said server

## Technical Stuff

Get on your server and use the following commands or variations thereof to shape your network to match you're real world situation. I'm only going to get into packet delay and loss, but to get a better approximation of your real-world network feel free to explore the netem documentation.

### The Lead

Skip this if you want real knowledge. For those who don't want to read what follows, the following will add 100ms of delay, with a random variation of 10ms and 25% correlation on previous, and drop 0.5% of packets with a 25% correlation on the previous:

```bash
$ sudo tc qdisc add dev eth0 root netem delay 100ms 10ms 25% loss 0.5% 25%
```

### Basis of tc

Adding an emulation when you haven't already:

```bash
$ sudo tc qdisc add dev [interface] root netem [emulation ...]
```

Changing/updating an emulation once you already added one:

```bash
$ sudo tc qdisc change dev [interface] root netem [emulation ...]
```

All of the examples below assume it's the first time you're adding a 

### Delay

You can add delay to each packet to emulate real-world transit times. You can get an estimate by using tools like ping or your own web service round-trip instrumentation.

Template:

```bash
delay [delay_amount] [random_variation] [correlation]
```

#### Examples:

Add 100ms of delay to all packets:

```bash
$ sudo tc qdisc add dev eth0 root netem delay 100ms
```

Add 100ms of delay to all packets, with a random variation of 10ms, essentially add a delay of 100±10ms:

```bash
$ sudo tc qdisc add dev eth0 root netem delay 100ms 10ms
```

Add 100ms of delay to all packets, with a random variation of 10ms, essentially add a delay of 100±10ms, BUT the next value will be dependent on the previous by 25%:

```bash
$ sudo tc qdisc add dev eth0 root netem delay 100ms 10ms 25%
```

### Delay with Distribution

If you want to get fancier you can use something like a normal distribution, you know, like those curves you learned about in Stats for Engineers.

```bash
delay [delay_amount] [random_variation] distribution [distribution_type]
```

#### Example:

```bash
$ sudo tc qdisc add dev eth0 root netem delay 100ms 10ms distribution normal
```

### Loss

Delay is only half the battle, loss allows you simulate the occasional dropped packet. Pushing the the drop percentage up can have some detrimental effects, so set wisely.

Template:

```bash
loss [percentage_drop] [correlation]
```

#### Examples:

Randomly drop 0.3% of the packets:

```bash
$ sudo tc qdisc add dev eth0 root netem loss 0.3%
```

Randomly drop 1% with each next value being 25% dependent on the previous:

```bash
$ sudo tc qdisc add dev eth0 root netem loss 1% 25%
```

### Putting the Two Together

Add some delay and packet loss:

```bash
$ sudo tc qdisc add dev eth0 root netem delay 100ms 10ms 25% loss 1% 25%
```

### Showing and Deleting Emulation Rules

Show current rules:

```bash
$ sudo tc -d qdisc
```

Delete rules:

```bash
$ sudo tc qdisc del dev eth0 root
```

## Wrapping Up

Go ahead and give it a try and see it helps. I was able to use this to reduce network performance to find how crappy things need to get to screw with my streaming video experiment, but it should work for any networking.

Be sure to remember to turn it off when you're done. Also, this is only to be used for good, not for screwing with your co-worker who left a root shell open on his computer, even if he's asking for it.

## Links and References

1. [The Inspiring StackOverflow Question](http://stackoverflow.com/questions/614795/simulate-delayed-and-dropped-packets-on-linux)
1. [netem Site](http://www.linuxfoundation.org/collaborate/workgroups/networking/netem)
1. [tcng (for the brave)](http://tcng.sourceforge.net/)








