---
layout: post
title: Look Mum, I Hacked the Hacker at J-Fall 2021
---

Due to COVID-19 there were hardly any in-person events in 2021,
but luckily [NLJUG](https://nljug.org)'s [J-Fall](https://jfall.nl) conference
— the biggest Java conference in the Netherlands —
actually happened.

I was in the audience for a Java security talk by [Brian Vermeer](https://brianvermeer.nl) ([NLJUG](https://nljug.org) board member, [Java Champion](https://apex.oracle.com/champions), [Snyk](https://snyk.io) developer advocate, [Foojay](https://foojay.io) community manager),
when during a live demo I saw his environment variables getting printed on the console on the venue's enormous cinema screen.
And among them was a GitHub token.
I poked my colleagues sitting next to me and said: "I know this is a demo, but could that be a real token?"

I had a laptop with me, and decided to check it out.
The talk was being recorded and broadcast live via the internet,
so I could just grab the token by rewinding the live video feed a bit.
I logged into GitHub and replaced the token in my GitHub cookie with the one that was just broadcast live,
and sure enough: I was now Brian Vermeer on GitHub.
Two-factor authentication didn't save him, with a valid token you're already past the authentication stage.

Brian was just explaining about [deserialization gadget chains](https://snyk.io/blog/serialization-and-deserialization-in-java/),
so I decided to make a [small change](https://github.com/bmvermeer/brianvermeer.nl/commit/bd118c991ddb63b0a7bd788f6b7b926933d411ec) to the repository for his personal website,
pretending to be [Inspector Gadget](https://en.wikipedia.org/wiki/Inspector_Gadget).
And surely enough Brian had made sure [his website](https://brianvermeer.nl) automatically gets updated whenever changes are made in the Git repository.

<img src="/images/brianvermeer.nl-hacked-on-j-fall-2021.jpg" width="400" alt="BrianVermeer.nl hacked on J-Fall 2021" />

I informed Brian of his mistake right after his talk.
He was a good sport about it and proceeded to invalidate all tokens that had been exposed.
He also decided to not rewrite his website's Git history when restoring his website, so he left [Inspector Gadget's commit](https://github.com/bmvermeer/brianvermeer.nl/commit/bd118c991ddb63b0a7bd788f6b7b926933d411ec) in there.
He took the opportunity to write about this incident for [his 2022 new years resolution on the Snyk blog](https://snyk.io/blog/dont-show-security-tokens-on-stage/).

Happy new year, and don't forget to not expose your tokens!

<img src="/images/brian-vermeer-and-nils-at-j-fall-2021.jpg" width="800" alt="Brian Vermeer and Nils at J-Fall 2021" />