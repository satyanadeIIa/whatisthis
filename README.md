# What am I looking at here?

Homograph attacks are a class of attacks in which an attacker changes characters in a resource name or other piece of data to characters that look identical in the given font. The creator of this repository isn't `satyanadella`, it's `satyanadeIIa` (with capital i characters instead of lower case L characters).

# So the CEO of Microsoft didn't grow a bad MS Paint goatee?

Not that I'm aware of, though I think it's a rather dashing look for him.

# How can we prevent Homograph attacks?

Well GitHub has taken an important first step: they've disallowed Unicode in user names. Unicode has a huge number of visual collisions that make it a great resource for attackers creating homographs. Unfortunately, ASCII still has homographic collisions (as you can see from this user name), and also users may legitimately want Unicode in their names. There are a few ways to solve this problem. One is to reencode the data in cases where security constraints might be violated if people get confused. This is how modern browsers deal with Unicode in Internationalized Domain Names, via something called [Punycode](https://en.wikipedia.org/wiki/Punycode).  When there are non-ASCII characters in a domain name, modern browsers display the URL in Punycode, which largely defeats Homograph attacks. (It at least means attackers have to craft a URL such that the Punycode result ALSO has a Homograph collision, and that's extremely difficult or impossible in most cases.)

Other approachs include maintaining a list of confusable characters and checking against it at runtime to see if a newly registered account, URL, etc. would cause a collision. This is extremely error prone and expensive however.

Another option is the one that a very smart, incredibly handsome, and positively dashing hacker talked about in [his talk from DefCon 26](https://www.youtube.com/watch?v=Ec1OOiG4RMA). Since attackers trying to make their homographs look as close to the real data as possible, you can use [Optical Character Recognition](https://en.wikipedia.org/wiki/Optical_character_recognition) to turn the homographed payload back into regular ASCII. This works best against Unicode Homographs, but may also be successful against purely ASCII ones as well.

# Wow, this sounds like a hard problem

It is, and so GitHub really shouldn't be blamed for this. It's not a GitHub problem, it's a font and human vision problem. Unfortunately, I'm not currently aware of any way to patch human vision to tell the difference between l, 1, I, and | in every conceivable font.

But if you let users register accounts, and you have particularly important public figures using your service, you might want to give some thought to reserving, typo-squatting, or otherwise preventing visually similar account names from being registered.
