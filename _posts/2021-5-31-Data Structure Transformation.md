# Data Structure Transformation

When I read a really terrible repository (my vegetables have exploded), it uses tensor and sparse matrix simultaneously for the same initial dataset. I'm so confused... and after I transform both of them into Numpy array, they are totally the same（乌鸡鲅鱼

I tried many times to understand it because every time I got tired before I understood it... and after several days I finally tried some codes and found the tensor list and csr_matrix list are the same thing（？不错子

I think the following commands are useful.

### csr_matrix to Numpy array

```
sp_matrixA.toarray()
```

### tensor to Numpy array

```
tensorB.numpy()
```

### Numpy array to csr_matrix

```
import scipy.sparse as sp
sp.csr_matrix(arrayC)
```

### Numpy array to tensor

```
import torch
torch.from_numpy(arrayD)
```

And another wonderful command to find whether 2 arrays/Numpy matrixs a and b are totally the same.

```
print((a==b).all())
```

If I want to see whether 2 arrays share some public elements,

```
print((a==b).any())
```

