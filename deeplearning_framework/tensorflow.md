## Train
```
    placeholder = Model.placeholder_inputs()
    pred = Model.get_model(placeholder)
    loss = Model.get_loss(pred,label)


    saver = tf.train.Saver()

    config = tf.ConfigProto()

    config.gpu_options.allow_growth = True
    ...

    sess = tf.Session(config=config)


    saver.restore(sess,path)
    train(sess,ops)


    def train():
        feed_dict = {variable:value}
        loss,pred = sess.run([ops['loss'],ops['pred']],feed_dict=feed_dict)
        correct = np.argmax(pred,1)
        loss_sum+=loss
        correct_sum +=correct
```


## Hook


## QUEUERUNNER
how it runs automenticly

## Some functions
1. tf.convert_to_tensor
2. tf.control_dependencies
3. tf.train.ExponentialMovingAverage
```
loss_averages = tf.train.ExponentialMovingAverage(0.9, name='avg')
# apply
loss_averages_op = loss_averages.apply(losses + [total_loss])
# average
loss_averages.average(l)
```
4. 




## Tips

### some important points
tensor is of immutability

### How to run numpy in tf operator
* tf.py_func
input and output of this function is numpy array

* encapusule it to tf operator
use tf.py_func

* rewrite by using tf.xxx to inplace of np.xxx
by this method the network can utilize GPU


### Operation and Tensor
* some operations like opt.apply_gradients return op


### tf.name_scope and tf.variable_scope
* name_scope example
```
def my_op(a,b,c,name):
    with tf.name_scope(name,'My_Op',[a,b]) as sc:
        a = tf.convert_to_tensor(a,name='a')
        b = tf.convert_to_tensor(b,name='b')
        ...
        return foo_op(...,name=sc)
```

* variable_scope example
```
with tf.variable_scope('foo'):
    with tf.variable_scope('bar'):
        tf.get_variable('')
```


### select method
tf.reshape(tf.where(x>3),[-1])
tf.boolean_mask(x>3,x)
```
cond = np.arange(10).reshape(2,5)>3
res_np = np.where(cond)
>>>res_np:
([0,1,1,1,1],[4,0,1,2,3])

res_tf = tf.where(cond)
>>>res_tf:
[[0 4],[1,0],...]
```


###array ops
* tf.tile
* tf.stack
* tf.gather
* tf.static_broadcast and dynamic_broadcast
* tf.random_shuffle
* tf.sparse_to_dense
* tf.size
* tf.squeeze
* tf.gather_nd
* tf.SparseTensor
