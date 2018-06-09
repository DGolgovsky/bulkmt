# bulkmt
Homework 10 task. [OTUS C++]

[![Build Status](https://travis-ci.org/DGolgovsky/bulkmt.svg?branch=master)](https://travis-ci.org/DGolgovsky/bulkmt)
[![Code Health](https://landscape.io/github/DGolgovsky/bulkmt/master/landscape.svg?style=flat)](https://landscape.io/github/DGolgovsky/bulkmt/master)
[ ![Download](https://api.bintray.com/packages/dgolgovsky/otus-cpp/bulkmt/images/download.svg) ](https://bintray.com/dgolgovsky/otus-cpp/bulkmt/_latestVersion)

**Task description**

The main goal is to rework task 7 so that the output of processed commands were executed in parallel. When the program starts, in addition to the existing mainstream, three more additional.

We give them conditional names:

• main - mainstream

• log - stream for output to the console

• file1 - the first thread to output to a file

• file2 - the second stream to output to a file

The main processing logic is changed in such a way that the instruction block, immediately after its formation must be sent to the console and file at the same time. At the same time, sending a block to a file must be is distributed between two streams.

Attention is drawn to the insufficient accuracy of the clock for the formation of a unique name. It is necessary, keeping the timestamp in name, add an additional section that will be guaranteed differ.

In multi-threaded processing, logging can be a costly procedure and an involuntary thread synchronizer. In this task, you must enter additional operation counters that are must be output to the console at the end of the program.

On each additional flow of two counters:

• number of blocks

• total number of teams in blocks

In the main thread, there are three counters:

• the number of lines reads from the file (commands + `{` + `}`)

• number of teams

• number of blocks

For consistency
```
{
cmd1
cmd2
{
cmd3
cmd4
}
cmd5
cmd6
}
```

the metrics must have values ​​respectively:
```
• main stream - 10 lines, 6 commands, 1 block
• log stream - 1 block, 6 commands
• file1 stream - 1 block, 6 commands
• file2 stream - 0 blocks, 0 commands
```

Optionally conduct an experiment to select the optimal amount flows. It is necessary to substantially increase the CPU load in the streams for writing to a file, for example making a very large number of random mixing or counting hash.
Any operation that consumes only the CPU will do. Do this operation cyclically, observing the speed of reading the data with disk, until the reading from the disk, is not significantly reduced.

The second stage will be an increase in the number of flows, increase the number of flows should be slow, prolonged Watch the speed of reading from the disks.

Should notice the following dynamics:

• increasing the CPU cost in one thread leads to a decrease disk read speed

• increasing the number of streams leads to an increase in speed read from disk

• further increase in quantity again leads to a decrease read speed

Pay attention to the fact that the experiment can interfere with any queues that can be in the program.

Detailed description on the [gh-pages](https://dgolgovsky.github.io/bulkmt/)

**Dockerfile**
```
FROM ubuntu:trusty
#### Bintray (by JFrog) 
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 379CE192D401AB61
#### Dmitry Golgovsky (Packages sign) 
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys D5CEB8D4D5185900
#### toolchain repo key
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1E9377A2BA9EF27F
RUN echo "deb http://dl.bintray.com/dgolgovsky/otus-cpp trusty main" | sudo tee -a /etc/apt/sources.list
RUN echo "deb http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu trusty main" | sudo tee -a /etc/apt/sources.list
RUN apt update
RUN apt install -y libstdc++6 bulkmt
```

**OTUS** C++ online [course](https://otus.ru/lessons/razrabotchik-c++/) studying repository.

**About the course**

Being one of the most popular programming languages, C++ is widely used for software development. The scope of usage includes the creation of operating systems, a variety of applications, device drivers, applications for embedded systems, high-performance servers, and entertainment applications (games).
In the course "C++ Developer" will be considered as introductory concepts, such as automation tools, STL, innovations of `11` and `14` standards; and more complex: asynchronous programming, design patterns, distributed high-availability services architectures.
