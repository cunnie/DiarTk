## DiarTk

This is a fork of the Speaker Diarization Toolkit, 
[DiarTk](https://www.idiap.ch/scientific-research/resources/speaker-diarization-toolkit),
originally created at the
[Idiap Research Institute](http://publications.idiap.ch/index.php/publications/show/2407).

### Quick Start

Use Vagrant to bring up an Ubuntu box if you're on OS X

```
vagrant box add precise64 http://files.vagrantup.com/precise64_vmware.box
vagrant up
vagrant ssh
sudo apt-get update
sudo apt-get install -y g++ cmake make libboost-all-dev
```

Compile DiarTk:

```
cd /vagrant/src/diarization/cmake/
cmake .
make
```

Run:

```
cd /vagrant
bash scripts/run.diarizeme.sh \
        data/mfcc/AMI_20050204-1206.fea \
        data/scp/AMI_20050204-1206.scp \
        result.dir/ \
        AMI_20050204-1206
perl md-eval-v21.pl -m -afc -c 0.25 -r data/rttm/AMI_20050204-1206.rttm \
        -s result.dir/AMI_20050204-1206.rttm
```

The expected DER is 8.79%

---

Trying to compile under OS X gave us the following error:

```
/usr/local/include/boost/smart_ptr/detail/array_count_impl.hpp:17:18: error: declaration of anonymous class must be a definition
        template<class P, class A>
```

Fixing the `#define P 2` in `global.h` got us only a little further:

```
/Users/cunnie/Downloads/ib_diarization_toolkit/src/aIB/src/aIB.cpp:34:10: fatal error: 'omp.h' file not found
#include <omp.h>
```
