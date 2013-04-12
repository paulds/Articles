# How To Contribute To Laravel 4

So a lot of people are submitting issues these days to [the Laravel 4 Framework repository](https://github.com/laravel/framework). Sometimes there's a pull request with code attached to fix a certain bug or to improve the framework by adding new functionality. I'll go over each step to submit a successful issue or pull request to the Laravel 4 repo and help you contribute to the framework.

Before we begin I really recommend your check out [this video](https://tutsplus.com/lesson/contributing-to-the-framework/) by **[Jeffrey Way](https://twitter.com/jeffrey_way)** which goes over the basic steps of submitting a pull request to Laravel 4. The video is less detailed than this post but it gives a good view on the basics.

## Make sure it's a framework bug

This is the first step and by far the most overlooked one. Some times, a bug you're experiencing isn't necessarily related to the framework itself. There could be a 3rd party plugin or package involved, some of your own code could trigger the issue, your web host could be the problem,... there are tons of reasons why the bug at hand could be triggered.

Often enough, the reason behind a bug is an update to one of these 3rd party plugins or packages and your code breaks because it's not compatible anymore. In a lot of cases, [people get issues from a composer update](https://github.com/laravel/framework/issues/598) because [they forgot to update their client side Laravel installation](https://github.com/laravel/framework/issues/708).

A good thing to keep your client side up to date is to clone it from Github and use the Laravel client side repo as an upstream branch instead of downloading it. If you have no idea what I mean by what I just said I suggest you read [this awesome post](http://niallobrien.me/2013/03/installing-and-updating-laravel-4/) from **[Niall O'Brien](https://twitter.com/niall_obrien)** about installing and updating Laravel 4.

Something that people often neglect to do is actually read the error message they get from a bug. Read the error message because the answer could be hidden in it.

Always do your research properly before rushing off to the issue button.

## Is the new feature actually necessary?

Something that I also see a lot is people trying to improve the framework in ways where it is not needed. Always think twice about the feature you're requesting or the improvement you're proposing. Perhaps a 3rd party package already solved an problem?

A framework shouldn't be able to do everything. It should be a basic layer on which you can build your own functionality or extend it with 3rd party libraries (packages). A framework should be fast and as easy to use as possible.

In the end, it's up to **[Taylor](https://twitter.com/taylorotwell)** to decide what’s best for Laravel and what functionality goes into the framework.

## Search the issue queue before posting

Always search [the issue queue on Github](https://github.com/laravel/framework/issues) before posting your issue. It could be that someone that someone already mentioned the issue. If so, help them prove their statement by verifying that you're experiencing the same problem.

When you're submitting a proposal for a feature, make sure that nobody asked for the feature before you and got it rejected. People always get annoyed if their suggestion stumbles on a simple no or is just plainly closed but it could be that it has been suggested a few times before and that you just should have done your research.

Should you still be convinced that the improvement would make a valid addition to the framework, then make sure you state your case better than the ones before you and try to say as best you could why the improvement is (still) needed, preferably with a few use cases. It’s also a good idea to have these discussions in [the Laravel forum](http://forums.laravel.io/viewforum.php?id=13) first before opening a new issue.

## Preparing your issue

When you're writing your issue title and description try to be as thorough as possible. Always try to sum up your issue description in a descriptive title of less than 50 characters. People should be able to figure out more or less what your issue is about by glimpsing your title quickly.

For bug reports, please provide as many code as possible. Give some OS specs, which php version you're using, which database system you're using, etc... Try to cover your code step by step and post the issue stack from an error page if you're getting one. Often enough, the issue can be derived from the issue stack on the error page so try reading it before posting an issue. You can also use [paste.laravel.com](http://paste.laravel.com) to post all of your code if you feel that the code blocks in the issue description are getting too long.

If you feel that you found a way to solve a bug then you can do two things. If it's a minor one-line documentation edit you can just use Github to edit the file and submit the PR like that. Otherwise you'll need to fork the repo and make a separate bug-fix branch. We'll go over that in a minute.

When you want to have a new feature in Laravel you can take 2 paths: propose a feature or request a feature.

If you're proposing a feature you mean to actually implement it yourself. You should create a Github issue with [Proposal] in the title. Try to be as descriptive as possible on what you're trying to improve, how it will help users (use cases!) and how you plan to implement it into the framework. If your proposal gets approved by Taylor, you can go ahead and create an implementation and submit a Pull Request. Don't forget that it's alway possible that Taylor will go ahead and implement it himself if he feels he already found a (better) way to do so. Don't let it discourage you though! You just proposed a valid feature for Laravel 4 and should be proud on that :)

Else if you're just requesting a feature but don't plan on implementing it yourself you should create an issue with [Request] in the title. Again, like a proposal, try to tell how it would improve the framework and provide some use cases.

If you just wanted to file a bug report or request a feature you're done now! If your proposed feature got approved or want to fix a large bug, read on!

## Forking the repository and setting up your development repo

The next step should be forking the repository to your personal Github account. Just click the button on the right about that says "fork" and choose one of your Github accounts/organisations to fork the repo to.

When it's done forking the repo, clone the repository to your local development machine.

	$ git clone <github url to your cloned repo> <directory>

Next, let's create a separate branch to work on. If it's a bug fix, prefix it to `bugfix/`. If it's a proposed feature, prefix it to `feature/`.

	$ git checkout -b prefix/short-descriptive-title
	
When your branch is set up, let's run a composer update to install the required packages for the framework.

	$ composer update --dev

Notice that I'm adding `—dev`. This is necessary to pull in packages that are required for development (like Mockery for unit testing).

We’re now all set to begin our work.

## Implementing the bug-fix or feature

Now that we've got a separate branch set up let's start writing our bug-fix or feature.

Before you commit anything you should try to run PHPunit to make sure the unit tests written for the framework aren't failing. It makes sure you don't break any previous implementations. You can run PHPunit from the root of the framework to run the unit tests. Now there's a slight problem for small memory machines. There are a lot of unit tests written for Laravel 4 and it takes some time before they all get processed. I've seen unit tests for Laravel 4 take up until 15 minutes on a Travis build. You might get some memory alloc failures when trying to run your unit tests. Don't worry, I'm gonna show you a neat trick in the next step so you can still run your unit tests without having to worry about installing PHPunit or running it on your dev machine.

If you're implementing a feature or fixing a bug never forget to check if it affects changes to the client side as well. If it does, try to reference the pull request that goes alongside in the [laravel/laravel](https://github.com/laravel/laravel/tree/develop) repo on Github in your pull request on [laravel/framework](https://github.com/laravel/framework).

When you're done with implementing, commit your changes (or commit it in pieces if it's a rather large feature). Before you commit your changes, make sure your code is coded according to [the Laravel coding standards](http://four.laravel.com/docs/contributing#coding-guidelines). Also, if you're fixing an issue which is in the Github issue queue, reference it in the commit title by saying: `Fixes #XX` (with `#XX` being changed to the actual issue number, of course). This will make sure the issue gets automatically closed when your pull request gets accepted.

Didn't forget your unit tests? Good! Let's proceed.

## Setting up Travis-ci with your forked repo

This is something I don't think much people know that they can do before submitting their Pull Request. [Travis-ci](https://travis-ci.org) is a free service which runs a `.travis.yml` file in your project and basically runs all your unit tests. It sends you an e-mail notification on wether your builds have failed, passed or didn't finish for some reason. This means there's a better chance at catching bugs before the pull request will be made. You don't have to do a thing but push to your forked repo and Travis will automatically start a new build. Just wait for the e-mail notification or check on [travis-ci.org](https://travis-ci.org) if your build has finished to know if your unit tests failed or succeeded.

Now how do you set it up with your forked repo? It's pretty easy actually. Go to [travis-ci.org/profile](https://travis-ci.org/profile), set Travis to "ON" for your forked repo and click on the wrench icon next to it. Travis will automatically set up a service hook in your Github repo's settings. Whenever you push to Github or publish a branch, Travis will start a new build and send you and an e-mail notification when it’s finished. 

Should your build fail you can do a couple of things. You could try to fix your code, commit again and push to your Pull Request branch again and start a new build but I prefer to do  it a little different. I'll just delete the Pull Request branch on Github, roll back some of my commits on my local development repo and commit again with the fixed code to keep the commits minimal and the Pull Request as small as possible. I suggest you do the same to prevent the Pull Request from growing so large with commits which are just attempts at fixing the unit tests.

## Submitting the Pull Request

So you've written your code, run your unit tests and you're good to go to submit your pull request. Proceed to your forked repo on Github, select the branch you've worked on and hit the button "Pull Request". Set a descriptive title (optionally with `Fixes #XX` again), create a description which details the bug you’re fixing or the feature you're implementing and go ahead and submit your Pull Request.

## Update your Pull Request (optionally)

During the time that you submit your PR and it gets accepted (or closed), Taylor (or others) can suggest further improvements for the PR. If so, you should try to write some new code, commit it again and push to the branch you've created the PR from. The PR will automatically be updated with the latest changes. You might have to do this a couple of times before the PR gets accepted.

## Cleaning up

You're all done and your Pull Request was finally accepted and merged into the master branch. Congratulations, you've now successfully contributed to the Laravel 4 framework!

You can now go to your local repo and do the following. First, add the Laravel Github repo as a remote:

	$ git remote add upstream https://github.com/laravel/framework.git

Next, checkout to the master branch, pull from the latest changes into your own master branch and update your forked repo on Github by pushing to the master branch.

	$ git checkout master
	$ git pull upstream master
	$ git push origin master

We won't be needing the branch anymore on which we created the feature or fixed the bug so let's delete them on the forked repo and locally.

	$ git push origin :prefix/short-descriptive-title
	$ git branch -d prefix/short-descriptive-title

Now we're all set. Next time you need to create a new feature, pull the latest changes in from the Laravel repo master branch and only then create your feature branch. This makes sure you have the latest changes when you start building your pull request.

Should your PR get closed rather than accepted, don't think of it as a negative point. See if Taylor provided a reason, learn from what you did wrong and next time you might be able to submit a better one. Everyone who wants to become better at submitting Pull Requests goes through this. You can only learn from these experiences and improve yourself as a developer. And the next time you submit a PR you'll be that much wiser from your last experience.

## Thanks for reading

Thank you for reading through this insanely long post!

I hope I helped you by providing the steps of successfully submitting a PR to Laravel 4 and by providing a few tips in the process. If you have any further questions or remarks feel free to contact me on twitter: [@driesvints](https://twitter.com/driesvints).

I also keep a blog post series here on [this website](http://driesvints.com) which is weekly updated with all the latest changes and resources for the Laravel 4 framework. Feel free to check it out!
