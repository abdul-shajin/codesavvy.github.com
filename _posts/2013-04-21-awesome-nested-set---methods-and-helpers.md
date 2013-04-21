---
layout: post
title: "Awesome Nested Set   Methods and Helpers"
category: posts
---
Given all helper methods that we can use in the gem [Awesome Nested Set](https://github.com/collectiveidea/awesome_nested_set)

#Class Methods
{% highlight ruby%}
Category.root   the first root node
Category.roots  all root nodes
{% endhighlight %}
 
#Instance Methods 
{% highlight ruby%}
my_cat.root                  root for this node
my_cat.level                 the level of this object in the tree (e.g. root = 0)
my_cat.parent                the node's immediate parent
my_cat.children              array of immediate children (just those in the next level)
my_cat.ancestors             array of all parents, parents' parents, etc, excluding self
my_cat.self_and_ancestors    array of all parents, parents' parents, etc, including self
my_cat.siblings              array of brothers and sisters (all at that level), excluding self
my_cat.self_and_siblings     array of brothers and sisters (all at that level), including self
my_cat.descendants           array of all children, children's children, etc., excluding self
my_cat.self_and_descendants  array of all children, children's children, etc., including self
my_cat.leaves     					 array of all descendants that have no children
{% endhighlight %}

Predicates
{% highlight ruby%}
my_cat.root?                         true if this is a root node
my_cat.child?                        true if this is a child node (i.e. it has a parent)
my_cat.is_ancestor_of?(obj)          true if nested by any obj
my_cat.is_or_is_ancestor_of?(obj)    true if nested by any obj or self is obj
my_cat.is_descendant_of?(obj)        true if self is nested under obj
my_cat.is_or_is_descendant_of?(obj)  true if self is nested under obj or self is obj
my_cat.leaf?
{% endhighlight %}
