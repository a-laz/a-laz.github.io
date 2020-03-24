---
layout: post
title:      "Moving Across The US with Hashes"
date:       2020-03-23 21:32:16 -0400
permalink:  moving_across_the_us_with_hashes
---


As im writing this i'm in Rapid City, SD. I drove for the  past two days all the way from Columbus, OH. To the say the least im tired.

![](https://mondrian.mashable.com/2013%252F10%252F04%252F96%252Ftiredcat.0ca42.gif%252Ffit-in__850x850.gif?signature=J_AVrG-PAmGFt7_yhQYwap0Gf3s=)

What to do with hashes, I thought? What about logging each place i've been to during my career as a professional mover?

So I started.

```
moved_to_locations = Hash.new
```

Oops stupid mistake. I realized i needed to my locations to equal an array

```
moved_to_locations = Array.new
```

Now to populate the array 

```
moved_to_locations = ["maine", "new_hampshire", "new_york", "massachusetts", "maryland", "pennsylvania", "kentucky", "missouri", "ohio", "north_carolina", "florida", "south_dakota", "michigan"]

```

That's a lot of places, and I've only included the states i've stayed in, not drove through.

My OCD naturally kicked in and i wanted to alphabetize the array so...

```
moved_to_locations.sort_by! {|state| state}
```


So where do the hashes come in you may ask?

Well i wanted to keep track of what my favorite thing was im every state, least favorite thing, and wheter or not i would live there.

But before that i wanted to change the items in my array to symbols. Just so nothing broke and because the states aren't going to change

```
moved_to_locations = moved_to_locations.collect {|state| state.to_sym}
```

So now onto the fun part! 

![](https://media.giphy.com/media/Ve20ojrMWiTo4/giphy.gif)

How do we make each element in our array a key value pair or a hash?

Well the keyword EACH should poput.

BUT now i realized my intial thought was right aand i do need a hash for locations moved to... ooops?

I DID say i was tired

```
moved_to_locations = {"maine" => [], "new_hampshire" =>[], "new_york" =>[], "massachusetts" =>[], "maryland"=>[], "pennsylvania"=>[], "kentucky"=>[], "missouri"=>[], "ohio"=>[], "north_carolina"=>[], "florida"=>[], "south_dakota"=>[], "michigan"=>[]}
```

Now lets change each state to a symbol

```
moved_to_locations.transform_keys! {|k| k.to_sym}
```

So the value of each state should be, using maine as an example, an array of hashes: my favorite thing, least favorite thing, and a boolean value for wheter or not i would live there. 

```
moved_to_locations[:maine] = ["favorite" => " ", "least_favorite" =>" ", "would_live" =>" ", ]
```


Is there an easy way to set that value to each state? Lets dive in!

![](https://chenisesblog.files.wordpress.com/2015/07/cliff-diving-meme-generator-i-regret-nothing-c86796.jpg)

since we used the #transform_keys! method maybe there is a #transform_values! method?

There is!

![](https://media.tenor.co/images/cbc45d60c53d9380119ca09c96d011c5/raw)

```
moved_to_locations.transform_values! {|v|  ["favorite" => " ", "least_favorite" =>" ", "would_live" =>" ", ] }
```

Now all i have to do is access each state with

```
moved_to_locations[:state]
```

and set each individual value!

Happy Coding Guys!!




