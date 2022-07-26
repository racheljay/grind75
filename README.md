# Grind 75 questions

This is a running collection of all of the grind 75 questions I have answered so far:
[https://www.techinterviewhandbook.org/grind75](https://www.techinterviewhandbook.org/grind75)
 <br>
 <br>

 # Contents:
 Week 1
 1. [Two Sum](#two-sum)
 1. [Valid Parentheses](#valid-parentheses)
 1. [Merge Two Sorted Lists](#merge-two-sorted-lists)
 1. [The Best Time to Buy and Sell Stock](#the-best-time-to-buy-and-sell-stock)
 1. [Valid Palindrome](#valid-palindrome)
 1. [Invert Binary Tree](#invert-binary-tree)
 1. [Valid Anagram](#valid-anagram)
 1. [Binary Search](#binary-search)
 1. [Flood Fill](#flood-fill)
 1. [Maximum Sub Array](#maximum-sub-array)
 1. [Lowest Common Ancestor of a Binary Search Tree](#lowest-common-ancestor-of-a-binary-search-tree)
 1. [Balanced Binary Tree](#balanced-binary-tree)
 1. [Linked List Cycle](#linked-list-cycle)

 Week 2
 1. [First Bad Version](#first-bad-version)
 1. [Ransome Note](#ransom-note)
 1. [Climbing Stairs](#climbing-stairs)
 1. [Longest Palindrome](#longest-palindrome)
 1. [Reverse Linked List](#reverse-linked-list)
 1. [Majority Element](#majority-element)
 1. [Add Binary](#add-binary)
 1. [Middle of a Linked List](#middle-of-the-linked-list)
 1. [Max Depth of a Binary Tree](#maximum-depth-of-binary-tree)


# Week 1

## Two Sum

##### _Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target._

##### _You may assume that each input would have exactly one solution, and you may not use the same element twice._

##### _You can return the answer in any order._
---

 For this solution iterated through the given array and added each iterable to an object that also stored its index. On each turn of the loop I would find a "partner" number by subtracting the current iterable from the target number. I would then check if the current partner was already _inside_ the object as a previous iterable. If it was I could push both that past iterable and the current iterable with their saved indexes, therefore returning the "coordinates" of the two numbers that would add up to the target.
 <br>
 <br>

 ## Valid Parentheses

 ##### _Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid._

##### _An input string is valid if:_

##### _1. Open brackets must be closed by the same type of brackets._
##### _2. Open brackets must be closed in the correct order._
---
In this solution, I initialized an object setting the relationship between open and closed parenthesis. I also initialized two sets. One for "openers" and one for "closers". I would then loop through the given string. On each step of the loop I would check if the iterable was an "opener", if so I would add it to the beginning of an array to track a record of which type of parens was open.
I would also check if the iterable was a "closer". If this is true, I would check the beginning of my paren tracking array. If the first item in the array was the complementary opener, it would get shifted off of the array. Once a paren has been closed, there is no more reason to track it. If they were not a match, I return false.
 <br>
 <br>

## Merge Two Sorted Lists

##### _You are given the heads of two sorted linked lists list1 and list2_.

##### _Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists._

##### _Return the head of the merged linked list._
---
This was my very first time using linked lists, so I had to do a lot of studying of the concept to get through this one.

I started with weeding out some of the easy edge cases. I then created a method that would insert a number in order to the first provided list. It includes logic on how to insert a given number _between_ two numbers in the list, and how to insert numbers at the end, if the numbers are outside the range of the first list. I also included logic that would add data values to the beginning of the list.

I then wrote a merge method that would iterate through the second list and implement this, "add in order" method for each value in the second list. 

**I plan to revisit this in the future. I believe that this one, while functional, could be a bit more performant*
 <br>
 <br>

## The Best Time to Buy and Sell Stock


##### _You are given an array prices where prices[i] is the price of a given stock on the ith day.s_

##### _You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock._

##### _Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0._
---
In this solution I was challenged by having to continually improve my answer to account for new edge cases for each new test leet code provided. As a result, I feel like I have a very solid performant solution.

I start by initializing a bunch of variables:
* lowest -> starts as a high safe number
* highest -> starts as a low safe number
* diff -> used to calculate the difference between the current highest and lowest prices
* profit -> initialized at 0, but will eventually return the maximum possible profit
* lowestIndex -> it turned out to be very important to keep track of the current index of whatever the lowest number was

I would then loop through the array of prices. If the price was less than the current lowest number, lowest would become the current price. I then record the current index. The current highest would also be reset.

To find the highest number, I would skip over the first index, since the highest could never come first, and then I would check if the current highest was less than or equal to the current price AND if its index was higher than the current lowest number. If these conditions are met, highest gets set to the current price, and a new diff is calculated. If that diff is more than the current profit, profit is reassigned to this new diff.

The returned profit will either equal the best possible max or 0, if the necessary conditions were not met.
<br>
<br>

## Valid Palindrome

##### _A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers._
---
This one was easy for me because I'd actually solved it a few times before :)

I started by doing some basic string sanitization by getting rid of spaces and punctuation, and converting everything to lowercase. However, due to some of the test cases, I had to include a check at this stage to check for strings that were just one piece of punctuation or just a single space.

After I was sure I had an array of only lowercase letters and numbers, I was then able to loop through the array from both ends, and making sure these two indexes matched. If there is a mismatch, the loop ends and returns false. If the beginning index becomes higher than the ending index, I know that I am crossing into characters that have already been checked, and I can safely return true.
<br>
<br>

## Invert Binary Tree

##### _Given the root of a binary tree, invert the tree, and return its root._
---
This was my first ever time working with binary trees! I found this to be a much smaller learning curve especially after all of the time I spent on linked lists. Before tackling this one I spent a lot of time getting familiar with binary trees as a concept and played around with lots of different methods I could use. Including one that would print all of the nodes in pre order by storing them on a queue. You could say I went wild.

It turned out that after all my messing around with trees, my actual solutions turned out to be a lot simpler that I thought it would be. I started with a null check to make sure the tree root was not empty, and then another one to return the root once the current node lefts and rights all returned null. To do the actually inverting, I saved the left node in a temporary variable, assigned the right to the left, and then gave the right value the stored previous left data. I then did a recursive call of the function for each left and right node throughout the tree, while checking that neither of them were null. Finally at the end I returned the root.
<br>
<br>

## Valid Anagram

##### _Given two strings s and t, return true if t is an anagram of s, and false otherwise._

##### _An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once_
---

This one was pretty easy actually. I started by checking for some edge cases. In order to be tested, strings but be the same length and they are automatically true if they are equal. I then created two objects, one for each string. Next I looped through the two strings and added their letters and the number of times they appear to their relevant object. After that I made a new loop that that will compare the values of the two objects and will return false if there is an inconsistency. If everything goes smoothly, the function returns true.
<br>
<br>

## Binary Search

##### _Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1._

##### _You must write an algorithm with O(log n) runtime complexity._
---
I had previously learned about binary search, so this question was a nice refresher. In doing further research to solve this, I learned that there are two main solutions, an iterative one and a recursive one. I chose to implement the iterative one, because that made my brain hurt less, but I am interested to test both in order to find which one is faster.

For the iterative version, I took an array and a target number as arguments. Then I declared a left variable, which starts at 0 and a right variable that starts at the last index of the array. In a while loop, as long as the left variable is not greater than the right variable, I declare a midpoint variable, which is the left plus the right divided by two. (Since I'm using JS I ended up having to wrap this in a Math.floor to get rid of any decimals).

If the number at the index of mid equals the target number, I return the index number. If the target is lower than the mid number, the right variable becomes mid minus one. If the target is bigger than the mid, left becomes mid + 1. If all these conditions fail and the number is not located, the function returns -1
<br>
<br>

## Flood Fill
##### _An image is represented by an m x n integer grid image where image[i][j] represents the pixel value of the image._

##### _You are also given three integers sr, sc, and color. You should perform a flood fill on the image starting from the pixel image[sr][sc]._

##### _To perform a flood fill, consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with color._

##### _Return the modified image after performing the flood fill._
---
Okay this one was super cool. It took me a bit to figure out, but once I did, my heart was _racing_. Which sounds dorky, but is accurate. I found myself remembering back to my bootcamp days as well because I had to make a tic tac toe game which used similar nested array edge case logic.

To be fair I did waste a _little_ bit of time with this one because I made an extra function, "visualizeImage", which did not go into my leetcode solution. It was purely for my own pleasure of seeing the results print out in a neat little box instead of a super boring nested array. Okay on to the actual solution.

For this one I take image, sr, sc, and color, as params. (I would explain what they are but I already left a comment in the actual file so...). I start out with a check to see if the target is already the number we are trying to change it into. If it is, we return the image in its current state. Next are just some peace of mind checks, to make sure that the given coordinates in the image are actually valid. These were actually super useful because they helped me find a bug during one of the test cases I didn't originally test with.

Next comes the definitions for the areas around our target square. Basically they return the value in the specified square, or they return null if that square goes off of the grid. After that I set the current target square value to be the new number that is passed in. AND THEN COMES THE COOL PART. I check the surrounding squares to see if they match the original target value. If they do I make a _recursive_ call and pass in altered coordinates to make the target value for the recursive calls the surrounding square values. And thus the new number or color or whatever spreads like a virus. This was very exciting.
<br>
<br>

## Maximum Sub Array

##### _Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum._

##### _A subarray is a contiguous part of an array._
---

*Edit:* I have now refactored this one and it is slightly more efficient. I keep track of a current total and an overall maximum total. The current total I'm tracking starts as the first index of the array. I then loop through the array starting at index 1. If the number at the current index is more than the current total plus that index number, the curren total gets updated with the previous total plus the new num. I also check if this is bigger than the previous overall max total. If the current num is not bigger than the num plus the current total, the current total becomes num plus the current total, updating the overall max like for the other condition. I then return the max total.

Old solution:

I tried two different approaches to this one with the first approach ultimately not working. The first attempt involved chopping the head and tail off the array and then finding the sum of it in a while loop every time it changed, and storing this in a results array. It kind of worked but not really. I kept running into weird edge cases once the array started to get smaller and it was very slow being O(n<sup>2</sup>).

For my final solution I still kept my solutions array but implemented it slightly differently. Instead of doing an expensive iterative math operation for each iteration, I started by saving the first index of the array in my results array. I then was able to loop through the rest of the array only once. Each time I compared the new number to the previous result. If the current number is higher than the most recent result plus itself, it gets added to the result array. If it is not bigger than the previous result, it adds itself with the previous result and that gets added to the result array. Then I run a separate loop through the result array to find the highest number solution.

This one could probably be fine tuned a bit down the road, but I am happy with the relatively succinct I was able to come up with. I'm just happy I was able to get it less than O(n<sup>2</sup>). 
<br>
<br>

## Lowest Common Ancestor of a Binary Search Tree
##### _Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST._
##### _According to the [definition of LCA on Wikipedia:](https://en.wikipedia.org/wiki/Lowest_common_ancestor) “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”_
---
In my lowest common ancestor function, I accept the root node, and p and q, which represent the two nodes I am finding the ancestor for.

I started by writing a helper function called "savePath". Save path takes a value and loops through the tree path, saving visited nodes to a set along the way, returning the set at the end. I call this function twice, once for p and once for q so that I have a set for each path.

Then I compare the two sets and return a new set that contains any shared nodes. This new set then gets converted to an array and I return the last item in the array, which should be the last added common node.
<br>
<br>

## Balanced Binary Tree
##### _Given a binary tree, determine if it is height-balanced._

##### _For this problem, a height-balanced binary tree is defined as:_

##### _a binary tree in which the left and right subtrees of every node differ in height by no more than 1._
---
This one has probably taken me the most amount of time to solve. I have two solutions for this one that I would like to hold on to in case they come in handy in the future.

For the first solution, there are two simple functions. One function simply recursively finds the height of a tree by returning -1 if we are on a null node, or adding 1 to the existing maximum tree height, as we bubble back up from the bottom.

The second function (isBalanced) returns true if our node is null. At the end I return if the height difference between the left and right tree is less than two AND call isBalanced recursively on the left and right sides. Our return resolves to either true or false depending if all the requirements are met.

Second solution:

The next solution is a little harder to grasp. Most of the actual logic is handled in a helper function, which is returned by a wrapper function. A big mental block for me in the solving of this problem, is that I needed to be able to return two things. A height and a boolean that determines wether a tree is balanced or not. One solution for this is to simply return the results in an array.

If the node is null, I return an array with true and -1. A null node is a balanced node. Next is I do a recursive call of the helper function and assign that to a variable. Because the data we need is in an array, I break it out into two variables to make it a bit more readable for myself. If the left side is not balanced, we return an array with false and 0. We do the same thing, getting data from the right side by recursively calling the balance helper until it finds one that is false.

Assuming on our given node we make it past our two fail checks for the left and right sides, we return an array that will give the boolean result of the current left and right height difference being less than two. The second spot in the array will return the current height, by finding the max of the left and right heights and adding one. If we make it all the way through the tree with no failures, we know it is balanced.

This solution is more efficient than the previous one because we are only calling our function on each node once, giving it an efficiency of O(n).
<br>
<br>

## Linked List Cycle
##### _Given head, the head of a linked list, determine if the linked list has a cycle in it._

##### _There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter._

##### _Return true if there is a cycle in the linked list. Otherwise, return false._
---
This one was fairly easy to implement. I start by catching the edge case of returning false if the linked list is empty. I then create a set to store visited nodes in the linked list. In a while loop, I check if a node is _not_ in the set. If it is not, it gets added, and the loop iterates to the next node. If the next node is null it breaks the loop and returns false. Outside the loop I check if the set already has one of the previously iterated nodes. If it does, this proves the cycle and I return true.

<br>

____

<br>


# Week 2

## First Bad Version

##### _You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad._

##### _Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad._

##### _You are given an API bool isBadVersion(version) which returns whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API._
---
This one tripped me up until I realized that this was a use case for binary search. In my first version of the solution, I generated an array of all of the possible previous versions so that I could perform the search on the array. This ended up being kind of silly, because making the array took lots of time and was able to do the binary search math on the number itself rather than a redundant array. This was my first impulse, because I have only ever done binary search on ordered lists before. It was easy to remove the need for the array from my logic, by simply replacing the last index spot of my array with the actual number I'm checking.

In the return function, I start by naming two variables: left and right. Left starts as 0 and right starts as the number being passed in (n). Next I used a while loop to run on the condition that the left number is less than or equal to the right number. Inside the loop, mid is defined as being whatever the left plus the right numbers are divided by two. I also define a variable that will show what the immediate previous version to the current version is. This is necessary because we want the _first_ bad version, so we need to check that the previous version is not also a bad version. I then do some if checks. The first check if we currently have the condition we want, if true, it returns the current mid. Next I check if the current version number is not a bad version. If the current mid is false we know that the first bad one must be a higher number. If the version is too low, left becomes mid + 1. Finally we check if the mid is a bad version, but the previous one is also a bad version, in which case we take the right and it becomes mid - 1.
<br>
<br>

## Ransom Note

##### _Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise._

##### _Each letter in magazine can only be used once in ransomNote._
---
For this one I started off with an edge case covering whether the length of the ransom note was longer than the length of the magazine. If this is true, I return false, because there are not enough letters to complete the note. Next I declare two objects, one for the magazine and one for the letters needed for the note, and a count variable. I then loop through the two strings and fill the objects with the letters that appear in each and how many times that letter appears.

In another loop I go through the keys of the letters needed. If a letter is in the cut up magazine, I also return false if it does not appear in the correct quantity. If the letter is not in the magazine, I return false. If the loop completes without failing, I return true.
<br>
<br>

## Climbing Stairs

##### _You are climbing a staircase. It takes n steps to reach the top._

##### _Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?_

This was one that I struggled with, but I feel like I came out the other side learning a lot about memoization. It was a bit tricky getting my head around all of the recursion in this problem but I think I was able to come up with solution that makes sense to me.

I did this in two stages. The first way being a brute force approach. I made a function that accepted two parameters: current step and last step. I then made some statements that would break the recursion. If the current step is greater than the current step, we know that the way we got to this number is not viable, and therefore we can return 0. If the current step is equal to the last step, we know that the way we got to this answer is valid, and we can return 1. I then recursed the function by returning my number of stairs function with current stair + 1 and adding that to another function call, passing in our current number + 2. This worked but was very inefficient so I made minor changes that greatly improved it with memoization.

After the two checks checking if our current step is greater than or equal, I added another check, looking if the current number is indexed in our memo array. If it is, we know we already have a solution for this one and we can return it. Then, instead of returning the product of two function calls, I assign the two recursive function calls to the index of our current step in the memo array. I can then return the index of our current step in the memo array.

This one threw me for a loop and it took me awhile to understand. I spent a long time drawing out diagrams, which took me further away from the solution, until I finally did a lot of studying on memoization and dynamic programming. This one was a bit frustrating because I didn't arrive at it organically. I doubt I would have ever come up with this on my own, but I guess not a lot of other people would either, given the number of tutorials there are about this on the internet.
<br>
<br>

## Longest Palindrome

##### _Given a string s which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters._

##### _Letters are case sensitive, for example, "Aa" is not considered a palindrome here._

I solved this one using a method I've used several times so far which includes converting a string to an objet that includes letters and how many times they appear in the string.

After I had an object tot work with, I looped through the keys of the object and determined if it was even or odd. If it was even, the total number of this letter could go towards the ultimate length total. If the number is odd, I allow the first one to be added, but after this happens, a boolean gets changed that will change the logic for the remaining odds. Any odds after the first one will have their total added to the ultimate length while subtracting one from each of them, so that they can be evenly placed around an odd in the center.
<br>
<br>

## Reverse Linked List

##### _Given the head of a singly linked list, reverse the list, and return the reversed list._

This one was pretty straight forward, and has shown me that I am becoming more and more comfortable with using linked lists.

I start by declaring a variable for the previous node that starts as null, and a variable for the current node, which starts as the head node. While the current node is not null, I have a new variable for the node after the current node, which starts as the current next. (This is important to save this link in the list, else it could be lost while reassigning list relationships.) Then I assign the current next to be what is stored in previous. Then a new previous gets set as the current, and a new current gets set as the node we saved in after. This loops until the whole list has been reversed. Finally I return the previous node.
<br>
<br>

## Majority Element

##### _Given an array nums of size n, return the majority element._

##### _The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array._

I feel like I've done this problem so many times now I can do it in my sleep, which is a good thing.

I make an empty object to capture numbers and how often they appear. I also set a highest frequency variable and a numString variable. I loop through the string. If the number is already in the object, I add one to the frequency, if it's not in the object, I add it.

While this is happening I check if the current number has a frequency higher than the number being stored in the appropriate variable. If it is, it becomes the new highest. I also update numString to record what that number is. Finally I return the numString value, parsed, so that it returns a number.
<br>
<br>

## Add Binary

##### _Given two binary strings a and b, return their sum as a binary string._

This one was super fun. Before this, I had no idea how binary numbers worked, so that was fun to learn. I also knew that I didn't want the hassle of converting binaries to ints and then back again, so I came up with the following solution:

I start by figuring out which of the two strings is the longest, and then I loop over that string, starting at the end. In the loop I do some basic math to find out what each digit of the two binary numbers comes out to be. If the two digits and any remainder equal 3, we add 1 to the solution and have a remainder of 1. If they equal 2 we have add a 0 to the solution and have a remainder of 1. If they equal 1, we add 1 to the solution and we have no remainder. 0 means we add 0 and we have no remainder. Unfortunately some logic is repeated for this part because I have separate statements depending on if we have run out of numbers in the shorter string or not. There's probably room for refactoring there. I then decrement the short string and long string indexes. After the loop completes I check and see if there is a remainder left over. If there is, I add that to the solution. 

## Diameter of Binary Tree

##### _Given the root of a binary tree, return the length of the diameter of the tree._

##### _The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root._

##### _The length of a path between two nodes is represented by the number of edges between them._

The key to this one for me was keeping track of the root node for which ever path is the longest. I first initialize a diameter variable outside of my recursive function. Inside the function, I have a base case to return 0 if the current node is null. I then save the left and right paths in variables which are recursive calls to the function for the left and right sides. I then update diameter by finding the max between the old diameter and the current left path plus the right path. Finally the function returns the max between the left and right path plus one, so that we can add adjusted heights to the recursions.

Outside of the recursing function, I call the function and pass in the root of the tree. I then return the diameter, which has been updated by the recursive function.
<br>
<br>

## Middle of the Linked List

##### _Given the head of a singly linked list, return the middle node of the linked list._

##### _If there are two middle nodes, return the second middle node._

I was really pleased with my solution for this one until I saw the optimized solution for this one and it blew my mind. So I am including both of them.

For the first solution I declare an index variable that starts at 1 and an empty object to store nodes as we arrive at them. I then loop through the linked list, and store nodes along with the incremented index as the key. Finally I can return the correct node from the object by dividing the final index by two.

The second solution saves space by not bothering to store any of the nodes. It traverses through the linked list with a slow pointer and a fast pointer. While the slow pointer passes through each individual node, the fast pointer skips a node each time, therefore moving at double speed. By the time the fast pointer makes it to the end we can assume that the slow pointer will be at the halfway point, and at that point we can just return that.
<br>
<br>

## Maximum Depth of Binary Tree

##### _Given the root of a binary tree, return its maximum depth._

##### _A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node._

Honestly I was really surprised by the placement of this one on the list. I've used this within several other binary tree problems, so it was weird to see it so far down the list.

This one is pretty simple. I have a check in place to return zero if we have reached a null node. I then return the max heights of the left and right trees by finding the max between recursing the left and right sides and adding one each time the recursive function is called.