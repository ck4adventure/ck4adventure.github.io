---
layout: page
title: RSpec
permalink: /rspec/
---

## Rspec Reference

### Factories
basic items
```ru
  factory :item do
    name { Faker::JapaneseMedia::SwordArtOnline.item }
    itype { Faker::Number.between(from: 1, to: 10) }
    le { false }
  
    trait :limited_edition do
      le { true }
    end
  end
```
s

### Shoulda Matchers
use `subject { build() }`

```ru
it { should validate_numericality_of(:luck) }
it { should validate_presence_of(:cheese_effect) }
it { should define_enum_for(:cheese_effect) }
```
