# BinaryTreeExtension


# What is this?

This is .NET extension methods build as .NET library. Extension help you build binary tree and flatten binary tree.

# How do I use it?

Install BinaryTreeExtension <br>
Add "using BinaryTree.Extension" if using .NET Framework (4.5 or higher) <br>
Add "using BinaryTree.Extension.Core" if using .NET Core (1.0 or higher) <br>

# Example

```csharp
class Program
    {
        static void Main(string[] args)
        {

            var list = new List<TreeModel>();
            list.Add(new TreeModel(1, null, "Parent Node 1"));
            list.Add(new TreeModel(11, 1, "Child Node 1.1"));
            list.Add(new TreeModel(12, 1, "Child Node 1.2"));
            list.Add(new TreeModel(2, null, "Parent Node 2"));
            list.Add(new TreeModel(111, 11, "Child Node 1.1.1"));
            list.Add(new TreeModel(112, 11, "Child Node 1.1.2"));
            list.Add(new TreeModel(121, 12, "Child Node 1.2.1"));
            list.Add(new TreeModel(122, 12, "Child Node 1.2.2"));
            list.Add(new TreeModel(21, 2, "Child Node 2.1"));
            list.Add(new TreeModel(22, 2, "Child Node 2.2"));
            var resultTree = list.AsEnumerable().BuildBinaryTree(x => x.Id, t => t.ParentId);
            /* Returns : Binary tree.
             * Output :
             * Parent Node 1
             * --Child Node 1.1
             * ----Child Node 1.1.1
             * ----Child Node 1.1.2
             * --Child Node 1.2
             * ----Child Node 1.2.1
             * ----Child Node 1.2.1
             * Parent Node 2
             * --Child Node 2.1
             * --Child Node 2.2
             * */
            var resultTreeStartWithRootId = list.AsEnumerable().BuildBinaryTree(x => x.Id, t => t.ParentId, 1);
            /* Returns : Binary tree.
             * Output :
             * --Child Node 1.1
             * ----Child Node 1.1.1
             * ----Child Node 1.1.1
             * --Child Node 1.2
             * ----Child Node 1.2.1
             * ----Child Node 1.2.1
             * 
             * */
            var resultFlattenTree = resultTree.FlattenBinaryTree();
            /* Returns : IEnumerable.
            * Output : 
            * Parent Node 1
            * Child Node 1.1
            * Child Node 1.1.1
            * Child Node 1.1.2
            * Child Node 1.2
            * Child Node 1.2.1
            * Child Node 1.2.1
            * Parent Node 2
            * Child Node 2.1
            * Child Node 2.2
            * 
            * */

        }


        public class TreeModel : BinaryTree<TreeModel>
        {
            public int Id { get; set; }
            public int? ParentId { get; set; }
            public string Name { get; set; }

            public TreeModel(int id, int? parentId, string name)
            {
                this.Id = id;
                this.ParentId = parentId;
                this.Name = name;
            }
        }
    }
```
# License
Licensed under the MIT License.
