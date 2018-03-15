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
    

