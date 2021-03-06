Title: The Tor BSD Diversity Project
CSS: torbsd.css
Author: gman
Editors: attila
Date: 2015-10-29
X-Note: These lines at the top are multimarkdown metadata; leave them.
{{meta.md}}

{{header.md}}

##A Blog, or a Central Location for Announces and Notes##

__March 2016__

[TB 5.5 on the Current Snapshots](#tb-snaps-status2) [%sep] [Porting PETs Updates](#portpets-up) [%sep] [March 10 OpenBSD Snapshots](#tb-snaps-status1) [%sep] [TDP at BSDCan 2016](#bsdcan0) [%sep] [TB 5.5 and i386/amd64 Snapshots](#tb-snaps-status0)

__February 2016__

[TB 5.5 and More New Snapshots](#tb55snaps1) [%sep] [TB 5.5 and New Snapshots](#tb55snaps) [%sep] [Onto the Next Phase](#next-phase) [%sep] [Tor Browser Releases](#tb-releases) [%sep] [Tor Browser 5.5 Ports Tagged](#tb-55-tagged)

__January 2016__

[Still Plugging Away](#still-here) [%sep] [Tor-in-a-Box?](#torbox)

__December 2015__

[Notes From The Front](#notes-from-the-front) [%sep] [Announcing Porting PETs](#pp-announce) [%sep] [Thinking About 2016](#2016-events)


__November 2015__

[PETs Porting Targets](#pets-ports) [%sep] [The Case of the Brazil Relays](#br-case) [%sep] [TB 5.0.3 Packages Updated, Again](#tb-update-again) [%sep] [Coming Soon: Quick-and-Dirty Reports](#dirty-reports) [%sep] [Thoughts on Reproducible Builds](#repro-builds) [%sep] [It's Up to You](#up-to-you)

__October 2015__

[Updated Tor Browser Packages](#tb-update) [%sep] [The BSD Relay Guides](#relay-guides) [%sep] [Our First Bells](#first-bells) [%sep] [Beyond OS Diversity](#beyond-os) [%sep] [Tor Browser version 5.0.3 for OpenBSD](#tb-5.0.3)

[From the Attic](#attic)

###20160331###

<a id="tb-snaps-status2">__TB 5.5 on the Current Snapshots__</a> by gman999

As of last week's OpenBSD's i386 and amd64 snapshots, TB 5.5 is no longer working.

We are looking to start building the Tor Project's most recent TB soon. Spending time on TB 5.5 is fruitless when 5.5.4 is the current TP release.

The OpenBSD project just announced the release 5.9 a month early, which I personally don't remember ever happening. The project usually follows a strict six-month release cycle. We are going to focus on getting TB into the next stable release of OpenBSD, which would be 6.0, planned for November 1. Of course we hope to have TB in the snapshots ports way before that date.

Meanwhile, the [Quick-and-Dirty Static Reports](dirty-stats.html) are still updated regularly, albeit manually still.

Additionally, a lot of time has been recently committed to [Porting Targets for PETs](porting-pets.html). It's a tough battle. You spend time getting the basic aspects of the Makefile operational, you figure the peculiarities of how a port is compiled, the array of licenses, and so on, but then you realized a host of unported Python libraries build or run dependencies. Jump out of vi(1) and into the rabbit hole.

A final note on porting PETs-related software, mostly directed at developers. Write your software to be portable, please. Creating a Python module port or package may be a simplistic example of portability, but a negative example is doing builds specific by each OS and Linux distribution. Don't give me setup_debian.py, or a setup file that relies on a handful of operating system choices. Give me an install script that can recognize the global variables and avoid hard-coded paths, that doesn't need one [shell](https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=bash) or another. What does [bash](https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=bash) provide that the install script requires? I mean, really? For the vast majority, a 1995 Bourne shell would be more than sufficient.

If you only want, say, Debian users, for your PETs application, you are definitely not looking at the basic diversity arguments so apparent to most people. You are also cutting off more potential downstream developers that could be making your life easier. Treated nicely, downstream developers can make you look significantly smarter than you might be. There are arguments whether the "many eyeballs" make open source software more secure when most people don't read code, but there's no question that more downstream developers hacking on your code really does. 

###20160320###

<a id="portpets-up">__Porting PETs Updates__</a> by gman999

[Porting Targets for PETs](porting-pets.html) is meant as a hit list of privacy enhanncing related ports that may or may not be in the main BSD port/package systems. As we make clear on the page, some should be considered for entry into BSD ports systems, while others may not be good candidates for a variety of reasons.

As we (manually) update the project page, a few points come to our attention:

* [pdf-redact-tools](https://firstlook.org/code/project/pdf-redact-tools/) is now in NetBSD's cross-platform ports system, pkgsrc.

* [torsocks](https://gitweb.torproject.org/torsocks.git/) isn't in the pkgsrc tree, which comes as a surprise (and correction).

* [onioncat](https://www.cypherpunk.at/onioncat_trac/) was added to the list, and it's also not in the pkgsrc tree. The OpenBSD version is outdated.

* Since our last update, we're happy to see that [ricochet](https://ricochet.im/) is now in DragonFly BSD's DPorts system.

* [obfsproxy](https://gitweb.torproject.org/pluggable-transports/obfsproxy.git) is not in the OpenBSD ports tree, but it is in the GitHub [work-in-progress ports](https://github.com/jasperla/openbsd-wip). [obfsproxy] also isn't in the pkgsrc tree. Pluggable transports are worthwhile ports to consider, since the censorers are fond of blocking Tor traffic.

* We are excited there's a pkgsrc [attempt to port Tor Browser](http://ftp.netbsd.org/pub/pkgsrc/current/pkgsrc/security/tor-browser/README.html). We have reached out to the developer directly and indirectly several times, but have not heard back unfortunately. Our __TDP__ fellow-travellers tried to reach out to the developer, ryoon AT netbsd.org, at [AsiaBSDCon](https://2016.asiabsdcon.org/] last week, but were unable to find him. We do hope to hear back from him at some point to synchronize our efforts. We are sure there's a lot to learn from each others' experiences.

* Besides torsocks, pkgsrc doesn't contain a [stem](https://stem.torproject.org/) port which is vital for tools like [arm](#pkg-arm) and for any tool that talks to the Tor control port.

Don't hesitate to ping us if you're interested in addressing anyone of the above ports. We can direct you to the appropriate mailing list or developers, or dump any Makefiles we may have already created.

At this point, __TDP__ isn't focusing on porting these applications, but unofficially we have begun to toy with some of them.

###20160310###

<a id="tb-snaps-status1">__STATUS: TB 5.5 and i386/amd64 Snapshots__</a> by gman999

Tor Browser 5.5 is still working with the newest OpenBSD snapshots, which is #1638 for [i386](http://www.openbsd.org/i386.html) and #1918 for [amd64](http://www.openbsd.org/amd64.html).

###20160303###

<a id="tb-snaps-status0">__STATUS: TB 5.5 and i386/amd64 Snapshots__</a> by gman999

TB 5.5 is working fine with the newest OpenBSD snapshots:

* amd64 is #1890

* i386 is #1618

###20160301###

<a id="bsdcan0">__TDP at BSDCan 2016__</a> by gman999

Our presentation entited ["Beyond Monocultures"](https://www.bsdcan.org/2016/list-of-talks.txt) was accepted for [BSDCan 2016](https://www.bsdcan.org/2016/) on June 10-11 in Ottawa, Canada.

We feel very fortunate, since there were a lot of submissions for what is the premier BSD event in the western hemisphere. BSDCan has grown substantially since 2004, with hundreds of attendees participating.

Last year we conducted a [birds-of-a-feather session](https://www.bsdcan.org/2015/schedule/track/BOF/624.en.html) which attracted around 50 people.

This year, we should hopefully have some good news to publicize about TDP. In the meantime, the actual presentation should start coming together in the next month or so. In all honesty, it's hard to determine what the focus of the presentation should be. We only have a general idea of where we'll be by mid-June.

At this point, the introductory part should start with "Why Tor Sucks" plagiarizing Henning Brauer's [OpenBSD Sucks](http://quigon.bsws.de/papers/2015/asiabsdcon/index.html) concept. This is a backhand approach to arguing why Tor matters. The reality is that a lot of people in the BSD community continue to see Tor as ineffective or insecure, so the case for Tor being full of problems yet the very best thing available needs to be made.

It's not that BSD people overwhelmingly aren't concerned with security and privacy. At the bar last at BSDCan last year, surrounded by some of the best known BSD veterans from the 1970's, I listened how they dealt with surveillance. One file system hacker with decades of experience mentioned how he always changed his MAC address when using public wireless.

But there's also a sense that Tor is too easily broken, such as with timing attacks from a global passive adversary. Or that if enough Tor relays are run by an adversary to anonymity, the network is useless. All are valid points and certainly need further attention. The heavy brains at the bar that night could infuse some assistance.

###20160223###

<a id="tb55snaps1">__TB 5.5 and More New Snapshots__</a> by gman999

Yesterday the OpenBSD snapshots updated to #1881 for amd64 and #1609 for i386. TB is working fine on both.

Meanwhile, the TB packages were updated. First we implemented a meta TB package, as per landry@'s comments. Note that the start-tor-browser script was also deprecated recently. All the sloppy setup gook was replaced by neater Firefox hacks.

Installing TB from the mirror is simple:

    $ doas env PKG_PATH=http://mirrors.nycbug.org/pub/snapshots/packages/amd64/ pkg_add tbb

For i386 installs, replace /amd64/ with /i386/.

__Be aware that that we are still tinkering with TB 5.5 which has some significant vulnerabilities that could disclose a user's identity. TB 5.5.2 is in the pipeline.__

A question for TB testers out there: does a Tor Browser icon appear on the desktop after TB installs?

According to the general standards on window manager desktops, it should as the installer places /usr/local/share/applications/tor-browser.desktop into ~/.local/share/applications. However, on XFCE it doesn't appear, and the file needs to be placed in ~/Desktop. How about KDE and GNOME users out there? Let us know.

We imagine that most users following -current are probably running cwm.

###20160221###

<a id="tb55snaps">__TB 5.5 and New Snapshots__</a> by gman999

Just a short note: Tor Browser for OpenBSD 5.5 is still working with the most recent OpenBSD snapshots (#1880 on amd64 and #1608 on i386).

We always use the most recent snapshots on our boxes, and usually update the TB packages when TB needs updating due to relevant snapshot changes. Since our build process significantly simplified with TB 5.5, primarily due to [landry@'s input](https://marc.info/?l=openbsd-ports&m=145581927415588&w=2/), updates to both amd64 and i386 builds became relatively painless.

And it should only get better in the near-future releases.

###20160216###

<a id="next-phase">__Onto the Next Phase__</a> by gman999

The progress we've made over the past five days was exhausting, yet exciting.

Some very significant steps were made with Tor Browser.  A revised 5.5 release does not contain the start-tor-browser script any longer; all the necessary setup steps are now done with Javascript, including the profile setup. The Firefox add-ons are now dumped into the profile as files, such as https-everywhere@eff.org.xpi, instead of being extracted into directories. Additionally, we are now building an i386 version of TB.

We are aware that [TB 5.5.2](https://blog.torproject.org/blog/tor-browser-552-released/) was released by the Tor Project this past Friday, a mere hour after we announced our 5.5 release. TB 5.5.2 includes some important security changes coming from the Mozilla upstream, although much can be mitigated by moving the security slider to high. And [TB 5.5.1](https://blog.torproject.org/blog/tor-browser-551-released/) was also released before our TB 5.5, but the changes were significant. Nevertheless, the last five days of constant hacking and testing on TB makes future releases less painful and more smooth.

Finally, for those doing TB testing, we have a brief guide to what to test in a [Testing Tor Browser](testing-tb.html) piece. The past week has already changed some of the steps, and we look to expand and formalize this document so it becomes a useful tool.

It's almost a year since our first commits to GitHub, and it's been a long and sometimes painful learning experience, but we think we're now in a great spot.

###20160205###

<a id="tb-55-tagged">__Tor Browser Ports for 5.5 Tagged__</a> by attila

I just merged 5.5 onto master and [tagged it](https://github.com/torbsd/openbsd-ports/releases/tag/tbb-5.5-sans-pt/).  This release was much easier after the work on 5.0.6, which has us using [mozilla.port.mk](http://cvsweb.openbsd.org/cgi-bin/cvsweb/~checkout~/ports/www/mozilla/mozilla.port.mk?rev=1.84&content-type=text/plain) instead of a bunch of cut-and-paste adapted from same.  This makes things a lot easier moving forward.  So far 5.5 on amd64 is looking good.

<a id="tb-releases">__Tor Browser Releases__</a> by gman999

It's been a while since our last Tor Browser releases, but it's not because we haven't been busy. Smaller projects like [Quick and Dirty Statistics](dirty-stats.html) and [Porting PETs](porting-pets.html) have continued to progress, and other stuff that attila can elaborate on in a future blog post.

While worked dragged on with the 5.0.6 Tor Browser release, we managed to not only finish that [release](http://mirrors.nycbug.org/pub/snapshots/packages/amd64/archive/tb-5.0.6.tgz), but also finish up the [5.5 release](http://mirrors.nycbug.org/pub/snapshots/packages/amd64/README-55.txt). That puts us parallel with the current Tor Project release.

We are now archiving previous versions of TB as tgz file in an [an archive directory](http://mirrors.nycbug.org/pub/snapshots/packages/amd64/archive/). Version 5.0.6, which barely saw the light of day, is there.

We are excited by the releases, and look forward to feedback from the testers out there.

One quick note about Tor Browser 5.5 on OpenBSD 5.8 stable. We have repeated ad nauseum, but it's worth reiterating again: OpenBSD development happens on -current, a.k.a., snapshots, which ultimately turn into the next stable release every six months.

Developing Tor Browser for OpenBSD stable means dealing with multiple levels of differences between stable and current, from the package versions to libraries in the base operating system. In *BSD land, userland applications and the base OS are meant to play nice together by default.

In the case of trying to run TB 5.5 on OpenBSD 5.8 stable, there are two package incongruities. First, 5.8-stable's Tor version is 0.2.6.10p1, while the current version is 0.2.7.6. Second, the nspr stable version is 4.10.8, while the current version is 4.11. Both current versions of the packages rely on operating system changes not present in stable. There is a ports freeze approaching for the May 1 OpenBSD 5.9 stable release, and we may use that as an opportunity to produce a stable version of the Tor Browser. Stay tuned.

###20160118###

<a id="torinabox">__Tor-in-a-Box__</a> by gman999

If someone reasonably technical bumps into Tor for the first time, eight or nine seconds later, they arrive at the concept of some type of Tor device that automagically routes all local network traffic through the Tor network.

Great idea. The fact that so many imagine such a concept certainly means something.

All too often, unfortunately, the implementation is wrong. Dead wrong.

In the early 1990's, a desktop's traffic to the public internet was simple. There might be some HTTP from a web browser, a dash of UDP for DNS lookups and maybe some POPing to a remote email server. All was relatively quiet.

Over the past two decades, the wall between the internet and the desktops evaporated. Why is Windows 10 a free upgrade? Likely because a "free" operating system is well-compensated by full control of the desktop environment. And that means a tcpdump(8) from 1994 bears no resemblance to the ugly spew of 2015.

After those initial eight or nine seconds, going back to the basics of design should be the next reaction. Stop trying to make tools that do everything half-way. Too often an all-in-one device that tries to solve multiple problems displays contradictions between those functions. Thus, the core Unix principle that is considered dated by many, yet justifies itself with each new "wonder box" incarnation: one tool for one function.

That is not an argument against innovation, products or progress on any level. The point is the moment an attempt is made to cast a wide net into a complex sea, the net is shredded. The net's target is not a school of sardines, but sardines, sharks, with rusted earth-moving equipment, yellow school buses and maybe a piece of space hardware or two.

More on this theme later, but the resilience of the classic Unix themes rises from the grave daily in an age of all-in-one products or services that tries to do everything, but succeeds at doing some things poorly and others dead-wrong.


###20160102###

<a id="still-here">__Still Plugging Away__</a> by gman999

We are still moving along.

Attila began working on the next Tor Browser release yesterday.

[Dirty Statistics](dirty-stats.html) are still being updated and tweaked. More reports are in the pipeline.

Some inferences from the Dirty Statistics reports:

* 'Bandwidth Ranking by Country Code' shows a disturbing concentration of public Tor bandwidth. The recent chatter in France about banning Tor would have a disastrous effect on available bandwidth, with a quarter of Tor bandwidth being from there. Two other countries, Germany and the Netherlands, also provide double-digits of Tor bandwidth. Lack of diversity is a critical Achilles' Heel.

* 'Bandwidth Ranking by Operating System Platform' continues to illustrate our main motivation, over 93% of Tor bandwidth is running on one Linux distro or another. Interestingly, FreeBSD is a strong second at over 5.6% of public bandwidth, with the next contender being OpenBSD at under .5%. Those BSD numbers are fascinating since in terms of quantity of relays, Windows far exceed the BSDs.

* 'Exit Relays by Country Code' shows that even though the US provides under 10% of public Tor bandwidth, it accounts for almost 18% of exit relays with Germany being distantly in second place with under 12% of exit relays. France, despite dominating in public bandwidth, only accounts for less than 9% of exit relays.

* 'Total Relay Count by Operating System' illustrates the hard numbers of public Tor relays by operating system. Windows maintains second place, with FreeBSD and OpenBSD occupying third and fourth places. Besides displaying the Linux monoculture, it also illustrates that a lot of Windows users, most likely running relays with the Tor Browser client software, are contributing relays.

* 'Relay Count by Country Code' shows the disturbing concentration of public relays with three countries, Germany, the US and France, having double-digits in relays. In terms of distribution, having as many countries as possible get up to having 1% of relays would be ideal, but not by decreasing the number of public relays in the top entries.

* 'Countries without Public Tor Relays' generally hovers between the high-70's to the mid-80's in numbers. Of course, in a lot of those countries it's dangerous or just cost-prohibitive to run relays, yet it is likely that Tor isn't well-known enough in some of them. If you are in one of those countries, drop us a note on why running a public Tor relay is difficult. If you know someone in one of those countries, ask them yourself and let us know.

Remarkably, Tor Browser 5.03 is still functional on OpenBSD/amd64 with the #1783 snapshot from December 27th. Snapshots frequently take hard twists and turns, as is to be expected with the development branch of any operating system, so this is something of a surprise. The early releases of __TDP's__ 5.03 faced some hiccups with various changes, but we are trouble-free since.

One thing to note is that the number of public *BSD Tor relays, not including BitRig, remains consistently above 5% of total relays. While we can't necessarily attribute to __TDP__, we like to think the noise we make helped a little bit.

Stay tuned. We are still very active, even when we are publicly quiet.

###20151216###

<a id="notes-from-the-front">__Notes From The Front__</a> by attila

First: hats off to gman999 for his incessant efforts in getting the content of this site in better shape. I especially applaud this low-tech/no-tech blog layout in MultiMarkdown.

I have been noticeably lacking, but not totally idle.  I've had to take some paying work, which has slowed me down on open source, but my path forward is fairly clear.  My main task is to rework the makefiles (mainly the stuff in Makefile.inc) that comprise the [OpenBSD ports](https://github.com/torbsd/openbsd-ports/) for TBB so that they dovetail with and use as much as possible of the Mozillan infrastructure already in the OpenBSD ports tree, much of it due to `landry@`, who has already helped me a couple of times.  I should've done this from the beginning but my head wasn't really on straight when I first started this.  I've been reticent about touching anything that I didn't write, choosing instead to adapt what others have done to get something working. Although this was perhaps effective in the short term if we want this in the tree it has to be consonant with it... in short: if you're serious about contributing to OpenBSD then pick up a shovel and start digging, but politely. I'm sure I can do that so I just have to get to it.

I hope to have a first cut at a rework of the ports, still based on 5.0.3, sometime next week... I don't really celebrate any holidays so I'm hoping to get a lot done while the rest of the world sleeps it off.  Once the makefiles are closer to right I'll work on an update to 5.0.5 (or whatever is current on the 5.0.x branch).  I'm afraid I might miss the next ports lock window because I've taken too long, but oh, well... _que sera sera_.

<a id="pp-announce">__Announcing Porting PETs__</a> by gman999

One of the small projects we have spent some time on recently is <a href="porting-pets.html">Porting PETs</a>. This is an attempt to list the various privacy-enhancing applications and their statuses in the BSD ports.

Most of these ports arose as non-commercial, open source reactions to mainstream applications and services. Some are ported to one BSD or another, others are not.

The list is not exhaustive, but it was certainly exhaustive to create. Updates will happen manually, so <a href="https://github.com/torbsd/torbsd.github.io/issues/">diffs</a> are appreciated.

Porting third-party applications is a frequent gateway for BSD users to become developers, this list will be circulated in the relevant BSD channels.


###20151202###

<a id="2016-events">__Thinking About 2016 __</a> by gman999

The BSDCan 2016 [call for papers](https://www.bsdcan.org/2016/papers.php) was issued yesterday, and a __TDP__-related submission was made. BSDCan is likely the largest BSD gathering globally, and an excellent opportunity to speak to *BSD developers and users.

EuroBSDCon 2016 [is tentatively slated for September 2016](https://2016.eurobsdcon.org/) in Belgrade, Serbia. It is another significant BSD event, attracting users and developers from Europe and beyond. At a glance, there are only two Tor relays in Serbia, and both are Linux. Beyond Serbia, there are few Tor relays in the Balkan states overall, making EuroBSDCon 2016 a great opportunity to extend not just BSD Tor relays, but *any* Tor relays.

No dates have been set for [AsiaBSDCon](https://2016.asiabsdcon.org/), but it's usually in March. Japan is well-wired with inexpensive residential broadband, yet there are only around 50-60 relays in the country. Considering it's a BSD-heavy nation, it's shocking that there are only a handful of *BSD relays. Yet another green field of opportunity.

Stay tuned. Whether we can speak at any of these events will also depend on financial support for __TDP__.

###20151119####

<a id="pets-ports">__PETs Porting Targets__</a> by gman999

After the June 2013 Snowden disclosures, a rush towards developing applications to counter mainstream, closed-source services commenced. Many focuse on Debian Linux as a development platform, but aim at more widely used Windows, OSX, iOS and Android user-base. Beyond client applications, there are also network-based servers and services seeking to provide privacy and anonymity.

The term "PETs" refers to privacy-enhancing technologies, and in this case, we use it as a catch-all for these server and client solutions.

Some of these projects have been ported to one or more BSD.  Others have not. On that note, we began a [list of applications and their status as BSD ports in the main BSD operating systems](porting-pets.html). We encourage feedback on this list, and also investigations into porting these applications. Some of well-worth reviewing and considering; others have ceased development or are broken beyond resurrection. Others just need some reworking towards sanity, as one will notice that ubiquitous build dependency [bash](https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=bash).

It's a call for engagement to the *BSD community.  Bring your sane, portable development approaches, your intransigent working and reworking of Makefiles, your austere mentality. This is an opportunity to improve applications whose user base might be someone whose life depends on it.

###20151112###

<a id="br-case">__The Case of Brazil Relays__</a> by gman999

Just a short note about the Brazil relays implemented after [BSDCon Brasil](http://2015.bsdcon.com.br/). Before the early October conference, it seems there was only one public Tor relay. After the event, there are up to five or six relays maintained by two separate individuals. It's understood that some bridges also joined the Tor network also, but we don't have any direct evidence.

It's not an enormous leap in relay numbers for Brazil, but adding a handful of relays to a country that only had around 20 is significant. More importantly, it seems that the new BSD relays contribute a decent amount of bandwidth.

However, there is a discrepancy between the "Tor Status" data provided by [https://torstatus.blutmagie.de/](https://torstatus.blutmagie.de/) and [https://torstatus.rueckgr.at](https://torstatus.rueckgr.at/). Part of this might be answered by the fact that both are statically updating at different intervals. Olaf Selke of BlutMagie.de, also notes that the "observed bandwidth" numbers are diffferent since only BlutMagie.de [shows the average bandwidth based on the "extra-info" descriptor](https://lists.torproject.org/pipermail/tor-talk/2015-November/039414.html) while other sites, including Rueckgr.at, display the peak bandwidth.

However, there still seems to be discrepancies beyond the "observed bandwidth" field, which we will look at further in the future. For instance, a bunch of AWS Tor relays appeared on BlutMagie.de the other day and remained for a few days, but never showed up on Rueckgr.at. And more oddly, all the relays quickly remained highest bandwidth providers for a few days, in contrast to the normal trajectory of a relay.

For now, either site is useful for giving a broad picture of the public Tor network. It is true that the Brazil relays look at a lot more significant in terms of observed bandwidth at Rueckgr.at.

###20151111###

<a id="tb-update-again">__TB 5.0.3 Packages Updated, Again__</a> by gman999

The <a href="http://mirrors.nycbug.org/pub/snapshots/packages/amd64/">Tor Browser 5.0.3 packages</a> were updated again, due to the need for icu4c version 56.1. Both devel/nspr and textproc/icu4c are updated in the OpenBSD ports tree, and the TB packages have been rebuilt for them. Be sure to make sure packages or ports are updated before installing. If the host is updated, there's no need to use our devel/nspr or textproc/icu4c packages.

This is all a true story of the constant attention necessary to develop sanely on any operating system: develop on the most current version, and look forward to an automated build process for it, but ultimately a stable version is a beautiful thing.

###20151108###

<a id="dirty-reports">__Coming Soon: Quick-and-Dirty Reports__</a> by gman999

This week we'll post "Quick-and-Dirty Reports," providing diversity-related snapshots of the public Tor network. Currently, the five reports are generated manually from the [ruckgr.at Tor Status](https://torstatus.rueckgr.at/) [CSV files](https://torstatus.rueckgr.at/query_export.php/Tor_query_EXPORT.csv), but they are being migrated to SQLite in the future.

A quick sample of the current reports were posted in an [earlier blog entry](#beyond-os).

The only comparable service we know of is the [Tor Metrics site](https://metrics.torproject.org/) which has the additional function of providing historical data. Our goal is considerably more mundane, yet also functional.

Nothing ground-breaking or revolutionary about the reports, but we do hope others find them useful, and maybe event extend their use.

###20151104###

<a id="repro-builds">__Thoughts on Reproducible Builds__</a> by gman999

Just a quick link to a pleasantly polemical post from September 19th by [OpenBSD's](http://www.openbsd.org) tedu@ entitled [reproducible builds are a waste of time](http://www.tedunangst.com/flak/post/reproducible-builds-are-a-waste-of-time). There's a follow-up postscript at the end of the post, reacting to a [lobste.rs thread](https://lobste.rs/s/5bbdbo/reproducible_builds_are_a_waste_of_time).

###20151103###

<a id="up-to-you">__It's Up to You__</a> by gman999

Since we launched __TDP__, two of us spend a lot of time, energy and resources getting the various projects designed and implemented.

But there's is always room for one, two, three more.

It's a perfect opportunity to start testing Tor Browser 5.0.3. [Fork the repository](https://github.com/torbsd/openbsd-ports), submit [issues](https://github.com/torbsd/openbsd-ports/issues) about the software.

There's more to do beyond TB though. If you are around a technical user group, get a discussion going about Tor. Have a how-to meeting on running a public relay, especially for those who have access to decent infrastructure and bandwidth, like those at universities or internet-facing firms.

Setting up a high-bandwidth Tor bridge is painless and it will just be a safe gateway for Tor users.

There is no excuse why every BSD user group or conference shouldn't have a discussion or session focused on "recruiting" BSD people to run Tor relays. Many people in the US, Europe and eastern Asia, in particular have excess bandwidth at home. Work at a firm that uses the BSDs in production? Get them to run a relay or two.

For those who dwell in BSD land, join the [Tor-BSD mailing list](http://lists.nycbug.org/mailman/listinfo/tor-bsd). Running a BSD Tor relay?  Join the [unofficial BSD Buildbot for Tor](http://buildbot.pixelminers.net).

There's a lot we'd like to accomplish with __TDP__, and we don't claim a monopoly on much of anything. We do encourage you to take some initiative and move things forward.

###20151031###

<a id="tb-update">__Updated Tor Browser Packages__</a> by gman999

The upstream code from the Tor Project and above them Mozilla is a moving target we contend with each release. Then there is the ultimate moving target: the incessant war between surveillance and anonymity, censorship and circumvention. Finally there is the operating system as a moving target all Tor Browser porters face.

Developing ports on OpenBSD means building on snapshots, a.k.a., [-current](http://www.openbsd.org/faq/faq5.html#Flavors). OpenBSD snapshots are often released several times a week, and as with any other development operating system branch, those changes are sometimes significant. What might work today may be broken tomorrow. It was no surprise that our TB 5.0.3 release was broken on the OpenBSD snapshot released just a few days later.

[Daniel Jakots](https://lists.torproject.org/pipermail/tor-talk/2015-October/039360.html) noticed this as we did, and we updated the Tor packages accordingly. We made an added change by removing the tbb meta-package, simplifying the 5.0.3 release a bit more.

###20151030###

<a id="relay-guides">__The BSD Relay Guides__</a> by gman999

In their current forms, the [BSD relay guides](relay-guides.html) are unclear and sloppy, and possibly inaccurate in some places. We are putting some work into the [FreeBSD Guide for Configuring Relays](fbsd-relays.html), and will probably divide it into two parts: the short version for the impatient, with other topics being migrated to another page entiled "Advanced."

There is a lot of related topics to cover: to ZFS or not, slimming down a FreeBSD build, etc.

Input is welcomed. Stay tuned.

###20151029###

<a id="first-bells">__Our First Bells__</a> by gman999

Over six months ago we launched __TDP__ in its current form. In March, the [GitHub repository] (https://github.com/torbsd) was initialized and we put some meat on the skeleton we had been toying around with.

We count a lot of accomplishments since launching, but should be honest about __TDP's__ weakest point: marketing and publicity. Of course, it's something we're proud of to an extent. Too many open source projects focus almost solely on publicity, and don't actually accomplish much else. Nevertheless, we will try to start providing a clearer picture of our progress and notes here.

Quite frankly in BSD land, all fluff and no product doesn't get you much credibility. Talk is considered cheap, while good code and real contributions are priceless.

We announced the sixth release of Tor Browser two days ago, version 5.0.3, which was a major milestone for us. We were excited by some of the [feedback](https://lists.torproject.org/pipermail/tor-talk/2015-October/039351.html) on the Tor-talk.

The [presentation](20151010-br/index.html) at [BSDCon Brasil](http://2015.bsdcon.com.br) was a success, with the first BSD relays launched in that country, and which now account for up to a third of observed Tor bandwidth there. More relays should be coming online in Brazil soon, and we know of a few BSD bridges that came online.

Interestingly, one of the relays running on a residential connection, had to be migrated to a bridge. Apparently, one of the relay admin's online services blocked the relay's IP. The IP wasn't an exit relay, but it was a public Tor IP. Let's hear it for collective punishment.

Finally, we will be catching up with the publicity we should have previously done in the near future. Bear with this blog's format, we are not really the WordPress types, if that wasn't already apparent.

###20151028###

<a id="beyond-os">__Beyond OS Diversity__</a> by gman999

__TDP__ focuses on operating system diversification for Tor with BSD Unix. But the need for diversity is more than just operating systems. A quick browse at [one of the Tor Status sites](https://torstatus.rueckgr.at), or more specifically the [Network Statistics Graphs](https://torstatus.rueckgr.at/network_detail.php), the lack of geographical diversity is disturbing.

Parsing the list of Tor relays, there are a number of ISO 8166-1 two-digit country codes [that have no relays](tor-less-ccs.txt). Spreading the Tor network out to those countries should be a primary concern, regardless of operating system.

* Antigua & Barbuda (AG), that hub of online gaming, has no relays?

* Angola (AO), whose capital Luanda is one of the more hopping cities in southern Africa now?

* Jordan (JO), which is apparently one of the better connected locations in the region?

* Latin America and Africa are particularly underrepresented. And for Brazil with over 200 million people and a developed infrastructure, possessing under 30 relays is shocking.

* Pakistan (PK), has no public Tor relays, and India (IN) has under ten, although we're working on the latter case.

We don't know the particulars of infrastructure, connectivity costs, etc., in a lot of those countries, but the underrepresented regions need a dedicated focus.

Also disturbing is the concentration of public relays [by country code](relays-by-cc.txt). Germany and the US contain more than a thousand relays each, accounting for more than a third of the total number of Tor relays globally.

Of course, using Tor in some of those places may be dangerous or cost prohibitive.

We will continue to tinker with the data about geographical diversity in the future, but in the meantime, if you have contacts, friends or families in the underrepresented country codes, now is the time to explore the possibility of getting Tor relays into the Tor-less country codes.

###20151026###

<a id="tb-5.0.3">__Tor Browser version 5.0.3 for OpenBSD__</a> by gman999

__The Tor BSD Diversity Project (TDP)__ is proud to announce the release of Tor Browser (TB) version 5.0.3 for OpenBSD.

__[TDP](https://torbsd.github.io)__ is an effort to extend the use of the BSD Unixes into the Tor ecosystem, from the desktop to the network.

The 5.0.3 release is the sixth release of the Tor Browser from __TDP__.

To install TB for OpenBSD, please see [http://mirrors.nycbug.org/pub/snapshots/packages/amd64/README](http://mirrors.nycbug.org/pub/snapshots/packages/amd64/README).

__TDP__ is focused on diversifying the Tor network, with TB being the flagship project. Additional efforts are made to increase the number of *BSD relays on the Tor network.

Since its launch in March 2015, __TDP__ contributed significantly. In addition to the TB releases, both BSDCan and BSDCon Brasil featured __TDP__-focused meetings.

In early October, a __TDP__ [presentation](20151010-br/index.html) prompted a significant increase in Brazilian Tor relays. Before the presentation, there were around 22 Tor relays, all of which were Linux in addition to two Windows nodes.

In the weeks after the presentation, several new *BSD Tor relays appeared, accounting for up to 35% of observed Tor bandwidth in Brazil.

Finally, __TDP__ is working to convince BSD-using businesses to follow Mozilla's December 2014 example to run Tor relays. At this point, New York Internet has committed to running two high-bandwidth relays, one FreeBSD and the other OpenBSD, at its facility in Bridgewater, New Jersey.

__TDP's__ source code repository resides at [https://github.com/torbsd](https://github.com/torbsd).

__TDP__ is seeking funding to continue and extend its efforts. Please contact us if interested in assisting __TDP__, allowing us to dedicate more time to the project.

###<a id="attic">From the Attic</a>###

Attila blog post on [OpenBSD Tor Browser Ports Status Update: July 2015, 4.5.3 (yes, I know it's August)](http://trac.haqistan.net/blog/tor-browser-ports-progress-3)

Attila blog post on [OpenBSD Tor Browser Ports Status Update: June 2015, v4.5.2](http://trac.haqistan.net/blog/tor-browser-ports-progress-2)

Attila blog post on [OpenBSD Tor Browser Port Progress and Status](http://trac.haqistan.net/blog/tor-browser-ports-progress)

Attila blog post on [Adventures in Ports: The Tor Browser](http://trac.haqistan.net/blog/adventures-ports-tor-browser)

Early Rings ["Porting Tor Browser to the BSDs" thread on Tor-BSD list](http://lists.nycbug.org/pipermail/tor-bsd/2015-February/000225.html)

{{footer.md}}
