# Btree

B-trees are similar to binary search trees in many ways, but they have two big differences: 
the number of children per node is not limited to two and the number of keys in the node is also variable (not just 1).

B-trees are self-balanced, rooted, sorted trees. They allow operations such as insert, search, deletion, and access in logarithmic time.

Each internal node has n keys. These keys are like dividing points between child nodes. So, for n keys, the internal node has n+1 child nodes.

This feature makes B-trees suitable for different applications in fields such as databases and external storage.
Having more than two children per node and multiple keys allows the B-tree to perform multiple comparisons for each internal node,
so it has less tree height and therefore reduces the time complexity to access and search nodes.

As has been said, each internal node in a B-tree has a different number of keys inside. 
These keys are used to divide the subtrees below them in order.
Look at the following example:

![btree](https://user-images.githubusercontent.com/66079439/183341737-42fa5a96-8871-4a5f-b8b0-78bbfc38b6e7.jpeg)

B-tree example
Internal node A has three children (subtrees). In order to separate them, it needs two keys [5, 20]. As you can imagine, it is easy to search for a specific node when you have a well-organized structure like this.
Let enumerate some mathematical properties for B-trees.
For a B-tree of order X:
* 		The root node may have 1 value and 0-2 children
* 		The other nodes have the following:
    * 		x/2 to x-1 ordered keys
    * 		x/2-1 to x children (subtrees)
* 		The worst height case is O(log(n))
* 		All the leaves have the same depth, which is the height of the tree


## 출처
https://learning.oreilly.com/library/view/swift-data-structure/9781785884504/ch05s05.html
