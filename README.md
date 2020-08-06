# For the Users - Info and FAQ

_Last Modified: 2020-08-06_

- [For the Users - Info and FAQ](#for-the-users--info-and-faq)
  * [About Us](#about-us)
    + [Questions](#questions)
      - [Who are you?](#who-are-you)
      - [Why the name "For the Users"?](#why-the-name-for-the-users)
      - [Why are projects on both Gitlab and Github?](#why-are-projects-on-both-gitlab-and-github)
  * [Homebrew App Store](#homebrew-app-store)
    + [Questions](#questions-1)
      - [How do I submit apps?](#how-do-i-submit-apps)
      - [How does it work?](#how-does-it-work)
      - [What are these `install.manifest` and `info.json` files?](#what-are-these-installmanifest-and-infojson-files)
      - [Why aren't some of my non-hbas apps detected?](#why-arent-some-of-my-non-hbas-apps-detected)
      - [What apps are allowed on the store?](#what-apps-are-allowed-on-the-store)
      - [How do apps get on the store? What about updates?](#how-do-apps-get-on-the-store-what-about-updates)
      - [Why are all the download counts 0?](#why-are-all-the-download-counts-0)
      - [Is there a 3DS / Wii version?](#is-there-a-3ds--wii-version)
    + [Troubleshooting](#troubleshooting)
      - [Generic crashing while using](#generic-crashing-while-using)
      - [Entering Recovery Mode](#entering-recovery-mode)
      - [Says no Internet is present](#says-no-internet-is-present)
      - [Downloading doesn't work](#downloading-doesnt-work)
      - [I'm having some controller issues](#im-having-some-controller-issues)
  * [DNS Service](#dns-service)
    + [Questions](#questions-2)
      - [How does it work?](#how-does-it-work-1)
      - [Can I self host?](#can-i-self-host)
      - [Is this secure? Can you see what websites I'm looking at?](#is-this-secure-can-you-see-what-websites-im-looking-at)
      - [Why can't I play videos? No cookies? Where's XYZ Feature? Tabs?](#why-cant-i-play-videos-no-cookies-wheres-xyz-feature-tabs)
      - [Does it block updates?](#does-it-block-updates)
    + [Troubleshooting](#troubleshooting-1)
      - [Not working!](#not-working)
      - [Can't get rid of it!](#cant-get-rid-of-it)
      - [Forgot password](#forgot-password)
  * [Discord Info](#discord-info)

## About Us
For the Users is a group dedicated to making homebrew easier to run, and contributing to some open-source projects. We run the hb-appstore project, a GUI for downloading/managing homebrew apps for video game consoles. We also host a DNS service for accessing the Internet on the Nintendo Switch.

Our website is [fortheusers.org](https://fortheusers.org), and we have an [OpenCollective page](https://opencollective.com/search?q=fortheusers) for accepting donations if you feel inclined! We also have a [Twitter](https://twitter.com/wiiubru) where we sparsely post updates.

### Questions

#### Who are you?
You can check [our Members page on Gitlab](https://gitlab.com/groups/4TU/-/group_members)! We come from all over the place, but a good number of us are coming from the Wii U scene, where we hosted homebrew, exploits, and forums on "wiiubru.com". We changed our domain name to 1) be more generic and 2) not to be confused with (and to be respectful of) the homebrew env groups named wiiubrew/switchbrew.

If you'd like to talk with us, our [Discord server is here](https://discord.com/invite/z8wBTvU), or you can email fight [at] fortheusers.org. An issue on [this repo](https://github.com/fortheusers/faq) also works!

#### Why the name "For the Users"?
We view our two primary services as being "for the user", as in, they help facilitate the device's user ability to accomplish a task that they want to do. This could be convenience (as in hb-appstore) or practicality (as in the DNS server), or any in-general move that increases the users rights on how they use their device.

Nintendo for instance hides access to the filesystem to the user, and also hides the web browser. We would consider these to be anti-features, and actively hostile decisions towards the user. Nintendo does perform some pro-user stuff of course too, such as the input mapping that was added in 10.0.0.

Defining what is and isn't "for" the user is a little subjective, but in our opinion tends to be pretty clear cut upon inspection when comparing a device's functionality to a regular personal computer's functionality. For this reason, most if not all homebrew apps, libraries, toolchain libraries, environments, and developers, by virtue of being [homebrew](https://en.wikipedia.org/wiki/Homebrew_(video_games)), are of course "for the user"!

#### Why are projects on both Gitlab and Github?
We originally uploaded all of our stuff to Github (fortheusers), but recently moved primary development to Gitlab (4TU). We have continued to update Github as there is a larger user-base on Github and the overhead of also updating it is small. In general, if you make an issue somewhere we can handle it / get it to the right spot.

The move to Gitlab is motivated by a preference for Gitlab's open-source core platform when compared to Github. The article [Why not GitHub?](https://sanctum.geek.nz/why-not-github.html) touches on some things that we don't like about GitHub.

## Homebrew App Store
[Homebrew App Store](https://gitlab.com/4TU/hb-appstore) is a homebrew app that runs on Switch, Wii U, and PC. It is the frontend to the [libget](https://gitlab.com/4TU/libget) package manager, which itself was designed as a lightweight, scaleable way to install, organize, and upgrade files on the SD card.

There is a [web frontend](https://gitlab.com/4TU/hbas-frontend) located at [apps.fortheusers.org](https://apps.fortheusers.org), where files can be downloaded like they are on the console, for manual extraction

### Questions
#### How do I submit apps?
Apps can be submitted at [submit.fortheusers.org](https://submit.fortheusers.org). Thank you!

#### How does it work?
The design of how libget works is detailed [on this wiki page](https://github.com/fortheusers/libget/wiki/Overview-&-Glossary). At a high-level, the app launches and fetches a big json summary of every package on the server. It then asynchronously downloads icons for each app in the listing for the user to browse/choose. Any previously installed apps will have their version codes checked against the ones on the server to notify the user of an update or not.

When a package is installed, the files within that package are compared to the ones on the filesystem, and certain decisions for each file determine whether or not existing files will be overridden, deleted, or left alone. This is to allow for user configs to persist, and for old file paths to e cleaned up.

#### What are these `install.manifest` and `info.json` files?
These are files that are used internally by hb-appstore to track the version and contents of the package that you downloaded. When using the homebrew app you should never see these files. When using the web frontend, they happen to also be in the zip as of this time of writing.

If you downloaded from the web, you can completely ignore these files and don't have to extract them to your SD card.

If you're poking around your SD card and you find these files inside a folder named `appstore/.get`, these are important and used to track the state of the packages that you've installed. If you delete this directory all info about currently installed packages will be deleted.

#### Why aren't some of my non-hbas apps detected?
This is an ongoing issue that we have been slowly working on, but hasn't been a primary focus compared to other things. The short answer is that it's complicated due to the different places that homebrew can be installed and the different forms it appears in.

[The long answer is here](https://github.com/fortheusers/hb-appstore/issues/49) and [also here](https://gitlab.com/4TU/libget/-/issues/1). Currently, the problem  is analogous on a computer to: manually copying over a binary on linux, and it doesn't appear in your distro's package manager. But there are some approaches!

#### What apps are allowed on the store?
Our current qualifications are non-destructive apps that 1) serve a purpose, 2) have source code available and 3) aren't just clones without major features of other apps. In the past, we wanted to collect as many homebrew apps as possible, but as the store has grown, we have updated our definitions to be a bit more selective.

In general, you're a developer and your app is open-source it is likely to be approved. If it's popular enough to have been requested by other users it may have been added already without your explicit sign-off by virtue of the open-source license. We are doing this automatic-adding less however following developer feedback.

On Profanity/Nudity, currently we do not have any major restrictions on this, although down the road we are interested in adding some NSFW controls.

#### How do apps get on the store? What about updates?
Most apps are submitted. Other times a developer is contacted by us. On some occasions, we have taken the liberty of re-hosting apps on our own (given that we have the license to rehost them).

When a developer updates an app, and that app is updated on Github, we have our bot [Dragonite](http://gitlab.com/4tu/dragonite) alert us of the update and it should be expected to be seen on the store anywhere between a few hours to a few days. At the time of writing this process of approval happens in a maintainers backroom channel, but in the future we would like the metadata surrounding the contents of the store to be visible/shareable in a public git repo.

The tool [Spinarak](https://gitlab.com/4TU/spinarak) is under development to make this process easier / more transparent.

#### Why are all the download counts 0?
This has been a bug we've had for a few months that we need to get around to fixing. We have the stats still but our method to surface them broke as we scaled more and as of this time of writing we have not fixed it yet.

Sorry!

#### Is there a 3DS / Wii version?
We have a work-in-progress port to these consoles using SDL1. We are looking for repo maintainers and also still working on the ports. To see the progress, check hb-appstore's README.

### Troubleshooting
#### Generic crashing while using
Crashing can sometimes be caused by running out of memory. Although we've tried to address these issues, if present, they can usually be solved by running the app in Title-Override mode (Holding L+R while launching a title within AMS).

If you continue to have problems when the app launches, something may be corrupted within your config files. You can try to address this via Homebrew App Store's recovery mode. (Detailed below)

#### Entering Recovery Mode
Repeatedly pressing L and R while Homebrew App Store is launching from hbmenu will bring up the recovery menu. This is a text-only mode that doesn't use as many network calls, and also provides an option to reset configuration data in case some issues are being experienced with the regular GUI.

You can also try downloading an app from within recovery mode and seeing if that solves the problem, or if you're still experiencing it.

#### Says no Internet is present
You should try to perform a connection test in settings and see if you're able to get online. In general, if the console can connect and our servers are up, you shouldn't see any issues. You may want to check if our website at `apps.fortheusers.org` is reachable or not on a PC on the same network.

#### Downloading doesn't work
In some cases, when you go to download an app, rather than showing a progress bar it will just kick you back to the homescreen. This can either indicate an issue with writing to the SD card or that the network connection was lost. In a future build we will have a specific error message.

For the SD card, if on Wii U, you should ensure that the write lock isn't flipped. This is a physical switch located on the SD card.

#### I'm having some controller issues
These should be fixed in the latest hb-appstore. If you are still having issues with your controller input, please file an input against the hb-appstore repo!

## DNS Service
The [DNS service](http://dns.switchbru.com) is a custom DNS server that takes advantage of the Nintendo Switch [captive portal](https://en.wikipedia.org/wiki/Captive_portal) functionality. Nintendo uses this feature normally to allow the user to sign in / authenticate to hotposts such as on airplanes or in hotels.

### Questions
#### How does it work?
The captive portal logic has the Switch request the URL `ctest.cdn.nintendo.net` over the Internet. If it does not receive the expected result, it pops up a web browser pointing to that page. Our DNS server reports every domain->IP mapping correctly, except for the one that the Switch is requesting we redirect to ourselves, and then redirect out to our landing page.

The landing page itself is just a regular website with some workarounds in order to function on the Switch!

#### Can I self host?
You can use dnsmasq to host something similar yourself using [these instructions](https://gist.github.com/vgmoose/c26fade59f58dcebc2d9eac8a0c7a876). There is also a GUI friendly program called [YourFriendlyDNS](https://github.com/softwareengineer1/YourFriendlyDNS) that can help accomplish this.

#### Is this secure? Can you see what websites I'm looking at?
In general, you should not go trusting random DNS servers to not be snooping on your data. In our case, we are not inspecting the traffic that you generate. (But of course we'd say that!)

Fortunately, the Switch respects SSL certificates, so even if we were malicious and mitm-ing/removing SSL from pages, you are able to verify that we aren't by pressing Plus while the browser is open to view the page's URL and certificate. If the certificate is valid, all of the traffic/information on that page is encrypted between you and the target website, and even if we were trying something shady we wouldn't be able to see any data on the page (beyond the actual domain name itself).

We hope that our reputation hosting other services alongside our public statements / track record does give you peace of mind beyond checking the SSL certificate, but definitely understand this concern and if you find it unacceptable, self-hosting your own server may be a preferred option.

#### Why can't I play videos? No cookies? Where's XYZ Feature? Tabs?
Nintendo explicitly disabled video playback in the web authlet. This is ostensibly a security feature, however it's more of "security by obscurity" as there are other ways to access this type of content on other applets as of this time of writing.

If you'd like to see Nintendo release a real browser with more fleshed out features, let them know by [signing our petition](https://www.change.org/p/nintendo-nintendo-expose-the-fully-functional-internet-browser-built-into-the-switch)! We do not have control over any of the specific features of the browser, and are only able to display the hidden one Nintendo shipped with the OS.

#### Does it block updates?
Yes, our DNS server will block Nintendo Wii U and Switch update domains. However, it is not explicitly for this purpose!

### Troubleshooting
#### Not working!
If you enter the IP of 45.55.142.122 and no web browser pops up, it's possible that your custom DNS settings are being ignored by your router/ISP. DNS is inherently an insecure protocol (which allows us to override it in the first place), so your ISP/router has the ability to override our overriding. This is generally known as [DNS Hijacking](https://en.wikipedia.org/wiki/DNS_hijacking).

One quick workaround is to try a phone hotspot, another router, or access point.

If you'd like to confirm that it's your network and not your Switch, you can try to run the following terminal/cmd commands on a PC on the same network:

```
nslookup conntest.nintendowifi.net 45.55.142.122
```

If this returns anything other than 45.55.142.122, it implies that your network stack is overriding DNS packets somewhere and won't allow it to be overridden. Sometimes routers have this as a feature, and it can be disabled in the Admin panel of your router. In general though, if the computer doesn't resolve the DNS properly, and you don't have another hotspot, you're going to have to look at self-hosting if you want to use the browser.

#### Can't get rid of it!
If you [check your DNS settings](https://en-americas-support.nintendo.com/app/answers/detail/a_id/22411/~/how-to-manually-enter-dns-settings) and restore it to "Automatic", but the web browser keeps popping up, try some of the following things:

1. Explicitly setting the DNS server to 8.8.8.8 ([Google DNS](https://dns.google.com))
2. Rebooting your console
3. Trying another wifi hotspot, access point, or router

In general, this should never happen unless there's some funny-business going on within your network stack, and the DNS is being both poisoned and overridden. We have not seen this happen where steps 1 or 2 didn't resolve the problem, and if they don't please let us know.

If step 3 isn't feasible for you, and nothing else fixes the problem, you may unfortunately have to wait until your network stack (any one of the computers between you and your ISP) flushes out the bad data. This shouldn't be happening as our TTL is extremely short, but some DNS servers will incorrectly disregard this.

#### Forgot password
Please contact us at our discord server (see below) and we will send you a recovery email. At this time we do not have a place to request this online.

## Discord Info
Our [Discord server](https://discord.com/invite/z8wBTvU) is used primarily by developers to talk about Wii U / Switch homebrew, and also by users to talk about app store / DNS issues and feedback. For more general CFW / Homebrew support, we recommend going to a place like [Nintendo Homebrew](https://discord.com/invite/C29hYvh).
