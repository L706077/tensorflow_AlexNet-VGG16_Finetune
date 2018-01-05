# tensorflow_AlexNet-VGG16_Finetune

---

## Train Finetune Model Reference:
- [kratzert/finetune_alexnet_with_tensorflow](https://github.com/kratzert/finetune_alexnet_with_tensorflow)
- [chenlongzhen/finetune_alexnet_with_tensorflow](https://github.com/chenlongzhen/finetune_alexnet_with_tensorflow-)
- [happenzZ/finetune_alexnet_with_tensorflow (test OK)](https://github.com/happenzZ/finetune_alexnet_with_tensorflow)


## Inference Finetune Model Reference:
- [stephen-v/tensorflow_alexnet_classify](https://github.com/stephen-v/tensorflow_alexnet_classify)
- [stephen-v Blog](http://www.cnblogs.com/vipyoumay/p/7686230.html)


- [machrisaa/tensorflow-vgg](https://github.com/machrisaa/tensorflow-vgg)

- [hjptriplebee/AlexNet_with_tensorflow](https://github.com/hjptriplebee/AlexNet_with_tensorflow)
- [hjptriplebee Blog](http://blog.csdn.net/accepthjp/article/details/69999309)



#!/usr/bin/env python

import sys
import os.path

# This is a tiny script to help you creating a CSV file from a face
# database with a similar hierarchie:
#
#  philipp@mango:~/facerec/data/at$ tree
#  .
#  |-- README
#  |-- s1
#  |   |-- 1.pgm
#  |   |-- ...
#  |   |-- 10.pgm
#  |-- s2
#  |   |-- 1.pgm
#  |   |-- ...
#  |   |-- 10.pgm
#  ...
#  |-- s40
#  |   |-- 1.pgm
#  |   |-- ...
#  |   |-- 10.pgm
#

if __name__ == "__main__":

    if len(sys.argv) != 2:
        print "usage: create_csv <base_path>"
        sys.exit(1)

    BASE_PATH=sys.argv[1]
    #SEPARATOR=";"
    SEPARATOR="	"
    
    file1 = open('train.txt','w')
    file2 = open('val.txt','w')
    label = 0
    count = 0
    for dirname, dirnames, filenames in os.walk(BASE_PATH):
        for subdirname in dirnames:
            subject_path = os.path.join(dirname, subdirname)
            for filename in os.listdir(subject_path):
                abs_path = "%s/%s" % (subject_path, filename)
                #print "%s%s%d" % (abs_path, SEPARATOR, label) >> file
                #STR=str(abs_path)+str(SEPARATOR)+str(label)
                #STR=str(abs_path)+'\t'+str(label)
                if count < 1:
                    file2.write(str(abs_path)+" "+str(label)+"\n")
                else:
                    file1.write(str(abs_path)+" "+str(label)+"\n")
                count = count +1
                #print(str(abs_path)) >> file
                #file.write(print('test'))
            count = 0
            label = label + 1
    file1.close()
    file2.close()
