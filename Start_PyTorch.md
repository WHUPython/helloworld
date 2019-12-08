> This article helps starters begin PyTorch programming as soon as possible. It assumes readers to have basic grasps on back propogation(bp), tensorflow programming and optional static and dynamic graph.



PyTorch is the most widely used （deep learning）DL framework in research field as a result of its dynamic graph feature. It enables users to programm in a pythonic way.

I think the best way to start PyTorch programming is to read official docs. So this passage might not be a good choice for some people.

PyTorch is very simple, just like python programming.

Let ‘s reflect what ingredients a dl framework should have.

- a **base datatype** containing weight and bp gradients, which can be regarged as model’s parameters
- **loss functions** to compute model’s outputs deviation to labels
- **optimizers** responsible to compute parameters’ gradients and then modify(update) them

Given the above three componets, model can be built, loss computed, model’s parameters updated. Let’s proceed to see how to accomplish those in PyTorch.

## Base DataType— **torch.Tensor**

`torch.Tensor` is PyTorch’s base datatype.

How to convert numpy array to `torch.Tensor` ? Very simple `torTensor = tor.as_tenor(a_numpy_array)`.

How to use this to build a model(suppose linear model: $y = Wx + b$ )?

```
W, b=torch.random(1), torch.random(1)
x = tor.as_tensor(x_ndarray)
y = W * x + b
```

That’s it, very simple. We can use common python operators to connect PyTorch **base datatype**, and its backward mechanism will help you manage each varaible’s bp gradients and store it to each **tensor’s** **.grad** attribute. You also can directly call its `.backward()` method with a gradient param to change its **grad** attribute’s content(value).



## loss fucntions**: torch.nn.MSE**

torch.nn module has many pre-defined loss function. **nn.MSE** is an example. Loss functions take as inputs two params, model’s outputs and label, then calcuate, return their deviation tensor **L**.

One important thing is that when you call **L.backward()**, its default argument is 1, and the backward operation will back propogate the gradients to the very begining tensor. And, as a result, for tensors on the back way, their **grad** attribute will be changed.

## optimizer: **torch.optim**

Aformentioned two componets can be used to created model, calculate parameters’ gradients. **torch.optim** can serves to update parameters. let’s see a code snippet copied from the official site.

```
`import` `torch.optim as optim` `# create your optimizer``optimizer ``=` `optim.SGD(net.parameters(), lr``=``0.01``)` `# in your training loop:``optimizer.zero_grad()   ``# zero the gradient buffers``output ``=` `net(``input``)` `loss ``=` `criterion(output, target)``loss.backward()``optimizer.step()    ``# Does the update`
```

It initialize an optimizer with model’s paramters as input, specifing what tensors the optimizer should manage(update). After loss function’s loss calcuating and **update** tensors’ grad attribute. **optimizer.step()**is called to update params it manage.

Of course, SGD is not the only optimizer torch supports, for more refer the official site.

Also, the last two componets can be customized in PyTorch.


  