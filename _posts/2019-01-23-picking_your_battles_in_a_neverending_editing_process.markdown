---
layout: post
title:      "Picking your battles in a neverending editing process"
date:       2019-01-23 08:42:40 +0000
permalink:  picking_your_battles_in_a_neverending_editing_process
---


While recently developing a fully functioning Rails application I found myself easily losing sight of what I was set on accomplishing. I'm certain that any developer has faced this feeling, web application or not, and it parallels any real life project. The sensation is as follows:

I can build something large, useful, and dynamic. I start developing the basics, in this case the User model and the landing page.

some background information that will be useful:
I know that I wanted my application to mirror the utility of helpx, a website that provides a marketplace for volunteers to meet volunteer hosts around the world. Where i see myself improving their formula is that with my application maybe volunteers can directly signup to volunteer for specific times, rather than everything being coordinated through email like it is on their website.

Great, I already have a place to finish and my important groundwork laid. Time to just create Post models for users to play with. I prefer the type of interface where you can immediately edit your profile and posts from show page rather than clicking a link to take you to an editing form. That takes some extra fidgeting to make things work right but they work okay. They are ugly, though, these show pages.

No problem, I'll just move onto creating an Appointment model so that users can sign up for appointments with other users. Without getting into the details, this takes a little bit of time but i'm fully comfortable implementing everything. Now the pages are starting to get proper ugly, and it's starting to get in the way of making sure I'm accomplishing my goals. Fine, I'll look into downloading some frameworks and getting error messages to render. And, you know, I prefer the type of interface where...

A pattern is starting to form: Each time you add something, it's not just making sure that ONE thing works. It becomes about shaping it to look and feel how you want, making sure it doesn't mess up anything you've done already, deciding the new element you've added makes you want to restart certain pieces, etc. The more you add on the more you are creating a new identity for your program and the more things you want to add and tweak that you've already made work! Aside from the Theseus ship guilt trip of "what kind of Frankenstein monster have I made?" and pastafication of your code, a strange phenomenon occurs.

You're constantly adding things, starting with the pieces you already know. They are less interesting and go faster... because you already know how to achieve it. Now you start fiddling with pieces that you don't know how to accomplish exactly. You've seen the functionality implemented before but you can't be certain how it was done nor how many people it took. You could do a hack solution to appease the immediacy of your needs, but then when you want to add the inevitable NEXT piece, you get into some trouble.

After doing this more than once you soon learn that you've gone down a dark path. Ultimately, a great one, because that's the starting sensation to endlessly refining and improving your products. However you need to finish making something before you can iterate on it, this whole problem is that you'll never get to a finishing point because you never were satisfied your initial goals.

It's not that there weren't initial goals, but as you started accomplishing them you inevitably found complexity and had to make some decisions along the way. That's all great, in fact it cannot be avoided. But to make sure that you don't get lost along the way you need to stick to ONLY accomplishing your initial goals. Once you've done so you can move onto the next level of functionality. Otherwise it's endless, your proverbial eyes see the whole galaxy when your stomach can fit... a few bites. Generously. 

The solution is nothing new, just an appreciation for what's already known. Test Driven Development is ugly, unfun, oldschool, unintuitive for my creative process, probably smells bad, has a poor taste in music, couldn't feel excitement if it was mid-bungee-jump, has a bowl-cut, speaks loudly in libraries. I may have missed a description or two, but you get the point of how horrendous it is. But it's the best way to stay on track and accomplish what you've set out to do. Unfortunately. Did I stress how poorly it smells? Rotten eggs envy the stench on this thing.
