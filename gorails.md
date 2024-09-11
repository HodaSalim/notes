## Ruby for beginners
There is a difference between double quoted string and a single quoted string in Ruby
من الحاجات اللي بنستخدم علشانها ال double quoted strings هو ال string formatting زي في لغات تانية بمعني انها string فيها expressions محتاجين ان ال runtime يحللها قبل ما يطبع السترنيج
```ruby
irb(main):007> "2 + 2 = #{ 2 + 2}"
=> "2 + 2 = 4"
```

spaceship operator 
```ruby
irb(main):013> 4 <=> 7
=> -1 #meaning that the left handside is bigger than the right handside

irb(main):014> 10 <=> 4
=> 1 # here the right hand side is bigger
```

constants in ruby must start with a capital letter, the convention is to make it all caps. Constants can be re-assigned in ruby but it will present us with a warning if we did to however it will actually go through.
