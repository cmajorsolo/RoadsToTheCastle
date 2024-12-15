# DropPath 
DropPath is a regularization technique that selectively drops entire paths (branches or residual connections) in a neural network during training. This method is particularly useful in architectures with many residual or skip connections, such as ResNets and transformers.

```python
# DropPath Implementation
def DropPath(nn.Module):
    def __init__(self, drop_prob=0.2):
        """
        Initialize DropPath.
        Args:
            drop_prob (float): Probability of dropping a path. Default is 0.2.        
        """
        super(DropPath, self).__init__()
        self.drop_prob = drop_prob
    
    def forward(self, x):
        if self.drop_prob == 0.0 or not self.training: 
            # No dropping when traning or when drop_prob is 0
            return x
        # Compute the keep probability
        keep_prob = 1 - drop_prob
        # Create a binary mask to drop paths
        mask = torch.rand(x.shape[0], 1, 1, device=x.device, dtype-x.dtype) < keep_prob
        # Scale the output during training
        x = x / keep_prob
        return x * mask

# Assume a batch size of 3
batch_size = 3
keep_prob = 0.8  # Probability of keeping a path
x = torch.randn(batch_size, 10)  # Example input tensor

# Generate the mask
mask = torch.rand(x.shape[0], 1, 1, device=x.device, dtype=x.dtype) < keep_prob
print(mask)
# tensor([[[ True]],
#         [[ True]],
#         [[False]]])
```



