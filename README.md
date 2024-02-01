# sustodon

I use Ivory as my daily driver mastodon client. It has lists (I think these are actually a first class feature of mastodon, but not entirely certain). It doesn't let me add someone to a list if I don't follow them. I moderate my followers as they come in and sometimes I get a new person who's obviously a person or just doesn't post much or whatever, and sometimes I get outright spam bots or people I don't want following me. But sometimes I get someone who rings some alarm bells but doesn't immediately merit blocking outright.

This is for those people. Those "sus" followers.

You could also read "sus" as like a shortlist for "sussing out" these new followers.

## feature ideas

at first it'll just be a list of people and it'll pull down their profile info and latest toots (maybe even a tui-ified version of their profile pic) and show a link I can open (or maybe it'll just open it for me if I do? this assumes you're running it on a desktop and .. macos :P, unless there's a cross platform library for opening a url from code (like on macos it uses `open`)

anywho something that would be cool is have it track changes to the profile:

- follower count
  - do I want it to track the followers? (who joined who left)
- following count
  - do I want it to track the followings? (who it followed who it stopped following (perhaps was blocked by))
- new profile pic
- changes to profile info
- post count
- new posts?
- should link to my mastodon account to keep track of notes I've placed (and maybe using the notes as storage for the metadata for change tracking?), assuming that's where ivory stores them and not on ivory sync method. If using ivory sync method, maybe tap into that some how, maybe even tap into that for metadata storage, but something tells me ivory doesn't really want that. I'll probably ask them.
- obviously since this is not going to be a thing that runs in the background and tracks, the over time stuff only is snapshotting whenever you do another load and sync, but that's fine, I suspect most of these accounts will be blocked or un-sused relatively quickly.
- one way to get around the "followers only" limitation is to briefly follow them, slurp the posts, and unfollow, but that will at the very least alert their server of the follow and unfollow, which leaks that you're sussing them


## limitations

- since you aren't actually *following* them using this, you won't see any followers only posts. However, accounts I know of that do primarily followers only posts are usually either up front about it on their profile, or their profile is fleshed out enough to lead me to believe they are legit based on that alone. Number and content of public posts isn't the only criteria I use after all.

## nice neighbor stuff

- try to hit the remote server with as few calls as possible.
- when checking the latest posts, only grab the first page, and if possible specify "first page up to X" where X is the latest post you already have cached, do that
- if enumerating followers, warn user if the follower list is more than a few pages long. Honestly, any account with tons of followers I'm probably going to allow and not "sus" to begin with, but y'know.

# anti goals

I don't want this to be a tool for silently following real accounts. This is just meant to look at new followers who maybe are not obviously legit, or obviously junk, and are a little sus. If you want to silently follow a real account, make an "anonymous" account somewhere and use a normal client. Like if you want to hate follow <some raging asshole> or something for your own self flagellation. This is also a better internet neighbor thing to do since you're leveraging proper federation protocols (meaning if you're using a large enough server for your alt account that server is probably already getting a copy of the post, it'll just also have your name on it) rather than scraping the other server's API. Or as @boogah suggested, use the rss interface to follow (though you then have the limitations of no-follower-only posts)

