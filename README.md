## All Elements in Two Binary Search Trees
#### Solution
  Returning all elements in Two Binary Search Trees can be broken down into two algorithms:

  __In-Order Tranversal:__ The first algorithm used is to construct an in-order array from each BST. This can be completed in O(N) time where N is the total number of elements in each BST while O(N) space is needed to store each value. Leveraging an implementation of in-order transversal of a BST while passing an array as a container for each visited value can be used to construct an ascending array for each BST.

  __Merge:__ A Merge algorithm from MergeSort or InsertionSort can be used to combine both of the arrays into a ascending array in O(N) time where N is the total number of elements in each tree and O(N) space is needed to store each value. Merge pops the least value between each BST array into the merged array then when one array is empty all values from the remaining BST are added to the merged array.

  __Time Complexity__ O(N)<br />
  __Space Complexity__ O(N)<br />
  Where N is the combined number of elements in each Binary Search Tree (BST). Since both algorithms total O(N) + O(N) Space and Time Complexity the total Space and Time Complexity of this algorithm reduces to O(2N) which is interpreted as O(N).

    # Definition for a binary tree node.
    # class TreeNode:
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution:
        #Inorder Tranversal of Bianry Tree to construct arrays of inorder values
        #Time Complexity: O(N)
        #Space Complexity: 0(N)
        #Where N is the number of elements in the array
        def getInorderList(self, node, array):
            #Terminating if statement if the current node is None
            if node == None:
                return
            #Visits Left Node, operates on self, then visits Right Node in inorder fashion
            self.getInorderList(node.left, array)
            array.append(node.val)
            self.getInorderList(node.right, array)
            return
        #Merge two ordered lists
        #Time Complexity: O(N+M)
        #Space Complexity: O(N+M)
        #Where N is the number of eleemnts in array1 and M is the number of elements in array2
        def mergeInorderList(self, array1, array2):
            #Declaring container list
            merged = []
            #While both arrays have values
            while(len(array1) > 0 or len(array2) > 0):
                #Insert the smallest value into the merged lists at the front of each array
                if len(array1) > 0 and len(array2) > 0:
                    if array1[0] > array2[0]:
                        merged.append(array2.pop(0))
                    else:
                        merged.append(array1.pop(0))
                #If only array1 has values then insert all remaining values into list
                elif len(array1) > 0:
                    while(len(array1) > 0):
                        merged.append(array1.pop(0))
                #If only array2 has values then insert all remaining values into list
                elif len(array2) > 0:
                    while(len(array2) > 0):
                        merged.append(array2.pop(0))
            return merged
        #Getting all elements algorithm is to:
        #1. Construct an inorder list of all nodes in both trees with inorder transversal
        #2. Merge sorted array into one array
        def getAllElements(self, root1: TreeNode, root2: TreeNode) -> List[int]:
            #Declaring container arrays
            array1 = []
            array2 = []
            #1. Construct an inorder list of all nodes in both trees with inorder transversal
            self.getInorderList(root1, array1)
            self.getInorderList(root2, array2)
            #2. Merge sorted array into one array
            merged = self.mergeInorderList(array1, array2)
            return merged
