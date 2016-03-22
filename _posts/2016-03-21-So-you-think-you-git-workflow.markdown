---
title: So you think you git workflow
layout: post
---
### What's so hard about git?
In Module 1, I thought I knew things about git. I saw this map [(source)](http://www.mnu.edu/business/software-skills-demand.html)

<img class= "image" src="/images/skills_map.png">
and I was seriously confused. What could possibly be difficult about git? And then we went into a series of team projects, and there is so much more that can go wrong when multiple people are trying to muck up master.

In life, I believe that many misunderstandings arise due to people making different assumptions, acting accordingly, and not recognizing someone else made different assumptions. So for our [lucky shop](https://polar-reef-22111.herokuapp.com/)([source](https://github.com/ksk5280/lucky-charms)), we came up with a multi-step workflow to ensure that we were on the same page when requesting code be merged to master.

### The workflow
This workflow was designed for building a Rails app in a small team. The basic understanding outside of the workflow was that:

* anything on the master branch could be deployed at any time
* the test suite on the master branch should pass
* no one should be committing directly to master
* no one could merge their own code onto the master branch

(I look back in horror at all the git violations that I committed.) The setup for this workflow was that the project was being managed through [waffle](https://waffle.io/) and was being style checked with [hound](https://houndci.com) (woof!). Whew... onto the workflow!

0. Load up the repo in waffle.
1. Choose a card from the backlog in waffle. If we're working separately, it's best to move that card that you've chosen into ready and perhaps assign it to yourself as well.
2. Checkout the master branch: `git checkout master`
3. Make sure you have the lastest master: `git pull origin master`
4. Run the test suite: `rspec`
5. Checkout a new branch and tag it with #issue_number: `git checkout -b new-branch-name-#issue_number`
6. Write the feature test associated with your waffle card.
7. Run rspec, and make sure that there are no errors that blow up the stack (missing ends, forgetting capitalization, etc.)
8. Commit your feature test
9. Push your branch up to github, create a pull request, and tag this with [WIP]
10. Start implementing the features
11. When you commit, remember to push up to remote, and wait for hound to respond
12. If there is an issue or question, add comments and reference other team members on your pull request. Wait for aid. Remember to ask for help on the slack channel as well.
13. Correct the hound issues you have, go to step 10.
14. When your test suite passes, commit and push up to GitHub. Wait for those hound comments to come back in.
15. Correct the style issues pointed out by hound. Push up to Github. Repeat until hound is dealt with.
16. Search the project for binding.pry and save_and_open_pages (or other debugger statements) leftover. Take those remnants out of the code.
17. Run `rails s` and see if everything looks and behaves like you want it to. Fix the unexpected issues and commit. Push up to Github and deal with any hound comments that may arise.
18. If there are really obvious sad paths for your feature test, you should write that test and return to Step 10.
19. Rebase and squash the commits that you do not want record for posterity.
20. Check if your branch comes from the latest master, and if not pull master into your branch. You may have to deal with merge conflicts.
21. Run rspec one more time. If tests are failing, due to the merge conflicts, fix the tests. Push up to github.
22. Remove [WIP] from your pull request. Request a code review and a merge to master through tagging in the PR and messaging in slack.
23. If there are changes requested from your code reviewer, make the changes and respond in the PR, or respond to comments made by your code reviewer.
24. After code is merged to master, remember to push to heroku with `git push heroku master` and `heroku run rake db:migrate`. Check if the app in production is behaving as it should.

### Do we really have to do all this?
Do you really have to do anything? No, but agreeing to a detailed workflow allows your team to be on the same page. The steps that tend to get overlooked are 17, 21, and 22. The last two steps are essential when working under the assumptions, as discussed before, that:

* anything on the master branch could be deployed at any time
* the test suite on the master branch should pass

Continuous integration would confirm that the test suite passes prior to a merge to master, and I will be looking at using [TravisCI](https://travis-ci.org/) in future projects. Until then, my mantra is: follow the workflow!
