# Lightning talks

## guardsjs.com

Will do validation guards in your forms using js

`gem install guardsjs-rails`


## hiring apprentices

devmynd out of chicago

* application review
  * essays and all sorts of stuff
* code challenge
* phone screen
* come for a couple of visits to pair
* go for beers to see about cultural fit
* not interns - pay them
* pairing - 2 brains/1 computer
* all apprentices get a mentor assigned to them
* rotate the mentors
* regular check-ins for feedback
* job of mentors is to instill values
* have them teach other people and present to team

sounds like a great company

## 2-step automated deployment

http://daveramsey.com

* cap deploy is one-step process
* sucks when deploying to multiple environments
* prod deployment looks just like staging deployment but needs to deploy from scratch again

Fix:

* build deployable "package"
* deploy package to all environments
* `cap build deploy` on build server
* `bundle install --deployment` is part of it
* push that package out to staging, produciton, etc
* uses rsync within cap to deploy the package
* http://gist.github.com/dugsmith/5109521



