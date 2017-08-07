# Learn Verilog: iverilog + gtkwave on Ubuntu

[![Build Status](https://travis-ci.org/fchollet/keras.svg?branch=master)](https://travis-ci.org/fchollet/keras)
[![license](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)](https://github.com/fchollet/keras/blob/master/LICENSE)

## You have just found iverilog + gtkwave.

Share some experience on Verilog.

------------------


## installation

- __iverilog.__ _What Is Icarus Verilog?_   
`Icarus Verilog` is a `Verilog simulation and synthesis tool`. It operates as a compiler, compiling source code written in Verilog (IEEE-1364) into some target format. For batch simulation, the compiler can generate an intermediate form called vvp assembly. This intermediate form is executed by the __``vvp''__ command. For synthesis, the compiler generates netlists in the desired format.

- __gtkwave.__ GTKWave is a fully featured GTK+ based wave viewer for Unix, Win32, and Mac OSX which reads LXT, LXT2, VZT, FST, and GHW files as well as standard Verilog VCD/EVCD files and allows their viewing.

- __Atom.__

------------------


## Getting started: 30 seconds to Verilog using iverilg and gtkwave

The "iverilog" and "vvp" commands are the most important commands available to users of Icarus Verilog. The
"iverilog" command is the compiler, and the "vvp" command is the simulation runtime engine. What sort of output the
compiler actually creates is controlled by command line switches, but normally it produces output in the default vvp
format, which is in turn executed by the vvp program

[Verilog instructions online](http://www.swarthmore.edu/NatSci/mzucker1/e15/iverilog-instructions.html)
[iverilog.wikia.com/wiki/Vvp_Flags](http://iverilog.wikia.com/wiki/Vvp_Flags)
[gtkwave](http://gtkwave.sourceforge.net/gtkwave.pdf)
Here is the `hello, world` for Verilog:

```Verilog
module main;  
  initial   
    begin  
      $display("Hello, World");  
      $finish ;  
    end  
endmodule  
```
command-lines:
```shell
$iverilog -o laoqiu hello.v
$vvp laoqiu
```
__What does vvp mean?__  
`vvp` means ___Verilog Preprocessor___   



__Examples:__
------------------
------------------

__eg1__:  
[Verilog作业1](http://www.codeweblog.com/verilog%E4%BD%9C%E4%B8%9A-%E4%B8%80/)  
[初探Linux下对Verilog代码实现功能前仿](http://blog.163.com/jacky_z/blog/static/22508213520138227659293/)  
`hello.v`
```Verilog
module mux4_1(out, in0, in1, in2, in3, sel);

    output out;
    input in0, in1, in2, in3;
    input [1:0] sel;
    reg out;

    always @(in0 or in1 or in2 or in3 or sel)
    case(sel)
        2'b00: out = in0;
        2'b01: out = in1;
        2'b10: out = in2;
        2'b11: out = in3;
        default: out = 2'bx;
    endcase

endmodule
```  
`hello_tb.v`
```Verilog
module test();

    wire out;
    reg in0, in1, in2, in3;
    reg [1:0] sel;

    mux4_1 dut(.out(out), .in0(in0), .in1(in1), .in2(in2), .in3(in3), .sel(sel));

    initial begin
        in0 = 2'b00;
        in1 = 2'b01;
        in2 = 2'b10;
        in3 = 2'b11;
        #1 sel = 2'b00;
        #1 sel = 2'b01;
        #1 sel = 2'b10;
        #1 sel = 2'b11;
    end

    initial begin
        $dumpfile("./test.vcd");
        $dumpvars(-1, test);
        $dumpon();
        #6
        $dumpoff();
        $finish;
    end

    always #1
    $display("%t:    cout=%b %h %h %h %h %b", $time, out, in0, in1, in2, in3, sel);

endmodule
```
___在Makefile文件中，命令必须以【tab】键开始。___
filename:`makefile`
```makefile
# encoding:utf-8
# 在Makefile文件中，命令必须以【tab】键开始。
#test.vcd 是代码里面生成的
#测试hello_tb.v里面有
# initial begin
# 		$dumpfile("./test.vcd");
# 		$dumpvars(-1, test);
# 		$dumpon();
# 		#6
# 		$dumpoff();
# 		$finish;
# end
ok:
	iverilog -o laji hello.v hello_tb.v
	vvp laji
	gtkwave test.vcd
```
`terminal:`
```shell
$make
```
------------------
__eg2__:  
 [Verilog testbench总结(一)](http://blog.csdn.net/wordwarwordwar/article/details/53885209)
 `hello.v`
 ```Verilog
 ```
 `hello_tb.v`
 ```Verilog
 ```
 filename:`makefile`
 ```makefile
 # encoding:utf-8
 # 在Makefile文件中，命令必须以【tab】键开始。
 #test.vcd 是代码里面生成的
 #测试hello_tb.v里面有
 # initial begin
 # 		$dumpfile("./test.vcd");
 # 		$dumpvars(-1, test);
 # 		$dumpon();
 # 		#6
 # 		$dumpoff();
 # 		$finish;
 # end
 ok:
 	iverilog -o laji hello.v hello_tb.v
 	vvp laji
 	gtkwave test.vcd
 ```
 `terminal:`
 ```shell
 $make
 ```
 ------------------

Or generate predictions on new data:

```python
classes = model.predict(x_test, batch_size=128)
```

Building a question answering system, an image classification model, a Neural Turing Machine, or any other model is just as fast. The ideas behind deep learning are simple, so why should their implementation be painful?

For a more in-depth tutorial about Keras, you can check out:

- [Getting started with the Sequential model](http://keras.io/getting-started/sequential-model-guide)
- [Getting started with the functional API](http://keras.io/getting-started/functional-api-guide)

In the [examples folder](https://github.com/fchollet/keras/tree/master/examples) of the repository, you will find more advanced models: question-answering with memory networks, text generation with stacked LSTMs, etc.


------------------


## Installation

Keras uses the following dependencies:

- numpy, scipy
- yaml
- HDF5 and h5py (optional, required if you use model saving/loading functions)
- Optional but recommended if you use CNNs: cuDNN.


*When using the TensorFlow backend:*

- TensorFlow
    - [See installation instructions](https://www.tensorflow.org/install/).

*When using the CNTK backend:*

- CNTK
    - [See installation instructions](https://docs.microsoft.com/en-us/cognitive-toolkit/setup-cntk-on-your-machine).

*When using the Theano backend:*

- Theano
    - [See installation instructions](http://deeplearning.net/software/theano/install.html#install).

To install Keras, `cd` to the Keras folder and run the install command:
```sh
sudo python setup.py install
```

You can also install Keras from PyPI:
```sh
sudo pip install keras
```

------------------


## Switching from TensorFlow to CNTK or Theano

By default, Keras will use TensorFlow as its tensor manipulation library. [Follow these instructions](http://keras.io/backend/) to configure the Keras backend.

------------------


## Support

You can ask questions and join the development discussion:

- On the [Keras Google group](https://groups.google.com/forum/#!forum/keras-users).
- On the [Keras Slack channel](https://kerasteam.slack.com). Use [this link](https://keras-slack-autojoin.herokuapp.com/) to request an invitation to the channel.

You can also post **bug reports and feature requests** (only) in [Github issues](https://github.com/fchollet/keras/issues). Make sure to read [our guidelines](https://github.com/fchollet/keras/blob/master/CONTRIBUTING.md) first.


------------------


## Why this name, Keras?

Keras (κέρας) means _horn_ in Greek. It is a reference to a literary image from ancient Greek and Latin literature, first found in the _Odyssey_, where dream spirits (_Oneiroi_, singular _Oneiros_) are divided between those who deceive men with false visions, who arrive to Earth through a gate of ivory, and those who announce a future that will come to pass, who arrive through a gate of horn. It's a play on the words κέρας (horn) / κραίνω (fulfill), and ἐλέφας (ivory) / ἐλεφαίρομαι (deceive).

Keras was initially developed as part of the research effort of project ONEIROS (Open-ended Neuro-Electronic Intelligent Robot Operating System).

>_"Oneiroi are beyond our unravelling --who can be sure what tale they tell? Not all that men look for comes to pass. Two gates there are that give passage to fleeting Oneiroi; one is made of horn, one of ivory. The Oneiroi that pass through sawn ivory are deceitful, bearing a message that will not be fulfilled; those that come out through polished horn have truth behind them, to be accomplished for men who see them."_ Homer, Odyssey 19. 562 ff (Shewring translation).

------------------
