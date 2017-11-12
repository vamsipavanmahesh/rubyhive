---
layout: post
title:  "Write better reading tests with shoulda-matchers"
date:   2017-11-12 12:53:00 +0530
categories: rspec
---

This article about comparing how tests are easier to read, when you use shoulda-matchers for testing associations and validations. shoulda-matchers is a nice gem in our toolkit which will help to test fairly trivial things, which are cumbersome to write in plain RSpec.

So this code is taken from one of my side projects, where User and Category has a has many through relationship with UserCategory.

Here is what my model looks like

{% highlight ruby %}
# frozen_string_literal: true

# middle table for the users and categories
class UserCategory < ApplicationRecord
  belongs_to :user
  belongs_to :category
end
{% endhighlight ruby %}
Let me show a user_category_spec, which is written in plain RSpec to test the associations and presence validations

{% highlight ruby %}
# frozen_string_literal: true

require 'rails_helper'

RSpec.describe UserCategory, type: :model do
  describe 'associations' do
    it { UserCategory.reflect_on_association(:user).macro.should  eq(:belongs_to) }
    it { UserCategory.reflect_on_association(:category).macro.should  eq(:belongs_to) }
  end

  describe 'validations' do
    it 'has a valid factory' do
      expect(FactoryGirl.build(:user_category)).to be_valid
    end

    it 'invalid without user' do
      expect(FactoryGirl.build(:user_category, user: nil)).to be_invalid
    end
    it 'is invalid without category' do
      expect(FactoryGirl.build(:user_category, category: nil)).to be_invalid
    end
  end
end
{% endhighlight ruby %}
Test output looks like this
```
associations
  should eq :belongs_to
  should eq :belongs_to
validations
  has a valid factory
  invalid without user
  is invalid without category
```

Let's see the one with the shoulda-matchers

{% highlight ruby %}
# frozen_string_literal: true

require 'rails_helper'

RSpec.describe UserCategory, type: :model do
  describe 'associations' do
    it { is_expected.to belong_to(:user) }
    it { is_expected.to belong_to(:category) }
  end

  describe 'validations' do
    it 'has a valid factory' do
      expect(FactoryGirl.build(:user_category)).to be_valid
    end

    it 'invalid without user' do
      should validate_presence_of(:user).with_message('must exist')
    end
    it 'is invalid without category' do
      should validate_presence_of(:category).with_message('must exist')
    end
  end
end
{% endhighlight ruby %}
Test output looks like this
```
associations
  should belong to user
  should belong to category
validations
  has a valid factory
  invalid without user
  is invalid without category
```

If you feel that the second one is easier to read and not so cumbersome, consider using shoulda-matchers[https://github.com/thoughtbot/shoulda-matchers] in your project
