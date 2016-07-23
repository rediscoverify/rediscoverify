# Rediscoverify

Rediscoverify is a Spotify-connected Web App for rediscovering your music library.

All you have to do is point rediscoverify to one of your playlists and rediscoverify will find similar artists in your library and build a playlist.

Similar to what [Guadayeque](http://guayadeque.org/) and my [Banshee Extension](http://banshee.fm/download/extensions/) did, but only with the music saved in your Spotify account.

## Modes

### One-Time Shuffle

In _One-Time-Shuffle_ Mode, rediscoverify retrieves the artists in your playlist and their similar artists (depth should be configurable), assigns all artists their maximum weight, combines (union) them with the artists in your library and then shuffles _n_ times to retrieve a random song from one of these artists.

This mode is perfect if you want a playlist that will stick to the artists you have in the source playlist.

### Iterative Shuffle

In _Iterative Shuffle_ Mode, Rediscoverify will reweight every artist it picked from your playlist so the playlist will eventually derail into a playlist built around the "path" that was chosen at random.

## Internals

### Weighting & Deduplication

Initial weights for the artists given in the playlist could be `m/n`, where `m` is the number of tracks by that artist in the playlist and `n` is the number of distinct artists in the playlist.

An easier approach would be _depth-weighting_, where rediscoverify assigns a weight of `1/d` to an artist, where `d` is the depth into the tree of similar artists.

Deduplication has to happen pretty early in order to avoid circular references. Thus, similar artists are resolved breadth-first and artists in lower nodes will be skipped if they've already been processed previously.

### One-Time Shuffle

The algorithm will resolve similar artists using Spotify and in turn will resolve similar artists to those up until a depth to be specified (d=2 should be fine for now).

The weights will be normalized to `sum(weights) == 1` and then a random number `[0; 1]` will be picked `n` times, where `n` is the number of desired tracks in the new playlist.

### Iterative Shuffle

The algorithm will resolve at most one depth of similar artists at the time. After normalization, the algorithms picks one artist with one song at random, then goes ahead, assigns this artist a new top-level weight and will restart the algorithm until `n` tracks are resolved.
