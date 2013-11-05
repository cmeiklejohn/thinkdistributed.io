thinkdistributed.io
===================

Think Distributed: The Distributed Systems Podcast

## Getting Started
This website uses [Middleman](http://middlemanapp.com/). 

  - Install Dependencies: `bundle install`
  - Development: `bundle exec middleman server`
  - Build Static Site: `bundle exec middleman build`

## Add an episode
Episodes are written in [HAML](http://haml.info/) with [Markdown](http://daringfireball.net/projects/markdown/syntax) filters.

The title and heading are written in markdown like so:
```haml
:markdown
  # Consensus

  A discussion about the problem of consensus in distributed computing, focusing on the Raft algorithm developed by Diego Ongaro and John Ousterhout at Stanford University.
```

Then the embed links for SoundCloud and Youtube (HTML is valid HAML so it's fine to just cut and paste):
```haml
<iframe width="100%" height="166" scrolling="no" frameborder="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/100811088&amp;color=2489a5&amp;auto_play=false&amp;theme_color=f0f0f0&amp;sharing=true "></iframe>

<iframe class="youtube-player" src="//www.youtube.com/embed/C8LrUZBxfdw?showinfo=0&amp;color=ffffff&amp;rel=0" frameborder="0" allowfullscreen="allowfullscreen"></iframe>
```

NOTE: You should add `&amp;color=2489a5&amp;auto_play=false&amp;theme_color=f0f0f0&amp;sharing=true` to the Soundcloud embed URL and `?showinfo=0&amp;color=ffffff&amp;rel=0` to the Youtube embed URL.

Next, you add the panelists. Currently I have them stored in an array, where each panelist is a hash with a name, title, and twitter. Each hash is then rendered with a panel_member partial:
``` haml
%h2 Panel
- panel = [{:name=> "Christopher Meiklejohn", :title=> "Software Engineer at Basho Technologies", :twitter=>"cmeik"}, {:name=> "Justin Sheehy", :title=> "CTO at Basho Technologies", :twitter=>"justinsheehy"}, {:name=> "Peter Bailis", :title=> "Graduate Student at UC Berkeley", :twitter=>"pbailis"}, {:name=> "Diego Ongaro", :title=> "Graduate Student at Stanford University", :twitter=>"ongardie"}, {:name=> "Andrew Stone", :title=> "Software Engineer at Basho Technologies", :twitter=>"andrew_j_stone"}]

%ul
  - panel.each do |member|
    = partial "layouts/panel_member", :locals=>{:member => member}
```

N.B. We'll need to add photo to this as well. And potential abstract it out further to avoid redundancy

Lastly, show notes are listed under a markdown filter:
```haml
:markdown
  ## Show Notes

  * [Consensus (computer science)](http://en.wikipedia.org/wiki/Consensus_(computer_science))
  * [Impossibility of Distributed Consensus with One Faulty Process](http://cs-www.cs.yale.edu/homes/arvind/cs425/doc/fischer.pdf)
  * [Paxos (computer science)](http://en.wikipedia.org/wiki/Paxos_(computer_science))
  * [Apache Zookeeper](http://zookeeper.apache.org) 
```