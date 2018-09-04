---
layout: post
title: Tensorflow Model export
date: 2018-02-03
---

written by Suhee Jo

## Tensorflow Model Save and Restore

based on https://www.tensorflow.org/programmers_guide/saved_model

- Checkpoint : *Only* **Variables** are stored
- Saved model : Not only **Variables** *but also* **graphs** are stored

### Using Checkpoint
- Saving and Restoring Variables
- tf.train.Saver saves & restores for or a specified list of the variables.

```
import tensorflow as tf

# Create some variables.
v1 = tf.get_variable("v1", shape=[3], initializer = tf.zeros_initializer)
v2 = tf.get_variable("v2", shape=[5], initializer = tf.zeros_initializer)

inc_v1 = v1.assign(v1+1)
dec_v2 = v2.assign(v2-1)

# Add an op to initialize the variables.
init_op = tf.global_variables_initializer()

# Add ops to save and restore all the variables.
saver = tf.train.Saver({"v1":v1})
# saver = tf.train.Saver()
# saver = tf.train.Saver({"v1":v1})

# Later, launch the model, initialize the variables, do some work, and save the
# variables to disk.
with tf.Session() as sess:
  sess.run(init_op)
  # Do some work with the model.
  inc_v1.op.run()
  dec_v2.op.run()
  # Save the variables to disk. makes directory when unavailable.
  save_path = saver.save(sess, "./tmp/model.ckpt")
  print("Model saved in path: %s" % save_path)


tf.get_default_graph()

with tf.Session() as sess:

    v2.initializer.run()
    saver.restore(sess, "/tmp/model.ckpt")

    print("v1 %s" %v1.eval())
    print("v2 %s" %v2.eval())
```
- can create as many as Saver objects and save&restore different subsets of the model variables


### Using SavedModel

#### Saving
- **SavedModelBuilder** class can save **MetaGraphDef** which is a protocol buffer for MetaGraph. MetaGraph is a dataflow graph containing its associated varialbes, assets and signatures.
- **signature** is the set of inputs to and outputs from a graph
- the first meta graph must be provided with variables
- if multiple **MetaGraphDef** are associated with an asset of the same name, only the first version is retained
- Each **MetaGraphDef** needs a user-specified tag which indicates its purpose(training/serving) or hardware(gpu)



```

def Save_Model(self,sess,x,y):
    #sess is session where model is saved
    # x is input which is a placeholder, y is output which is an operation by tf.
    #set up export path
    export_path="./exp_model"
    #set up builder
    builder = tf.saved_model.builder.SavedModelBuilder(export_path)
    #read info
    tensor_info_x = tf.saved_model.utils.build_tensor_info(x)
    tensor_info_y = tf.saved_model.utils.build_tensor_info(y)

    prediction_signature = (
        tf.saved_model.signature_def_utils.build_signature_def(
            inputs={'input': tensor_info_x},
            outputs={'output': tensor_info_y},
                method_name=tf.saved_model.signature_constants.PREDICT_METHOD_NAME))

    legacy_init_op = tf.group(tf.tables_initializer(), name='legacy_init_op')

    builder.add_meta_graph_and_variables(
        sess, [tf.saved_model.tag_constants.SERVING],
        signature_def_map={
            'prediction':
                prediction_signature,
        },
        legacy_init_op=legacy_init_op)

    builder.save()
```

#### SignatureDef

- SignatureDef defines the signature of a computation.
- requires **inputs**, **outputs**, **method_name**
- SignatureDef's method has 3 categories, **Regression**, **Prediction**, **Classification**

#### Loading

```
export_dir = ...
...
with tf.Session(graph=tf.Graph()) as sess:
  tf.saved_model.loader.load(sess, [tf.saved_model.tag_constants.TRAINING], export_dir)
  ...
```

#### SavedModel Directory
- When a model is saved in SavedModel format, following subdirectories are created

```

variables/
    variables.data-?????-of-?????
    variables.index
saved_model.pb|saved_model.pbtxt

```


- variables: outpus from tf.train.Saver
- saved_model.pb or saved\_model.pbtxt : SavedModel protocol buffer. includes the graph definitions as MetaGraphDef protocol buffers


```bash
|-- export_model_path
     |-- 1
        |-- variables/
        |-- saved_model.pb
     |-- 2
        |-- variables/
        |-- saved_model.pb

```
- 주의 사항: 위와 같은 hierarchy로 구성되어 있어야 한다.

## Tensorflow Serving
-Tensorflow serving system for production environment

```
~/tensorflow_model_server --port=9000 --model_name=model_name --model_base_path=/home/ninas96211/hdd/tacotron/exp_model
```



