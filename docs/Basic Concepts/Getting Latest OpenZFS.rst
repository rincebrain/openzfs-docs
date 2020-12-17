OpenZFS Update Timetables
=========================

Simple Concepts
~~~~~~~~~~~~~~~

The short thing you need to take home is basically that:
For your distro to support X, upstream OpenZFS needs to support X, plus however long your distro takes to integrate and test the fixes from upstream.

So if OpenZFS 2.0 doesn't have patches to support Linux 5.19 yet, that needs to happen first, plus whatever needs to happen for your distro to integrate and roll out those fixes themselves.

These times are all ballpark estimates, intended to give you some way of estimating when you might expect support to show up in your distro compared to the first day a version changes.


OpenZFS and Kernel Versions
~~~~~~~~~~~~~~~~~~~~~~~~~~~
================================================  =======
Updated component								  Time to update
================================================  =======
Update to support new kernel (released edition)   weeks
Update to support new kernel (unreleased)   	  unpredictable
================================================  =======

Distro package updates to new version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Debian
~~~~~~
================================================  =======
Updated component								  Time to update
================================================  =======
Update to support new version (major release)     TBD
Update to support new version (point release)     weeks
Update to support new kernel (released edition)   weeks
Update to support new kernel (unreleased)   	  unpredictable
================================================  =======

Getting an update into Debian stable looks like:
Update into unstable -> update into testing -> update stable

Getting a bigger update into stable looks the same, except the end step is, assuming the maintainer is willing,
Update into unstable -> update into testing -> update -backports

So for Debian, barring catastrophe, any new version (major or point release) is going to take some amount of time packaging the update, then about a week percolating into testing, and then a variable amount of time before the maintainers upload the package to -backports or propose it for stable (assuming it's just a point release).

Consider, for example, the following situation:

* stretch is Debian oldstable
* buster is Debian stable
* bullseye is Debian testing 
* sid is Debian unstable

* stretch has 0.6.5.9-5 in stretch proper, 0.7.12-2 in backports, and 0.7.13-1 in backports-sloppy.
* buster has 0.7.12-2 in buster proper, 0.8.5-3 in backports
* bullseye has 0.8.5-3 in bullseye proper
* sid has 0.8.5-3 in sid proper``

For pushing OpenZFS 2.0 into bullseye, ultimately, what will happen is:

* 2.0.0-1 will get pushed into sid
* Several days later, 2.0.0-1 will get pushed into bullseye, possibly with bugfixes being submitted in the interim and restarting the timer
* Depending on whether the Debian release freeze is happening, they may need to get an override agreeing that they can push the newer version into bullseye and not have it in -backports.
* from there, you would next get 2.0.0 in buster-backports (probably), and any further backporting would be an open question.

Whereas for just pushing 0.8.6 into bullseye, we'd get:

* 0.8.6-1 into sid
* Several days pass, pushed into bullseye
* Several days pass, we see 0.8.6 in buster-backports