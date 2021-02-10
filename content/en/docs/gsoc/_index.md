---
title: Google Summer of Code 2021
linkTitle: "Navidrome GSoC 2021"
weight: 9
description: >
  Navidrome GSoC 2021 information
---

Introduction
------------

Navidrome started in Feburary 2016 as an modern and lightweight alternative to [Subsonic](http://subsonic.org):
written in [Go]( https://golang.org/ )/[React](https://reactjs.org/), implementing the [subsonic API]( http://www.subsonic.org/pages/api.jsp ) and thus compatible with all the [subsonic clients]( http://www.subsonic.org/pages/apps.jsp ) in the world, licensed under GPL3, … Being relatively young, it does come/use modern development practices like continuous integration, a comprehensive testsuite, a relatively clean codebase, automatic dependency upgrades, automatic linting/CI/static analysis/… on each pull-request, [comprehensive documentation]( https://www.navidrome.org/docs/ ) … It recently gained popularity due to the decay of [Subsonic](http://subsonic.org)/[Airsonic](http://airsonic.org), and currently has more than 4M download of its [docker image]( https://hub.docker.com/r/deluan/navidrome ), and had its binaries downloaded more than 10k times.

<p align="left">
<img width="600" src="/screenshots/gsoc-2021/ss-desktop-player.png">
</p>

A demo version is available as well: https://demo.navidrome.org

Mentors
-------

Feel free to reach out to any of them:

- Deluan Quintão ([ETZ](https://en.wikipedia.org/wiki/Eastern_Time_Zone)): deluan -- [@deluan](https://twitter.com/deluan)
- Julien Voisin ([CET](https://en.wikipedia.org/wiki/Central_European_Time)): jvoisin -- [@dustriorg](https://twitter.com/dustriorg)


Development methodology
-----------------------

The main repository is hosted on [Github](https://github.com/deluan/navidrome), which is also used for tracking bugs and running the continuous integration. The main communication medium is [Discord]( https://discord.gg/xh7j7yF ), along with [Twitter]( https://twitter.com/navidrome ) for announcements, and [Reddit](https://www.reddit.com/r/navidrome/) as general purpose forum.
The usual way to get code in is to submit a pull-request, which will be reviewed by the community and merged. Adding some tests might of course speed up this process.


Instructions for students
-------------------------
Students willing to take part of the Google Summer of Code 2021 with navidrome should send a couple of pull-requests, to demonstrate that they're both motivated and capable of writing code and contributing to the project.


Tech stack
----------
- Server:
    -  [Go](https://golang.org)
    -  [SQLite3](https://www.sqlite.org/)
- Frontend (WebUI)
    -  [React.JS](https://reactjs.org/)
    -  [React Admin](https://marmelab.com/react-admin/)
    -  [Meterial-UI](https://material-ui.com/)


Recommended steps
-----------------
1. Read [Google's instructions for participating]( https://google.github.io/gsocguides/student/ )
2. Grab any project from list of ideas that you're interested in (or even suggest your own!).
3. Write a first draft proposal and ask one of the mentors to review it with you.
4. Submit it using Google's web interface.


Student proposal guidelines
---------------------------
- Keep it simple enough to fit in no more than a couple of pages. Try to be clear and concise in your writing.
- Try to split GSoC period into tasks, and each task into subtasks. It helps us to understand how you plan to accomplish your goals, but more importantly, it'll help you to understand the task deep enough before starting, and prioritize important things to do first.
- Please, note, how much time a day/week you are able to spend on this project. We do expect something between 30h and 40h.
- Submit your proposal early, not at the last minute!
- Feel free to choose a “backup” idea (the second task you want to do), so that conflicts (two students for one task) can be resolved.


Ideas
-----

### Media sharing

One of the nice features of Subsonic is its [ability to generate a sharing link](http://www.subsonic.org/pages/features.jsp) for a track/album/artist/playlist to send to friends, so that they can listen/download the music without having an account on your instance. This is a nice replacement to alternative to youtube links to share music.
A nice way to implement this would be to have a table of shares, with a shorturl as ID. The table would store a reference to what is being shared.  This shorturl would be used by a public endpoint.
We would also need a standalone player similar to what is provided by Spotify when you share music through their service. Ex:

<p align="left">
<img width="600" src="/screenshots/gsoc-2021/spotify-share.png">
</p>

#### Steps

- Add a table for shares
- Add a way to create shares in the UI
- Implement the Subsonic API related endpoints: [getShares](http://subsonic.org/pages/api.jsp#getShares), [createShare](http://subsonic.org/pages/api.jsp#createShare), [updateShare](http://subsonic.org/pages/api.jsp#updateShare) and [deleteShare](http://subsonic.org/pages/api.jsp#deleteShare)
- Add a standalone player (could be based on our current React Player)

Skill level: Medium
Required abilities: Go and willing to learn a bit of React
Expected outcome: Ability to share music with friends.

#### Links and further reading

- https://github.com/deluan/navidrome/issues/748


### Jukebox mode

Some servers can be run in ["jukebox"]( http://www.subsonic.org/pages/features.jsp ) mode where the music is played directly on the server's audio hardware, ex: mpd and Subsonic. A tricky part of this task might be to properly expose the "jukebox client" in the WebUI interface, as the current react-music-player used by Navidrome would have to somehow control the jukebox (via API) instead of the browser's Audio component.

#### Steps

- Implementing a minimal subsonic client in go to connect to the server
- Implementing an audio output for the subsonic client
- Implementing the frontend part to select the jukebox mode and control the subsonic client
- Implementing the Subsonic API's `jukeboxControl` endpoint

Skill level: Hard
Abilities: Go and React, a bit of UX would be nice
Expected outcome: Ability to play music from the device running navidrome.

#### Links and further reading

- https://github.com/deluan/navidrome/issues/364
- https://airsonic.github.io/docs/jukebox/
- http://subsonic.org/pages/api.jsp#jukeboxControl


### Google home/alexa integration

Nowadays, tech-oriented people tend to have a home assistant, and thus might want to be able to use it to control their subsonic instance. Since there is already the subsonic API to perform actions, this task on "only" a matter of writing the glue between Alexa/Google home and the API. Some *actions* might require a bit more than glue, for example, to play specific tracks/albums.

This task can be nicely paired with the jukebox one.

#### Steps

- Implementing the glue between Alexa/Google home and the Subsonic API
- Implementing the frontend part to configure this machinerie

Skill level: Hard
Required abilities: Go, having an Alexa/Google Home is a plus, but worse case we can send the student a device.
Expected outcome: Ability to play/pause/next/previous the music via a home assistant

#### Links and further reading

- https://github.com/deluan/navidrome/issues/682
- https://developers.google.com/assistant/
- https://developer.amazon.com/en-US/alexa/alexa-skills-kit


### Multiple libraries support

Some users want to use multiple libraries at the same time, for example to separate lossy/lossless albums, one for official albums and an other for bootlegs/lives, or one ofr audiobooks, some are even dreaming about having remote ones to listen to their friend's music without leaving their navidrome instance!

#### Steps

- Implement support for multiple libraries
- Implement the UI allowing users to switch between libraries
- Implement permissions: Which user has access to which library
- Implement the `musicFolderId` attribute in most Subsonic API endpoints
- Plus: Implement support to access remote libraries from the WebUI

Skill level: Hard
Required abilities: Go and SQL, and a teensy bit of react for the UX
Expected outcome: Ability to use multiple libraries withint a single user account

#### Links and further reading

- https://github.com/deluan/navidrome/issues/192
- http://subsonic.org/pages/api.jsp#getMusicFolders

### Omnisearch

One search bar to search across the whole library, using proper [SQLite's Full Text Search]( https://www.sqlite.org/fts5.html ), instead of having one separate search field per domain (artist, album, …)

#### Steps

- Replace current search implementation on the server with a new one using SQLite3's FTS5
- Implement a search bar in the WebUI on the NavBar
- Implement a Search Results page, with links to artists, albums, songs and playlists
- Plus: integrate FTS5 with Spellfix1, to enable search for close matches. May not be supported by `go-sqlite3` library used by Navidrome

Skill level: Medium
Required abilities: Go and React.JS
Expected outcome: Ability to have a single search field operating accross all the library

#### Links and further reading

- https://github.com/deluan/navidrome/issues/255
- https://github.com/deluan/navidrome/issues/468
- https://www.sqlite.org/fts5.html
- https://www.sqlite.org/spellfix1.html#overview

### Infinite Scroll

Currently, navidrome is using pagination instead of providing a more convenient infinite-scroll. The implementation isn't trivial because navidrome is using [react-admin](https://marmelab.com/react-admin/), which not only doesn't provide this feature out of the box, but make it non-trivial to implement.

#### Steps

- Implement a new List component for React-Admin, that does not use pagination. It should load new data on demand. This component should be usable in all places where we currently use React-Admin's List

Skill level: Medium
Required abilities: React.JS, with a bit of Go and SQL
Expected outcome: Infinite scrolling is implemented and usable.

#### Links and further reading

- https://github.com/deluan/navidrome/issues/132
- https://marmelab.com/blog/2019/01/17/react-timeline.html
- https://marmelab.com/react-admin/List.html#uselistcontroller


### Lyrics support

It would be nice for navidrome to support [LRC files]( https://en.wikipedia.org/wiki/LRC_(file_format) ) to display lyrics. A possible stretch goal would be to implement lyrics fetching.

#### Steps

- Implement lyrics importing (from tags or external .lrc files)
- Make navidrome library aware of the presence of lyrics
- Implement Subsonic API's `getLyrics` endpoint
- In the WebUI, when lyrics are available for the current song being played, set the appropriate attributes of the Reac Music Player used

Skill level: Easy
Required abilities: Go and React.JS
Expected outcome: Ability to see lyrics in the WebUI or Subsonic client when playing a song

#### Links and further reading

- https://github.com/deluan/navidrome/issues/249
- http://subsonic.org/pages/api.jsp#getLyrics
- https://github.com/lijinke666/react-music-player


### Volume normalization

It would be nice if navidrome could perform audio normalization, to avoid having to fiddle with the volume when listening to different trackes of various volumes.

#### Steps

- Expose a preference to the user
- Implement per-track normalization
- Implement per-album normalization

Skill level: Easy
Required abilities: Go and React.JS
Expected outcome: Ability to have constant volume output in navidrome

#### Links and further reading

- https://github.com/deluan/navidrome/issues/233
- https://en.wikipedia.org/wiki/Audio_normalization
- https://trac.ffmpeg.org/wiki/AudioVolume


### New Album grid

It would be nice to have something ressembling [Plex](https://www.plex.tv/)'s interface, with covert art fading in, as well as a *slider* to adjust their size.

#### Steps

- Implement the slider for the covers
- Implement asynchonous loading for the covers
- Implement the fading in upon loading

Skill level: Medium
Required abilities: React.JS / Material-UI
Expected outcome: Ability to have constant volume output in navidrome

#### Links and further reading

- https://github.com/deluan/navidrome/issues/323
- https://www.plex.tv/


Links and resources
-------------------

- [GSoC 2021 timeline]( https://developers.google.com/open-source/gsoc/timeline )
- [GSoC FAQ]( https://developers.google.com/open-source/gsoc/faq )
- [GSoC student guide]( https://google.github.io/gsocguides/student/ )