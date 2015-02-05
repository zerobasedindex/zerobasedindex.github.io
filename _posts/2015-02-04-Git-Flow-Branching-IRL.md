---
layout: post
title: Git Flow Branching IRL
---

## Setting the Scene

I've been using git for about 2 years now and it's by far the best version control system I've used. I was taught CVS at school and then eventually picked up SVN at my first job. In the beginning, I was hesitant to really start using it since I thought SVN was good enough, not realizing how much better git suited my needs.

As with all tools, they are only as good as those wielding them. My first team development work using git was less than optimal. We had multiple projects inside a single repo all on the same branch! (cheap boss saving money with GitHub) So if anyone changed anything between your pull and push, git would get unhappy, it happened a lot.

When we did setup repos appropriately (loosely defined as one project per repo) we didn't really do all things we should. Our branching strategy was developer ad hoc, everyone did whatever they liked as long as it eventually ended up back in master. This made things unnecessarily complicated and prone to breaking.

After about year learning the git ropes, I got the chance to help establish software engineering practices for a new team. This led to some searching, and how I found out about Git Flow.

Git Flow was originally presented by Vincent Driessen in his [blog](http://nvie.com/posts/a-successful-git-branching-model/). Go read that if you haven't, he does a great job explaining it and drew some really pretty pictures. If you'd rather read my summary, have at it a few sections [below](#gitflowsummary).

## A year with Git Flow

### What I Like

1. It's pretty easy to pickup on your own, and really easy to teach other engineers as they come onto an existing project.
1. The built-in saving of your project state is really valuable. I don't have to worry about the state of the repo when trying to recreate demos or fix bugs after I've started working on the next set of features.
1. It works great solo or within a team environment. It's my go to for any project that I have control over. I'd use it with this blog (and still may) depending on how I want to play with GitHub Pages going forward.
1. The strategy gives you structure and helps prevent errors but still allows you to respond quickly to production errors via hotfix branches, combined with the 'saved state' of production, you don't have to worry about new/untested code creeping in.
1. Amenable to CI in creating both development and release builds.
1. A lot of people have embraced it and are using it, thus giving us a 'pattern' to share when talking with others.
1. Helps isolate rogue/ignorant developers that may be only marginally playing by the rules. As long as they stay on develop you can mitigate them.
1. Plays to git strengths, branches are cheap, use them to make your life better.

### What I Don't Like or Haven't Figured Out

1. I haven't figured out a good way to include a code review step outside using a commit purgatory like that provided by Gerrit or other review tools. May not be possible given the nature of some code review ideals (don't commit until reviewed), or just may need more branches.
1. Integration with QA from a day-to-day perspective was difficult to decide on how best to integrate. Do we give them nightly development branches or create ephemeral QA nightlies?
1. Tough to integrate with tools like Gerrit and repo, when working across multiple repositories at once (search for building the entire Android OS for what I'm talking about).
1. Can lead to a lot of merge commits in your git history if you aren't mindful, and some or inevitable.

## What is Git Flow<a name="gitflowsummary"></a>

Git Flow is a branching strategy that leverages two everlasting branches, a master/production branch and a development branch, that are supplemented with various ephemeral branches (e.g., release, feature, hotfix).

Essentially, all of your current work happens on the development branch. You can have feature branches off development for long running additions that may span multiple deployments that can be easily rebased and merged back when ready. When it's time to freeze your code and push to production, create a release branch off development. From now on, all bug fixes/tweaks/etc that are targeted for the release happen on the release branch, no new features should be making their way into the code base via a release branch, just fixes. 

Creating the release branch frees the development branch to go forward, worry free, as work starts on the next set of features for the next deployment. But what about those fixes in the release branch? Well, you can merge them in at the end of the release or piecemeal as things go along depending on their severity. This is a one way road though, release can merge into develop but not the other way.

Once the release branch is fully-tested and ready to rock, you can merge that into the master/production branch, and be deployed. The release branch is also merged into develop (to keep all those fixes from QA testing) and then deleted. Additionally, it's good practice to tag the commit on master with the version information and other relevant details.

So what happens when a bug sneaks pass your kick-ass QA team and makes it into production? Well, you don't have to fret at all, as you tagged master with the last release and all the work you've done since happened in develop. So we can create a clean hotfix branch off master (the only time it's allowed to branch off master) and fix the problem. Once it's tested, merge the hotfix branch into your development (again, to keep it for the next release) and master branches, tag master with an updated version number, and then delete the hotfix branch. Do what ya gotta do to turn master into production (hopefully through some CI) and profit!

That's pretty much it, Git Flow also has good tool support either through [scripts and git-hooks written by the man himself](https://github.com/nvie/gitflow) or [SourceTree](http://www.sourcetreeapp.com/).
