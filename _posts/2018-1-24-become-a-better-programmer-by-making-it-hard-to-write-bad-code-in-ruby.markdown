This is a follow up article to https://blog.daftcode.pl/become-a-better-programmer-by-making-it-hard-to-write-bad-code-d118ab90e0f7, but the OP mentioned the tricks that are applicable in JS. So, I thought I will write something in the same style, but for Ruby :)

###  Ruby static code analyzer

My personal favorite and  most popular linting tool is [Rubocop](https://github.com/bbatsov/rubocop). This tool will let you know the code smells and the anti patterns in your code base, based on the community ruby style guide. But you can also configure it based on your team's preferences.

### Testing

I know this may seem tedious or time consuming in the beginning, but time of writing tests will pay off in the long term (or even short term), because you will be able to add the new features confidently without the fear that you might have broken the existing functionality

If you follow strict Test Driven Development, you may end up writing code for the features that are defined in the spec, which helps you in avoiding over engineering solutions or in other words, it will help write lesser code that just meets the specifications

I use the following gems for the testing purposes

[Rspec-Rails](https://github.com/rspec/rspec-rails), [Factory Girl](https://github.com/thoughtbot/factory_bot), [Capybara](https://github.com/teamcapybara/capybara), [Faker](https://github.com/stympy/faker)

### Continuous Integration

A CI tool spawns up a virtual machine, installs all the required software in the system for your application to run, setup the DB, and run all the linting tools and the tests that you have in your application

This tool is generally triggered when you make a new PR to master or any other branch like testing or staging from your feature branch

So before merging the branch the branch it's generally a good idea to check the build status of CI tool

We use [Travis](https://docs.travis-ci.com/user/languages/ruby/) as a CI tool at [Rietta](https://rietta.com/)

### Commit Messages

Writing a good commit message is VERY important, because it will help other developers to determine what kind of code change is triggered for what reason in the file throughout it’s existence, if they happen to see the history of the file.

An ideal commit should be only making one functional change, describe what is the goal of the commit message and which files are affected

You can read more about  from https://chris.beams.io/posts/git-commit/

ps: My contract with Rietta Inc ended recently. I am looking for a fulltime remote job from India in the salary range of $40 k. Please let me know if you or anyone you know is hiring. [Here](https://1drv.ms/w/s!AqqymJehTnCGhm6EHP2wRHGwvPl3) is my resume.
