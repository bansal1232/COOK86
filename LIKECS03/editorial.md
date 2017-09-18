# Problem Link
[Practice](https://www.codechef.com/problems/LIKECS03)

[Contest](https://www.codechef.com/COOK86/problems/LIKECS03)

**Author:** [Bhuvnesh Jain](https://www.codechef.com/users/likecs)

**Tester:** [Hasan Jaddouh](https://www.codechef.com/users/kingofnumbers)

**Editorialist:** [Bhuvnesh Jain](https://www.codechef.com/users/likecs)

# Difficulty
EASY-MEDIUM

# Prerequisites
Bitwise Operations, Greedy Algorithm

# Problem
Given an array and a recursive algorithm which operates on this array, find the minimum number of elements to be inserted so that the algorithm on the resultant array never goes into infinite loop. The algorithm is as follows :
<code>
<pre>
void recurse ( array a, int n )
{
	// n = size of array
	define array b currently empty
	consider all 2^n subsets of a[]
	{
		x = bitwise OR of elements in the subsets
		add x into "b" if it is not present yet
	}
	if (sizeof( b ) == 1 << k)
	{
		printf(“Won”);
		return;
	}
	recurse ( b, sizeof( b ) );
}
</pre>
</code>

# Quick Explanation
Try to think about powers of $2$. Answer is simply the number of missing powers of $2$.

# Explanation
It suffices to consider only the unique elements in the initial array because $a$ OR $a = a$.

Now, assume we stop the recursion the moment when we see there are no new addition of elements in the array. At this moment 2 things can happen, either the array will contain all numbers from $0$ to $(2^K - 1)$ i.e. it size will be $2^K$ or some of the elements might we missing from the array. Let us assume for now, we have a black box which can effectively give us the final array after we stop this recursion, i.e. generate all elements in the final array formed. If the size of array is $2^K$, we do not need to insert any element and the answer is trivially $0$. Otherwise, let the smallest number that is not generated be $x$. We will insert this number into the array and run the same black box again. This is because, since $x$ was not generated by the previous array, for the new array to prevent infinite loop in the algorithm, $x$ should be present. If we insert any larger number which was not generated, then again we can’t form $x$ as <b>OR</b> operations always generates a number which is greater than or equal to the minimum of 2 numbers.

We will now prove that the smallest number which is not found the black box is indeed a power of $2$. Let $y$ be the number of bits set in $x$. Then, there are exactly $3^y$ ordered pairs, $(u, v)$, whose bitwise OR is $x$.

One can observe that once a bit is set while doing $OR$ operation, it will remain set in the end also. So if the algorithm given in the problem generates $x$, it must do so in maximum $k$ steps of iterations. So, if it doesn't generate $x$, then there should not also not generate both of $(u, v)$ for all $u$, and $v$, such that their bitwise $OR$ is $x$. Since, $x >= min(u, v)$. So, our claim that $x$ is the smallest number not generated will be wrong unless $x$ is power of $2$, as the only possible ordered pairs are $(0, x)$, $(x, 0)$ and $(x, x)$.

Since, we proved $x$ should be power of $2$, so even after inserting $x$ into the array, we will not generate $y$ where $y$ is power of $2$ not initially present in array and is greater than $x$. Thus, we do this step again and again and greedily insert only powers of $2$ into the array. In the end once all powers of $2$ are present in the array, then considering only subsets of these, we can generate all numbers using $OR$ operations. Thus, greedy strategy will be optimal here.

Hence, we simply need to find the count of powers of $2$ not present in the initial array. For this, you can either mark the elements in other auxilliary space (of size $2^k$) or simply insert only powers of $2$ into a set and check it's size.

### Bonus Problem
Try to above black box mentioned with complexity $O(2^k \log{n})$.

# Time Complexity
$O(N \log{n})$ or $O(N + 2^K)$

# Space Complexity
$O(N)$ or $O(2^K)$

# Solution Links
[Setter's solution]()

[Tester's solution]()